## Tables
Maak 2 tables aan in de Todo database.

* Users     
    In deze table komen alle gebruikers met (gehasht) wachtwoord. 
    * **id**        *(int)*
    * **username**  *(varchar(32))*
    * **password**  *(varchar(255))*
* Tokens
    * **id**                *(int)*
    * **userID**            *(int)*     
    User ID is een referentie naar de ID van de user. Een user kan zo meerdere Tokens hebben.
    * **token**             *(varchar(255))*
    * **expiration_date**   *(datetime)*

