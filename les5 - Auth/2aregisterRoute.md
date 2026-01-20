# Registratie pt1
Om te kunnen registreren moeten we drie stukken schrijven.

* De registratie route (register.php)
* De HTML pagina
    * Met javascript

## Registratie backend route
Maak in de php folder een bestand genaamd `register.php`. In dit bestand wordt de route gemaakt waar de gebruiker zich kan registreren. 

### Headers
We beginnen met de headers. Deze headers staat POST requests toe en JSON data. We kunnen nu een POST request versturen met JSON data.
De JSON data bevat straks twee properties: **Username** en **Password**
```php
header("Access-Control-Allow-Methods: POST, OPTIONS");
header("Access-Control-Allow-Headers: Content-Type");
header("Content-Type: application/json; charset=UTF-8");
```

### Verbinding met de database
In een van de vorige hoofdstukken hebben we `connect.php` aangemaakt. Deze importeren we (gebruik require once)

### JSON Data uitlezen
We kunnen een POST request versturen naar ons PHP script. Bij dit PHP request zit de JSON, en als we deze willen uitlezen, dan moeten we 2 regels code toevoegen.

```php
$json_data = file_get_contents('php://input');
$data = json_decode($json_data, true);
```

De data kunnen we ook nog verifieren. Met de volgende regels kijken we of de data die we nodig hebben meegegeven is.

```php
$username = $data["username"] ?? '';
$plain_pw = $data["password"] ?? '';

if($username == '' || $plain_pw == ''){
    exit("Error, username or pw are missing"); 
}
```

### Basis beveiliging
We willen natuurlijk geen ongehashde wachtwoorden in de database hebben. Dat is heel slecht.
```php
    $hashed_pw = password_hash($plain_pw, PASSWORD_DEFAULT);
```

### Registreren in DB
We voegen de username en wachtwoord toe aan de database. 

```php
$stmt = $db->prepare("INSERT INTO users (username, password) VALUES (?, ?)");
$stmt->bind_param("ss", $username, $hashed_pw);
if ($stmt->execute()) {
    echo json_encode(["message" => "Registration successful"]);
} else {
    echo json_encode(["message" => "Registration failed"]);
}
$stmt->close();
$db->close();
```
Hier gebruiken we een prepared statement, want we willen geen *Bobby Tables* in onze database krijgen. 
![](https://imgs.xkcd.com/comics/exploits_of_a_mom.png)

## Test de route
Open insomnia en probeer de route uit. Registreer je via Insomnia.
Als het registreren werkt, dan kan je verder naar het volgende hoofdstuk. Daar gaan we de HTML en javascript schrijven.