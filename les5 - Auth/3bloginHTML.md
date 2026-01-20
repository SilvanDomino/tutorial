# Login pt 2
Eigenlijk het zelfde als `register.html` alleen dan een andere (php) route.

1. Je vult een wachtwoord in. Je vult een gebruikersnaam in, 
2. Druk op de knop en dit wordt verstuurd naar de server. 
3. De server stuurt dan een JSON bericht terug 
```json
{
  "message": "Login successful",
  "token": "4110f87aed22a1372e54b4895b0a63499c2f1cdb4488f51d87f3d3f3c091f418",
  "expiration": "2026-01-12 17:22:03"
}
```

Het enige verschil is dat we nu iets moeten gaan doen met het antwoord van de server. We hebben een token terug gekregen, deze slaan we op in de cookies.

## Token opslaan in cookies
De token opslaan doen we met de volgende functie:
```js
function setToken(token, expiration){
    document.cookie = `token=${token}; expires=${expiration}; path=/; SameSite=Lax; Secure`
}
```

Probeer het uit. Kijk of je op de website kan inloggen, en dat er dan een token wordt aangemaakt. 


---
Dit is alweer het einde van Stap 3. We kunnen nu inloggen. In de volgende stap gaan we de token gebruiken om te zorgen dat we alleen Todo's kunnen zien als we ingelogd zijn.

