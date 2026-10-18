# Group Inventory – Firebase-test

Versionsnummeret står øverst til højre i appen. Sammenlign det lokalt og på GitHub Pages for at se, om du kører den nyeste.

- v2.0.0 · Firebase live-synk
- v2.1.0 · Dropdown til flere kampagner
- v2.2.0 · Arkiv og versionsnummer
- v2.3.0 · Google-login, godkendelse af spillere, kun DM-kontoen kan oprette kampagner
- v2.3.1 · Rettet fejl ved oprettelse af kampagne ("child failed: invalid path")
- v2.3.2 · Gendannelse fra backup (Import JSON uden merge) mister ikke længere ting, der var arkiveret i mellemtiden
- v2.4.0 · Spillere & logins (e-mails på forhånd, karakterer pr. spiller, ★ aktiv), "myself" i I am, retired karakterer, hvem er online, Use 1 på forbrugsting, oprydning af GitHub-sync-rester. **Kræver nye regler.**
- v2.4.1 · "use 1" flyttet ud til højre i navnekolonnen, lige før antal
- v2.4.2 · Kolonner centreret, "Quantity" skrevet helt ud, vogn-hjul (☸) som ikon for vehicles
- v2.4.3 · Spillere ser "＋ Join campaign…" i kampagne-dropdownen, kun DM-kontoen ser "Join / create"
- v2.4.4 · Mønter direkte på karakter- og container-siden; mønternes vægt tælles nu med i containerens vægt
- v2.5.0 · Ny fane "Party Overview" (oversigt + redigering af karakterernes stats, som i Campaign maker)

## Filer
- `index.html` – appen
- `items-data.js` – item-kataloget
- `loot_import.json` – kopi af loot-importen, til test (upload den ikke til GitHub)
- `database.rules.json` – sikkerhedsregler til Firebase

## Engangsopsætning i Firebase (v2.3.0)
1. Authentication → Sign-in method → **Google** → slå til, og vælg din e-mail som support-mail → Save.
2. Authentication → Settings → **Authorized domains** → tilføj `<dit-brugernavn>.github.io`.
3. Realtime Database → **Rules** → erstat alt med indholdet af `database.rules.json` → **Publish**.
4. Valgfrit: slå **Anonymous** fra under Sign-in method. Den bruges ikke længere.

Kun tinman4700@gmail.com kan oprette kampagner. Det står både i reglerne og i `OWNER_EMAIL` øverst i Firebase-delen af index.html.

## Sådan virker det
- Google-login virker kun fra web-adressen (GitHub Pages), ikke når filen åbnes direkte fra disken. Uden login kan appen stadig bruges lokalt.
- **DM:** log ind under Settings → Live sync → opret kampagnen → **Copy share link**.
- **Spiller:** åbner linket → **Sign in with Google** → ser "Venter på godkendelse".
- **DM:** får en rød tæller på ☁ → Settings → Live sync → **Approve** eller **Decline**. Spillerens side åbner af sig selv, når de er godkendt.
- DM kan fjerne en spiller igen under "Players with access".
- Kampagner, man er godkendt til, følger ens Google-konto, også på en ny enhed.
- Kampagner fra før v2.3.0 kan ikke åbnes længere. Åbn dem som DM i den browser, der har dataene, og klik **Create a new private campaign from this copy**.

## Spillere & logins (v2.4.0)
- Settings → Characters → **Players & logins**: skriv spillerens navn og Google-mail (og evt. karakter) → **+ Add player**. De kommer ind, så snart de logger ind — uden godkendelse.
- Tilknyt flere karakterer pr. spiller med "+ character". ★ markerer den aktive, som "I am" starter på.
- I "I am" kan spilleren vælge sine egne karakterer eller sig selv ("myself"). DM kan vælge alle og "DM".
- ✕ fjerner spillerens adgang. Spillere der sender en anmodning og bliver godkendt, havner automatisk på listen.

## Mønter i containere (v2.4.4)
- Åbn en karakter eller container under fanen Locations → rækken **Coins** (pp/gp/ep/sp/cp). Skriv antallet, så regner appen selv vægten ud (50 mønter = 1 lb) og lægger den til containerens vægt.
- Ændringer logges. Mønterne indgår stadig i Coins-fanens totaler og kan flyttes med en transaktion dér.
- Vægten tæller kun, når "coin weight" er slået til i Settings.

## Party Overview (v2.5.0)
- Fanen **Party Overview** (efter Settings) viser ét kort pr. aktiv karakter side om side, med samme rækker som Campaign makers Party Overview: Core + Combat, Passive Scores, Abilities & Saves, Skills, Languages & Tools — plus **Inventory** (båret vægt, antal ting, mønter).
- **Overview / Edit** øverst. I Edit vælger man karakter til venstre og udfylder stats; det gemmes, så snart man forlader feltet, og synkroniseres live. "✎ Edit" på et kort springer direkte dertil.
- Modifier regnes ud fra ability score, og saves udfyldes automatisk (+ prof. bonus når "Prof." er sat). STR er det samme felt som STR under Characters (bæreevne).
- **Display Options** (foldet sammen): vælg hvilke grupper og hvilke karakterer ("Players here today") der vises. Huskes pr. browser og pr. kampagne.
- Retired karakterer vises ikke.
- Skjul fanen: Settings → Rules & browser → **Party rules** (for alle i kampagnen) eller **This browser** (kun dig).

## Retired karakterer
- Settings → Characters → Status: **Retired** (død, forladt gruppen…). Skjules fra lister, men log, arkiv og det de bærer bevares. Bærer de stadig noget, vises de nedtonet i chips, så det kan flyttes.

## Hvem er online
- Små runde ikoner i headeren viser hvem der har siden åben. Hold musen over for navne og hvem de er "som".

## Use 1
- Potions, scrolls, ammunition (eller tag "consumable") har en **use 1**-knap. Den lægger én i arkivet som "Used up" af den aktive karakter. Flere brug i træk samles i samme arkiv-post.

## Flere kampagner
- Settings → Live sync viser **My campaigns**. Med to eller flere kampagner bliver navnet øverst til venstre en dropdown.
- "I am" og den lokale kopi huskes for hver kampagne.
- **Remove** fjerner kun kampagnen fra din liste. Selve kampagnen slettes ikke.

## Arkiv
- På et item-kort: **Archive** (fold ud) → vælg antal, årsag, hvem og evt. note.
- Arkiverede ting forsvinder fra inventaret, vægt og totaler, men intet går tabt. Se fanen **Archive**.
- Del af en stak: ved **Reactivate** til samme sted lægges de oven i stakken igen.
- Containere: indholdet kan falde ud til den, der bar den, eller arkiveres sammen med den.
- Loggen og hvert korts **History** viser tingens forløb.
