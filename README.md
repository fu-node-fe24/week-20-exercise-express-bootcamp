# Vecka 20: Express Bootcamp

## Grunder

### Övning 1 - Express-template

1. Skapa upp en enkel Node.js applikation genom att köra ```npm init -y``` i terminalen.
2. Installera *express* och *nodemon* genom att köra ```npm i express nodemon``` i terminalen.
3. Konfigurera din **package.json** fil. Lägg till ```"type" : "module"```, samt skapa ett nytt script genom att lägga till ```"dev" : "nodemon [filnamn]"``` under *scripts*.
4. Skape filen *server.js* och skriv in koden nedan. Detta kan fungera som ett template för alla dina express-applikationer.
```
import express from 'express';

const app = express(); // Detta skapar upp en express-applikation
const PORT = 8080;

app.listen(PORT, () => {
    console.log(`Server is running on port ${PORT}`);
});
```
5. Starta din utvecklingsserver och titta i terminalen. Du bör nu se ```Server is running on port 8080```.

### Övning 2 - HTTP-anrop

Följande övningar testar ni med hjälp av insomnia. När er utvecklingsserver är igång så når ni den på ```https://localhost:8080```, följt utav de endpoints ni skapar upp (ex "/hello").

1. Skapa ett GET-anrop mot endpointen */hello*. Logga ut ett meddelande i konsollen, och i ditt response skickar du med ett hälsningsmeddelande.
2. Skapa ett POST anrop mot endpointen */hello*, i anropets body kommer ett namn skickas med. Läs in namnet i koden och i ditt response skickar du med en hälsning till namnet som angavs. Tips: leta efter namnet i *req.body*.
3. Skapa ett GET-anrop mot endpointen */hello* där man kan skicka med *query parametrar* ex. ```?name=Jesper``` i url:en. Läs in namnet i koden och i ditt response skickar du med en hälsning till namnet som angavs. Tips: leta efter namnet i *req.query*.
4. Skapa en egen modul i filen *greeting.js*. Här skapar du en funktion som tar emot ett namn och som returnerar en hälsning innehållandes namnet. Exportera modulen, och importera den i din *server.js*. Använd nu modulen för att returnera hälsningen i uppgift 2 och 3.
5. Skapa ett POST-anrop mot endpointen */sum*, i anropets body kommer två tal skickas med ex. ```{ "a": 5, "b": 8 }```. Läs in talen och skicka tillbaks summan i ditt response.
6. Skapa ett GET-anrop mot endpointen */color/:color*, där man i anropet ersätter ```:color``` med en faktisk färg. Läs in den angivna färgen och skicka meddelandet "Din favoritfärg är [färg]" i responset.
7. Skapa ett POST-anrop mot endpointen */feedback*, där man i anropets body skickar med ett objekt med nycklarna *name* och *message*. Anropet skall sedan returnera ```Tack {name} för din feedback: "{message}"```, ex. "Tack Jesper  för din feedback: "Dålig genomgång!"".

## API Grunder

För följande övningar behöver du skapa en ny mapp som heter data. I den mappen skapar du filen pokemons.js där du klistrar in innehållet från [den här filen](). Importera sedan filen i din *server.js*-fil. Alla dina anrop skall nu starta med endpointen */pokemons*.
Försök även göra dina responses lite med "API:iga" (likt de svar v själva fått när vi anropat APIer).

1. Skapa ett GET-anrop som returnerar ALLA pokemons.
2. Skapa ett GET-anrop mot */pokemons/random* som returnerar en slumpad pokemon.
3. Skapa ett GET-anrop som tar emot query parametern *name*, och som returnerar alla pokemons som har den strängen i sitt namn.
4. Skapa ett GET-anrop mot */pokemons/:id* där du returnerar pokmonen med motsvarande ID.
5. Skapa ett POST-anrop där du skickar in nyckeln *type* innehållandet en type, och som returnerar alla pokemons med den angivna typen.
6. Skapa ett GET-anrop mot */pokemons/stats* där man även kan lägga till query parametern *total*, ex. ```/pokemons/stats?total=470```. Anropet skall sedan returnera alla pokemons som har mer än 470 i total base stat.

### Pagination Levelup!

Om användaren gör ett anrop mot */pokemons* och skickar med query parametrar för *offset* och *limit* och limit så skall ni endast returnera enligt dessa. Ex. om vi har en endpoint som ser ut enligt följande: ```/pokemons?offset=5&limit=5``` så returneras pokemon 6-10 då offset anger startpunkten, och limit antalet som önskas.

### Pagination Levelup 2!

Returnera även nyckeln *next* där användaren hittar "nästa sida". Ex. om användaren angett url:en ovan så hittar man även i svaret ```"next" : "/pokemons?offset=10&limit=5"``` osv. 
