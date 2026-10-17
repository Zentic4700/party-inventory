# Group Inventory – Firebase-test

Versionsnummeret står øverst til højre i appen (fx v2.2.0). Sammenlign det lokalt og på GitHub Pages for at se, om du kører den nyeste.

- v2.0.0 · Firebase live-synk
- v2.1.0 · Dropdown til flere kampagner
- v2.2.0 · Arkiv og versionsnummer

Kopi af group_inventory.html med live-synk via Firebase Realtime Database i stedet for GitHub.
Den gamle version i mappen ovenover er urørt, og de to bruger hver sin browser-lagring, så de ikke blander data.

## Filer
- `index.html` – appen
- `items-data.js` – item-kataloget (kopi)
- `loot_import.json` – kopi af dit loot-import, til test
- `database.rules.json` – sikkerhedsregler til Firebase

## Engangsopsætning i Firebase
1. Realtime Database → fanen **Rules** → indsæt indholdet af `database.rules.json` → **Publish**.
2. Authentication → Sign-in method → **Anonymous** skal være slået til.

## Kom i gang
1. Åbn `index.html` → Settings → **Live sync** → **Create a new campaign**.
   (Vil du starte med loot-dataen: Settings → Data → Import JSON… → `loot_import.json` først.)
2. Klik **Copy share link** og send linket til spillerne. Linket indeholder kampagnekoden (`?c=...`).
   Til spillerne skal siden ligge online, fx på GitHub Pages sammen med `items-data.js`.

## Sådan virker det
- Ændringer gemmes med det samme, felt for felt. To spillere kan rette samme genstand samtidig, så længe det er forskellige felter.
- Antal og mønter gemmes som ændringer (+5 gp, −1), så samtidige betalinger begge tæller.
- Mister man forbindelsen, gemmes ændringer og sendes, når man er online igen (så længe fanen er åben).
- Kampagnekoden er nøglen: alle med linket kan læse og rette. Del den kun med gruppen.

## Flere kampagner
- Settings → Live sync viser **My campaigns**. Her kan du oprette, joine, åbne og fjerne kampagner.
- Med to eller flere kampagner bliver kampagnenavnet øverst til venstre en dropdown, så du kan skifte hurtigt.
- "I am" og den lokale kopi huskes for hver kampagne.
- **Remove** fjerner kun kampagnen fra din liste. Selve kampagnen i Firebase slettes ikke.

## Arkiv
- På et item-kort: **Archive** (fold ud) → vælg antal, årsag (til karakterark, solgt, mistet, brugt op, ødelagt, givet væk, andet), hvem og evt. note.
- Arkiverede ting forsvinder fra inventaret, vægt og totaler, men intet går tabt. De ligger under fanen **Archive**, hvor de kan søges og filtreres.
- Del af en stak: arkivér fx 3 af 10. Ved **Reactivate** til samme sted lægges de oven i stakken igen.
- Containere: vælg om indholdet falder ud til den, der bar den, eller arkiveres sammen med den. Mønter i containeren går til Party Fund.
- Loggen registrerer "Archived" og "Returned", og hvert kort har en **History**-sektion med tingens forløb.
- Flere valgte ting kan arkiveres på én gang fra bulk-linjen i inventaret.
