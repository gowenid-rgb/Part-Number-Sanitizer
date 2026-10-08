# Part-Number-Sanitizer (PDM Batch Search String Generator)

A lightweight, zero-dependency engineering utility designed to extract, clean, and format engineering part numbers (`\d{2}-\d{6}`) from noisy source data (BOM tables, CAD filenames, ERP exports, email bodies, or concatenated strings) into an OR-delimited search string directly compatible with SOLIDWORKS PDM multi-item search inputs.

---

## 🚀 Live Demo & Quick Start

* **Direct Browser Launch:** Open `index.html` or `pdm-batch-search-generator.html` in any browser (Chrome, Edge, Firefox). No build step, node modules, or server required.
* **GitHub Pages Ready:** Enabling GitHub Pages on this repository instantly serves the tool online for your team.

---

## 🎯 Features

* **Intelligent Pattern Matching:**
  * Primary regex: `/(?:\d{2}-\d{6})/g` targeting standard 8-character part numbers (`XX-XXXXXX`).
  * Recovers concatenated, back-to-back codes lacking delimiters (e.g., `93-02374993-023748` → `93-023749` and `93-023748`).
  * Flexible hyphen handling for accidental spaces or en/em dashes (e.g., `93 - 023749`).
* **Noise Stripping:** Automatically removes drawing extensions (`.pdf`, `.sldprt`), revisions (`REV B`, `P-01`), BOM descriptions, and tabular noise.
* **Deduplication:**
  * Enabled by default to prevent redundant query load in PDM.
  * Preserves original appearance order.
  * Toggleable if duplicate occurrence verification is required.
* **Standard PDM Output:**
  * Formatted with the PDM OR-operator: `XX-XXXXXX | XX-XXXXXX | XX-XXXXXX`.
  * Alternative format options: Newline (for Excel column paste), comma-delimited, and semicolon-delimited.
* **Interactive UI & Metrics:**
  * Live metrics: **Total Found**, **Unique Items**, and **Dupes Removed**.
  * 1-Click **Copy to Clipboard** with visual toast confirmation.
  * Clickable part number badges/chips for copying individual items.
  * Keyboard shortcut: <kbd>Ctrl</kbd> + <kbd>Enter</kbd> or <kbd>Alt</kbd> + <kbd>C</kbd> to copy.

---

## 📋 Sample Test Input

Paste the following sample into the tool to verify extraction:

```text
From: Martinez, Carlos <carlos.martinez@exemplis.com>
Subject: RE: ECO-2026-441 - Task Chair Sub-Assembly Components for PDM Check

Hi Greg,
Can you please run a quick PDM check on the following components:
1. 93-023749 REV B.pdf (main cross-bracket)
2. 93-023748 P-01 (armrest socket sleeve)
3. 93-11442293-667788 (concatenated run from table export)
4. Part_93-445566_REV_A.SLDPRT - lumbar spring pin
5. Also check 93-889901 and 93-023749 again.
6. Vendor drawing: 93 - 991122.
```

### Expected Output
```text
93-023749 | 93-023748 | 93-114422 | 93-667788 | 93-445566 | 93-889901 | 93-991122
```

---

## 🛠️ Tech Stack

* Single-file HTML5 / CSS3 / Vanilla JavaScript
* Fully responsive and theme-compatible
* Zero external dependencies or build pipeline
