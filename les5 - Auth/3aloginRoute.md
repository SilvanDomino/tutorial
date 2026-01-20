# Log in pt1
Om in te kunnen loggen moeten we drie stukken schrijven.

* De registratie route (register.php)
* De HTML pagina
    * Met javascript

## Flow
Deze stap voor de authentication is best wel groot, want er moeten een heleboel dingen gebeuren.
1. Wachtwoord en gebruikersnaam ontvangen
2. Kijken of gebruikernaam en wachtwoord in de database staan.
3. Token aanmaken en opslaan in database.
4. Token terugsturen naar client.

### Login backend route
Maak in de php folder een bestand genaamd `login.php`. In dit bestand wordt de route gemaakt waar de gebruiker zich kan inloggen. 

## 1: Wachtwoord en gebruikersnaam ontvangen
### Kopieren van register.php
De eerste stappen zijn hetzelfde bij inloggen als bij registreren.

1. Headers
2. Verbinding met database (connect.php)
3. JSON data uitlezen

## 2: Kijken of gebruikernaam en wachtwoord in de database staan.
### SQL
Deze keer gaan we gebruik maken van een **SELECT** SQL statement om gegevens op te halen uit de database.

```php
$sql = "SELECT id, password FROM users WHERE username = ?";
$stmt = $db->prepare($sql);
$stmt->bind_param("s", $username);

$stmt->execute();
$result = $stmt->get_result();
$user = $result->fetch_assoc();
$stmt->close();
```

### Wachtwoord
We hebben nu de gebruiker opgehaald, en kunnen nu kijken of het wachtwoord klopt. Met `$user` kunnen we kijken of zo een gebruiker bestaat. Met `password_verify($plain_pw, $user['password'])` controlleren we ook of het wachtwoord klopt. 

```php
if($user && password_verify($plain_pw, $user['password'])){
    //===> HIER KOMT DE VOLGENDE STAP <=== 
} else{
    echo "username or password incorrect";
}
```

## 3 en 4: Token aanmaken en opslaan in database en terugsturen
De token is een tijdelijk wachtwoord+gebruikersnaam. Dit token kan enkele uren geldig zijn, maar ook enkele jaren. Dit wachtwoord kan ook ingetrokken worden.

De token is in principe een **string van een heleboel willekeurige characters** die *in principe* uniek zijn. 

```php
$token = bin2hex(random_bytes(32));
$expires_at = date('Y-m-d H:i:s', time() + 360000);
```

Deze token willen we opslaan in de database. We willen opslaan:
* Token    
    De unieke string
* Expires_at
    Tot hoe laat de token geldig is. (Wordt aan de server en aan de backend zo gehanteerd)
* User_id
    Welke user gekoppeld is aan de token.

```php
//thanks gemini for the SQL query
$sql_token = "INSERT INTO auth_tokens (user_id, token, expires_at) VALUES (?, ?, ?) ON DUPLICATE KEY UPDATE token = VALUES(token), expires_at = VALUES(expires_at)";
$stmt_token = $mysqli->prepare($sql_token);
$stmt_token->bind_param("iss", $user_id, $token, $expires_at);
if ($stmt_token->execute()) {
    $stmt_token->close();
    header("Content-Type: application/json; charset=UTF-8");

    //Dit is deel 4 het terugsturen van de token
    echo json_encode(["message" => "Login successful", "token" => $token]);
    //Einde deel 4
} else {
    $stmt_token->close();
    header("Content-Type: application/json; charset=UTF-8");
    echo json_encode(["error" => "Could not issue authentication token."]);
}
```

## Probeer de route uit
Open Insomnia en probeer de route uit. Kijk of je kan 'inloggen' door de account gegevens te sturen naar de `login` route. Als het klopt krijg je terug

```json
{
	"message": "Login successful",
	"token": "1b56610d77720030811ac84ba03be659433220ff12fe76a5163f673ece3a8561"
}
```