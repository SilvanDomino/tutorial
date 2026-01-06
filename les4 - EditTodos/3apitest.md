# Stap 2: API testen in Insomnia

Voordat we de frontend verbinden, testen we de `editTodo.php` API direct om er zeker van te zijn dat het werkt.

## Setup: Een PATCH request maken
Nu gaan we de **edit todo** route testen. Hiervoor moeten we een paar stappen meer doen dan bij het ophalen van de todos. 

### 1. Insomnia openen

- Klik op **+** → **New Request**
- Geef het een naam, bijvoorbeeld "Edit Todo"

### 2. URL en method instellen

```
POST http://localhost:8080/api/editTodo.php
```

Zorg dat:
- **Method** = `PATCH` (niet GET!)
- **URL** = exact bovenstaand adres

### 3. Headers instellen

Klik op het **Header** tabblad en voeg deze toe:

| Key | Value |
|-----|-------|
| Content-Type | application/json |

Dit vertelt de server dat we JSON sturen.

### 4. Body instellen

Klik op het **Body** tabblad en:
1. Selecteer **JSON** van de dropdown
2. Vul in:

```json
{
  "id": "3",
  "status": "done"
}
```

*Afhankelijk* natuurlijk wat je gebruikt voor status. Sommige mensen gebruiken getallen of hoofdletters of iets anders. 

### 5. Request versturen

Klik op de **Send** knop.

### 6. Verificatie in phpMyAdmin

Nu controleren we dat de todo echt in de database staat:

1. Open je browser op `localhost:8081`
2. Log in (standaard: root / root)
3. Kies database `todo_app` → tabel `todos`
4. Je zou de todo aangepast moeten zien!


**Volgende stap**: [Stap 3 - Frontend integratie](./3frontend.md)
