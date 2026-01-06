# Stap 1: PHP Route bouwen

Nu gaan we de backend klaar maken: een `editTodo.php` endpoint dat todos aanpast in de database. Hierbij maken heel veel gebruik van knip en plak werk van de vorige les.

## Wat gaat er gebeuren?

Hier is de flow van een PATCH request:

```
Frontend (JavaScript)
       ↓
  PATCH request
  JSON body: { "id": "1", "status": "done" }
       ↓
Backend (PHP): /api/editTodo.php
       ↓
  Database [UPDATE](https://www.w3schools.com/sql/sql_update.asp)
       ↓
Response: "Success!" (of error)
       ↓
Frontend: Refresh todo list
```

## Bestand
Maak een bestand naast *todos.php* genaamd `editTodo.php`. In dit bestand gaan we dit hoofdstuk werken.

### 1. Headers en Database connectie
Voeg de headers toe. (Zie vorige les)
In plaats van de POST methode gebruiken we de PATCH methode.

### 2. JSON data uitlezen
Lees de JSON code uit. (Zie vorige les).
Check ipv de *text* de **id**. Die gaan we gebruiken.

### 3. Database UPDATE met Prepared Statement
De SQL statement is in principe:
```php
$stmt = $mysqli->prepare("UPDATE todos SET status=? WHERE id = ?");
```

We passen alleen maar de status aan van een todo. Welke todo we aanpassen selecteren we op basis van de **id**.

```php
$stmt->bind_param("si", $status, $id);
```

**Volgende stap**: [Stap 2 - Testen in Postman/Insomnia](./3apitesten.md)
