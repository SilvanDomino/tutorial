# Stap 1: PHP Route bouwen

Nu gaan we de backend klaar maken: een `addTodo.php` endpoint dat todos opslaat in de database.

## Voorbereiding: connect.php

Eerst moeten we zorgen dat we verbinding hebben met de database. We gebruiken het bestand `connect.php` voor de MySQL connectie. Als we dit in een apart bestand stoppen hoeven we niet elke keer deze code opnieuw uit te schrijven (en aan te passen als er iets mis gaat)

### Maak connect.php aan (als je het nog niet hebt)

Maak het bestand `connect.php` aan met de volgende inhoud:

```php
<?php
// MySQL verbinding
$mysqli = new mysqli("db", "root", "root", "todo_app");

// Check voor verbindingsfouten
if ($mysqli->connect_error) {
    die("Verbinding mislukt: " . $mysqli->connect_error);
}
```

Dit bestand:
- Maakt verbinding met de MySQL server (`host: db`, `user: root`, `password: root`)
- Selecteert de `todo_app` database
- Checkt voor fouten

**Opmerking**: De hostname is `db` (niet `localhost`) omdat het in Docker draait. De containers kunnen elkaar bereiken via servicenaam.

### Verificatie

Test of de connectie werkt:
1. Maak een testbestand `test.php`:

```php
<?php
require_once(connect.php');
echo "Verbonden met database!";
$mysqli->close();
?>
```

2. Open in je browser: `http://localhost:8080/test.php`
3. Je zou moeten zien: "Verbonden met database!"

Treedt een fout op? Controleer:
- [ ] Docker containers draaien? (`docker-compose ps`)
- [ ] PHP service is accessible op `localhost:8080`?
- [ ] MySQL service naam in Docker is `db`?

---

## Wat gaat er gebeuren?

Hier is de flow van een POST request:

```
Frontend (JavaScript)
       ↓
  POST request
  JSON body: { "text": "Boodschappen doen" }
       ↓
Backend (PHP): /api/addTodo.php
       ↓
  Database INSERT
       ↓
Response: "Success!" (of error)
       ↓
Frontend: Refresh todo list
```

## Het bestand aanmaken

Maak een nieuw bestand aan: `backend/php/api/addTodo.php`

## PHP Code - Stap voor stap

### 1. Headers en Database connectie

```php
<?php
header("Access-Control-Allow-Origin: http://localhost:5173");
header("Access-Control-Allow-Methods: POST, OPTIONS");
header("Access-Control-Allow-Headers: Content-Type");

require_once(connect.php');
```

Dit zorgt dat:
- Onze frontend (op `localhost:5173`) de API mag aanroepen
- POST requests welkom zijn
- JSON-headers correct ingesteld zijn

### 2. JSON data uitlezen

```php
$data = json_decode(file_get_contents("php://input"), true);

if (empty($data['text'])) {
    echo "Geen of incorrecte JSON!";
    exit;
}

$text = $data['text'];
```

De frontend stuurt dit: `{ "text": "Boodschappen doen" }`  
We lezen dit uit met `json_decode()` en controleren of het niet leeg is.

### 3. Database INSERT met Prepared Statement

```php
$stmt = $mysqli->prepare("INSERT INTO todos (text, status) VALUES (?, ?)");

$status = "todo";
$stmt->bind_param("ss", $text, $status);

if ($stmt->execute()) {
    echo "Success!";
} else {
    echo "Failure!";
}

$stmt->close();
$mysqli->close();
?>
```

Dit doet:
- `?` placeholders gebruiken (SQL injection veilig)
- `bind_param("ss", ...)` - beide parameters zijn strings
- De query uitvoeren
- Bevestiging teruggeven

---

**Volgende stap**: [Stap 2 - Testen in Postman/Insomnia](./3apitesten.md)
