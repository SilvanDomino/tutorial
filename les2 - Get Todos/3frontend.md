# Frontend
Nu gaan we de frontend bouwen. Dit doen we op een klein beetje een andere manier. We gaan gebruik maken van Javascript **OOP**.

1. Haal de default vite code weg. Laat de bestanden wel staan.
    * Gaat vooral om `main.js` en `style.css`.
2.	Pas de HTML aan. Maak een leuke en eenvoudige HTML pagina met de todo’s in een (unsorted) list.
    * Maak ook de CSS. Gebruik hier **geen** *AI* voor. 

## OOP
[Video (over de voorbereiding)](https://mediacollegeamsterdam.sharepoint.com/:v:/r/teams/BeroepsvakkenC24/Gedeelde%20documenten/Skills/M6%20Todo/Les%202%20Videos/API1%20Voorbereiding.mp4?csf=1&web=1&e=t8K3rU)      
Dit project gaan we gebruik maken van **OOP** *javascript*. We gaan Object Oriented Programmeren. Dankzij OOP krijgt onze code een duidelijkere *structuur* en *opbouw*. Daarvoor gaan we 2 **classes** maken:
* TodoList
* Todo

Elke TodoList die we hebben is een instantie van de TodoList class. Elke Todo die we hebben is een instantie van de Todo class.

## Todo
[Video (over maken todo)](https://mediacollegeamsterdam.sharepoint.com/:v:/r/teams/BeroepsvakkenC24/Gedeelde%20documenten/Skills/M6%20Todo/Les%202%20Videos/API2%20Todo.mp4?csf=1&web=1&e=Trbczc)      
Todo is de class die bepaalt hoe onze Todo aangemaakt wordt. Ook kunnen we hier alle functionaliteit definieeren van de Todo

Een **class** maak je met het `class` keyword. 
```js
class Todo{

}
```

### Constructor
De constructor is de functie die uitgevoerd wordt zodra er een instantie wordt gemaakt van de class. Meer uitleg hier over gebeurt **in de les**. 

In de *class* zet de volgende code.
```js
constructor(text, root){
    this.data = data;
    this.root = root;
}
```
Bij het aanmaken van het object geven we 2 dingen mee:
* De text van de Todo
* Het html element waarin de Todo komt te staan.

## TodoList
[Video (over maken TodoList)](https://mediacollegeamsterdam.sharepoint.com/:v:/r/teams/BeroepsvakkenC24/Gedeelde%20documenten/Skills/M6%20Todo/Les%202%20Videos/API3%20TodoList.mp4?csf=1&web=1&e=tnzFGD)     
TodoList is een class die al onze Todo's bijhoudt, en ook de todo's ophaalt uit onze API. 

Wanneer onze frontend een verzoek doet naar de API, krijgen we een error. Dit heeft te maken met CORS. Dit gaan we volgend hoofdstuk oplossen.