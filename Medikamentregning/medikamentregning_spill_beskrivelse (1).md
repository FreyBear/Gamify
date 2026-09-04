# Produktkonsept og Kravspesifikasjon: Medikamentregning for Sykepleierstudenter

Dette dokumentet beskriver arkitekturen, spillmekanikken, den faglige realismen og brukergrensesnittet for et interaktivt læringsspill i medikamentregning for sykepleierstudenter. Spillet realiseres som en frittstående, selvstendig **enkel HTML-fil** med integrert CSS og JavaScript.

## 0. Navn og visuell retning

Produktet skal ha et faglig, rolig og tillitvekkende uttrykk. Det skal oppleves som et digitalt treningsverktøy for sykepleierutdanning, ikke som et underholdningsspill eller et personlig prosjekt. Språket skal være presist og støttende, med vekt på pasientsikkerhet, dokumentasjon og kontrollregning.

### Navnealternativer

1. **Medikamentprøven** – tydelig, seriøst og direkte knyttet til fagområdet.
2. **Klinisk Dose** – seriøst og direkte, med tydelig kobling til praksis.
3. **MedReg** – enkelt og funksjonelt, egnet som navn på et verktøy eller en læringsplattform.
4. **Nullfeil: Medikamentregning** – tydelig kobling til fagets krav, men med et mer alvorlig og prestasjonspreget uttrykk.
5. **DoseKlar** – studentvennlig og positivt, samtidig som det beholder den kliniske retningen.
6. **RegnRiktig: Medikamentregning** – forklarende og lett tilgjengelig, men mindre egnet som et formelt produktnavn.

**Endelig navn:** **Medikamentprøven**. Undertittel: *Digital trening i klinisk medikamentregning*.

### Sertifikat ved fullføring

Ved fullført treningsprogram vises et nøytralt sertifikat, ikke et personlig diplom. Sertifikatet skal:

- bruke tittelen **Sertifikat for gjennomført treningsprogram**
- vise studentens valgte navn og dato for gjennomføring
- angi programnavnet **Medikamentprøven – Digital trening i klinisk medikamentregning**
- oppsummere at studenten har fullført spillets treningsnivåer og bestått den innebygde sluttprøven
- ikke inneholde personlig signatur eller hilsen fra utvikler eller lærer
- kunne ha teksten **Utviklet av Ingve Bjørnå** diskret nederst i sertifikatet, med liten typografi og dempet kontrast
- tydelig markere at sertifikatet dokumenterer gjennomføring av treningsprogrammet, og ikke erstatter formell eksamen eller autorisasjon

Visuelle effekter og tekst skal være nedtonet: bruk diskret bekreftelse ved riktig svar og en saklig, pedagogisk forklaring ved feil. Unngå overdreven bruk av emojier, fyrverkeri, konkurransepreg og uformelle personreferanser.

---

## 1. Konsept og Målsetning

Medikamentregning er et fag ved sykepleierutdanningen preget av nullfeilstoleranse (100 % må være rett for å bestå ordinær nasjonal/lokal eksamen). Målet med spillet er å:
- Bygge klinisk intuisjon, selvtillit og regnepresisjon gjennom gradvis stigende vanskelighetsgrad.
- Tvinge fram nøyaktighet rundt enheter, tier-potenser og formeltrekanten (**Dose = Styrke × Mengde**).
- Gi en virkelighetstro opplevelse med ekte medikamenter, standardiserte formuleringer og klinisk plausible pasientkasus.
- Gi tilgang til en realistisk «Eksamensmodus» (Prøvemodus) først når studenten har bevist feilfrihet på tvers av samtlige nivåer.

---

## 2. Teknisk Arkitektur & Responsivt Design

Spillet implementeres som én samlet web-applikasjon i én fil (`index.html`):
- **Struktur:** Semantisk HTML5 optimalisert for både stasjonære og mobile enheter.
- **Responsivt Brukergrensesnitt (Mobil, Nettbrett, PC):**
  - Mobile-first tilnærming med fleksible CSS Grid/Flexbox-layouter.
  - Tydelig typografi, høye kontraster og store berøringsflater (touch targets) for mobil og nettbrett.
  - Skjermtilpassede inndatafelt og numerisk tastaturvennlig oppsett (`inputmode="decimal"`).
- **Logikk (Vanilla JavaScript):**
  - Tilstandsmaskin (State Machine) for nivåer, oppgaver og poengberegning.
  - **Dynamisk oppgavegenerator med randomisering og anti-repetisjonsfilter:**
    - Genererer tilfeldige tallverdier innenfor realistiske, klinisk trygge doseringsintervaller.
    - Sørger for at etterfølgende oppgaver har ulik struktur og ulike preparater (unngår monotoni).
  - Robust inndatavalidering med støtte for både komma (`,`) og punktum (`.`).
  - Passordgenerering og lokal progresjonslagring via `localStorage`.

---

## 3. Klinisk Realisme og Oppgaveautentisitet

For at oppgavene skal oppleves relevante og eksamensnære, stilles strenge krav til medisinsk realisme:

1. **Reelle legemidler og handelsnavn/virkestoff:**
   - Det skal utelukkende benyttes preparater og formuleringer som faktisk brukes i norsk helsevesen (jf. Felleskatalogen).
   - Eksempler:
     - *Tabletter:* Paracetamol (500 mg, 1 g), Sobril/Oksazepam (10 mg, 15 mg, 25 mg), Metoprolol (25 mg, 50 mg, 100 mg), Prednisolon (5 mg, 20 mg).
     - *Injeksjoner/ampuller:* Morfin (10 mg/ml), Ketorolak (30 mg/ml), Furosemid (10 mg/ml), Haloperidol (5 mg/ml).
     - *Infusjonsvæsker & tilsetninger:* Ringer-acetat 1000 ml, Glukose 50 mg/ml (5 %), NaCl 9 mg/ml, KCl konsentrat (1 mmol/ml eller 2 mmol/ml).
2. **Klinisk plausible doser:**
   - Doseringsintervaller må ligge innenfor terapeutiske rammer for voksne og barn (f.eks. aldri 50 tabletter eller 4 liter Morfin).
   - Utregningene skal ende opp i tallverdier som lar seg administrere i praksis (f.eks. halv-tablettdeling kun for delbare tabletter, opptrekkbare sprøytevolum).
3. **Randomisering med variasjon:**
   - Tallene i oppgaveteksten genereres dynamisk innenfor logiske spenn for hvert medikament.
   - En innebygd historikk-sjekk sikrer at to oppgaver på rad verken handler om samme preparat eller samme regnetype.

---

## 4. Spesialtegn & Virtuelle Hurtigtaster

Studenter mangler ofte enkel tilgang til spesialtegn på vanlige mobil- og PC-tastaturer. Grensesnittet skal derfor inkludere **klikkbare knapper/hurtigtaster** under inndatafeltet:
- **Mikro-tegnet:** `µ` / `µg` (mikrogram)
- **Matematiske tegn & brøker:** `·` (gangetegn), `/` (deletegn), `½`
- **Vanlige kliniske enheter (ett-klikks innsetting):**
  - `mg`
  - `µg` / `mikrog`
  - `g`
  - `ml`
  - `mmol`
  - `dr/min`
  - `ml/t`

Dette forhindrer skrivefeil som skyldes tastaturforskjeller mellom iOS, Android, macOS og Windows.

---

## 5. Spillmekanikk og Regler

### 5.1 Nivåprogresjon (Treningsmodus)
- **Nivåkrav:** Studenten må svare **5 rette svar på rad** på et nivå for å låse opp det neste.
- **Nullfeilstoleranse underveis:**
  - Ved feil nullstilles teller for uavbrutte rette svar på nivået (for å etterligne eksamenspresset om null feil).
  - Det vises en grundig pedagogisk løsningsforklaring:
    1. Formelen som gjelder.
    2. Innsetting av tall med enheter.
    3. Trinnvis utregning og avrunding.
- **Visuell fremdrift:**
  - Fremdriftsmåler (1/5, 2/5, 3/5, 4/5, 5/5).
  - Skjermelement som viser gjeldende nivå, oppgavenummer og poeng.

### 5.2 Eksamenspassord
- Når Nivå 5 er bestått med 5 rette på rad, tildeles et unikt eller fast eksamenspassord (f.eks. `NULLFEIL-2026`).
- Passordet gir tilgang til **Prøvemodus / Simulert Eksamen**.

### 5.3 Prøvemodus (Simulert Eksamensprøve)
- **Oppbygging:** 8–10 representative oppgaver hentet på tvers av alle nivåer og vanskelighetsgrader.
- **Eksamensvilkår:**
  - Ingen fasit eller hjelp underveis.
  - Mulighet for tidsbegrensning (f.eks. 60 minutter).
  - Egen oversiktsside der studenten kan bla frem og tilbake mellom oppgavene og endre svar før endelig innlevering.
- **Sensur:**
  - Krav for bestått: **100 % korrekt** (0 feil).
  - Ved innlevering vises en samlet sensurprotokoll med karakter (Bestått / Ikke bestått) samt detaljert gjennomgang av eventuelle feil.

---

## 6. Nivåoversikt og Doseringsrammer

| Nivå | Tittel | Typiske eksempler (reelle medikamenter) | Faglig fokus & Avrunding |
| :--- | :--- | :--- | :--- |
| **Nivå 1** | *Grunnleggende enhetsomregning & tabletter* | Paracetamol tabletter 500 mg, Sobril 10 mg/15 mg/25 mg, Prednisolon 5 mg. Omregning g ↔ mg ↔ µg ↔ mmol. | Tier-potenser, flytting av komma, deling av hele og halve tabletter ($Mengde = \frac{Dose}{Styrke}$). |
| **Nivå 2** | *Flytende legemidler & injeksjoner* | Morfin ampuller 10 mg/ml, Ketorolak 30 mg/ml, Mikstur Apocillin 50 mg/ml. Volum fra 0,2 ml til 20 ml. | Desimaltall, sprøytedoser, avrunding til 1 desimal for volum $> 1\text{ ml}$ og 2 desimaler for volum $< 1\text{ ml}$. |
| **Nivå 3** | *Vekt- og overflatebasert dosering (pediatri)* | Paracetamol mikstur (24 mg/ml) dosert som 15 mg/kg/dose til barn på 12–25 kg. Døgndose vs. enkeltdose fordelt på 3–4 doser. | Flerleddet regning, pasientsikkerhet i barneavdeling, kontroll av døgndose vs. enkeltdose. |
| **Nivå 4** | *Infusjonshastighet & dråpetakt* | Ringer-acetat 1000 ml over 4–12 timer, NaCl 500 ml over 2 timer. Standard dråpetaktteller: Væske ($20\text{ dr/ml}$), SAG/blod ($60\text{ dr/ml}$). | Formel: $\frac{\text{Volum (ml)} \times 20\text{ dr/ml}}{\text{Tid (min)}}$. **Alltid heltall** ved dråper/minutt. Beregning av ml/t. |
| **Nivå 5** | *Fortynninger & sprøytepumper (intensiv)* | Tilsette 20 mmol KCl i 1000 ml Ringer. Beregne ny sluttstyrke (mmol/ml). Noradrenalin infusjon dosert i µg/kg/min til intensivpasient på pumpe (ml/t). | Sammensatte formler, tynning av stamløsninger, tid- og vektberegning i sprøytepumper under press. |

---

## 7. Valideringsregler for Svar

1. **Numerisk toleranse:**
   - Komma (`,`) og punktum (`.`) skal tolkes likt.
   - Avrunding må stemme nøyaktig med standard reglement i medikamentregning (f.eks. hele dråper på dråpetakt, standard desimalregler for injeksjonsvolum).
2. **Krav til benevning / enhet:**
   - Svaret skal kreve korrekt benevning (f.eks. `1.5 ml`, `2 tabletter`, `28 dr/min`).
   - Tastaturknapper for spesialtegn og enheter skal gjøre det sømløst å legge til riktig format uten formateringskrøll på mobil.
