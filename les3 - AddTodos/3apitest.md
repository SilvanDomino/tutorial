# Stap 2: API testen in Insomnia

Voordat we de frontend verbinden, testen we de `addTodo.php` API direct om er zeker van te zijn dat het werkt.

Je hebt Insomnia al geïnstalleerd, dus we kunnen direct beginnen!

## Setup: Een GET request maken
We gaan eerst testen de route waarvan we weten dat deze werkt, de *get todos* route. Deze heb je vorige les gemaakt en geimplementeerd.

### 1. Insomnia openen

- Start Insomnia
- Klik op **+** → **New Request**
- Geef het een naam, bijvoorbeeld "Get Todos"

### 2. URL en method instellen

```
GET http://localhost:8080/api/todos.php
```

Zorg dat:
- **Method** = `GET` (de default)
- **URL** = bovenstaand adres

### 3. Request versturen

Klik op de **Send** knop.
Als het goed is zie je het resultaat van de GET request.

## Setup: Een POST request maken
Nu gaan we de **add todo** route testen. Hiervoor moeten we een paar stappen meer doen dan bij het ophalen van de todos. 

### 1. Insomnia openen

- Klik op **+** → **New Request**
- Geef het een naam, bijvoorbeeld "Add Todo"

### 2. URL en method instellen

```
POST http://localhost:8080/api/addTodo.php
```

Zorg dat:
- **Method** = `POST` (niet GET!)
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
  "text": "Boodschappen doen"
}
```

Je mag natuurlijk een ander todo-tekst gebruiken!

### 5. Request versturen

Klik op de **Send** knop.

### 6. Verificatie in phpMyAdmin

Nu controleren we dat de todo echt in de database staat:

1. Open je browser op `localhost:8081`
2. Log in (standaard: root / root)
3. Kies database `todo_app` → tabel `todos`
4. Je zou de nieuwe todo moeten zien!

Zie je hem? Geweldig!

## Meer testen

Stuur nog een paar requests om zeker te zijn:

```json
{
  "text": "Python leren"
}
```

```json
{
  "text": "Email checken"
}
```

Elke request zou "Success!" moeten teruggeven en in phpMyAdmin verschijnen.

## Edge case: Leeg veld

Test ook wat er gebeurt als je een leeg todo stuurt:

```json
{
  "text": ""
}
```

Dit zou "Failure!" moeten geven (vanwege onze validatie in PHP).

---

**Volgende stap**: [Stap 3 - Frontend integratie](./3frontend.md)
