# API
Deze stap gaan we onze PHP code schrijven. 
Aan het einde van dit hoofdstuk kunnen we naar [https://127.0.0.1:8080/api/todos.php](http://localhost:8080/api/todos.php) gaan en dan komt ongeveer het volgende er uit:

```json
[
  {
    "text": "Wash dishes",
    "id": "1",
    "status": "todo"
  },
  {
    "text": "Walk pidgeon",
    "id": "2",
    "status": "todo"
  }
]
```
Ik ga er hierbij vanuit dat je de basis beheerst van SQL en PHP, en de basis kent van CRUD (create, read, update delete) operaties. 

1. Maak verbinding met de database    
    * Gebruik mysqli om een verbinding te maken met jouw database.
    * Controleer of de verbinding werkt.
2. Voer een SELECT-query uit     `SELECT * FROM todos`
    * Haal alle todo’s op uit de tabel todos.
3. Zet de resultaten om naar JSON    
    * Gebruik json_encode() om de data om te zetten naar JSON.
    * Zorg dat je een array terugstuurt.
4. Stuur de juiste header mee    
    * Voeg bovenhet terugsturen toe:  `header('Content-Type: application/json');`
