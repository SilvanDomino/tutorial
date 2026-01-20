# Authentication

Bij dit hoofdstuk gaan we authentication toe passen. De gebruiker mag alleen gebruik maken van de routes als de gebruiker *authenticated* is. De gebruiker moet dus toegang hebben voordat deze gebruik kan maken van de routes.

Daarvoor moeten we 2 dingen doen.

* De token meesturen met onze request.
* De token opvangen (en kijken of deze token klopt).

## Frontend
### Token Ophalen
Om de token mee te sturen moeten we eerst de token uit de cookies halen. 

* Maak een nieuw map in in de src van de frontend.     
Noem deze map `util`. Dit staat voor *utilities*. In deze map komen alle losse functies die in veel meer bestanden gebruikt kunnen worden. 
* Maak een bestaand aang genaamd `getCookies.js`.     
Doe daar de volgende code in
```js
//Source: https://www.w3schools.com/js/js_cookies.asp
export function getCookie(cname) {
  let name = cname + "=";
  let decodedCookie = decodeURIComponent(document.cookie);
  console.log(decodedCookie);
  let ca = decodedCookie.split(';');
  for(let i = 0; i <ca.length; i++) {
    let c = ca[i];
    while (c.charAt(0) == ' ') {
      c = c.substring(1);
    }
    if (c.indexOf(name) == 0) {
      return c.substring(name.length, c.length);
    }
  }
  return "";
}
```
Deze functie kan je straks in elk bestand importeren en gebruiken.

### Token meesturen
We gaan de token meesturen wanneer we de Todo's uit onze database ophalen. 

1) Open `Todolist.js`. 
2) Importeer de `getCookie` functie. 
3) We pakken de token uit de cookies, en geven deze mee in de header. 
```js
let token = getCookie('token');
let response = await fetch(this.url, {
    headers: {
        'Authorization': `Bearer ${token}`
    }
});
```


## Backend
In de PHP moeten we de token afvangen, en kijken of de token klopt. Open `getTodos.php` (of `todos.php`).

### Headers
Om te zorgen dat CORS geen problemen geeft, moeten we toestemming geven voor een request met een *Authorization* header. 
```php
header("Access-Control-Allow-Headers: Authorization");
```
Zet alle volgende code **BOVEN** de SQL query waarmee alle todo's worden opgevraagd. We vragen alle headers op die de fetch request van Javascript heeft meegegeven.
```php
$headers = getallheaders();
$auth_header = $headers['Authorization'];
```

### Token uit header
Deze code pakt onze (Authorization) header.

```php
//thanks stack overflow: https://stackoverflow.com/questions/40582161/how-to-properly-use-bearer-tokens
$token = null;
if (preg_match('/Bearer\s(\S+)/', $auth_header, $matches)) {
    $token = $matches[1];
}
if (!$token) {
    exit("Token is missing or invalid in Authorization header.");
}
```

En als het goed is hebben we nu de token. De client (frontend) kan inloggen, en de token meesturen naar de server toe.

### Token controlleren
Nu moeten we controlleren of de Token daadwerkelijk in de database staat. Dit kunnen we (helaas) alleen doen door gebruik te maken van SQL en onze database. 

```php
$sql_token_check = "SELECT user_id FROM auth_tokens WHERE token =? AND expires_at > NOW()";
```
Onze SQL statement betaat uit 3 (opvallende) dingen. 
* `SELECT`    
    We selecteren alleen de userID. De overige informatie is onnodig.
* `WHERE token = ?`     
    We selecteren straks alleen de token die overeenkomt. De client en de server moeten allebei dezelfde token hebben.
* `expires_at > NOW()`     
    Mooie manier om alleen de tokens die niet expired zijn te filteren.

De volgende stap is het uitvoeren van de SQL statement.
```php 
//We bereiden de SQL statement voor, en voeren deze uit
$stmt_token = $db->prepare($sql_token_check);
$stmt_token->bind_param("s", $token);
$stmt_token->execute();
//We pakken de resultaat van onze SQL query. Hele lelijke syntax
$result_token = $stmt_token->get_result();
$auth_data = $result_token->fetch_assoc();
//We kijken of er resultaat is. Als er geen resultaat is, dan is de token niet gevonden.
if (!$auth_data) {
    exit("Invalid or expired token. You must be logged in to do that.");
}

//Deze is belangrijk voor de volgende les.
$authenticated_user_id = $auth_data['user_id'];
```

#### Resultaat
We kunnen nu alleen nog maar de Todos zien als we ingelogd zijn. 

### Refractoren.
De code die we net geschreven hebben, die gaan we ook gebruiken als we Todos gaan toevogen (`addTodo.php`) of Todos gaan aanpassen (`editTodo.php`). We kunnen dus twee dingen doen:
* De code kopieeren en plakken.
* Een **checkAuth** script schrijven die we vervolgens importeren. Hetzelfde hebben we ook al gedaan met `connect.php`. 
    * Maak een `check_auth.php` bestand aan.
    * Zet daar *alle* php code van **deze** les.

## Doe zelf
Voeg zelf de authentication toe aan de andere API routes.
