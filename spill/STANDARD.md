# Gamify spillpakke

Dette er den ferdig testede spillpakken. Originalfilene i foreldremappen er beholdt separat.

## Omfang

Spillpakken inneholder:

- `TallTreneren.html`
- `milliGame.html`
- `kretsMester.html`
- `kretsMesterBM.html`
- `effektMester.html`
- `sikringsMester.html`
- `kursBeregneren.html`
- `kretsSymbolerLegend.html`

## Prinsipper

1. Hver HTML-fil skal fortsatt kunne åpnes direkte og fungere selvstendig.
2. Felles brukerflyt skal være gjenkjennelig på tvers av spillene.
3. Spillene skal beholde egen karakter gjennom tema, farger, simulatorer og grafer.
4. Kretsdiagrammer og symboler skal følge `kretsSymbolerLegend.html`.
5. Nye symboler skal først beskrives eller korrigeres i legenden, og deretter brukes i spillene.
6. Lokal lagring skal være enkel progresjonslagring på samme enhet.
7. Hash, salt, navnelås, sikkerhets-ID og skjult juksemarkering skal ikke være del av den nye standarden.
8. Et feil svar skal støtte læring: vis forklaring og gi en tydelig vei videre eller nytt forsøk.

## Felles spillramme

Spill som har nivåprogresjon skal normalt ha:

- toppfelt med navn og hjelpetilgang
- nivå- og progresjonslinje
- oppgaveområde
- svarområde
- feedbackområde
- teori-/hjelpemodal
- enkel nullstilling
- lokal lagring av progresjon
- utskriftsvennlig diplom når det passer spillet

Beregningsverktøy som `kursBeregneren.html` kan beholde en arbeidsflyt uten streak og nivåer, men skal bruke samme visuelle grunnregler og modal-/knappemønster.

## Temaer

Felles struktur betyr ikke likt utseende:

- `TallTreneren.html`: tydelig tall- og tastaturfokus
- `milliGame.html`: lett og presis enhetskonvertering
- `kretsMester.html`: lys og pedagogisk kretsanalyse
- `kretsMesterBM.html`: mørk og intensiv avansert analyse
- `effektMester.html`: teknisk simulator- og grafpreg
- `sikringsMester.html`: vern, sikkerhet og installasjonsfag
- `kursBeregneren.html`: dokumentasjon og kontrollskjema

## Lagringsmodell

Ny lagring skal være lesbar og lokal, for eksempel:

```js
{
    level: 1,
    streak: 0,
    completedLevels: [],
    playerName: ""
}
```

Lagringen skal ikke presenteres som sikkerhet eller vurderingsbevis. Den skal kun gjøre det mulig å fortsette på samme enhet.

## Migreringsrekkefølge

1. `TallTreneren.html` - migrert og testet
2. `milliGame.html` - migrert og testet
3. `kretsMester.html` - migrert og testet
4. `kretsMesterBM.html` - migrert og testet
5. `effektMester.html` - migrert og testet
6. `sikringsMester.html` - migrert og testet
7. `kursBeregneren.html` - kontrollert som beregningsverktøy
8. `index.html` - portal for spillpakken

## Status

`spill/TallTreneren.html` bruker lokal progresjonslagring med nivå, streak og valgfritt navn. Hash, lagringskode, navnelås, sikkerhets-ID og juksemarkering er fjernet. Oppgavegenerator, tastatur, teori, simulatorfri layout og diplomflyt er beholdt.

`spill/milliGame.html` bruker samme lokale lagringsmodell. Prefiks-, enhets- og avrundingslogikken er beholdt.

`spill/kretsMester.html` og `spill/kretsMesterBM.html` bruker lokal progresjonslagring med hvert sitt tema. Kretsgeneratorer, retningstaster, nivåteori og symbolrendering er beholdt.

`spill/effektMester.html` bruker lokal lagring som også bevarer Vg1/Vg2-modus, fullførte nivåer, per-nivå streaks, total løsningsmengde og aktiv progresjon. Simulatorer, lyd, hint og teorimateriell er beholdt.

`spill/sikringsMester.html` bruker samme rike lokale progresjonsmodell som EffektMesteren, med modus, fullførte nivåer og nivåstreaks. Simulatorer, fagordforklaringer og beregningsoppgaver er beholdt.

`spill/kursBeregneren.html` har ingen elev-/hashlagring og er derfor beholdt som et selvstendig beregnings- og utskriftsverktøy. JavaScript-syntaksen er kontrollert.

## Kvalitetssjekk per fil

- åpner direkte som lokal HTML
- ingen JavaScript-feil ved oppstart
- oppgave og svarflyt fungerer
- feil svar gir relevant forklaring
- nivå/progresjon oppdateres riktig
- refresh gjenoppretter lagret progresjon
- nullstilling fjerner lokal progresjon
- modal kan lukkes med Escape
- mobilbredde fungerer uten skjult innhold
- eksisterende simulatorer og grafer er bevart
- kretsdiagrammer følger symbolstandarden
