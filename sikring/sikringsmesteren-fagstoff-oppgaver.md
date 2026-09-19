# SikringsMesteren: Fagstoff, Bildelenker og Utvidet Oppgavebank

Dette dokumentet inneholder en komplett pedagogisk rapport, faglige spesifikasjoner, åpne NDLA-bildelenker og en utvidet oppgavebank for utvikling av det interaktive læringsopplegget **SikringsMesteren** (bygget etter `GAMIFY_TEKNISK_SPESIFIKASJON.md`).

---

## 📋 Innholdsfortegnelse
1. [Pedagogisk Progresjon og Læreplanforankring](#1-pedagogisk-progresjon-og-læreplanforankring)
2. [Oversikt over Åpne Bilde- og Medieressurser (NDLA m.fl.)](#2-oversikt-over-åpne-bilde--og-medieressurser-ndla-mfl)
3. [Del 1: Vg1 Elektro og datateknologi (Nivå 1–3)](#3-del-1-vg1-elektro-og-datateknologi-nivå-13)
   - [Nivå 1: Smeltesikringer vs. Automater & Begreper](#nivå-1-smeltesikringer-vs-automater--begreper)
   - [Nivå 2: Overbelastningsvern – Generelle Anlegg (NEK 400-533.2)](#nivå-2-overbelastningsvern--generelle-anlegg-nek-400-5332)
   - [Nivå 3: Utløserkarakteristikker (B, C, D) & Motorstart](#nivå-3-utløserkarakteristikker-b-c-d--motorstart)
4. [Del 2: Vg2 Automatisering og Elenergi (Nivå 4–6)](#4-del-2-vg2-automatisering-og-elenergi-nivå-46)
   - [Nivå 4: Skjerpede Krav i Boliginstallasjoner (NEK 400-823)](#nivå-4-skjerpede-krav-i-boliginstallasjoner-nek-400-823)
   - [Nivå 5: Kortslutningsvern, Bryteevne & Gjennomsluppet Energi (I²t)](#nivå-5-kortslutningsvern-bryteevne--gjennomsluppet-energi-i²t)
   - [Nivå 6: Boss-nivå – Jordfeilvern, Feilstrømmer & Berøringsspenning (Ub)](#nivå-6-boss-nivå--jordfeilvern-feilstrømmer--berøringsspenning-ub)
5. [Integrasjonsveiledning for AntiGravity & Gamify-skalering](#5-integrasjonsveiledning-for-antigravity--gamify-skalering)

---

## 1. Pedagogisk Progresjon og Læreplanforankring

Læringsopplegget er delt i to utdanningstrinn for å passe direkte til kompetansemålene i LK20:
- **Vg1 Elektro og datateknologi (ELE01-03)**: Fokus på kretsteori, valg av ledning/kabel/vern, virkemåte for automatsikringer og grunnleggende kretsoverbelastning.
- **Vg2 Automatisering (AUT02-03) / Elenergisystemer**: Fokus på avansert dimensjonering, boligspesifikke krav (NEK 400-823), motordrifter, kortslutningsberegninger ($I_{k\text{min}}, I^2t$) og feilstrømmer/berøringsspenning ($U_b \le 50\text{ V}$).

---

## 2. Oversikt over Åpne Bilde- og Medieressurser (NDLA m.fl.)

NDLA sine læringsressurser har åpne lisenser (CC BY-SA / CC BY-NC-SA) og kan benyttes fritt i klasserom og i den interaktive HTML5-applikasjonen.

### Illustrasjoner og Bildelenker per Kategori

| Kategori / Emne | Bildebeskrivelse / Innhold | Kilde- / Artikkellenke (NDLA) |
| :--- | :--- | :--- |
| **Sikringsskap & Fordeling** | Elektriker utfører måling og montasje i fordelingsskap | [NDLA: Koble i et fordelingsskap](https://ndla.no/r/energi--og-styresystemer-el-ele-vg1/koble-i-et-fordelingsskap/5941c82611) |
| **Automatsikring** | Oppbygging av termo-magnetisk utløser | [NDLA: Automatsikringer](https://ndla.no/r/energi--og-styresystemer-el-ele-vg1/automatsikringer/c494c2d6bc) |
| **Jordfeilautomat** | Sumstrømtransformator og testknapp | [NDLA: Jordfeilautomat](https://ndla.no/r/energi--og-styresystemer-el-ele-vg1/jordfeilautomat/58dee6de0c) |
| **Motoranlegg** | Kontaktor, termisk bimetallrelé og asynkronmotor | [NDLA: Hovedkomponenter i motoranlegg](https://ndla.no/r/energi--og-styresystemer-el-ele-vg1/hovedkomponenter-i-motoranlegg/d48257ea41) |
| **Termisk Vern** | Snittbilde av asynkronmotor og bimetallbryter | [NDLA: Termisk vern](https://ndla.no/nn/r/energi--og-styresystem-el-ele-vg1/termisk-vern/873d5619ab) |
| **Kabel og Vern** | Tabellvalg, forlegningsmåter og tverrsnitt | [NDLA: Dokumentasjon av kabel og vern](https://ndla.no/r/energi--og-styresystemer-el-ele-vg1/dokumentasjon-av-kabel-og-vern/00edcccfbb) |
| **Boligdokumentasjon** | Måling og sjekkliste ved sluttkontroll (Fem sikre) | [NDLA: Fem sikre for boligdokumentasjon](https://ndla.no/r/energi--og-styresystemer-el-ele-vg1/fem-sikre---for-standard-boligdokumentasjon/1599e629ac) |
| **HMS og Skilting** | Påbudsskilt, fareskilt og merking | [NDLA: Skilting og merking](https://ndla.no/r/produktivitet-og-kvalitetsstyring-tp-tip-vg1/skilting-og-merking/9fc3ffd229) |
| **Ledningsreparasjon** | Avisolering, oppbygging av leder/isolasjon og pluggkobling | [NDLA: Reparer en elektrisk ledning](https://ndla.no/r/natural-science-tp/reparer-en-elektrisk-ledning/8241ac7086) |

---

# 📗 DEL 1: VG1 ELEKTRO OG DATATEKNOLOGI (NIVÅ 1–3)

---

## Nivå 1: Smeltesikringer vs. Automater & Begreper

### Fagstoff og Sentrale Formler
- **Formål med overstrømsvern**: Beskytte kretser og ledere mot overoppheting og brannfare forårsaket av overbelastning eller kortslutning (FEL § 21 og § 23).
- **Smeltesikring**: Inneholder en kalibrert smeltetråd i en sandfylt patron. Det er et engangsvern med svært høy bryteevne.
- **Automatsikring**: Bruker to uavhengige utløsermekanismer:
  1. *Termisk utløser (Bimetall)*: Reagerer tidsforsinket på modeste overbelastninger.
  2. *Elektromagnetisk utløser (Spole)*: Reagerer momentant på høye kortslutningsstrømmer.
- **Hovedstørrelser**:
  - $I_b$: Dimensjonerende belastningsstrøm ($I_b = \frac{P}{U \cdot \cos\phi}$ for enfase, $I_b = \frac{P}{\sqrt{3} \cdot U \cdot \cos\phi}$ for trefase).
  - $I_n$: Vernets nominelle merkestrøm.
  - $I_z$: Kabelens kontinuerlige strømføringsevne under gitte forlegningsforhold.

### Relevante Læringslenker
- 🔗 [NDLA: Automatsikringer og virkemåte](https://ndla.no/r/energi--og-styresystemer-el-ele-vg1/automatsikringer/c494c2d6bc)
- 🔗 [NDLA: Reparer en ledning og elsikkerhet](https://ndla.no/r/natural-science-tp/reparer-en-elektrisk-ledning/8241ac7086)
- 🔗 [YouTube: Fuses vs Circuit Breakers Explained](https://www.youtube.com/watch?v=...)

### Utvidet Oppgavebank Nivå 1
1. **[Beregning]** En enfase lyskurs forsynes med $2300\text{ W}$ ved $230\text{ V}$ ($\cos\phi = 1{,}0$). Hva blir belastningsstrømmen ($I_b$)?
   - *Fasit*: $10\text{ A}$ ($I_b = 2300 / 230$).
2. **[Flervalg]** Hvilken komponent i en automatsikring sørger for utkopling ved varig overbelastning?
   - *Alternativer*: A) Elektromagnetisk spole B) Bimetall C) Sumstrømtransformator D) Slukkeammer
   - *Fasit*: B) Bimetall.
3. **[Flervalg]** Hva er en hovedfordel med automatsikringer sammenlignet med tradisjonelle smeltesikringer?
   - *Alternativer*: A) Lavere innkjøpspris B) Kan tilbakestilles etter utkopling uten å bytte komponent C) Reagerer alltid raskere ved ekstreme kortslutninger D) Krever ikke jording
   - *Fasit*: B) Kan tilbakestilles etter utkopling uten å bytte komponent.
4. **[Beregning]** En 3-fase varmeovn på $3980\text{ W}$ kobles til et $230\text{ V}$ IT-nett ($\cos\phi = 1{,}0$). Beregn belastningsstrømmen ($I_b$).
   - *Fasit*: $10\text{ A}$ ($I_b = 3980 / (\sqrt{3} \cdot 230)$).
5. **[Velg vern $I_n$]** En kurs har $I_b = 13\text{ A}$ og kabelens strømføringsevne er $I_z = 21\text{ A}$. Velg riktig standard merkestrøm ($I_n$).
   - *Alternativer*: $10\text{ A}, 16\text{ A}, 20\text{ A}, 25\text{ A}$
   - *Fasit*: $16\text{ A}$ ($13\text{ A} \le 16\text{ A} \le 21\text{ A}$).
6. **[Begrepsforståelse]** Hva representerer symbolet $I_z$ i installasjonsdokumentasjonen?
   - *Alternativer*: A) Vernets bryteevne B) Kabelens kontinuerlige strømføringsevne C) Minste kortslutningsstrøm D) Utløsestrøm etter 1 time
   - *Fasit*: B) Kabelens kontinuerlige strømføringsevne.
7. **[Case/Feilsøking]** En elev måler $32\text{ A}$ gjennom en $16\text{ A}$ automatbryter, men den kobler ikke ut de første 5 sekundene. Er automaten defekt?
   - *Fasit*: Nei, $32\text{ A}$ ($2 \cdot I_n$) ligger i det termiske utløserområdet, som krever oppvarmingstid av bimetallet før utkopling skjer.
8. **[Formelomforming]** Omform effektformelen $P = U \cdot I$ til å finne motstanden $R$ uttrykt ved $P$ og $U$.
   - *Fasit*: $R = \frac{U^2}{P}$.

---

## Nivå 2: Overbelastningsvern – Generelle Anlegg (NEK 400-533.2)

### Fagstoff og Sentrale Formler
- **Generelle anlegg (NEK 400-533.2)**:
  - **Krav 1**: $I_b \le I_n \le I_z$
  - **Krav 2**: $I_2 \le 1{,}45 \cdot I_z$
- Standard automatsikringer har $I_2 = 1{,}45 \cdot I_n$. Sett inn i Krav 2 gir det $1{,}45 \cdot I_n \le 1{,}45 \cdot I_z \implies I_n \le I_z$.
- **Korreksjonsfaktorer**: $I_z = I_{z,\text{tabell}} \cdot k_t \cdot k_g$ (temperatur $k_t$ og oppsamling/gruppering $k_g$).
- **Spenningsfall**: $\Delta u = \frac{I \cdot \rho \cdot l \cdot 2 \cdot \cos\phi}{A}$ for enfase kobber ($\rho = 0{,}0178\text{ }\Omega\text{mm}^2/\text{m}$).

### Relevante Læringslenker
- 🔗 [NDLA: Dokumentasjon av kabel og vern](https://ndla.no/r/energi--og-styresystemer-el-ele-vg1/dokumentasjon-av-kabel-og-vern/00edcccfbb)
- 🔗 [NDLA YFF: Pristilbud og kabelberegning](https://ndla.no/r/vocational-specialization-el-ele-vg1/trinn-1-utarbeide-pristilbud/b2209f02bf)

### Utvidet Oppgavebank Nivå 2
1. **[Beregning]** Tabellverdien for en kabel er $I_z = 26\text{ A}$. Kabelen føres gjennom et rom med omgivelsestemperatur $40\text{ }^\circ\text{C}$ ($k_t = 0{,}87$). Beregn korrigert strømføringsevne $I_z$.
   - *Fasit*: $22{,}62\text{ A}$ ($26 \cdot 0{,}87$).
2. **[Sjekk av Krav 1 & 2]** I et næringsbygg er $I_b = 18\text{ A}$, valgt vern er $I_n = 20\text{ A}$, og korrigert $I_z = 22\text{ A}$. Er Krav 1 og Krav 2 oppfylt?
   - *Fasit*: Ja. Krav 1: $18 \le 20 \le 22$. Krav 2: $I_2 = 1{,}45 \cdot 20 = 29\text{ A} \le 1{,}45 \cdot 22 = 31{,}9\text{ A}$.
3. **[Dimensjonering]** Hva er høyeste tillatte standard merkestrøm ($I_n$) for en kabel med korrigert $I_z = 24\text{ A}$ i et generelt anlegg?
   - *Fasit*: $20\text{ A}$ (siden $25\text{ A} > 24\text{ A}$).
4. **[Spenningsfall i Volt]** Beregn spenningsfallet ($\Delta u$) på en $230\text{ V}$ enfasekurs med $2{,}5\text{ mm}^2$ kobberkabel, lengde $l = 25\text{ m}$, strøm $I = 16\text{ A}$ og $\cos\phi = 1{,}0$.
   - *Fasit*: $5{,}70\text{ V}$ ($\Delta u = \frac{16 \cdot 0{,}0178 \cdot 25 \cdot 2 \cdot 1}{2{,}5}$).
5. **[Spenningsfall i Prosent]** Hvor mange prosent utgjør et spenningsfall på $5{,}70\text{ V}$ av nominell spenning $230\text{ V}$?
   - *Fasit*: $2{,}48\text{ \%}$ ($(5{,}70 / 230) \cdot 100$).
6. **[Flervalg]** Hva må gjøres med kabelens strømføringsevne dersom flere belaste kabler legges inntil hverandre på samme kabelbro?
   - *Alternativer*: A) Ingen endring B) Man må bruke en reduksjonsfaktor ($k_g < 1{,}0$) som reduserer $I_z$ C) Man må øke sikringsstørrelsen D) Spenningsfallet minker
   - *Fasit*: B) Man må bruke en reduksjonsfaktor ($k_g < 1{,}0$) som reduserer $I_z$.
7. **[Dimensjonering]** En industriell kurs har $I_b = 27\text{ A}$. Velg standard overbelastningsvern ($I_n$) og minste tillatte kabel-$I_z$.
   - *Fasit*: Vern $I_n = 32\text{ A}$ og kabel-$I_z \ge 32\text{ A}$.
8. **[Case]** Hvilken korreksjonsfaktor må benyttes dersom tilførselskabelen forlegges gjennom et varmt takrom over et bakeri?
   - *Fasit*: Korreksjonsfaktor for omgivelsestemperatur ($k_t$).

---

## Nivå 3: Utløserkarakteristikker (B, C, D) & Motorstart

### Fagstoff og Sentrale Formler
- **Elektromagnetisk momentanutkopling ($I_5$)**:
  - **B-karakteristikk**: $3–5 \cdot I_n$ (Resistive laster, belysning, varme)
  - **C-karakteristikk**: $5–10 \cdot I_n$ (Generell last, pumper, standard motorer)
  - **D-karakteristikk**: $10–20 \cdot I_n$ (Tunge starter, trafoer, store motorer)
- **Motorstart**: Asynkronmotorer trekker en startstrøm (*inrush current*) på 5–10 ganger nominell strøm i startøyeblikket.
- **Termisk motorvern**: Justerbart bimetallrelé som innstilles på motorens merke-arbeidsstrøm ($I_n$).

### Relevante Læringslenker
- 🔗 [NDLA: Termisk vern i motoranlegg](https://ndla.no/nn/r/energi--og-styresystem-el-ele-vg1/termisk-vern/873d5619ab)
- 🔗 [NDLA: Hovedkomponenter i motoranlegg](https://ndla.no/r/energi--og-styresystemer-el-ele-vg1/hovedkomponenter-i-motoranlegg/d48257ea41)
- 🔗 [Chint Global: Guide to MCB Trip Curves](https://www.chintglobal.com/global/en/about-us/news-center/blog/guide-to-mcb-trip-curves--selecting-the-right-b--c--or-d-curve-f.html)

### Utvidet Oppgavebank Nivå 3
1. **[Beregning]** Hva er minste strøm ($I_5$) som garanterer at en $16\text{ A}$ C-automat kobler ut momentant?
   - *Fasit*: $160\text{ A}$ ($10 \cdot 16\text{ A}$).
2. **[Beregning]** Hva er grenseområdet for elektromagnetisk momentanutkopling for en $10\text{ A}$ B-automat?
   - *Fasit*: $30\text{ A}$ til $50\text{ A}$ ($3 \cdot 10\text{ A}$ til $5 \cdot 10\text{ A}$).
3. **[Flervalg]** Hvilken automatkarakteristikk bør velges for en transformator med startstrømspiss på $12 \cdot I_n$?
   - *Alternativer*: A) B-karakteristikk B) C-karakteristikk C) D-karakteristikk D) A-karakteristikk
   - *Fasit*: C) D-karakteristikk.
4. **[Case/Motorstart]** En motor har merkestrøm $I_n = 12\text{ A}$ og startstrøm $72\text{ A}$. Hvorfor slår en $16\text{ A}$ B-automat ut under start?
   - *Fasit*: B-karakteristikken garanterer momentanutkopling mellom $48\text{ A}$ og $80\text{ A}$ ($3–5 \cdot 16\text{ A}$). Startstrømmen på $72\text{ A}$ overstiger nedre grense.
5. **[Innstilling motorvern]** En trefaseasynkronmotor har merkeskilt med $I_n = 8{,}5\text{ A}$ ved $400\text{ V}$ Y-kobling. Hva skal det termiske motorvernet stilles inn på?
   - *Fasit*: $8{,}5\text{ A}$ (motorens merkestrøm).
6. **[Flervalg]** Hva er hovedfunksjonen til det termiske motorvernet?
   - *Alternativer*: A) Kortslutningsbeskyttelse i tilførselen B) Beskytte motoren mot mekanisk overbelastning og varmgang i viklingene C) Forhindre høy startstrøm D) Beskytte mot overspenning
   - *Fasit*: B) Beskytte motoren mot mekanisk overbelastning og varmgang i viklingene.
7. **[Feilsøking]** Hvorfor slår en $10\text{ A}$ B-automat ut idet en stor vinkelsliper startes, selv om driftstrømmen bare er $6\text{ A}$?
   - *Fasit*: Vinkelsliperens startstrømstøt overstiger B-karakteristikkens $I_5$-grense på $30\text{ A}$ ($3 \cdot 10\text{ A}$). Man bør skifte til C-karakteristikk.
8. **[Beregning]** Hva er høyeste strøm en $25\text{ A}$ D-automat kan føre uten at man garanterer momentan elektromagnetisk utkopling?
   - *Fasit*: Opptil $250\text{ A}$ ($10 \cdot 25\text{ A}$). Garantert momentanutkopling skjer først ved $500\text{ A}$ ($20 \cdot 25\text{ A}$).

---

# 📘 DEL 2: VG2 AUTOMATISERING OG ELENERGI (NIVÅ 4–6)

---

## Nivå 4: Skjerpede Krav i Boliginstallasjoner (NEK 400-823)

### Fagstoff og Sentrale Formler
- **NEK 400-823.431.4**: For kobberkabler $\le 4\text{ mm}^2$ i bolig gjelder skjerpede krav:
  - **Krav 1**: $I_b \le I_n$
  - **Krav 2**: $I_2 \le I_z$
- Standard elementautomater ($I_2 = 1{,}45 \cdot I_n$) krever at $1{,}45 \cdot I_n \le I_z \implies I_n \le \frac{I_z}{1{,}45}$.
- **Spesialvern (Bk / Ck)**: Har lavere utløsestrøm ($I_2 = 1{,}2 \cdot I_n$), som muliggjør utnyttelse av $15\text{ A}$ vern på $2{,}5\text{ mm}^2$ skjult kabel ($I_z = 19{,}5\text{ A}$).

### Relevante Læringslenker
- 🔗 [NDLA: Fem sikre for boligdokumentasjon](https://ndla.no/r/energi--og-styresystemer-el-ele-vg1/fem-sikre---for-standard-boligdokumentasjon/1599e629ac)
- 🔗 [NDLA: Dokumentasjon av kabel og vern](https://ndla.no/r/energi--og-styresystemer-el-ele-vg1/dokumentasjon-av-kabel-og-vern/00edcccfbb)

### Utvidet Oppgavebank Nivå 4
1. **[Beregning - Bolig]** En stikkontaktkurs i bolig legges med $2{,}5\text{ mm}^2$ PN i rør i isolert vegg (A1, $I_z = 19{,}5\text{ A}$). Hva er maksimal $I_n$ for en standard automatbryter ($I_2 = 1{,}45 \cdot I_n$)?
   - *Fasit*: $13\text{ A}$ ($I_n \le 19{,}5 / 1{,}45 = 13{,}44\text{ A} \rightarrow \mathbf{13\text{ A}}$).
2. **[Beregning - Bk-spesialvern]** Kan et $15\text{ A}$ Bk-spesialvern ($I_2 = 1{,}2 \cdot I_n$) brukes på en $2{,}5\text{ mm}^2$ A1-kabel ($I_z = 19{,}5\text{ A}$) i bolig?
   - *Fasit*: Ja. $I_2 = 1{,}2 \cdot 15\text{ A} = 18\text{ A}$. Siden $18\text{ A} \le 19{,}5\text{ A}$, er Krav 2 oppfylt.
3. **[Flervalg - Regelsammenligning]** Hvorfor er $16\text{ A}$ standard automat tillatt på $2{,}5\text{ mm}^2$ A1 i næringsbygg, men forbudt i bolig?
   - *Alternativer*: A) Næringsbygg har lavere spenning B) Bolignormen krever $I_2 \le I_z$, mens næringsbygg følger den generelle regelen $I_2 \le 1{,}45 \cdot I_z$ C) Boligkabler blir varmere D) Næringsbygg har ikke jordfeilbryter
   - *Fasit*: B) Bolignormen krever $I_2 \le I_z$, mens næringsbygg følger den generelle regelen $I_2 \le 1{,}45 \cdot I_z$.
4. **[Dimensjonering - VVB]** En varmtvannsbereder i bolig er på $2000\text{ W}$ ($230\text{ V}$). Velg egnet vern ($I_n$) og kabeltverrsnitt.
   - *Fasit*: $I_b = 8{,}7\text{ A}$. Velg $10\text{ A}$ vern og $1{,}5\text{ mm}^2$ kabel ($I_z = 14{,}5\text{ A}$, $I_2 = 1{,}45 \cdot 10 = 14{,}5\text{ A} \le 14{,}5\text{ A}$).
5. **[Feilsøking / Tilsyn]** Eltilsynet gir avvik på en nymontert $16\text{ A}$ C-automat på en skjult $2{,}5\text{ mm}^2$ stuekurs i en enebolig. Hvorfor?
   - *Fasit*: $I_2 = 1{,}45 \cdot 16 = 23{,}2\text{ A}$, som bryter boligkravet $I_2 \le I_z$ ($23{,}2\text{ A} > 19{,}5\text{ A}$).
6. **[Beregning]** For en $4\text{ mm}^2$ PR-kabel åpent på vegg (C-forlegning, $I_z = 36\text{ A}$) i bolig, hva er maksimal $I_n$ for et standard vern?
   - *Fasit*: $20\text{ A}$ ($I_n \le 36 / 1{,}45 = 24{,}8\text{ A} \rightarrow 20\text{ A}$).
7. **[Flervalg]** Hvilke kabler omfattes av NEK 400-823.431.4?
   - *Alternativer*: A) Alle kabler uansett tverrsnitt B) Kobberkabler med tverrsnitt til og med $4\text{ mm}^2$ C) Kun $1{,}5\text{ mm}^2$ D) Aluminiumskabler over $16\text{ mm}^2$
   - *Fasit*: B) Kobberkabler med tverrsnitt til og med $4\text{ mm}^2$.
8. **[Rehabilitering]** Hvorfor byttes gamle $16\text{ A}$ skrusikringer ut med $13\text{ A}$ eller $15\text{ A}$ Bk-automater ved rehabilitering av sikringsskap i bolig?
   - *Fasit*: For å tilfredsstille kravet om $I_2 \le I_z$ på eksisterende skjult $2{,}5\text{ mm}^2$ anlegg ($I_z = 19{,}5\text{ A}$).

---

## Nivå 5: Kortslutningsvern, Bryteevne & Gjennomsluppet Energi (I²t)

### Fagstoff og Sentrale Formler
- **Bryteevne**: $I_{cn} / I_{cu} \ge I_{k\text{maks}}$ (Maksimal forventet kortslutningsstrøm i fordelingen).
- **Momentan utkopling**: $I_5 \le I_{k\text{min}}$ (Minste kortslutningsstrøm ytterst på kursen).
- **Formel for minste tofaset kortslutningsstrøm**:
  $$I_{k2\text{min}} = \frac{0{,}95 \cdot U_n}{2 \cdot 1{,}2 \cdot [Z_{\text{ytre}} + (R_{\text{fase}} \cdot l)]}$$
- **Termisk tåleevne ($t < 0{,}1\text{ s}$)**:
  $$I^2 t \le k^2 S^2$$
  hvor $k = 115$ for PVC/Cu og $S$ er ledertverrsnitt i $\text{mm}^2$.

### Relevante Læringslenker
- 🔗 [Wikipedia: Breaking Capacity](https://en.wikipedia.org/wiki/Breaking_capacity)
- 🔗 [ECalPro: What is Let-Through Energy (I²t)?](https://ecalpro.com/en/glossary/let-through-energy)
- 🔗 [JUTRION Electric: Understanding MCCB Ratings (Icu, Ics, Icw)](https://www.juqielec.com/mccb-icu-ics-icw-difference)

### Utvidet Oppgavebank Nivå 5
1. **[Beregning - $k^2 S^2$]** Hvor mye termisk energi ($A^2s$) tåler en $2{,}5\text{ mm}^2$ PVC/Cu-kabel ($k = 115$) under en kortslutning?
   - *Fasit*: $82\text{ }656\text{ A}^2\text{s}$ ($115^2 \cdot 2{,}5^2 = 13225 \cdot 6{,}25$).
2. **[Sjekk av $I^2t$]** En $16\text{ A}$ C-automat slipper gjennom $I^2 t = 42\text{ }000\text{ A}^2\text{s}$ ved kortslutning. Kabelen tåler $k^2 S^2 = 82\text{ }656\text{ A}^2\text{s}$. Er kabelen beskyttet?
   - *Fasit*: Ja, da $42\text{ }000\text{ A}^2\text{s} \le 82\text{ }656\text{ A}^2\text{s}$.
3. **[Sjekk av $I_5 \le I_{k\text{min}}$]** Beregnet $I_{k\text{min}} = 130\text{ A}$. Vernet er en $16\text{ A}$ C-automat ($I_5 = 160\text{ A}$). Kobler vernet ut momentant?
   - *Fasit*: Nei, fordi $160\text{ A} > 130\text{ A}$. Vernet garanterer ikke elektromagnetisk utkopling ytterst på kursen.
4. **[Flervalg - Bryteevne]** Forventet $I_{k\text{maks}} = 8{,}5\text{ kA}$. Hvilken bryteevne må vernet minst ha?
   - *Alternativer*: A) $3\text{ kA}$ B) $6\text{ kA}$ C) $10\text{ kA}$ D) $4{,}5\text{ kA}$
   - *Fasit*: C) $10\text{ kA}$ ($10\text{ kA} \ge 8{,}5\text{ kA}$).
5. **[Begrepsforståelse]** Hva er forskjellen på $I_{cu}$ (Ultimate) og $I_{cs}$ (Service) bryteevne?
   - *Fasit*: $I_{cu}$ er grenseverdien vernet kan bryte én gang. $I_{cs}$ er strømmen vernet kan bryte gjentatte ganger og fortsette i videre drift etterpå.
6. **[Beregning - Kabellengde]** Hva skjer med $I_{k\text{min}}$ når kabellengden $l$ øker?
   - *Fasit*: Resistansen øker ($R = \frac{\rho \cdot l}{A}$), noe som fører til at $I_{k\text{min}}$ reduseres og kan gi fare for manglede utkopling ($I_5 > I_{k\text{min}}$).
7. **[Beregning - $k^2 S^2$]** Beregn den termiske tåleevnen for en $1{,}5\text{ mm}^2$ PVC/Cu-kabel ($k = 115$).
   - *Fasit*: $29\text{ }756\text{ A}^2\text{s}$ ($115^2 \cdot 1{,}5^2$).
8. **[Case]** Hvordan kan man utbedre et anlegg der $I_5 > I_{k\text{min}}$ på en lang kurs uten å bytte kabel?
   - *Fasit*: Bytte fra C-karakteristikk til B-karakteristikk (halverer $I_5$ fra $10 \cdot I_n$ til $5 \cdot I_n$).

---

## Nivå 6: Boss-nivå – Jordfeilvern, Feilstrømmer & Berøringsspenning (Ub)

### Fagstoff og Sentrale Formler
- **Sumstrømtransformator**: Sammenligner strøm inn vs. strøm ut. Ubalanse induserer spenning i sekundærviklingen som utløser vernet.
- **IT-nett (1. jordfeilstrøm)**: $I_{\text{feil}} \approx 2\text{ mA per kVA}$ trafoytelse.
- **TT-nett (feilstrøm)**: $I_{\text{feil}} = \frac{U_0}{R_a + R_b}$.
- **Krav til berøringsspenning**:
  $$U_b = R_a \cdot I_{\text{feil}} \le 50\text{ V (AC)}$$
- **Jordfeilverntyper**:
  - **Type A**: Vekselstrøm + pulserende likestrøm (standard).
  - **Type B**: Glatt DC-feilstrøm (påkrevd for elbilladere, frekvensomformere og solcelleomformere).

### Relevante Læringslenker
- 🔗 [NDLA: Jordfeilautomat](https://ndla.no/r/energi--og-styresystemer-el-ele-vg1/jordfeilautomat/58dee6de0c)
- 🔗 [NDLA: Dokumentasjon av kabel og vern](https://ndla.no/r/energi--og-styresystemer-el-ele-vg1/dokumentasjon-av-kabel-og-vern/00edcccfbb)

### Utvidet Oppgavebank Nivå 6
1. **[Beregning - IT-nett]** Et IT-nett forsynes av en trafo på $400\text{ kVA}$. Beregn forventet 1. jordfeilstrøm ($I_{\text{feil}}$).
   - *Fasit*: $800\text{ mA}$ eller $0{,}8\text{ A}$ ($2\text{ mA} \cdot 400$).
2. **[Beregning - Berøringsspenning]** I anlegget over ($I_{\text{feil}} = 0{,}8\text{ A}$) er jordingsresistansen $R_a = 70\text{ }\Omega$. Beregn berøringsspenningen ($U_b$) og vurder om den er lovlig ($U_b \le 50\text{ V}$).
   - *Fasit*: $U_b = 70 \cdot 0{,}8 = \mathbf{56\text{ V}}$. Dette er ULOVLIG ($56\text{ V} > 50\text{ V}$).
3. **[Beregning - Maks $R_a$]** Hva er maksimalt tillatte $R_a$ i et IT-anlegg med 1. jordfeilstrøm på $1{,}6\text{ A}$ dersom det ikke benyttes jordfeilbryter?
   - *Fasit*: $R_a \le 50 / 1{,}6 = \mathbf{31{,}25\text{ }\Omega}$.
4. **[Beregning - TT-nett]** I et $230\text{ V}$ TT-nett ($U_0 = 132\text{ V}$) er $R_a = 30\text{ }\Omega$ og trafoens jordmotsand $R_b = 10\text{ }\Omega$. Beregn jordfeilstrømmen.
   - *Fasit*: $3{,}3\text{ A}$ ($I_{\text{feil}} = 132 / (30 + 10) = 132 / 40$).
5. **[Flervalg - Vern-typer]** Hvorfor må man benytte Type B jordfeilvern på kurser til elbilladere eller frekvensomformere?
   - *Alternativer*: A) Type B reagerer raskere B) Glatte DC-feilstrømmer kan «mette» kjernen i Type A-vern og gjøre dem blinde C) Type B tåler mer varme D) Det er billigere
   - *Fasit*: B) Glatte DC-feilstrømmer kan «mette» kjernen i Type A-vern og gjøre dem blinde.
6. **[Flervalg - Sumstrømtrafo]** Hvordan registrerer jordfeilbryteren en feil mot jord?
   - *Alternativer*: A) Ved å måle kabeltemperaturen B) Ved at summen av strømmene gjennom faselederne ikke er lik null, som induserer spenning i sekundærviklingen C) Ved å måle spenningen på jordlederen D) Ved motstandsmåling
   - *Fasit*: B) Ved at summen av strømmene gjennom faselederne ikke er lik null, som induserer spenning i sekundærviklingen.
7. **[Selektivitet]** Hva slags jordfeilbryter monteres oppstrøms for å oppnå tidsselektivitet mot nedstrøms $30\text{ mA}$ automater?
   - *Fasit*: Et tidsforsinket selektivt jordfeilvern (Type S, f.eks. $100\text{ mA}$ eller $300\text{ mA}$).
8. **[Beregning - Berøringsspenning med RCD]** En kurs er beskyttet av en $30\text{ mA}$ ($0{,}03\text{ A}$) jordfeilautomat. Hva er høyeste tillatte jordingsresistans ($R_a$) for å oppfylle $U_b \le 50\text{ V}$?
   - *Fasit*: $1666\text{ }\Omega$ ($R_a \le 50 / 0{,}03$).

---

## 5. Integrasjonsveiledning for AntiGravity & Gamify-skalering

Ved videreutvikling i AntiGravity:
1. **Bildevisning i Simulator**: Benytt NDLA sine åpne bildelenker i teorigrensesnittet via standard `<img>`-tagger med responsiv CSS (`max-width: 100%; height: auto; border-radius: 8px;`).
2. **Kortstokk/Rundebunke**: Bruk Fisher-Yates shuffle på arrayer med 8 oppgaver per nivå slik at elevene møter tilfeldige, unike utfordringer hver runde.
3. **Tooltip-berikelse**: Koble alle fagbegreper (`I_b`, `I_n`, `I_z`, `I_2`, `I_5`, `I_{cu}`, `I^2t`, `U_b`, `R_a`, `Bimetall`, `Sumstrømtransformator`) mot `ELECTRICAL_GLOSSARY` for automatisk utheving.
