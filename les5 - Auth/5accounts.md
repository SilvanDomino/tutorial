# Accounts
We kunnen nu registreren en inloggen. Ook werken de routes pas als de gebruiker/client een auth/bearer token meestuurt om identiteit aan te tonen. 

De volgende stap is de Todos koppelen aan de gebruiker. 

## Todo Table  aanpassen
Voeg een nieuwe column, `user_id` toe aan de **Todo** table. 

## PHP aanpassen
In de PHP moeten we ook wat dingen aanpassen. We moeten er voor zorgen dat de `user_id` gebruikt wordt in alle onderdelen van de todo.

* In *getTodos.php* gaan we gebruik maken van de `user_id` om te zorgen dat de gebruiker alleen zijn eigen *Todo's* kan inzien.
* In *addTodo.php* maken we gebruik van `user_id` om te zorgen dat elke gemaakte Todo aan de gebruiker gekoppeld is.
* In *editTodos.php* maken we gebruik van `user_id`, om te zorgen dat alleen de **eigenaar** van een *todo* de todo kan aanpassen.

### getTodos.php
Vorige stap hebben we al de **Authentication** gedaan. Alles wordt eigenlijk al gedaan in `check_auth.php`. 

Als je de SQL aanpast naar `"SELECT * FROM todos WHERE user_id = ".$authenticated_user_id` ben je al klaar.

Aantekening: Dit kan veel beter als je de SQL statement prepared. Maar Silvan is niet zo goed in PHP en SQL.

### addTodo.php
Gebruik `check_auth.php` om de `user_id` op te halen. Voeg de *user_id* toe aan de SQL query. 

### editTodo.php
Gebruik `check_auth.php` om de `user_id` op te halen. Je hoeft user_id verder **niet** te gebruiken, want check_auth doet al genog.