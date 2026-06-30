# PhilFIDA Property Sticker Generator

A simple, single‑page web app that turns an Excel spreadsheet of property records
into a print‑ready PDF of property stickers — formatted to the **PhilFIDA Property**
sticker layout.

Everything runs **in your browser**. There is no server, no installation of
programming tools, and **no internet connection needed** after the first load.
Your Excel file never leaves your computer.

---

## What it does

1. You **import an Excel file** (`.xlsx` or `.xls`).
2. You **map** each Excel column to a sticker field (the app auto‑matches by name).
3. You **preview and export** a PDF — one sticker per row, arranged in a neat grid.

### Each sticker contains

| Sticker field | Source |
|---|---|
| Tag No. | *always left blank* |
| Property No. | from Excel |
| Article | from Excel |
| Description | from Excel |
| Model/Serial No. | from Excel |
| Amount | from Excel (auto‑formatted, e.g. `₱161,750.00`) |
| Date of Acquisition | from Excel |
| Issued to | from Excel |

Plus the fixed header (**PhilFIDA PROPERTY** + an editable **Region**), the year
series `2025 – 2031`, the **PhilFIDA** / **COA** signature lines, and the
**PLEASE DO NOT REMOVE** footer.

### Key features

- **9 stickers per page** by default (3 × 3 on Legal paper), perfectly aligned.
  You can also choose 6, 8, 12, 16 per page, or a fixed 2 × 3 inch sticker size.
- **Editable Region** — defaults to `REGION XIII`, but any region can be typed in,
  so other regional offices can reuse the same tool.
- **Text auto‑fits its cell** — long descriptions or serial numbers never spill
  outside their box. In "Fit by sticker size" mode it can even grow the sticker to
  make room.
- **True fonts embedded in the PDF** — headings in **Arial Black**, body text in
  **Cambria** — so the print looks the same on any computer.
- **Scale slider** to size the stickers up or down.
- **Row range filter** — export only rows 1–50, for example.

---

## Installation

This app is just an HTML file. You do **not** need Node.js, Python, or any build
step. You only need a modern web browser (Chrome, Edge, Firefox, or Safari).

### Option A — Download and open (easiest)

1. On the GitHub page, click the green **`Code`** button → **Download ZIP**.
2. Unzip the folder anywhere on your computer.
3. Double‑click **`property-sticker-generator.html`** to open it in your browser.

That's it.

> **Important:** keep **`property-sticker-generator.html`** and **`fonts.js`** in the
> **same folder**. `fonts.js` contains the embedded Cambria + Arial Black fonts used
> for the PDF. If it's missing, the app still works but the PDF falls back to
> standard fonts (Times / Helvetica).

### Option B — Clone with Git

```bash
git clone https://github.com/<your-username>/<your-repo>.git
cd <your-repo>
```

Then open `property-sticker-generator.html` in your browser
(`open property-sticker-generator.html` on macOS, or just double‑click it).

### Option C — Host it online (optional)

Because it is a static file, you can publish it for free with **GitHub Pages**:

1. Push these files to a GitHub repository.
2. Go to **Settings → Pages**.
3. Under *Build and deployment*, set **Source** to *Deploy from a branch*, pick the
   `main` branch and the `/ (root)` folder, and **Save**.
4. After a minute, your app is live at
   `https://<your-username>.github.io/<your-repo>/property-sticker-generator.html`.

---

## How to use

When you open the app, a notice appears explaining how the Excel file must be
prepared (see below). Click **Got it — continue**, then:

1. **Import Excel** — drag your file onto the upload box, or click to browse.
   If the workbook has multiple sheets, pick the right one. A small preview of the
   data is shown.
2. **Map fields** — the app guesses which column goes to which sticker field based on
   the column names. Adjust any of them with the dropdowns. *Tag No.* is always blank.
3. **Preview & export** — set the **Region**, **page size**, and **per‑page** layout,
   review the on‑screen stickers, then click **Export PDF**.

---

## ⚠️ Preparing your Excel file (read this first)

For the app to read your data correctly, the spreadsheet must be **clean and
headerless** — meaning no decorative header block, only column names and data:

- ✅ **Row 1 = the column names only** (e.g. `Property No.`, `Article`,
  `Description`, `Model/Serial No.`, `Amount`, `Date of Acquisition`, `Issued to`).
- ✅ **Row 2 onward = the actual records.**
- ❌ **No title rows** above the data — remove things like *"Republic of the
  Philippines"*, *"PhilFIDA"*, office numbers, addresses, or contact details.
- ❌ **No images** — no logos, signatures, or scanned photos inside the sheet.
- ❌ **No merged cells** and **no blank spacer rows.**

**In short: one header row, then the data. Nothing else.**

#### Example of a correct sheet

| Property No. | Article | Description | Model/Serial No. | Amount | Date of Acquisition | Issued to |
|---|---|---|---|---|---|---|
| 2025-05-04-00003-13TA-01 | Heavy duty Spindle | … | MDL-123 / SN-456 | 161750 | 2025 | ANDAP UPLAND FARMERS |

The column names don't have to match exactly — the app matches similar names
(e.g. "Brand" → Article, "Serial No." → Model/Serial No.) and you can always
re‑map them manually in Step 2.

---

## Files in this project

| File | Purpose |
|---|---|
| `property-sticker-generator.html` | The whole application (open this). |
| `fonts.js` | Embedded Cambria + Arial Black fonts for the PDF. Keep beside the HTML. |
| `format.png` | Reference photo of the official sticker layout. |
| `README.md` | This file. |

---

## Troubleshooting

- **"Could not read file"** — make sure it is a real `.xlsx` or `.xls` file and that
  it follows the clean/headerless rules above.
- **Columns look wrong / shifted** — your sheet probably has title rows or merged
  cells at the top. Delete them so row 1 is the column names.
- **PDF fonts look different** — `fonts.js` is missing or was separated from the
  HTML file. Keep both files together.
- **The peso sign (₱) shows as a box** — this only happens when `fonts.js` is missing;
  with the fonts present it renders correctly.

---

## Technology

- [SheetJS (xlsx)](https://sheetjs.com/) — reads Excel files.
- [jsPDF](https://github.com/parallax/jsPDF) — generates the PDF.
- Plain HTML, CSS, and JavaScript — no framework, no build step.

Both libraries are loaded from a CDN, so the **first** open needs internet; after
that your browser caches them.

---

## License

Free to use and modify for PhilFIDA / government property tagging purposes.
