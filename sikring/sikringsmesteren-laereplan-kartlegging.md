# Overordnet Læreplan- og Didaktisk Kartleggingsrapport: SikringsMesteren

**Prosjekt:** SikringsMesteren – Interaktivt Spill og Simuleringsverktøy for Elektrofag  
**Referanse:** `GAMIFY_TEKNISK_SPESIFIKASJON.md`  
**Målgruppe:** Vg1 Elektro og datateknologi (ELE01-03) & Vg2 Automatisering (AUT02-03) / Elenergi  

---

## 1. Innledning og Didaktisk Rammeverk

SikringsMesteren er et selvstendig, browserbasert digitalt læringsopplegg utviklet for å gi elever i videregående opplæring en dyp, opplevelsesbasert og matematisk forankret forståelse av elektriske vern, kabeldimensjonering, kortslutningsfysikk og elsikkerhet.

Læringsopplegget kombinerer **interaktiv simulering (HTML5 Canvas)**, **utforskende eksperimentering** og en **progressiv oppgavebank («5 på rad» med rundebunke-mekanisme)**. Dette sikrer at elevene møter alle relevante faglige problemstillinger og formelvariasjoner i henhold til kravene i Læreplanverket for Kunnskapsløftet 2020 (LK20).

---

## 2. Detaljert Læreplankartlegging (Udir ELE01-03 & AUT02-03)

### 2.1 Oversiktsmatrise: Mål mot Spillmoduler

| Spillnivå & Tema | Trinn | Sentralt Faginnhold & Formelverk | Udir Kompetansemål (ELE01-03 / AUT02-03) | Relevante Lover & Standarder |
| :--- | :--- | :--- | :--- | :--- |
| **Nivå 1: Smeltesikringer vs. Automater & Kretsteori** | Vg1 | • $I_b = \frac{P}{U \cdot \cos\phi}$<br>• Ohms lov ($U=I \cdot R$)<br>• Bimetall vs. elektromagnetisk spole<br>• $I_b \le I_n \le I_z$ | **Vg1 ELE01-03:** "velge egnet ledning, kabel og vern, beregne og vurdere spenningsfall..."<br>**Vg1 ELE01-03:** "beregne strøm, spenning, resistans..." | FEL § 21/23<br>NEK 400-533.2 |
| **Nivå 2: Overbelastningsvern – Generelle Anlegg** | Vg1 | • Krav 1: $I_b \le I_n \le I_z$<br>• Krav 2: $I_2 \le 1{,}45 \cdot I_z$<br>• Korreksjonsfaktorer: $I_z = I_{z,\text{tab}} \cdot k_t \cdot k_g$<br>• Spenningsfall: $\Delta u = \frac{I \cdot \rho \cdot l \cdot 2 \cdot \cos\phi}{A}$ | **Vg1 ELE01-03:** "velge egnet ledning, kabel og vern, beregne og vurdere spenningsfall og dokumentere beskyttelse..." | NEK 400-533.2<br>Montørhåndboka Tabell 6.2a |
| **Nivå 3: Utløserkarakteristikker & Motorstart** | Vg1 / Vg2 | • Karakteristikk B ($3–5 I_n$), C ($5–10 I_n$), D ($10–20 I_n$)<br>• $I_5$ momentan utkopling<br>• Startstrømstøt ($I_{\text{start}}$)<br>• Termisk motorvern (bimetall) | **Vg1 ELE01-03:** "forklare den prinsipielle virkemåten til motor og styresystem..."<br>**Vg2 AUT02-03:** "montere... flere typer motordrift, gjøre rede for start- og reguleringsmetoder" | NEK 400-431.5<br>FEL § 23 |
| **Nivå 4: Skjerpede Krav i Boliginstallasjoner** | Vg2 | • Krav 1: $I_b \le I_n$<br>• Krav 2: $I_2 \le I_z$ (for $S \le 4\text{ mm}^2$ Cu)<br>• Spesialvern Bk/Ck ($I_2 = 1{,}2 \cdot I_n$)<br>• Skjult vs. åpen forlegning | **Vg2 AUT02-03:** "velge ledning, kabel og vern og dokumentere beskyttelse mot overbelastning..."<br>**Vg1 ELE01-03:** "montere et mindre fordelingsystem..." | NEK 400-823.431.4<br>DSB Fem Sikre |
| **Nivå 5: Kortslutningsvern, Bryteevne & $I^2t$** | Vg2 | • $I_{cu} / I_{cs} \ge I_{k\text{maks}}$<br>• $I_5 \le I_{k\text{min}}$<br>• Minste $I_{k2\text{min}} = \frac{0{,}95 U_n}{2 \cdot 1{,}2 [Z_{\text{ytre}} + R_{\text{fase}} \cdot l]}$<br>• Gjennomsluppet energi: $I^2t \le k^2 S^2$ | **Vg2 AUT02-03:** "velge ledning, kabel og vern og dokumentere beskyttelse mot... kortslutning basert på beregninger" | NEK 400-431.5 / 533.3<br>IEC 60947-2 |
| **Nivå 6: Jordfeilvern, Feilstrømmer & Berøringsspenning** | Vg2 | • IT-nett ($I_{\text{feil}} \approx 2\text{ mA/kVA}$)<br>• TT-nett ($I_{\text{feil}} = \frac{U_0}{R_a + R_b}$)<br>• Berøringsspenning $U_b = R_a \cdot I_{\text{feil}} \le 50\text{ V}$<br>• RCD Type A vs. Type B | **Vg2 AUT02-03:** "installere... fordelingsanlegg i industri basert på ulike spenningssystemer og... jordingssystemer"<br>**Vg2 AUT02-03:** "utføre sluttkontroll..." | FEL § 21<br>NEK 400-411.3 / 823 |

---

## 3. Fordypning per Læreplanmål og Pedagogisk Gjennomføring

### 3.1 Vg1 Elektro og datateknologi (ELE01-03)

#### 🎯 Kompetansemål 1: "Velge egnet ledning, kabel og vern, beregne og vurdere spenningsfall og dokumentere beskyttelse mot overbelastning og elektrisk sjokk"
* **Knytning i SikringsMesteren (Nivå 1 & Nivå 2):**
  - **Teori:** Introduksjon til kabelstrukturer, forlegningsmåter (A1, B1, C) og temperaturfaktorer ($k_t$).
  - **Simulator (Enlinjeskjema):** Elevene manipulerer kabellengde, tverrsnitt og belastning i sanntid. Simulatoren viser automatisk beregnet spenningsfall ($\Delta u$ i volt og prosent) og kabelkjernetemperatur ($T$ i °C).
  - **Beregningsoppgaver:** Elevene må kontrollere Krav 1 ($I_b \le I_n \le I_z$) og Krav 2 ($I_2 \le 1{,}45 \cdot I_z$), samt beregne spenningsfall med formelen:
    $$\Delta u = \frac{I \cdot \rho \cdot l \cdot 2 \cdot \cos\phi}{A}$$

#### 🎯 Kompetansemål 2: "Montere et mindre fordelingsystem med tilhørende jordingssystem og beskrive den prinsipielle oppbygningen av TN-, IT- og TT-nett"
* **Knytning i SikringsMesteren (Nivå 1 & Nivå 6):**
  - **Teori:** Gjennomgang av fordelingssystemenes bokstavkoder (første og andre bokstav for forholdet til jord) og spenningsnivåer ($230\text{ V}$ IT/TT vs. $230/400\text{ V}$ TN-S).
  - **Simulator (Feilstrømssirkel):** Viser forskjellen på kapasitiv tilbakekobling i IT-nett og direkte galvanisk returvei i TT/TN-nett.

#### 🎯 Kompetansemål 3: "Beregne strøm, spenning, resistans, impedans og effekt i like- og vekselstrømskretser..."
* **Knytning i SikringsMesteren (Nivå 1):**
  - **Oppgavebank:** Grunnleggende formelomforming for enfase og trefase effektberegning:
    $$I_b = \frac{P}{U \cdot \cos\phi} \quad \text{og} \quad I_b = \frac{P}{\sqrt{3} \cdot U \cdot \cos\phi}$$

---

### 3.2 Vg2 Automatisering (AUT02-03) / Elenergisystemer

#### 🎯 Kompetansemål 4: "Velge ledning, kabel og vern og dokumentere beskyttelse mot overbelastning, elektrisk sjokk og kortslutning basert på beregninger"
* **Knytning i SikringsMesteren (Nivå 4 & Nivå 5):**
  - **Skjerpede krav (NEK 400-823):** Dypdykk i forskjellene mellom generelle installasjoner og bolignanlegg hvor $I_2 \le I_z$ for kabler $\le 4\text{ mm}^2$. Elevene lærer hvorfor en standard $16\text{ A}$ C-automat bryter regelverket på $2{,}5\text{ mm}^2$ A1-kabel, og løser oppgaver med Bk/Ck-spesialvern ($I_2 = 1{,}2 \cdot I_n$).
  - **Kortslutningsfysikk (Nivå 5):**
    - Beregne minste kortslutningsstrøm:
      $$I_{k2\text{min}} = \frac{0{,}95 \cdot U_n}{2 \cdot 1{,}2 \cdot [Z_{\text{ytre}} + (R_{\text{fase}} \cdot l)]}$$
    - Verifisere at den elektromagnetiske utløseren slår ut momentant: $I_5 \le I_{k\text{min}}$.
    - Kontrollere termisk tåleevne for kabel under rask utkopling ($t < 0{,}1\text{ s}$):
      $$I^2 t \le k^2 S^2$$

#### 🎯 Kompetansemål 5: "Montere, koble opp, sette i drift og funksjonsteste flere typer motordrift, gjøre rede for ulike start- og reguleringsmetoder..."
* **Knytning i SikringsMesteren (Nivå 3):**
  - **Utløserkarakteristikker:** Analyse av startstrømstøt (*inrush current*, 5–14 $\times I_n$).
  - **Canvas-Simulator:** Logaritmisk $I/I_n$ vs. $t$-diagram der elevene legger motorstartgrafen over B-, C- og D-kurvene for å forhindre "falsk utkopling".

#### 🎯 Kompetansemål 6: "Installere, sette i drift og dokumentere automatiserte anlegg i bygg og fordelingsanlegg i industri basert på ulike spenningssystemer... med tilhørende jordingssystemer"
* **Knytning i SikringsMesteren (Nivå 6):**
  - **Jordfeil- og berøringsspenning:** Beregne 1. jordfeilstrøm i IT-nett ($I_{\text{feil}} = 2\text{ mA/kVA}$) og TT-nett ($I_{\text{feil}} = \frac{U_0}{R_a + R_b}$).
  - **Beregne berøringsspenning:** $U_b = R_a \cdot I_{\text{feil}} \le 50\text{ V}$.
  - **Materiellvalg:** Begrunne valg av Type B jordfeilvern ved nærvær av glatte DC-feilstrømmer fra frekvensomformere og elbilladere.

---

## 4. Evaluering, Didaktisk Progresjon og Lærerkontroll

### 4.1 Rundebunke-mekanismen (Card Deck Shuffle)
For å tilfredsstille LK20s krav til **dybdelæring** og forhindre flaksbasert gjennomføring, benytter spillet en rundebunke-algoritme (Fisher-Yates shuffle). For å oppnå en 5-stjerners streak på et nivå må eleven besvare 5 unike oppgavetyper:
1. Direkte numerisk beregning (f.eks. finn $I_b$ eller $I^2t$).
2. Formelomforming / grenseverdisjekk (f.eks. sjekk $I_5 \le I_{k\text{min}}$ eller Krav 2).
3. Materiell- og karakteristikkvalg (f.eks. B, C eller D / Type A vs. Type B RCD).
4. Begrepsforståelse og regelverk (f.eks. NEK 400-823 vs. generelle anlegg).
5. Praktisk feilsøking / case fra yrkeslivet.

### 4.2 Tredelt Lærerspor på Diplomet
Ved fullført Nivå 3 (Vg1-sertifikat) og Nivå 6 (Vg2-mesterdiplom) genereres et offisielt diplom. For å sikre pålitelig standpunkts- og underveisvurdering inneholder diplomet usynlige verifiseringsmarkører dersom eleven har benyttet lærermenyen / fasitmodus under økten:
1. **Sikkerhets-ID:** Prefix `-V` (Verifisert) vs. `-K` (Kontroll/Modus-K).
2. **Bakgrunnsvannmerke:** Lite amber stempel `★ MODUS-K ★` ved juks.
3. **Mikromarkører:** Typografisk stjerne `*` ved lærersignatur.

---

## 5. Konklusjon og Veien Videre

Denne læreplankartleggingen viser at **SikringsMesteren** dekker kjerneelementene i elektro- og automatiseringsfagene på en helhetlig måte. Ved å kombinere teoretiske utledninger med visuelle, interaktive simulatorer får elevene en unik mulighet til å eksperimentere med komplekse sammenhenger som kabeloppvarming, spenningsfall og feilstrømmer før de utfører beregninger og praktisk installasjonsarbeid i verkstedet.
