# Stap 3: Frontend integratie

Nu gaan we JavaScript en HTML code schrijven om de frontend te verbinden met de `addTodo.php` route van de API.

## HTML form (index.html)

Zorg dat je HTML een input field en knop hebt:

```html
<div id="input-wrapper">
    <input type="text" id="todo-input" placeholder="Voer een nieuw todo in...">
    <button id="todo-add">Toevoegen</button>
</div>

<ul id="todoList"></ul>
```

De IDs zijn belangrijk:
- `#todo-input` - het input veld
- `#todo-add` - de add-knop
- `#todoList` - de ul waar todos verschijnen

## JavaScript: addTodo() functie

Nu voegen we JavaScript toe in `src/addTodo.js`:

### Basis structuur

```javascript
export async function addTodo() {
    const text = document.querySelector("#todo-input").value;

    const response = await fetch('http://localhost:8080/api/addTodo.php');
    if(response.ok != true){
        throw new Error("Response status: " + response.status);
    } else{
        const data = await response.text();
        // TODO: refresh todo list
    }
    

}
```

We maken een basis fetch request naar de `addTodos.php`, en vangen de eventuele errors op!

### Options
Maar hoe weet de javascript dat dit een POST request moet zijn? Of wat de text is van de Todo? Dit moeten we nog mee geven, en dat doen we als tweede argument in de **fetch** request. 
```js
const options = {
    method: 'POST',
    headers: {
        'Content-Type': 'application/json'
    },
    body: JSON.stringify({ text: text })
}
```
Zet de bovenstaande code boven de fetch request (liefst wel in de addTodo functie).

Pas de fetch request aan om ook de options mee te geven. 
```js
const response = await fetch('http://localhost:8080/api/addTodo.php', options);
```

### De functie toevoegen aan de knop.
Om de functie toe te voegen aan de knop moeten we werken in `main.js`. Importeer de `addTodo` functie boven in main.js, *net zoals je hebt gedaan met TodoList*.
```js
const button = document.querySelector("#todo-add");
button.addEventListener("click", ()=>addTodo());
```

Als je verder niets van plan bent om met de button te doen, dan kan je ook leuk zijn en deze twee regels gaan combineren. Maar het is wel een stuk minder fijn leesbaar.
```js
document.querySelector("#todo-add").addEventListener("click", ()=>addTodo());
```

We pakken de button. En voegen de functie aan de **click** *event* van de button.

## De Todolist refreshen
We hebben een nieuwe Todo toegevoegd, alleen om dit te zien, moeten we de todolist eerst refreshen. Als we dit willen doen hebben we in de todoList een referentie nodig naar ons `todoList` *instantie*. 

Dit kunnen we doen door de *instantie* van todoList mee te geven aan de *addTodo* functie. Pas de `addTodo` functie aan, en zorg dat deze een argument vraagt.
```js
//addTodo.js
export async function addTodo(todoList) {
```

Vervolgens geven we de *todoList* mee aan de functie.
```js
//main js
let todoList = new TodoList();
const button = document.querySelector("#todo-add");
button.addEventListener("click", ()=>addTodo(todoList));
```

Voeg de volgende regel uit wanneer je de **todo** ***succesvol*** hebt toegevoegd aan de database. Doe dit in de **TodoList** class.
```js
    todolist.getTodos();
```

## Samenvatting

We hebben:
- PHP route gebouwd (`addTodo.php`)
- API getest in Insomnia
- JavaScript functie geschreven (`addTodo()`)
- Todo list gerefresht na toevoegen

Je frontend kan nu todos **toevoegen** en ze verschijnen **direct** in de database en UI!

---

**Volgende**: Editen en verwijderen van todos (volgende les!)
