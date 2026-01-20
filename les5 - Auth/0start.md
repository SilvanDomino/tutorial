# Authorization
Bij de Authorization stap willen we een heleboel doen. Het einddoel is uiteindelijk dat we kunnen *registreren* en *inloggen*. Iedere user heeft dan een **eigen lijst** van Todo's. 

Om dit voor elkaar te krijgen moeten we veel grote stappen zetten.

## Stappen
1) Tables opzetten
    * Users
    * Tokens

    We gaan de nodige tables aanmaken. Een table voor de users en een table voor de tokens.
2) Registreren
    * PHP
        * User en password in de database.
    * Testen met Insomnia of Postman
    * HTML en javascript
        * Register.html
        * POST Request
    
    We gaan een registratie formulier maken en de route om de registratie te implementeren. Aan het einde van de stap kan een gebruiker zich registreren. Het formulier ga je (redelijk) zelfstandig maken met de kennis van de vorige lessen.
3) Log in
    * PHP
        * Gebruikernaam en wachtwoord vergelijken
        * Token aanmaken, opslaan en terug geven
    * Testen met Insomna of Postman
    * HTML en Javascript
        * login.html
        * POST request maken
        * Token terug krijgen en opslaan

    We gaan een login formulier maken. Ook de achterkant van het inloggen werkt.
4) Authenticatie
    * PHP aanpassen. Gebruiker krijgt alleen toegang als hij een auth token heeft.
        * (Get) Todos
        * AddTodo
        * Edit Todo
    * Javascript
        * Auth token meegeven
5) Accounts
    * Database aanpassen
        * User ID's toevoegen bij Todos
    * PHP aanpassen. 
        * Gebruiker krijgt alleen zijn Todos uit (get)todos.php
        * Gebruiker geeft user id mee bij maken van todo. 
