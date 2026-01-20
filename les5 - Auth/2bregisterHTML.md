# Registratie pt2
Om te kunnen registreren moeten we twee stukken schrijven.

* De registratie route (register.php)
* De HTML pagina
    * Met javascript

De route hebben we vorig hoofdstuk gemaakt. Dit hoofdstuk gaan we de *HTML pagina* en *javascript* schrijven. Dit ga je **zelfstandig doen**

## HTML pagina
Voor de HTML pagina heb je *drie* dingen nodig om te kunnen registreren.
* Input field voor de username
* Input field voor het wachtwoord
* Knop om het registreren te activeren.

## Javascript
Maak een bestand aan, `registration.js`. In dit bestand gaan we een HTTP request versturen naar onze *register route* (register.php).

1. Maak een functie `register()` in de *registration.js* script. 
2. Haal de username en wachtwoord op uit de HTML pagina. Bijvoorbeeld zo: `const username = document.querySelector("#username").value;`
3. Maak de options voor de POST request. 
    * Kijk als voorbeeld hoe je dat bij *editTodos* stap hebt gedaan vorige les.
    * De options heeft een method eigenschap, headers, en de body.
4. Voer de fetch uit.
5. Print het resultaat van de fetch uit naar de console.
5. Koppel de functie aan de knop.