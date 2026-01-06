# Stap 3: Frontend integratie

Nu gaan we JavaScript code schrijven om de frontend te verbinden met de `addTodo.php` API.
De bedoeling is dat je Todo afgevinkt wordt als we er op klikken.

## Javascript
In principe hoeven we geen HTML te schrijven, we gaan de TODO status aanpassen als we op de Todo klikken. 

Dit gaan we doen in de **Todo Class**. 

### De event
Maak in de Todo class een nieuwe (async) functie aan
```js
onClickEvent = async () =>{
    console.log("Edit Todo");
}
```

Hang de event aan het htmlElement. 

```js
    this.htmlElement.addEventListener('click', this.onClickEvent);
```

en probeer maar uit! Als het goed is kan je nu klikken en dan werkt de click event.

### De PATCH request
Als het goed is heb je nu alle kennis en ervaring die je nodig hebt voor de PATCH request.

* Je weet hoe je fetch moet gebruiken
* Je weet hoe je de options moet aanpassen en meegeven
* Je weet hoe je de errors kan afvangen.
* Je weet hoe je de lijst kan refreshen.

Je mag nu zelf uitzoeken hoe je de Todo kan updaten.