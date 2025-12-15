# Les 3: Todo toevoegen

In deze les gaan we todos **toevoegen** aan onze database. We volgen dezelfde aanpak als in Les 2:
1. **Backend**: PHP route bouwen voor het opslaan van todos
2. **Testen**: De route testen in Postman of Insomnia
3. **Frontend**: JavaScript code schrijven om de form te verbinden met de API

## Overzicht van de stappen

### Stap 1: PHP API Route bouwen
We gaan een `addTodo.php` endpoint maken in `/php/api/` die:
- Een HTTP request ontvangt met de todo-text (in JSON format)
- De todo in de database opslaat (met status "todo")
- Een bevestiging terugstuurt

### Stap 2: Testen in Postman/Insomnia
We testen de route voordat we het in de frontend gebruiken:
- POST request versturen met JSON body
- Response controleren
- Database verificatie
Dit doen we om zeker te weten dat als er straks iets mis gaat, dat het niet aan de backend ligt.

### Stap 3: Frontend integratie
We voegen HTML (en CSS) toe aan de `index.html`
- Textfield input
- Submit knop
Hier hoeven we geen gebruik te maken van een *form*.

We voegen JavaScript toe aan `/src/addTodo.js` die:
- De form-submit event opvangt
- De todo-tekst naar de API stuurt
- De todo list ververst na succes

## Voorbereiding

Zorg dat je het volgende hebt klaargemaakt:

- [ ] Docker containers draaien (`docker-compose up` in `backend/`)
- [ ] Les 2 afgerond (getTodos werkt in je frontend)
- [ ] Postman of Insomnia geïnstalleerd
- [ ] Database/phpMyAdmin toegankelijk op `localhost:8081`



## Wat ga je leren

- POST requests maken (in plaats van GET)
- JSON data versturen naar de backend
- JSON data ontvangen in de backend.
- Data opslaan in de database met PHP
- API routes testen voor je ze in frontend gebruikt
- Form submissions afhandelen in JavaScript


