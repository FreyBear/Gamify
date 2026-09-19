# Sjekkliste & Beregningsskjema for Kursdimensjonering
**Prosjektering og dokumentasjon i henhold til NEK 400**

---

### Prosjektinformasjon
| Felt | Verdi | Felt | Verdi |
| :--- | :--- | :--- | :--- |
| **Prosjekt / Kunde:** | ____________________________________ | **Dato:** | ______________ |
| **Anleggsadresse:** | ____________________________________ | **Utført av:** | ______________ |
| **Fordeling / Skap:** | ____________________________________ | **Kursbetegnelse:** | ______________ |

---

### 1. Grunnlagsdata og installasjonsmiljø

* **Nettsystem:** `[ ]` TN-C-S (400 V) &nbsp;&nbsp;&nbsp;&nbsp; `[ ]` TN-S (400 V / 230 V) &nbsp;&nbsp;&nbsp;&nbsp; `[ ]` IT (230 V) &nbsp;&nbsp;&nbsp;&nbsp; `[ ]` TT (230 V)
* **Lasttype:** `[ ]` Allment / Stikk &nbsp;&nbsp;&nbsp;&nbsp; `[ ]` Varme &nbsp;&nbsp;&nbsp;&nbsp; `[ ]` Motor / Pumpe &nbsp;&nbsp;&nbsp;&nbsp; `[ ]` Elbillading &nbsp;&nbsp;&nbsp;&nbsp; `[ ]` Annet: _________
* **Merkeeffekt ($P$):** ________ kW / W &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **Effektfaktor ($\cos\varphi$):** ________ &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **Fasesystem:** `[ ]` 1-fase `[ ]` 3-fase
* **Forlegningsmåte (Tabell 52):** `[ ]` A1 &nbsp;&nbsp; `[ ]` A2 &nbsp;&nbsp; `[ ]` B1 &nbsp;&nbsp; `[ ]` B2 &nbsp;&nbsp; `[ ]` C &nbsp;&nbsp; `[ ]` D1 &nbsp;&nbsp; `[ ]` E &nbsp;&nbsp; `[ ]` Annet: ______
* **Kabeltype:** _______________________ &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **Isolasjon:** `[ ]` PVC (70 °C) `[ ]` PEX/XLPE (90 °C)
* **Ledermateriale:** `[ ]` Kobber (Cu) `[ ]` Aluminium (Al) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **Valgt tverrsnitt ($A$):** ________ $\text{mm}^2$
* **Kurslengde ($l$):** ________ meter
* **Korreksjonsfaktorer:**
  * Temperaturfaktor ($k_1$): ________ (Omgivelsestemperatur: _____ °C)
  * Samføringsfaktor ($k_2$): ________ (Antall belastede kurser i samme føringsvei: _____)
  * Total reduksjonsfaktor ($k_{\text{tot}} = k_1 \times k_2$): ________

---

### 2. Trinn-for-trinn beregning og verifikasjon

#### Trinn 1: Belastningsstrøm ($I_b$)
* **1-fase formel:** $I_b = \frac{P}{U \cdot \cos\varphi}$
* **3-fase formel:** $I_b = \frac{P}{\sqrt{3} \cdot U \cdot \cos\varphi}$
* **Beregnet verdi:** $I_b =$ **_____________ A**

---

#### Trinn 2: Valg av nominell vernstrøm ($I_n$)
* **Betingelse (Krav 1):** $I_b \le I_n$
* **Valgt vernstørrelse ($I_n$):** **_____________ A**
* **Vernkarakteristikk:** `[ ]` B &nbsp;&nbsp;&nbsp;&nbsp; `[ ]` C &nbsp;&nbsp;&nbsp;&nbsp; `[ ]` D &nbsp;&nbsp;&nbsp;&nbsp; `[ ]` Annet: _____
* **Status:** `[ ]` OK ($I_b \le I_n$)

---

#### Trinn 3: Korrigert strømføringsevne ($I_z$)
* **Tabellverdi fra NEK 400 Tabell 52B ($I_{\text{tab}}$):** _____________ A
* **Beregning:** $I_z = I_{\text{tab}} \cdot k_1 \cdot k_2 =$ ___________________________ A
* **Betingelse:** $I_n \le I_z$
* **Status:** `[ ]` OK ($I_n \le I_z$)

---

#### Trinn 4: Overbelastningsbeskyttelse (Krav 2 / Bolignorm)
* **Vernets øvre prøvestrøm ($I_2$):** $I_2 =$ _____________ A  *(For standard automater normalt $1{,}45 \cdot I_n$, evt. $1{,}2$ – $1{,}3 \cdot I_n$ for boligautomater)*
* **Krav:**
  * **Standard (NEK 400-4-43):** $I_2 \le 1{,}45 \cdot I_z$
  * **Boliginstallasjon $\le 4\text{ mm}^2$ Cu (NEK 400-8-823):** $I_2 \le I_z$
* **Kontroll:** $I_2$ (________ A) $\le$ Grenseverdi (________ A)
* **Status:** `[ ]` OK

---

#### Trinn 5: Spenningsfall ($\Delta U$)
* **Maksimalt tillatt spenningsfall:** `[ ]` 4 % (Belysning) &nbsp;&nbsp;&nbsp;&nbsp; `[ ]` 5 % (Annet) &nbsp;&nbsp;&nbsp;&nbsp; `[ ]` Egendefinert: _____ %
* **Formel:**
  * 1-fase: $\Delta U = \frac{2 \cdot l \cdot I_b \cdot \rho \cdot \cos\varphi}{A}$
  * 3-fase: $\Delta U = \frac{\sqrt{3} \cdot l \cdot I_b \cdot \rho \cdot \cos\varphi}{A}$  
  *(Resistivitet Cu varm leder: $\rho \approx 0{,}0215\ \Omega\cdot\text{mm}^2/\text{m}$ ved 70 °C)*
* **Beregnet spenningsfall:** $\Delta U =$ _____________ V
* **Prosentvis spenningsfall:** $\frac{\Delta U}{U} \cdot 100\ \% =$ **_____________ %**
* **Status:** `[ ]` OK ($\le$ tillatt grense)

---

#### Trinn 6: Minste kortslutningsstrøm og momentan utkobling ($I_{k\text{min}}$)
* **Minste kortslutningsstrøm ytterst på kabelen ($I_{k2\text{pmin}}$):** _____________ A
* **Vernets elektromagnetiske utløsegrense ($I_{\text{inst}}$):**
  * B-karakteristikk: $3 \text{–} 5 \cdot I_n \rightarrow I_5 = 5 \cdot I_n =$ ________ A
  * C-karakteristikk: $5 \text{–} 10 \cdot I_n \rightarrow I_5 = 10 \cdot I_n =$ ________ A
  * D-karakteristikk: $10 \text{–} 20 \cdot I_n \rightarrow I_5 = 20 \cdot I_n =$ ________ A
* **Betingelse:** $I_{k2\text{pmin}} > I_{\text{inst}}$
* **Status:** `[ ]` OK (Momentan utkobling garantert)

---

#### Trinn 7: Maksimal kortslutningsstrøm og bryteevne ($I_{k\text{maks}}$)
* **Maksimal beregnet/målt kortslutningsstrøm ved vernet ($I_{k\text{maks}}$):** _____________ kA
* **Vernets nominelle bryteevne ($I_{\text{cn}}$ / $I_{\text{cu}}$):** _____________ kA
* **Betingelse:** $I_{\text{cn}} \ge I_{k\text{maks}}$
* **Status:** `[ ]` OK

---

#### Trinn 8: Termisk tålegrense ved kortslutning ($I^2t$)
* **Kabelens tålegrense ($k^2 \cdot S^2$):** ________ $\text{A}^2\text{s}$ *(Cu/PVC: $k = 115$, Cu/PEX: $k = 143$)*
* **Vernets gjennomslupne energi ($I^2t$):** ________ $\text{A}^2\text{s}$
* **Betingelse:** $I^2t \le k^2 \cdot S^2$
* **Status:** `[ ]` OK

---

### 3. Konklusjon og signatur

| Kontrollpunkt | Konklusjon / Merknad |
| :--- | :--- |
| **Valgt vern:** | Produsent / Type: ________________________ &nbsp; Strøm: ______ A &nbsp; Karakt.: _____ |
| **Valgt kabel:** | Type: ________________________ &nbsp; Tverrsnitt: ______ $\text{mm}^2$ Cu/Al |
| **Jordfeilvern:** | Type: `[ ]` A `[ ]` B `[ ]` F &nbsp;&nbsp;&nbsp; Merkeutløsestrøm ($I_{\Delta n}$): `[ ]` 30 mA `[ ]` Annet: _____ |

**Installatør / Saksbehandler signatur:** __________________________________ &nbsp;&nbsp;&nbsp;&nbsp; **Dato:** ______________