# Teknisk og Funksjonell Rapport: Simulatorene i SikringsMesteren

Dette dokumentet beskriver den tekniske oppbygningen, matematiske modellene, visuelle skjemategningene og interaktiviteten for de tre HTML5 Canvas-simulatorene i læringsapplikasjonen **SikringsMesteren**. Rapportens struktur og kodeblokker er optimalisert for direkte import til **VS Code** og videre bearbeiding i **AntiGravity**.

---

## 📋 Innholdsfortegnelse
1. [Oversikt og Integrasjonsarkitektur](#1-oversikt-og-integrasjonsarkitektur)
2. [Simulator 1: Utløserkarakteristikk (B, C, D) & Startstrøm](#2-simulator-1-utløserkarakteristikk-b-c-d--startstrøm)
3. [Simulator 2: Enlinjeskjema, Kabeltemperatur & Spenningsfall](#3-simulator-2-enlinjeskjema-kabeltemperatur--spenningsfall)
4. [Simulator 3: Jordfeilsløyfe & Berøringsspenning ($U_b$)](#4-simulator-3-jordfeilsløyfe--berøringsspenning-ub)
5. [Instruksjoner for AntiGravity & VS Code](#5-instruksjoner-for-antigravity--vs-code)

---

## 1. Oversikt og Integrasjonsarkitektur

Simulatorene er utformet som selvstendige, hendelsesdrevne HTML5 Canvas-moduler uten eksterne biblioteker. De fungerer som det interaktive venstrepanelet i **SikringsMesteren** i henhold til spesifikasjonene i `GAMIFY_TEKNISK_SPESIFIKASJON.md` [9].

### Hovedprinsipper
* **Ren HTML5 Canvas & JavaScript**: Ingen tunge rammeverk; kjører direkte i nettleseren og kan lett moduleres i AntiGravity.
* **Faglig forankring**: Alle beregninger følger forskrift om elektriske lavspenningsanlegg (FEL) [4], NEK 400:2022 (inkludert NEK 400-823 for bolig) [6] og standardutløserkurver for automatsikringer [1, 10].
* **Visuell sanntidsrespons**: Endringer i glidere og valgfelter oppdaterer beregninger og visuelle elementer (kabeloppvarming, kollisjonspunkter, støtindikatorer) umiddelbart [4, 10].

---

## 2. Simulator 1: Utløserkarakteristikk (B, C, D) & Startstrøm

### 2.1 Formål og Faglig Grunnlag
Simulatoren visualiserer sammenhengen mellom en automatsikrings utløserkarakteristikk og belastingens strømprofil over tid [1, 10]. Den viser hvordan innkoblingsstrømmer (*inrush current*) fra motorer og transformatorer kan føre til utilsiktet utkopling dersom feil karakteristikk velges [10, 11].

### 2.2 Matematisk Modell og Grenseverdier
* **Koordinatsystem**: Logaritmisk akse for strøm $I/I_n \in [1, 30]$ på X-aksen og logaritmisk akse for tid $t \in [0.01\text{s}, 1000\text{s}]$ på Y-aksen [10].
* **Termisk utkopling (Bimetall)**: Tilnærmes ved tidsfunksjonen:
  $$t(I) \approx \frac{80}{\left(\frac{I}{I_n} - 1.05\right)^{2.2}}$$
  Gjelder for overbelastningsstrømmer over $1.13 \cdot I_n$ til $1.45 \cdot I_n$ [1, 18].
* **Elektromagnetisk momentanutkopling ($I_5$)**:
  * **B-karakteristikk**: $3 \cdot I_n$ til $5 \cdot I_n$ (Resistive laster, belysning) [1, 10].
  * **C-karakteristikk**: $5 \cdot I_n$ til $10 \cdot I_n$ (Generell last, pumper, standard motorer) [1, 10, 11].
  * **D-karakteristikk**: $10 \cdot I_n$ til $20 \cdot I_n$ (Tunge starter, trafoer, store kompressorer) [10].

### 2.3 Interaktive Kontroller
* **Karakteristikk-velger**: B, C eller D [10].
* **Scenarier / Presets**: Panelovn (1× $I_n$), Standard motor (7× $I_n$, 200 ms), Tung trafo (12× $I_n$, 400 ms), Varig overbelastning (1.6× $I_n$) [10, 11].
* **Manuelle glidere**: Startstrøm-støt ($1\text{x}$ til $25\text{x}$ $I_n$), Startstrømvarighet ($10\text{ ms}$ til $1000\text{ ms}$), Kontinuerlig driftstrøm ($0.5\text{x}$ til $3.0\text{x}$ $I_n$).

### 2.4 Kildekode for Simulator 1

```html
<div class="simulator-container" style="background: #1e1e2e; color: #fff; padding: 20px; border-radius: 12px; font-family: sans-serif;">
  <h3 style="margin-top:0; color: #89b4fa;">⚡ Simulator 1: Utløserkarakteristikk & Startstrøm</h3>
  
  <canvas id="tripCanvas" width="560" height="380" style="background: #181825; border-radius: 8px; width: 100%; height: auto; display: block;"></canvas>
  
  <div class="controls" style="margin-top: 15px; display: grid; grid-template-columns: 1fr 1fr; gap: 12px;">
    <div>
      <label style="font-size: 12px; color: #a6adc8;">Sikringskarakteristikk:</label>
      <select id="curveType" onchange="runSimulation()" style="width: 100%; padding: 8px; background: #313244; color: #fff; border: 1px solid #45475a; border-radius: 6px;">
        <option value="B">B-karakteristikk (3 - 5 × In)</option>
        <option value="C" selected>C-karakteristikk (5 - 10 × In)</option>
        <option value="D">D-karakteristikk (10 - 20 × In)</option>
      </select>
    </div>

    <div>
      <label style="font-size: 12px; color: #a6adc8;">Lastprofil (Scenario):</label>
      <select id="loadPreset" onchange="applyPreset()" style="width: 100%; padding: 8px; background: #313244; color: #fff; border: 1px solid #45475a; border-radius: 6px;">
        <option value="custom">Egendefinert</option>
        <option value="resistor">Panelovn / Lys (Inrush 1×, Drift 1.0×)</option>
        <option value="standard_motor" selected>Standard pumpe/motor (Inrush 7×, 200ms)</option>
        <option value="heavy_motor">Tung trafo / kompressor (Inrush 12×, 400ms)</option>
        <option value="overload">Varig overbelastning (Ingen inrush, Drift 1.6×)</option>
      </select>
    </div>

    <div>
      <label style="font-size: 12px; color: #a6adc8;">Startstrøm-støt (× In): <span id="inrushVal" style="color:#f9e2af; font-weight:bold;">7.0×</span></label>
      <input type="range" id="inrushRatio" min="1" max="25" step="0.5" value="7" oninput="runSimulation()" style="width: 100%;">
    </div>

    <div>
      <label style="font-size: 12px; color: #a6adc8;">Varighet på startstrøm (ms): <span id="durationVal" style="color:#f9e2af; font-weight:bold;">200 ms</span></label>
      <input type="range" id="inrushDuration" min="10" max="1000" step="10" value="200" oninput="runSimulation()" style="width: 100%;">
    </div>

    <div style="grid-column: span 2;">
      <label style="font-size: 12px; color: #a6adc8;">Kontinuerlig driftstrøm (× In): <span id="runVal" style="color:#f9e2af; font-weight:bold;">0.9×</span></label>
      <input type="range" id="runCurrent" min="0.5" max="3.0" step="0.1" value="0.9" oninput="runSimulation()" style="width: 100%;">
    </div>
  </div>

  <div id="statusBox" style="margin-top: 15px; padding: 12px; border-radius: 8px; font-weight: bold; text-align: center; background: #313244; color: #a6e3a1;">
    Sjekker simulering...
  </div>
</div>

<script>
const canvas = document.getElementById('tripCanvas');
const ctx = canvas.getContext('2d');

const BORDERS = { left: 55, right: 20, top: 25, bottom: 40 };
const W = canvas.width - BORDERS.left - BORDERS.right;
const H = canvas.height - BORDERS.top - BORDERS.bottom;

const minX = 1, maxX = 30;
const minY = 0.01, maxY = 1000;

function logX(val) {
  return BORDERS.left + (Math.log10(val / minX) / Math.log10(maxX / minX)) * W;
}

function logY(val) {
  return BORDERS.top + H - (Math.log10(val / minY) / Math.log10(maxY / minY)) * H;
}

const CURVE_LIMITS = {
  'B': { magMin: 3, magMax: 5, color: '#f38ba8' },
  'C': { magMin: 5, magMax: 10, color: '#89b4fa' },
  'D': { magMin: 10, magMax: 20, color: '#fab387' }
};

function applyPreset() {
  const preset = document.getElementById('loadPreset').value;
  if (preset === 'resistor') {
    document.getElementById('inrushRatio').value = 1;
    document.getElementById('inrushDuration').value = 10;
    document.getElementById('runCurrent').value = 0.9;
  } else if (preset === 'standard_motor') {
    document.getElementById('inrushRatio').value = 7;
    document.getElementById('inrushDuration').value = 200;
    document.getElementById('runCurrent').value = 0.9;
  } else if (preset === 'heavy_motor') {
    document.getElementById('inrushRatio').value = 12;
    document.getElementById('inrushDuration').value = 400;
    document.getElementById('runCurrent').value = 0.95;
  } else if (preset === 'overload') {
    document.getElementById('inrushRatio').value = 1.6;
    document.getElementById('inrushDuration').value = 100;
    document.getElementById('runCurrent').value = 1.6;
  }
  runSimulation();
}

function runSimulation() {
  const curve = document.getElementById('curveType').value;
  const inrush = parseFloat(document.getElementById('inrushRatio').value);
  const durationMs = parseFloat(document.getElementById('inrushDuration').value);
  const runI = parseFloat(document.getElementById('runCurrent').value);

  document.getElementById('inrushVal').innerText = inrush.toFixed(1) + '×';
  document.getElementById('durationVal').innerText = durationMs + ' ms';
  document.getElementById('runVal').innerText = runI.toFixed(1) + '×';

  drawGrid();
  drawTripCurve(curve);

  const tripResult = drawAndEvaluateLoad(inrush, durationMs / 1000, runI, curve);

  const statusBox = document.getElementById('statusBox');
  if (tripResult.tripped) {
    if (tripResult.reason === 'magnetic') {
      statusBox.style.background = '#f38ba8'; statusBox.style.color = '#11111b';
      statusBox.innerHTML = `⚠️ TRIPPET MOMENTANT! (Elektromagnetisk utkopling ved ${inrush}× In)`;
    } else {
      statusBox.style.background = '#fab387'; statusBox.style.color = '#11111b';
      statusBox.innerHTML = `🔥 TRIPPET TERMISK! (Overbelastning utkoplet etter ca. ${tripResult.time.toFixed(1)}s)`;
    }
  } else {
    statusBox.style.background = '#a6e3a1'; statusBox.style.color = '#11111b';
    statusBox.innerHTML = `✅ SIKKER DRIFT! Vernet tåler startstrømmen og kontinuerlig last.`;
  }
}

function drawGrid() {
  ctx.clearRect(0, 0, canvas.width, canvas.height);
  ctx.lineWidth = 1;

  const xTicks = [1, 2, 3, 5, 10, 20, 30];
  xTicks.forEach(x => {
    const px = logX(x);
    ctx.strokeStyle = '#313244';
    ctx.beginPath(); ctx.moveTo(px, BORDERS.top); ctx.lineTo(px, BORDERS.top + H); ctx.stroke();
    ctx.fillStyle = '#a6adc8'; ctx.font = '10px sans-serif'; ctx.textAlign = 'center';
    ctx.fillText(x + 'x', px, BORDERS.top + H + 15);
  });

  const yTicks = [0.01, 0.1, 1, 10, 100, 1000];
  yTicks.forEach(y => {
    const py = logY(y);
    ctx.strokeStyle = '#313244';
    ctx.beginPath(); ctx.moveTo(BORDERS.left, py); ctx.lineTo(BORDERS.left + W, py); ctx.stroke();
    ctx.fillStyle = '#a6adc8'; ctx.font = '10px sans-serif'; ctx.textAlign = 'right';
    let label = y < 1 ? (y * 1000) + 'ms' : y + 's';
    ctx.fillText(label, BORDERS.left - 5, py + 3);
  });

  ctx.fillStyle = '#cdd6f4';
  ctx.fillText('Strøm (× In)', BORDERS.left + W / 2, canvas.height - 5);
}

function drawTripCurve(type) {
  const cfg = CURVE_LIMITS[type];
  ctx.strokeStyle = cfg.color; ctx.lineWidth = 3;
  ctx.beginPath();

  let first = true;
  for (let ratio = 1.15; ratio <= cfg.magMax; ratio += 0.1) {
    let t = 80 / Math.pow(ratio - 1.05, 2.2);
    if (ratio >= cfg.magMin) t = Math.min(t, 0.01);
    const px = logX(ratio);
    const py = logY(Math.max(t, 0.01));
    if (first) { ctx.moveTo(px, py); first = false; }
    else { ctx.lineTo(px, py); }
  }

  const pxMag = logX(cfg.magMax);
  ctx.lineTo(pxMag, logY(0.01));
  ctx.lineTo(logX(30), logY(0.01));
  ctx.stroke();

  ctx.fillStyle = cfg.color + '22';
  ctx.lineTo(logX(30), logY(1000));
  ctx.lineTo(logX(1.15), logY(1000));
  ctx.fill();
}

function drawAndEvaluateLoad(inrush, durationSec, runI, type) {
  const cfg = CURVE_LIMITS[type];

  if (inrush >= cfg.magMax && durationSec >= 0.01) {
    drawCollisionPoint(inrush, 0.01);
    return { tripped: true, reason: 'magnetic', time: 0.01 };
  }

  if (runI > 1.13) {
    let tripTime = 80 / Math.pow(runI - 1.05, 2.2);
    drawCollisionPoint(runI, tripTime);
    return { tripped: true, reason: 'thermal', time: tripTime };
  }

  ctx.strokeStyle = '#f9e2af'; ctx.lineWidth = 2;
  ctx.beginPath();
  ctx.moveTo(logX(inrush), logY(1000));
  ctx.lineTo(logX(inrush), logY(durationSec));
  ctx.lineTo(logX(runI), logY(durationSec));
  ctx.lineTo(logX(runI), logY(1000));
  ctx.stroke();

  return { tripped: false };
}

function drawCollisionPoint(ratio, time) {
  const px = logX(Math.min(ratio, 30));
  const py = logY(Math.max(time, 0.01));

  ctx.fillStyle = '#f38ba8';
  ctx.beginPath(); ctx.arc(px, py, 7, 0, 2 * Math.PI); ctx.fill();
  ctx.strokeStyle = '#fff'; ctx.lineWidth = 2; ctx.stroke();
}

runSimulation();
</script>
```

---

## 3. Simulator 2: Enlinjeskjema, Kabeltemperatur & Spenningsfall

### 3.1 Formål og Faglig Grunnlag
Simulatoren viser et dynamisk **enlinjeskjema** for en elektrisk kurs. Den kontrollerer dimensjoneringskravene etter FEL § 21/23 [4] og NEK 400-533.2 / NEK 400-823 [4, 6], samt beregner spenningsfall og kabelens oppvarming under belastning [4, 5].

### 3.2 Formler og Beregningslogikk
* **Belastningsstrøm ($I_b$)**:
  $$I_b = \frac{P}{U \cdot \cos\phi} \quad \text{(Enfase } 230\text{ V, } \cos\phi = 1.0\text{)} [4, 5]$$
* **Korrigert strømføringsevne ($I_z$)**:
  $$I_z = I_{z,\text{tabell}} \cdot k_t [4]$$
  der $k_t$ er korreksjonsfaktor for omgivelsestemperatur ($20\text{ }^\circ\text{C}$ til $50\text{ }^\circ\text{C}$) [4].
* **Spenningsfall ($\Delta u$)**:
  $$\Delta u = \frac{I_b \cdot \rho \cdot L \cdot 2}{A} \quad \text{og} \quad \Delta u_{\%} = \left(\frac{\Delta u}{230}\right) \cdot 100 [4, 5]$$
  ($\rho_{\text{Cu}} = 0.0178\text{ }\Omega\text{mm}^2/\text{m}$) [4].
* **Estimert kabeltemperatur ($T$)**:
  $$T = T_{\text{omg}} + (70 - T_{\text{omg}}) \cdot \left(\frac{I_b}{I_z}\right)^2$$
* **Regelverkssjekk**:
  * **Generelt anlegg**: Krav 1: $I_b \le I_n \le I_z$, Krav 2: $I_2 \le 1.45 \cdot I_z$ ($I_2 = 1.45 \cdot I_n$) [4].
  * **Bolig NEK 400-823**: Krav 1: $I_b \le I_n$, Krav 2: $I_2 \le I_z$ (Spesialvern $I_2 = 1.2 \cdot I_n$ vs. standard $I_2 = 1.45 \cdot I_n$) [6].

### 3.3 Visuelle Elementer
* **Skjemategning**: Tavlefelt, overstrømsvern, kabel og mottaker (last) [4].
* **Dynamisk kabelfarge**: Kabelen endrer farge fra grønn/blå ($20\text{ }^\circ\text{C}$) til glødende rød ($> 70\text{ }^\circ\text{C}$) basert på $T$.
* **Animert elektronstrøm**: Prikker som beveger seg langs kabelen med hastighet proporsjonal med $I_b$.

### 3.4 Kildekode for Simulator 2

```html
<div style="background: #1e1e2e; color: #cdd6f4; padding: 20px; border-radius: 12px; font-family: sans-serif;">
  <h3 style="margin-top:0; color: #89b4fa;">⚡ Simulator 2: Enlinjeskjema, Kabeltemp & Spenningsfall</h3>
  
  <canvas id="schematicCanvas" width="600" height="260" style="background: #181825; border-radius: 8px; width: 100%; display: block;"></canvas>

  <div style="margin-top: 15px; display: grid; grid-template-columns: repeat(auto-fit, minmax(180px, 1fr)); gap: 10px;">
    <div>
      <label style="font-size: 11px; color: #a6adc8;">Regelverk:</label>
      <select id="regType" onchange="updateSchematic()" style="width: 100%; padding: 6px; background: #313244; color: #fff; border: 1px solid #45475a; border-radius: 4px;">
        <option value="general">Generelt anlegg (I₂ ≤ 1.45 Iz)</option>
        <option value="residential" selected>Bolig NEK 400-823 (I₂ ≤ Iz)</option>
      </select>
    </div>

    <div>
      <label style="font-size: 11px; color: #a6adc8;">Lasteffekt P (Watt): <span id="pText" style="color:#f9e2af;">2300 W</span></label>
      <input type="range" id="loadP" min="500" max="6000" step="100" value="2300" oninput="updateSchematic()" style="width: 100%;">
    </div>

    <div>
      <label style="font-size: 11px; color: #a6adc8;">Kabeltverrsnitt (mm²):</label>
      <select id="crossSection" onchange="updateSchematic()" style="width: 100%; padding: 6px; background: #313244; color: #fff; border: 1px solid #45475a; border-radius: 4px;">
        <option value="1.5">1.5 mm² (Iz = 14.5A A1)</option>
        <option value="2.5" selected>2.5 mm² (Iz = 19.5A A1)</option>
        <option value="4.0">4.0 mm² (Iz = 26.0A A1)</option>
        <option value="6.0">6.0 mm² (Iz = 34.0A A1)</option>
      </select>
    </div>

    <div>
      <label style="font-size: 11px; color: #a6adc8;">Kabellengde l (meter): <span id="lText" style="color:#f9e2af;">25 m</span></label>
      <input type="range" id="cableL" min="5" max="80" step="5" value="25" oninput="updateSchematic()" style="width: 100%;">
    </div>

    <div>
      <label style="font-size: 11px; color: #a6adc8;">Vern merkestrøm In:</label>
      <select id="inSelect" onchange="updateSchematic()" style="width: 100%; padding: 6px; background: #313244; color: #fff; border: 1px solid #45475a; border-radius: 4px;">
        <option value="10">10 A</option>
        <option value="13">13 A</option>
        <option value="15">15 A (Bk/Ck)</option>
        <option value="16" selected>16 A</option>
        <option value="20">20 A</option>
      </select>
    </div>

    <div>
      <label style="font-size: 11px; color: #a6adc8;">Omgivelsestemp (°C): <span id="tText" style="color:#f9e2af;">30 °C</span></label>
      <input type="range" id="ambTemp" min="20" max="50" step="5" value="30" oninput="updateSchematic()" style="width: 100%;">
    </div>
  </div>

  <div id="readoutBox" style="margin-top: 12px; padding: 10px; border-radius: 6px; background: #313244; font-size: 13px; line-height: 1.5;">
    Beregningsresultat vises her...
  </div>
</div>

<script>
const c1 = document.getElementById('schematicCanvas');
const ctx1 = c1.getContext('2d');

const TABELL_IZ = { '1.5': 14.5, '2.5': 19.5, '4.0': 26.0, '6.0': 34.0 };
const KT_MAP = { 20: 1.08, 25: 1.04, 30: 1.00, 35: 0.94, 40: 0.87, 45: 0.79, 50: 0.71 };

function updateSchematic() {
  const P = parseFloat(document.getElementById('loadP').value);
  const A = parseFloat(document.getElementById('crossSection').value);
  const L = parseFloat(document.getElementById('cableL').value);
  const In = parseFloat(document.getElementById('inSelect').value);
  const T_omg = parseInt(document.getElementById('ambTemp').value);
  const reg = document.getElementById('regType').value;

  document.getElementById('pText').innerText = P + ' W';
  document.getElementById('lText').innerText = L + ' m';
  document.getElementById('tText').innerText = T_omg + ' °C';

  const Ib = P / 230;
  const kt = KT_MAP[T_omg] || 1.0;
  const Iz = TABELL_IZ[A] * kt;
  
  const dU = (Ib * 0.0178 * L * 2) / A;
  const dU_pct = (dU / 230) * 100;
  const U_mottaker = 230 - dU;

  const cableTemp = T_omg + (70 - T_omg) * Math.pow(Ib / Iz, 2);

  const isBk = (In === 15);
  const I2 = isBk ? 1.2 * In : 1.45 * In;
  const krav1 = (Ib <= In) && (In <= Iz);
  const krav2 = (reg === 'residential') ? (I2 <= Iz) : (I2 <= 1.45 * Iz);

  drawSchematic(Ib, In, Iz, L, A, dU_pct, cableTemp, krav1 && krav2);

  const readout = document.getElementById('readoutBox');
  let statusHtml = `<strong>Beregninger:</strong> Ib = <b>${Ib.toFixed(1)}A</b> | In = <b>${In}A</b> | Korrigert Iz = <b>${Iz.toFixed(1)}A</b><br>`;
  statusHtml += `<strong>Spenningsfall:</strong> Δu = <b>${dU.toFixed(2)}V (${dU_pct.toFixed(2)}%)</b> → Spenning ved last: <b>${U_mottaker.toFixed(1)}V</b><br>`;
  statusHtml += `<strong>Kabeltemperatur:</strong> Estimert kjernetemp: <b style="color:${cableTemp > 70 ? '#f38ba8' : '#a6e3a1'}">${cableTemp.toFixed(0)} °C</b> (Maks 70 °C for PVC)<br>`;

  if (krav1 && krav2 && dU_pct <= 4) {
    statusHtml += `<span style="color:#a6e3a1;">✅ INSTALLASJONEN ER GODKJENT! (Krav 1, Krav 2 og Spenningsfall ≤ 4% OK)</span>`;
  } else {
    statusHtml += `<span style="color:#f38ba8;">❌ AVVIK DETEKTERT: `;
    if (!krav1) statusHtml += `[Krav 1 feilet: Ib ≤ In ≤ Iz] `;
    if (!krav2) statusHtml += `[Krav 2 feilet: I₂ (${I2.toFixed(1)}A) > Iz (${Iz.toFixed(1)}A)] `;
    if (dU_pct > 4) statusHtml += `[Spenningsfall overstiger 4%] `;
    statusHtml += `</span>`;
  }
  readout.innerHTML = statusHtml;
}

function drawSchematic(Ib, In, Iz, L, A, dU_pct, temp, isOk) {
  ctx1.clearRect(0, 0, c1.width, c1.height);

  ctx1.fillStyle = '#89b4fa'; ctx1.fillRect(30, 80, 50, 100);
  ctx1.fillStyle = '#11111b'; ctx1.font = 'bold 12px sans-serif'; ctx1.fillText('TAVLE', 37, 135);

  ctx1.strokeStyle = '#cdd6f4'; ctx1.lineWidth = 3;
  ctx1.beginPath(); ctx1.moveTo(80, 130); ctx1.lineTo(130, 130); ctx1.stroke();
  
  ctx1.fillStyle = '#313244'; ctx1.strokeStyle = '#f9e2af';
  ctx1.fillRect(130, 110, 40, 40); ctx1.strokeRect(130, 110, 40, 40);
  ctx1.fillStyle = '#f9e2af'; ctx1.font = '11px sans-serif'; ctx1.fillText(In + 'A', 140, 134);

  const tempRatio = Math.min(Math.max((temp - 20) / 60, 0), 1);
  const r = Math.round(255 * tempRatio);
  const g = Math.round(255 * (1 - tempRatio));
  const b = Math.round(200 * (1 - tempRatio));
  const cableColor = `rgb(${r},${g},${b})`;

  ctx1.strokeStyle = cableColor; ctx1.lineWidth = Math.max(A * 1.5, 4);
  ctx1.beginPath(); ctx1.moveTo(170, 130); ctx1.lineTo(470, 130); ctx1.stroke();

  const time = Date.now() * 0.003;
  const animX = 170 + ((time * (Ib * 10)) % 300);
  ctx1.fillStyle = '#fff'; ctx1.beginPath(); ctx1.arc(animX, 130, 4, 0, Math.PI * 2); ctx1.fill();

  ctx1.fillStyle = '#a6adc8'; ctx1.font = '11px sans-serif'; ctx1.fillText(`Kabel: ${A}mm² Cu (${L}m)`, 270, 105);
  ctx1.fillStyle = cableColor; ctx1.fillText(`Temp: ${temp.toFixed(0)}°C`, 290, 155);

  ctx1.fillStyle = isOk ? '#a6e3a1' : '#f38ba8';
  ctx1.beginPath(); ctx1.arc(510, 130, 30, 0, Math.PI * 2); ctx1.fill();
  ctx1.fillStyle = '#11111b'; ctx1.font = 'bold 11px sans-serif';
  ctx1.fillText('LAST', 496, 128); ctx1.fillText(`${Ib.toFixed(1)}A`, 496, 142);
}

setInterval(updateSchematic, 100);
</script>
```

---

## 4. Simulator 3: Jordfeilsløyfe & Berøringsspenning ($U_b$)

### 4.1 Formål og Faglig Grunnlag
Simulatoren visualiserer feilstrømsveien og spenningsforholdene ved en 1. jordfeil i henholdsvis **IT-nett** og **TT-nett** [7]. Den demonstrerer beskyttelse mot elektrisk sjokk ved å beregne berøringsspenning ($U_b$) på utvendig apparatkapsling og sjekke kravet $U_b \le 50\text{ V}$ AC [7].

### 4.2 Formler og Beregningslogikk
* **1. Jordfeilstrøm i IT-nett ($I_{\text{feil}}$)**:
  $$I_{\text{feil}} \approx 2\text{ mA} \cdot S_{\text{trafo (kVA)}} [7]$$
  (Basert på systemets kapasitive jordstrømmer) [7].
* **Jordfeilstrøm i TT-nett ($I_{\text{feil}}$)**:
  $$I_{\text{feil}} = \frac{U_0}{R_a + R_b} \quad \text{hvor } U_0 = 132\text{ V (enfase fasespenning)} [7]$$
* **Berøringsspenning ($U_b$)**:
  $$U_b = R_a \cdot I_{\text{feil}} \le 50\text{ V (AC)} [7]$$
* **Jordfeilbryter (RCD)**: Sjekker om strømstrømmen overstiger märkutløsestrømmen ($30\text{ mA}$). Ved utkopling kobles spenningen fra på under $0.2\text{ s}$ [7].

### 4.3 Visuelle Elementer
* **Kretsdiagram**: Viser forsyningstransformator, faseledere, jordfeilvern (RCD), elektrisk apparatkapsling med jordfeil, jordingsresistans ($R_a$) og en person som berører kapslingen [7].
* **Visuell Støt-Advarsel**: Dersom $U_b > 50\text{ V}$ og ingen RCD kopter ut, vises lynsymbol og rød advarsel ved personen [7].

### 4.4 Kildekode for Simulator 3

```html
<div style="background: #1e1e2e; color: #cdd6f4; padding: 20px; border-radius: 12px; font-family: sans-serif; margin-top: 20px;">
  <h3 style="margin-top:0; color: #f9e2af;">⚡ Simulator 3: Jordfeilsløyfe & Berøringsspenning (Ub)</h3>
  
  <canvas id="earthCanvas" width="600" height="280" style="background: #181825; border-radius: 8px; width: 100%; display: block;"></canvas>

  <div style="margin-top: 15px; display: grid; grid-template-columns: repeat(auto-fit, minmax(180px, 1fr)); gap: 10px;">
    <div>
      <label style="font-size: 11px; color: #a6adc8;">Fordelingsnett:</label>
      <select id="netType" onchange="updateEarth()" style="width: 100%; padding: 6px; background: #313244; color: #fff; border: 1px solid #45475a; border-radius: 4px;">
        <option value="IT" selected>IT-nett (230V, 1. feilstrøm ≈ 2mA/kVA)</option>
        <option value="TT">TT-nett (230V / U₀=132V, direkte jord)</option>
      </select>
    </div>

    <div>
      <label style="font-size: 11px; color: #a6adc8;">Trafo ytelse (IT) / Rb (TT):</label>
      <input type="range" id="trafoParam" min="100" max="1000" step="100" value="500" oninput="updateEarth()" style="width: 100%;">
      <span id="trafoText" style="font-size:11px; color:#f9e2af;">500 kVA</span>
    </div>

    <div>
      <label style="font-size: 11px; color: #a6adc8;">Jordingsmotstand Ra (Ω): <span id="raText" style="color:#f9e2af;">60 Ω</span></label>
      <input type="range" id="raInput" min="5" max="150" step="5" value="60" oninput="updateEarth()" style="width: 100%;">
    </div>

    <div>
      <label style="font-size: 11px; color: #a6adc8;">Jordfeilbryter (RCD):</label>
      <select id="rcdSelect" onchange="updateEarth()" style="width: 100%; padding: 6px; background: #313244; color: #fff; border: 1px solid #45475a; border-radius: 4px;">
        <option value="none">Ingen RCD (Kun anleggsjord)</option>
        <option value="30" selected>30 mA Jordfeilautomat</option>
      </select>
    </div>
  </div>

  <div id="earthReadout" style="margin-top: 12px; padding: 10px; border-radius: 6px; background: #313244; font-size: 13px;">
    Jordfeilberegning...
  </div>
</div>

<script>
const c2 = document.getElementById('earthCanvas');
const ctx2 = c2.getContext('2d');

function updateEarth() {
  const net = document.getElementById('netType').value;
  const trafoVal = parseFloat(document.getElementById('trafoParam').value);
  const Ra = parseFloat(document.getElementById('raInput').value);
  const rcd = document.getElementById('rcdSelect').value;

  document.getElementById('trafoText').innerText = net === 'IT' ? trafoVal + ' kVA' : (trafoVal / 50) + ' Ω (Rb)';
  document.getElementById('raText').innerText = Ra + ' Ω';

  let Ifeil = 0;
  if (net === 'IT') {
    Ifeil = (2 * trafoVal) / 1000;
  } else {
    const Rb = trafoVal / 50;
    Ifeil = 132 / (Ra + Rb);
  }

  const Ub = Ra * Ifeil;
  const rcdTripped = (rcd === '30' && Ifeil >= 0.03);

  drawEarthCircuit(net, Ra, Ifeil, Ub, rcdTripped);

  const readout = document.getElementById('earthReadout');
  let html = `<strong>Nettutregning:</strong> 1. Jordfeilstrøm (I_feil) = <b>${Ifeil.toFixed(2)} A</b><br>`;
  html += `<strong>Berøringsspenning:</strong> Ub = Ra · I_feil = ${Ra}Ω · ${Ifeil.toFixed(2)}A = <b style="color:${Ub > 50 && !rcdTripped ? '#f38ba8' : '#a6e3a1'}">${Ub.toFixed(1)} V</b> (Maks 50V AC)<br>`;

  if (rcdTripped) {
    html += `<span style="color:#a6e3a1;">✅ JORDFEILBRYTER UTKOPLET! (30mA RCD brøt kretsen på under 0.2s - Person er trygg)</span>`;
  } else if (Ub <= 50) {
    html += `<span style="color:#a6e3a1;">✅ LOVLIG BERØRINGSSPENNING (Ub ≤ 50V uten utkopling)</span>`;
  } else {
    html += `<span style="color:#f38ba8;">🚨 ULOVLIG OG FARLIG! Ub overstiger 50V! Fare for elektrisk sjokk!</span>`;
  }
  readout.innerHTML = html;
}

function drawEarthCircuit(net, Ra, Ifeil, Ub, rcdTripped) {
  ctx2.clearRect(0, 0, c2.width, c2.height);

  ctx2.fillStyle = '#89b4fa'; ctx2.fillRect(40, 60, 60, 80);
  ctx2.fillStyle = '#11111b'; ctx2.font = 'bold 11px sans-serif'; ctx2.fillText('TRAFO', 50, 105);

  ctx2.fillStyle = '#45475a'; ctx2.fillRect(380, 60, 90, 100);
  ctx2.fillStyle = '#cdd6f4'; ctx2.fillText('APPARAT', 395, 100);

  ctx2.strokeStyle = '#f9e2af'; ctx2.lineWidth = 2;
  ctx2.beginPath(); ctx2.moveTo(100, 80); ctx2.lineTo(380, 80); ctx2.stroke();
  ctx2.beginPath(); ctx2.moveTo(100, 120); ctx2.lineTo(380, 120); ctx2.stroke();

  ctx2.fillStyle = rcdTripped ? '#f38ba8' : '#a6e3a1';
  ctx2.fillRect(220, 70, 30, 60);
  ctx2.fillStyle = '#11111b'; ctx2.fillText('RCD', 223, 104);

  ctx2.fillStyle = '#f38ba8';
  ctx2.beginPath(); ctx2.arc(380, 80, 6, 0, Math.PI * 2); ctx2.fill();

  ctx2.strokeStyle = '#a6e3a1'; ctx2.lineWidth = 3;
  ctx2.beginPath(); ctx2.moveTo(425, 160); ctx2.lineTo(425, 220); ctx2.stroke();

  ctx2.fillStyle = '#a6e3a1'; ctx2.font = '12px sans-serif';
  ctx2.fillText(`Ra = ${Ra}Ω`, 435, 210);

  ctx2.fillStyle = (Ub > 50 && !rcdTripped) ? '#f38ba8' : '#cdd6f4';
  ctx2.beginPath(); ctx2.arc(520, 100, 12, 0, Math.PI*2); ctx2.fill();
  ctx2.fillRect(516, 112, 8, 35);
  ctx2.fillRect(470, 115, 46, 4);

  if (Ub > 50 && !rcdTripped) {
    ctx2.fillStyle = '#f38ba8';
    ctx2.font = 'bold 14px sans-serif';
    ctx2.fillText('⚡ STØT!', 500, 80);
  }
}

updateEarth();
</script>
```

---

## 5. Instruksjoner for AntiGravity & VS Code

### Arbeidsflyt i VS Code
1. Kopier dette dokumentet (`sikringsmesteren-simulatorene.md`) direkte inn i rotmappen i prosjektet ditt.
2. I **AntiGravity** kan du referere til hver enkelt simulatorseksjon når du genererer eller oppdaterer grensesnittet.
3. For å tilpasse Canvas-skalering for mobil/nettbrett, kan du legge til en generell `window.devicePixelRatio`-skalering på Canvas-elementene:

```javascript
function setupResponsiveCanvas(canvasId) {
  const c = document.getElementById(canvasId);
  const dpr = window.devicePixelRatio || 1;
  const rect = c.getBoundingClientRect();
  c.width = rect.width * dpr;
  c.height = rect.height * dpr;
  const ctx = c.getContext('2d');
  ctx.scale(dpr, dpr);
}
```

---
