# Gamify: læringsspill for elektro og datateknologi

Dette prosjektet består av enkle, interaktive HTML-spill for elever på videregående skole, spesielt innen elektro og datateknologi. Spillene trener sentrale ferdigheter gjennom korte oppgaver, umiddelbar tilbakemelding og gradvis høyere vanskelighetsgrad.

Alle spillene er selvstendige HTML-filer. De bruker HTML, CSS og JavaScript som ligger direkte i hver fil, og krever ingen installasjon, server eller eksterne biblioteker.

## Spillene

| Fil | Tema | Kort beskrivelse |
| --- | --- | --- |
| `kretsMester.html` | Ohms lov og grunnleggende kretsberegning | Oppgaver i Ohms lov, serie- og parallellkoblinger, Kirchhoffs lover og mer avanserte kretsnettverk. |
| `kretsMesterBM.html` | Kretsberegning: BEAST MODE | En videre utfordring med blant annet effekt, flere parallelle grener, indre motstand, superposisjon og Wheatstone-bro. |
| `milliGame.html` | SI-prefikser og enhetskonvertering | Trening på kilo, milli, mega, mikro, nano og piko med enhetene V, A, W og Ω. |
| `TallTreneren.html` | Binær, heksadesimal og desimal | Konvertering mellom 4-bit og 8-bit binærtall, heksadesimale tall og desimaltall. |
| `effektMester.html` | Effektfaktor, vekselstrøm og motorberegninger | Interaktivt spill med innebygd Vg1- og Vg2-modus, simuleringer, effekttrekant ($P, Q, S$), $\cos\varphi$, virkningsgrad ($\eta$) og fasekompensering. |
| `Medikamentregning/medikamentProven.html` | Klinisk medikamentregning | Nivåbasert trening i doser, enheter, væske, pediatri, infusjon, fortynning og sprøytepumper. |

## Pedagogisk innhold

Spillene er laget for å øve på kompetanse som er relevant i elektrofag og datateknologi:

- bruke Ohms lov: `U = R · I`
- beregne totalresistans og strøm i serie- og parallellkoblinger
- bruke Kirchhoffs spenningslov (KVL) og strømlov (KCL)
- forstå elektrisk effekt: `P = U · I`, effektivverdier og vekselspenning
- mestre effekttrekanten: aktiv effekt ($P_t$), reaktiv effekt ($Q$) og tilsynelatende effekt ($S$)
- forstå effektfaktoren ($\cos\varphi$), faseforskyvning og retureffekt
- beregne 1-fasede og 3-fasede asynkronmotorer, virkningsgrad ($\eta$) og avgitt/tilført effekt
- dimensjonere fasekompensering med kondensatorer og redusere nettselskapets overføringstap
- konvertere mellom måleenheter og SI-prefikser
- lese og konvertere mellom binær-, heksa- og desimaltall
- arbeide nøyaktig med enheter, fortegn og avrunding

## Slik starter du

1. Last ned eller klon prosjektet.
2. Åpne en av HTML-filene i en moderne nettleser.
3. Les oppgaven, skriv inn svaret og trykk **Sjekk svar**.
4. Bruk **Hjelp** når du trenger en forklaring eller et eksempel.

Filene kan også åpnes direkte fra VS Code med nettleserens «Open with»-funksjon eller ved å dobbeltklikke på filen i Filutforsker.

## Spillmekanikk

- Oppgavene genereres automatisk, slik at elevene får nye tall og kombinasjoner.
- Riktige svar bygger en rekke med riktige besvarelser.
- Neste nivå låses opp etter nødvendig antall riktige svar på rad.
- Ved feil vises fasit, mellomregning og en forklaring som kan brukes til egenretting.
- **Save Game med personlig hash, navnelås og utlogging** (i `effektMester.html`): Eleven kan oppgi sitt navn og generere en unik, saltet lagringskode (f.eks. `EM-L4-938124E8`). Ved å oppgi navnet og koden kan eleven fortsette der de slapp på en hvilken som helst enhet. Navnet låses til spilløkten og diplomet for å hindre juks. En egen «🚪 Logg ut / Start fra scratch»-knapp i statuslinjen og lagringsmenyen gjør det enkelt å tømme økten og nullstille maskinen for neste elev.
- **Permanent nivåminne og stjernebevaring** (i `effektMester.html`): Nivåer som er fullført merkes med `✅` på nivåknappene og husker sine 5/5 stjerner permanent når man navigerer frem og tilbake mellom nivåene. Eleven kan også fritt repetere og øve på allerede beståtte nivåer uten å miste stjernene sine. Ved innlasting med navn og hash-kode markeres alle forutgående nivåer automatisk som bestått med 5 stjerner.
- **Skjult hint med beskyttet rekke** (i `effektMester.html`): Hint er skjult bak en knapp («💡 Vis hint»). Å svare riktig med aktivt hint gir ingen ny stjerne på rekken («5 på rad»), men rekken beholdes uendret i stedet for å nullstilles. Feil svar nullstiller rekken som vanlig.
- **Faglige læringsressurser (NDLA & animerte videoer)** (i `effektMester.html`): Hvert nivå inneholder direkte lenker til relevante artikler på NDLA (Ohms lov, faseforskyvning, effekttrekant, motorberegning og fasekompensering) samt pedagogiske 3D-animerte YouTube-forklaringer med tidsstempler (Prof MAD) i teorikortet, teorioversikten og ved feil svar for målrettet repetisjon.
- **Hemmelig lærermeny** (i spillene, `Ctrl + Shift + K` eller `Ctrl + Alt + K`, evt. 7 klikk på logoen): Eget diagnosepanel for læreren for hurtigtesting. Lar deg hoppe direkte til et hvilket som helst nivå, bytte modus, se og auto-utfylle fasit for aktiv oppgave, hoppe over oppgaver, øke streeken, trigge nivåfullføring og åpne diplomene direkte.
- Ved fullført progresjon kan eleven få et digitalt diplom som kan skrives ut eller lagres som PDF.

## Forslag til bruk i undervisningen

Spillene kan brukes individuelt som oppvarming, repetisjon eller egenvurdering. De egner seg også som stasjonsaktivitet eller som en kort konkurranse mellom elever. Lærer kan be elevene forklare framgangsmåten, ikke bare oppgi svaret, for å koble spilltreningen til praktisk feilsøking og dokumentasjon.

En naturlig progresjon er:

1. `milliGame.html` og `TallTreneren.html` for enheter og tallforståelse.
2. `kretsMester.html` for grunnleggende kretsberegning.
3. `kretsMesterBM.html` for elever som trenger større faglige utfordringer.
4. `effektMester.html` for vekselstrøm, effekttrekant, motorer og fasekompensering.

## Teknisk informasjon

- Språk: HTML, CSS og JavaScript
- Språk i brukergrensesnittet: norsk (`lang="no"`)
- Responsivt grensesnitt som kan brukes på PC, nettbrett og mobil
- Ingen npm-pakker, byggeverktøy eller eksterne avhengigheter
- Ingen backend eller database

Prosjektet er dermed enkelt å dele, bruke offline og tilpasse. Nye oppgaver, nivåer og forklaringer kan legges til direkte i den aktuelle HTML-filen.

## Lisens og videre utvikling

Det er ikke lagt inn en egen lisens i prosjektet ennå. Legg til en lisensfil dersom prosjektet skal deles offentlig eller videreutvikles av flere.

Mulige videre utvidelser er lagring av resultat og progresjon, lærerrapport med statistikk, flere oppgavetyper og en felles startside som lenker til alle spillene.