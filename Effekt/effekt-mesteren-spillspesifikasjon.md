# PROMPTING- OG SPESIFIKASJONSDOKUMENT FOR ANTIGRAVITY
## Prosjekt: EffektMesteren (`effektMester.html`)
### Et interaktivt, nivåbasert HTML5-læringsspill om Faseforskyvning, Effekttrekant og Motorberegninger

---

## 1. PROSJEKTOVERSIKT & TEKNISK RAMMEVERK

Dette dokumentet inneholder den komplette spesifikasjonen og kildekodeinstruksjonen for å utvikle spillet **`effektMester.html`** i **Gamify**-repoet (`github.com/FreyBear/Gamify`).

### 1.1 Formål og Målgruppe
* **Målgruppe:** Elever innen Elektro og datateknologi (både Vg1 og Vg2 Elenergi og ekom / Automatisering) som arbeider med vekselstrøm, effekttrekant, motorer og fasekompensering.
* **Pedagogisk mål:** Gi elevene en dyp, intuitiv og beregningsmessig kontroll på:
  1. Vekselspenning, effektivverdier og faseforskyvning (selvinduksjon).
  2. Effekttrekanten (Aktiv $P_t$, Reaktiv $Q$, og Tilsynelatende effekt $S$).
  3. Trigonometri og effektfaktor ($\cos\varphi$).
  4. Motorberegninger for 1-fasede og 3-fasede asynkronmotorer.
  5. Motorens virkningsgrad ($\eta$) og avgitt effekt ($P_a$) kontra tilført effekt ($P_t$).
  6. Praktisk og økonomisk betydning av fasekompensering med kondensatorer.

### 1.2 Krav til Kode og Teknisk Stack
* **Enkeltfil-arkitektur:** Hele spillet skal ligge i en ren `.html`-fil (`effektMester.html`).
* **Ingen eksterne avhengigheter:** 0 npm-pakker, 0 eksterne CSS/JS-biblioteker, ingen CDN-lenker. Rent JavaScript (ES6+), HTML5 og CSS3.
* **Full Offline-støtte:** Spillet skal fungere 100 % lokalt ved å dobbeltklikke på HTML-filen i filutforskeren eller åpne den i VS Code.
* **Responsivt Design:** Vises universelt på PC, nettbrett og mobil med moderne CSS Grid og Flexbox.
* **UI-Språk:** Norsk (bokmål) (`lang="no"`).

---

## 2. SPILLMEKANIKK & PEDAGOGISK STRUKTUR

I tråd med Gamify-rammeverket bygges spillet rundt en **nivåbasert progresjon**, utvidet med **mikrolæring og interaktive simuleringer** før hver testsekvens.

```
+-------------------------------------------------------------------------+
|                         NIVÅPROGRESJON (1 til 6)                        |
|                                                                         |
|  +---------------------+   +-----------------------+   +-------------+  |
|  | Fase A: Teorikort   |-->| Fase B: Interaktiv    |-->| Fase C:     |  |
|  | (Begrepsforståelse) |   |    Simulering/Canvas  |   | 5 På Rad    |  |
|  +---------------------+   +-----------------------+   +-------------+  |
+-------------------------------------------------------------------------+
```

### 2.1 Tre-faset Nivåstruktur (A, B, C)
For hvert av de 6 nivåene gjennomgår eleven følgende tre faser:

1. **Fase A: Læringskort (Mikrolæring)**
   * Korte, presise tekstblokker som forklarer *hvorfor* fysikken/elektroteknikken oppfører seg som den gjør.
   * Formelboks med uthevede NDLA-formler og enheter ($W$, $var$, $VA$, $\eta$).
2. **Fase B: Interaktiv Simulering (Sandkasse)**
   * Hvert nivå inneholder et visuelt HTML5 Canvas-element eller interaktiv grafikk der eleven selv kan justere variabler (sliders/knapper) for å observere sammenhengene visuelt.
3. **Fase C: Spillutfordring ("5 På Rad")**
   * Automatisk generering av matematiske og teoretiske oppgaver med tilfeldige tall.
   * KRAV: Eleven må svare **riktig på 5 oppgaver på rad** for å fullføre nivået.
   * **Feilhåndtering:** Ved feil svar nullstilles rekken, og spillet viser en pedagogisk steg-for-steg-forklaring samt et hint knyttet til teorikortet fra Fase A.
   * **Duplikatsjekk:** Spørsmålsgeneratoren garanterer at to identiske oppgaver ikke oppstår etter hverandre.

### 2.2 Tilleggsfunksjoner (Gamify-standard)
* **Statuslinje:** Viser nåværende nivå (1–6), nåværende «5 på rad»-rekke (visualisert med 5 stjerner/indikatorer), samt totalt antall løste oppgaver.
* **Lærermeny / Hurtighopp:** En skjult eller tilgjengelig meny for lærer/testing for å hoppe direkte mellom nivåer.
* **Utskrivbart Diplom:** Ved gjennomført Nivå 6 genereres et personlig diplom med elevens navn, dato, tidsbruk og sluttkarakter/akademisk utmerkelse («Sertifisert Effekt-Mester»).

---

## 3. DETALJERT STEG-FOR-STEG INNHOLDSSTRUKTUR (NIVÅ 1 TIL 6)

### NIVÅ 1: Ohmsk motstand & Vekselspenning (DC vs. AC)
* **Teori & Begreper:**
  * Ren motstand (f.eks. glødelampe eller varmeelement). Spenning ($U$) og strøm ($I$) svinger i hel fase (samtidig).
  * Vekselspenning i stikkontakten: $230\text{ V}$ er **effektivverdien** ($U_{eff}$). Toppverdien ($U_{maks}$) er ca. $325\text{ V}$ ($U_{eff} = U_{maks} / \sqrt{2}$).
  * For ren ohmsk motstand gjelder den kjente effektformelen: $P = U \cdot I$. 100 % av energien blir til nyttig varme/lys.
* **Interaktiv Simulering:**
  * Canvas som tegner sinuskurver for spenning (blå) og strøm (rød) som svinger helt i takt ($\varphi = 0^\circ$).
  * Slider for spenning ($U$) og motstand ($R$), som sanntidsoppdaterer effektgrafen $P(t) = U(t) \cdot I(t)$ (alltid over 0).
* **Oppgavetyper i Spillmodus (5 på rad):**
  1. *Regne ut effekt $P$ ($P = U \cdot I$) ved oppgitt $U$ og $I$.*
  2. *Beregne effektivverdi $U_{eff}$ ut fra oppgitt maksspenning $U_{maks}$.*
  3. *Beregne strøm $I$ ($I = P / U$) for varmeelementer.*

---

### NIVÅ 2: Induktiv last & Selvinduksjon (Faseforskyvning)
* **Teori & Begreper:**
  * Elektromotorer har spoler. Når strømmen endrer seg i en spole, oppstår **selvinduksjon** som skaper en motspenning.
  * Dette gjør at strømmen bremses og henger etter spenningen (**faseforskyvning** / *lagging current*).
  * Viserdiagram: Spenning og strøm representeres som roterende vektorer. En hel periode ($50\text{ Hz}$) tar $0{,}02\text{ s} = 360^\circ$. En faseforskyvning på $0{,}002\text{ s}$ tilsvarer $36^\circ$.
  * Når $U$ og $I$ har motsatt fortegn, oppstår **negativ effekt** – energi strømmer midlertidig tilbake til kilden!
* **Interaktiv Simulering (NDLA-kopi/Canvas):**
  * Canvas-viserdiagram til venstre koblet til sinuskurver til høyre.
  * Glidebryter for faseforskyvning ($0\text{ ms}$ til $5\text{ ms}$ / $0^\circ$ til $90^\circ$).
  * Målepunkt-slider ($t$) som flytter viserne i sirkelen og viser momentanverdier.
* **Oppgavetyper i Spillmodus (5 på rad):**
  1. *Konvertere tidsforskyvning i sekunder/millisekunder til fasevinkel $\varphi$ i grader ($\varphi = (t / 0{,}02\text{ s}) \cdot 360^\circ$).*
  2. *Forklare hva som skjer med effekten når strøm og spenning har motsatt fortegn (negativ effekt/returenergi).*
  3. *Gjenkjenne om strømmen ligger foran eller bak spenningen i en induktiv krets.*

---

### NIVÅ 3: Effekttrekanten – De tre effekttypene ($P_t, Q, S$)
* **Teori & Begreper:**
  * Effekten deles inn i tre komponenter som danner en rettvinklet trekant:
    1. **Tilsynelatende effekt ($S$):** Hypotenusen. Den totale effekten nettet må levere ($S = U \cdot I$). Måles i **Voltampere (VA)**.
    2. **Aktiv / Tilført effekt ($P_t$):** Hosliggende katet. Arbeidet som faktisk utføres. Måles i **Watt (W)**.
    3. **Reaktiv effekt ($Q$):** Motstående katet. Energi som svinger fram og tilbake i magnetfeltet uten å gjøre nyttig arbeid. Måles i **voltampere reaktiv (var)**.
  * Pytagoras' læresetning for effekttrekanten:
    $$S^2 = P_t^2 + Q^2 \quad \Longrightarrow \quad Q = \sqrt{S^2 - P_t^2} \quad \text{og} \quad P_t = \sqrt{S^2 - Q^2}$$
* **Interaktiv Simulering:**
  * Canvas-tegning av den rettvinklede effekttrekanten der sidene endres dynamisk.
  * Drag-and-drop eller interaktive knapper for å plassere riktige enheter (W, var, VA) på riktige sider av trekanten.
* **Oppgavetyper i Spillmodus (5 på rad):**
  1. *Beregne $S$ (VA) ut fra oppgitt $U$ og $I$.*
  2. *Beregne reaktiv effekt $Q$ (var) gitt $S$ og $P_t$ ved hjelp av Pytagoras.*
  3. *Beregne tilført aktiv effekt $P_t$ (W) gitt $S$ og $Q$.*
  4. *Identifisere korrekt enhet for $P_t$, $Q$ og $S$.*

---

### NIVÅ 4: Effektfaktor ($\cos\varphi$) & Trigonometri
* **Teori & Begreper:**
  * **Effektfaktoren ($\cos\varphi$):** Forholdet mellom den nyttbare aktive effekten og den tilsynelatende effekten:
    $$\cos\varphi = \frac{\text{Hosliggende katet}}{\text{Hypotenus}} = \frac{P_t}{S}$$
  * Formelen for tilført aktiv effekt (1-fase):
    $$P_t = S \cdot \cos\varphi = U \cdot I \cdot \cos\varphi$$
  * Effektfaktoren er et tall mellom $0$ og $1{,}0$. Høy $\cos\varphi$ betyr god utnyttelse.
  * Finne fasevinkel $\varphi$ fra effektfaktor: $\varphi = \arccos(\cos\varphi)$ (Bruk av `Math.acos()` i JS, eller `acosd` i GeoGebra/OneNote).
* **Interaktiv Simulering:**
  * Vår publiserte **Effekttrekant-Canvas** med trinnløse sliders for $U$, $I$ og $\cos\varphi$.
  * Viser dynamisk oppdatering av vinkelen $\varphi$, katetlengdene og resultatkortene i sanntid.
* **Oppgavetyper i Spillmodus (5 på rad):**
  1. *Beregne tilført effekt $P_t$ gitt $U = 230\text{ V}$, $I$ og $\cos\varphi$.*
  2. *Beregne effektfaktor $\cos\varphi$ gitt $P_t$ og $S$.*
  3. *Regne ut fasevinkelen $\varphi$ i grader ut fra oppgitt $\cos\varphi$.*

---

### NIVÅ 5: Motorens Merkeskilt, 3-fase og Virkningsgrad ($\eta$)
* **Teori & Begreper:**
  * **Tilført effekt ($P_1$ / $P_t$):** Effekten motoren trekker fra el-nettet.
  * **Avgitt effekt ($P_2$ / $P_a$):** Den mekaniske effekten vi får ut på motorakslingen (måles i W eller kW).
  * **Virkningsgrad ($\eta$):** Forholdet mellom avgitt og tilført effekt på grunn av tap i varme, friksjon og lagermotstand:
    $$\eta = \frac{P_a}{P_t} \quad (\text{eller i prosent: } \eta\% = \frac{P_a}{P_t} \cdot 100\%)$$
  * **1-fase vs 3-fase motorberegning:**
    * 1-fase: $P_t = U \cdot I \cdot \cos\varphi$
    * 3-fase: $P_t = \sqrt{3} \cdot U \cdot I \cdot \cos\varphi \approx 1{,}732 \cdot U \cdot I \cdot \cos\varphi$
* **Interaktiv Simulering:**
  * **"Merkeskilt-detektiven":** Et realistisk grafisk motormerkeskilt hvor enkelte data (f.eks. $P_1$, $P_2$, $I$, eller $\cos\varphi$) er visket ut eller skjult. Eleven kan taste inn verdier for å sjekke om skiltet blir komplett.
* **Oppgavetyper i Spillmodus (5 på rad):**
  1. *Regne ut tilført effekt $P_t$ for en 3-faset motor ($400\text{ V}$ eller $230\text{ V}$).*
  2. *Beregne motorens virkningsgrad $\eta$ i prosent ut fra merkeskiltets $P_1$ og $P_2$.*
  3. *Beregne strømmen $I$ motoren trekker fra nettet når $P_a$, $\eta$, $U$ og $\cos\varphi$ er oppgitt.*

---

### NIVÅ 6: Boss-Nivå – Fasekompensering & Økonomi
* **Teori & Begreper:**
  * Hvorfor kompensere? Lav $\cos\varphi$ fører til at det går unødvendig mye strøm i nettet for å overføre samme aktive effekt. Dette krever tykkere kabler, større transformatorer, gir økt spenningstap og medfører straffegebyr fra nettselskapet!
  * **Kondensatorkompensering:** Kondensatorer trekker *ledende* reaktiv effekt ($Q_c$) som nøytraliserer den *etterslepende* reaktive effekten ($Q_L$) fra motorene.
  * Målet er å heve $\cos\varphi$ opp mot $0{,}95 - 1{,}0$.
* **Interaktiv Simulering:**
  * **"Fabrikksjefen":** Et kontrollpanel for et industrianlegg med en generator, en stor motorlast og et innkoblingsbart kondensatorbatteri. Spilleren slår på kondensatorer og ser ampermeteret for nettet falle mens motoren yter det samme.
* **Oppgavetyper i Spillmodus (5 på rad):**
  1. *Beregne hvor mye strømmen i tilførselsledningen reduseres når $\cos\varphi$ økes fra f.eks. $0{,}65$ til $0{,}95$.*
  2. *Avverge straffegebyr: Beregne nødvendig reaktiv effekt $Q_c$ som må tilføres for å oppnå ønsket $\cos\varphi$.*
  3. *Kompleks kombinasjonsoppgave som trekker inn $P_t$, $Q$, $S$, $\eta$ og kompensering.*

---

## 4. JAVASCRIPT-ARKITEKTUR OG MALKODE

Følgende kodelogikk skal benyttes for å strukturere spillet i `effektMester.html`:

```javascript
// Global Spill-Tilstand (State)
const GameState = {
  currentLevel: 1,
  streak: 0,
  targetStreak: 5,
  totalSolved: 0,
  currentQuestion: null,
  lastQuestionParams: null
};

// Konfigurasjon for alle 6 nivåer
const LevelConfig = {
  1: { title: "Nivå 1: Ohmsk motstand & Vekselspenning", unit: "W" },
  2: { title: "Nivå 2: Induktiv last & Selvinduksjon", unit: "grader" },
  3: { title: "Nivå 3: Effekttrekanten (P, Q, S)", unit: "var / VA / W" },
  4: { title: "Nivå 4: Effektfaktor (cos φ)", unit: "W" },
  5: { title: "Nivå 5: Motorberegninger & Virkningsgrad", unit: "% / W / A" },
  6: { title: "Nivå 6: Boss-nivå: Fasekompensering", unit: "A / kvar" }
};

// Spørsmålsgenerator med duplikatsjekk
function generateQuestion(level) {
  let q = {};
  let isDuplicate = true;
  let attempts = 0;

  while (isDuplicate && attempts < 50) {
    attempts++;
    switch(level) {
      case 1:
        q = generateLevel1();
        break;
      case 2:
        q = generateLevel2();
        break;
      case 3:
        q = generateLevel3();
        break;
      case 4:
        q = generateLevel4();
        break;
      case 5:
        q = generateLevel5();
        break;
      case 6:
        q = generateLevel6();
        break;
    }

    if (JSON.stringify(q.params) !== JSON.stringify(GameState.lastQuestionParams)) {
      isDuplicate = false;
    }
  }

  GameState.lastQuestionParams = q.params;
  GameState.currentQuestion = q;
  renderQuestion(q);
}

// Sjekk av brukerens svar (Godtar liten avrundingsmargin)
function checkAnswer(userVal) {
  const q = GameState.currentQuestion;
  const numericUser = parseFloat(userVal.toString().replace(',', '.'));
  const margin = q.margin || 1.0;

  if (!isNaN(numericUser) && Math.abs(numericUser - q.correctAnswer) <= margin) {
    // RIKTIG SVAR
    GameState.streak++;
    GameState.totalSolved++;
    updateUI();

    if (GameState.streak >= GameState.targetStreak) {
      showLevelCompleteModal();
    } else {
      showFeedback(true, "Riktig svar! Bra jobba.");
      setTimeout(() => generateQuestion(GameState.currentLevel), 1200);
    }
  } else {
    // FEIL SVAR
    GameState.streak = 0; // Nullstill rekken
    updateUI();
    showPedagogicExplanation(q, numericUser);
  }
}
```

---

## 5. DESIGN & BRUKERGRENSESNITT (CSS STYLING)

* **Fargepalett:** Modern, profesjonell elektro-profil:
  * Primær (Aktiv effekt $P_t$): `#2563eb` (Elektro-blå)
  * Reaktiv effekt $Q$: `#dc2626` (Rød)
  * Tilsynelatende effekt $S$: `#8b5cf6` (Lilla)
  * Suksess / Fasevinkel $\varphi$: `#059669` (Grønn)
  * Bakgrunn: `#f8fafc` med mørke grå kontrasttekster (`#1e293b`).
* **Typografi:** Systemfonger (`system-ui, -apple-system, sans-serif`). Formler formatteres med god avstand og uthevet skrift.
* **Layout:**
  * Øverst: Header med Gamify-logo, Tittel, Nivåindikator og 5-stjerners streak-bar.
  * Midten: To-kolonners layout på desktop:
    * Venstre kolonne: **Teorikort & Interaktiv Canvas-simulering**.
    * Høyre kolonne: **Spørsmålspanel, Inputfelt og Pedagogisk Tilbakemelding**.
  * Nederst: Footer med diplomknapp (synlig ved fullført spill) og lærermeny.

---

## 6. SJEKKLISTE FOR LEVERANSE (DEFINITION OF DONE)

Før spillet godkjennes i repoet må følges sjekkes:
- [x] Filen heter `effektMester.html` og kjører uten feilmeldinger i nettleserkonsollet.
- [x] Alle 6 nivåer har fungerende teorikort, interaktive simuleringer og spørsmålsgeneratorer.
- [x] Spørsmålsgeneratoren garanterer unike oppgaver og godtar fornuftige avrundingsmarginer (f.eks. `±1%`).
- [x] Feilsvar gir pedagogisk steg-for-steg utregning før streak nullstilles.
- [x] Spillet kan fullføres og gir et utskrivbart diplom på sluttgjelden.
