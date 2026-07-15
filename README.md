# CRRT Recorder — CiCa / Heparin

A single-file, offline web app for recording **Continuous Renal Replacement Therapy (CRRT)** runs at the bedside — capturing the prescription, anticoagulation (regional citrate **CiCa** or **heparin**), circuit pressures and labs at each timepoint — so you can generate trend charts and a case‑ready report afterward.

**▶ Run it live:** https://larrysoo.github.io/CRRT_recording/ (best in Chrome or Edge for NAS folder sync)

Everything is contained in one HTML file (`index.html`, also provided as `crrt-recorder.html`). No installation, no server, no internet required (the charting library is bundled in). Just open the live link above, or download the file and open it in a browser.

> **Not a medical device.** This is a documentation and case‑report aid. It does not provide clinical decision support, and nothing in it should override institutional protocols or clinical judgement. Use only de‑identified data. See the disclaimer at the bottom.

---

## Features

- **Per‑patient CRRT sessions** — modality (CVVH / CVVHD / CVVHDF / SCUF), access, filter/membrane, diagnosis, indication, and full prescription (blood flow, dialysate, replacement pre/post, net UF, dose target).
- **Both anticoagulation protocols** — the form switches automatically:
  - **CiCa (regional citrate):** citrate dose, citrate flow, calcium compensation, post‑filter iCa, systemic iCa, systemic total Ca, and total Ca / iCa ratio.
  - **Heparin:** bolus, infusion rate, aPTT, ACT.
- **Timepoint log** — add as many timepoints as you like (hourly, per lab draw, per adjustment), each with circuit pressures/TMP, blood gas and electrolytes, fluid balance, filter‑change flag, and notes.
- **Automatic safety flags** — out‑of‑range values are highlighted: post‑filter iCa target 0.25–0.35, systemic iCa 1.1–1.3, total Ca/iCa ratio > 2.5 (citrate accumulation), TMP > 200 mmHg, aPTT outside 45–90 s, plus K⁺ and pH ranges.
- **Trend charts** — calcium control, dosing, circuit pressures/TMP, acid–base and K⁺, citrate‑accumulation marker, lactate and cumulative fluid balance.
- **Case‑ready report** — an auto‑written narrative summary plus prescription and timepoint tables. Print / Save as PDF, or download as a Word (`.doc`) file.
- **Exports** — timepoints as CSV, a single case as JSON, and a full JSON backup of all patients (with import).
- **NAS / Synology folder sync** — connect a folder (e.g. your Synology Drive sync folder) and the whole database auto‑saves there as `crrt-database.json`, which the NAS app mirrors up automatically. Includes manual Save/Load and newer‑wins multi‑device merge.

---

## Getting started

1. Download **`crrt-recorder.html`**.
2. Open it in a browser (double‑click, or drag it into a browser window).
   - For **NAS folder sync**, use **Chrome** or **Edge** — the folder‑saving capability (File System Access API) is only available there. All other features work in any modern browser.
3. Click **“+ New patient / session”** and start recording.

Your records are stored in that browser's local storage on that device. Use the **Data / export** tab to back up (JSON) or to connect a NAS folder.

---

## NAS / Synology sync

1. Open the app in Chrome or Edge.
2. Go to the **Data / export** tab → **Connect NAS / Synology folder** → pick your Synology Drive sync folder.
3. Every change now auto‑saves to `crrt-database.json` in that folder; Synology Drive mirrors it to the NAS.
4. On another computer, connect the **same** folder to pick up the records (the more recently edited version of a patient wins when merging).

Because the app is opened as a local file, the browser may occasionally ask you to re‑allow folder access after reopening — click **reconnect** and choose the same folder. The browser copy is always kept as an instant working copy, so no data is lost. To avoid the re‑prompt entirely, serve the file from `http://localhost` instead of opening it directly.

---

## Data & privacy

- All data lives **only in your browser** (and, if you enable it, in the JSON file inside your chosen local/NAS folder). **Nothing is uploaded to any external service** by the app.
- Clearing browser data or switching device/browser will not show records that were only stored locally — **export a JSON backup periodically**, or use folder sync.
- **Keep data de‑identified** — use initials or a study code, never full names or medical record numbers, especially if the NAS or repository is shared.

---

## Reference ranges used for flags

| Field | Flagged when |
|---|---|
| Post‑filter iCa | < 0.25 or > 0.40 mmol/L (target 0.25–0.35) |
| Systemic iCa | < 1.0 or > 1.3 mmol/L |
| Total Ca / iCa ratio | > 2.5 (suggests citrate accumulation) |
| TMP | > 200 mmHg |
| Filter pressure | > 250 mmHg |
| aPTT | < 45 or > 90 s |
| K⁺ | < 3.0 or > 5.5 mmol/L |
| pH | < 7.30 or > 7.50 |
| HCO₃⁻ | < 18 or > 30 mmol/L |
| Lactate | > 4 mmol/L |

These are general surveillance thresholds for highlighting values; **confirm against your unit's own CRRT/CiCa protocol** — targets vary between institutions and machines.

---

## Disclaimer

This software is provided for record‑keeping and case‑report preparation only. It is **not** a medical device and is **not** intended for diagnosis, treatment, or clinical decision‑making. No warranty is given as to accuracy or fitness for any purpose. The user is responsible for the correctness of entered data and for compliance with local privacy regulations and institutional policy. Always follow your institution's protocols and clinical judgement.

## License

Released under the [MIT License](LICENSE).
