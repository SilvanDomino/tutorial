# Cross Origin Resource Sharing
Cors is de vijand van veel front en backend developers. CORS bepaald namelijk of resources gedeelt worden en met welke websites.

CORS is een beveiligingsmechanisme dat is ingebouwd in moderne webbrowsers. Het bepaalt of webpagina's die afkomstig zijn van één domein (de origin of oorsprong) toegang mogen vragen tot bronnen (zoals data of API's) van een ander domein.

Stel je voor dat je een website hebt op mijnwebsite.com en deze probeert gegevens op te halen van een API op gegevensbank.com. Dit is een "cross-origin" verzoek, omdat de domeinen verschillend zijn.

## Tldr
Onze backend krijgt op dit moment een verzoek van een website genaamd ??? en neemt niet eens op. Doet iedereen als die gebeld wordt door een onbekend nummer.

```php
header("Access-Control-Allow-Origin: http://localhost:5173");
header("Access-Control-Allow-Methods: GET, POST, PUT, DELETE, OPTIONS");
```
Zet de volgende regels code boven in de **gettodos.php**