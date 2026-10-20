# Easy SDS (Open Source) — Chemical Safety Label Generator

A free, browser-based tool for generating GHS-compliant chemical safety labels with live preview. No installation, no account, no downloads required.

**→ [Open the Tool](https://sam-j-heller.github.io/Easy-SDS-Open-Source/)**

> This is the free open-source edition. Need facility accounts, an approval workflow, an admin console, or a restricted-chemicals list? See the full **[Easy SDS](https://sam-j-heller.github.io/SDSLabelGenerator/)** (facility account required).

---

## What It Does

Easy SDS generates print-ready chemical safety labels in these formats:

- **Full Label** — landscape label that fills a full sheet
- **Sticker Label** — 3 × 4 in, or 4 × 5 in for OL475LP label stock
- **Sticker Sheet** — four stickers laid out on one sheet for bulk printing, plus a **Test 1×** option that prints only the first slot so you can check alignment without wasting a sheet
- **Paper size** — Letter, A4, or SRA3

Both label formats include all six GHS label elements required under OSHA's HazCom 2012 standard, plus NFPA 704 and HMIS rating systems for workplace use.

---

## Getting Started

1. Open the tool in your browser
2. Fill in the left-hand form — the label preview on the right updates in real time
3. When ready, click **Print / Save as PDF** to print or export

That's it. No sign-in required.

---

## The Form — Field by Field

### Chemical Database (Library)
Save and reload chemicals you use regularly. The library is stored in your browser's local storage, so it persists between sessions on the same device.

**Search box** — Type any part of a chemical name to filter the list. Click the box (or press ↓) to browse the full library. Recently used chemicals float to the top.

- **Click a result** — loads the chemical immediately, no extra button needed
- **Arrow keys ↑ ↓** — navigate the list; Enter to select, Escape to close
- **✓ checkmark** — indicates the currently loaded chemical
- **Remove Selected** — appears after a chemical is loaded; deletes it from the library
- **+ Save Current to Library** — saves the current form as a new entry (or overwrites if the product name matches). If the name is very close to an existing chemical (for example a typo or a variant spelling), you get a **Possible Duplicate** warning and can go back or save anyway.

> **Google Drive Sync** — Click **Connect Google Drive** to sync your library across devices. Your library is stored as `chem_label_library.json` in your Drive. Local and remote libraries are merged on sign-in — no data is overwritten. If you're self-hosting this tool, Drive sync needs your own Google OAuth Client ID first — see [Setting Up Google Drive Sync](#setting-up-google-drive-sync-optional) below.

---

### Product
**Product Identifier** — The full name of the chemical or mixture as it appears on the SDS (e.g., `Acetone, 99% ACS`). This populates the large banner at the top of the label. The text automatically shrinks to fit on a single line.

> The browser will suggest the product name as the filename when saving as PDF.

---

### Signal Word
Select the appropriate GHS signal word:

| Option | When to use |
|---|---|
| **DANGER** | More severe hazard category |
| **WARNING** | Less severe hazard category |
| **None** | Chemical is not classified as hazardous — displays "NOT HAZARDOUS" |

---

### Hazard Information
Enter **Hazard Statements** and **Precautionary Statements** from the SDS, one per line, in the single Hazard Information box. (Older exported labels and libraries with a separate precautionary field are merged into this box on import.) A warning appears under the box if the text is too long to fit the printed label. On the full label, statements are automatically split into two columns to make better use of space.

**Example:**
```
H225 Highly flammable liquid and vapour.
H319 Causes serious eye irritation.
P210 Keep away from heat and open flames.
P233 Keep container tightly closed.
```

---

### First Aid
Enter first aid measures from the SDS Section 4. Lines beginning with a phrase followed by a colon (e.g., `If inhaled:`) are automatically bolded on the label for quick readability.

**Example:**
```
If inhaled: Remove to fresh air. Call a doctor if symptoms persist.
If on skin: Wash thoroughly with soap and water.
If in eyes: Rinse with water for 15 minutes. Seek medical attention.
If swallowed: Call Poison Control Center (1-800-222-1222).
```

---

### GHS Pictograms
Check any pictograms that apply. The selected symbols appear in the rotating diamond cluster on the label. All 9 GHS pictograms are available:

| Pictogram | Hazard |
|---|---|
| Flammable | Flammable liquids, solids, gases, pyrophorics |
| Toxic | Acute toxicity (fatal/toxic) |
| Corrosive | Skin/eye corrosion, metal corrosion |
| Oxidizer | Oxidizing liquids, solids, gases |
| Gas Cylinder | Gases under pressure |
| Explosive | Unstable explosives, self-reactives, organic peroxides |
| Health Hazard | Carcinogens, respiratory sensitizers, reproductive toxins |
| Environmental | Aquatic toxicity |
| Irritant | Skin/eye irritation, skin sensitizer, narcotic effects |

Active pictograms are also listed in the **GHS Hazards Present** line of the label's rating guide section.

---

### NFPA 704
The fire diamond displayed on the label. Set each quadrant (0–4) from the SDS or your facility's chemical inventory.

| Quadrant | Color | Meaning |
|---|---|---|
| **Health** | Blue (left) | 0 = No hazard → 4 = Deadly |
| **Flammability** | Red (top) | 0 = Won't burn → 4 = Flash point < 73°F |
| **Instability** | Yellow (right) | 0 = Stable → 4 = May explode at normal conditions |
| **Special** | White (bottom) | OX = Oxidizer, W = Water reactive, SA = Simple asphyxiant |

---

### HMIS
The color-coded bar system used for daily worker safety. HMIS uses the same 0–4 scale as NFPA for Health, Flammability, and Reactivity.

**Sync from NFPA** — Click the blue **↓ Sync from NFPA** button to automatically copy the NFPA Health, Flammability, and Instability values into the corresponding HMIS fields.

**Personal Protection (PPE)** — Select the HMIS PPE letter code from the SDS. The label automatically expands the code into plain-English equipment requirements:

| Code | PPE Required |
|---|---|
| A | Safety Glasses |
| B | Safety Glasses + Gloves |
| C | Safety Glasses + Gloves + Apron |
| D | Face Shield + Gloves + Apron |
| E | Safety Glasses + Gloves + Dust Respirator |
| F | Safety Glasses + Gloves + Apron + Dust Respirator |
| G | Safety Glasses + Gloves + Vapor Respirator |
| H | Splash Goggles + Gloves + Apron + Vapor Respirator |
| I | Safety Glasses + Gloves + Dust & Vapor Respirator |
| J | Splash Goggles + Gloves + Apron + Dust & Vapor Respirator |
| K | Air-Line Hood/Mask + Gloves + Full Suit + Boots |

**Additional PPE** — Automatically computed from the selected HMIS code by removing baseline facility PPE (safety glasses, gloves) that all employees already wear. This appears in the sticker footer and the GHS Hazards Present bar on the full label. Type in the field to override it; clear the field to go back to the automatic value.

> Baseline facility PPE requirements always apply regardless of HMIS code.

---

### Supplier Info

Fills the bottom-right section of the label. All fields are optional but **Company Name**, **Address**, and **Emergency Phone** are required for a fully GHS-compliant label.

| Field | Example |
|---|---|
| **Company Logo** | Upload an image (PNG, JPG, SVG) — appears top-right on the full label and bottom-left on the sticker. Use **Remove logo** to clear it. |
| Company Name | Acme Manufacturing |
| Address | 123 Warehouse Blvd, Richmond, VA 23220 |
| Emergency Phone | 1-800-424-9300 (CHEMTREC) |
| Prepared By | J. Smith |
| Date | Auto-filled with today's date |

The logo is stored in your browser's local storage and persists between sessions.

---

### Favorites
**★ Favorites** (next to the print controls) keeps a short list of labels you reprint often. Click **★ Favorite** to pin the current form, click a favorite to load it, and use the ✕ to remove it. Favorites are stored in your browser.

---

## Printing

1. Click **Print / Save as PDF** (red button at the top of the form)
2. In your browser's print dialog:
   - Set paper size to match the **Letter / A4 / SRA3** button you selected, and orientation to **Landscape** (for the full label)
   - Set margins to **None**
   - Enable **Background graphics** so colors print correctly
3. Print, or choose **Save as PDF** to get a file

> The sticker (3×4 in) mode prints portrait. The Sheet mode arranges four stickers on a single letter-size sheet for cutting.

---

## Label Size Toggle

Use the buttons below the print button to switch between formats:

| Button | Format |
|---|---|
| **Full Label** | Full-size landscape label |
| **Sticker** | Single sticker, portrait, in **3×4in** or **4×5in (OL475LP)** |
| **Sheet 4×** | Sub-option under Sticker — four stickers on one sheet |
| **Test 1×** | Sub-option under Sticker — prints only the first slot of the sheet for an alignment check |
| **Letter / A4 / SRA3** | Paper size for the print page |

The preview and print output switch together.

---

## Export / Import

The **Export / Import** dropdown (green button) offers these options:

| Option | What it does |
|---|---|
| **Export label as JSON** | Saves the current form as a `.json` file you can re-import later |
| **Import label from JSON** | Loads a previously exported label `.json` back into the form |
| **Export full library** | Saves your entire chemical library as a `.json` file. Prompts for your name and auto-includes the export date in the filename. |
| **Import into library** | Merges a library `.json` into your current library — skips any chemical whose name already exists |
| **Save HTML with Library** | Downloads a copy of this page with your library baked in, so you can hand it to someone else. On first open it merges into their library without overwriting anything they already have. |

---

## Setting Up Google Drive Sync (Optional)

Drive sync lets your chemical library follow you across browsers and devices instead of staying stuck in one browser's localStorage. It's entirely optional — the tool works fully without it via the **Export/Import JSON** buttons.

Because this is a no-backend, single-file tool, Drive sync needs its own Google OAuth Client ID tied to *your* hosted copy — the original author's Client ID only works for their own GitHub Pages URL. Setting up your own takes about 5 minutes and is free:

1. **Create a Google Cloud project** at [console.cloud.google.com](https://console.cloud.google.com/) (or reuse an existing one).
2. **Enable the Google Drive API**: *APIs & Services → Library* → search "Google Drive API" → **Enable**.
3. **Configure the OAuth consent screen**: *APIs & Services → OAuth consent screen*.
   - User type: **External**
   - Add the scope `https://www.googleapis.com/auth/drive.file`
   - Add yourself (and anyone else who'll use Drive sync) as a **test user** — or click **Publish App** to allow any Google account to sign in without an allowlist. (`drive.file` is a low-sensitivity scope, so Google typically doesn't require a verification review for it.)
4. **Create an OAuth Client ID**: *APIs & Services → Credentials → Create Credentials → OAuth client ID*.
   - Application type: **Web application**
   - Authorized JavaScript origins: the URL you're hosting the tool at (e.g. `https://yourusername.github.io`), plus `http://localhost:PORT` if you also test locally
   - No redirect URI needed
5. **Copy the generated Client ID** (looks like `123456789-abc...apps.googleusercontent.com`).
6. **Paste it into `index.html`**, replacing the placeholder:
   ```js
   const GOOGLE_CLIENT_ID = 'YOUR_GOOGLE_CLIENT_ID.apps.googleusercontent.com';
   ```
7. Upload the edited `index.html` to your GitHub repo. Drive sync now works for anyone using your hosted copy.

> Client IDs aren't secret — they're safe to commit — but each one is locked to the "Authorized JavaScript origins" you configured, so it only works on the domain(s) you listed. If someone forks this repo to host their own copy, they'll need to repeat these steps with their own Client ID.

---

## What's on the Label

The printed label includes all six GHS-required elements:

1. **Product Identifier** — chemical name (top banner, auto-sizing)
2. **Signal Word** — DANGER or WARNING
3. **GHS Pictograms** — rotating diamond cluster
4. **Hazard & Precautionary Statements** — bottom left, two-column layout
5. **First Aid** — bottom center
6. **Supplier Information** — bottom right (including company logo if uploaded)

Additionally, the label includes:
- **NFPA 704 diamond** with color-coded quadrants and a built-in 0–4 rating guide
- **HMIS bars** with PPE code and plain-English equipment requirements
- **GHS Hazards Present** bar listing all active pictogram names, with Additional PPE Required on the right
- **Emergency reference bar** — Call 911 · Poison Control 1-800-222-1222 · CHEMTREC 1-800-424-9300

---

## Tips

- **Work from the SDS** — all values (signal word, H/P statements, NFPA/HMIS ratings, pictograms) are found in the SDS for the chemical.
- **Save frequently used chemicals** to the library so you can reload them without re-entering data. Type in the search box to filter quickly.
- **Use Google Drive sync** if multiple people need access to the same chemical library.
- **First Aid formatting** — start each line with `Scenario:` (e.g., `If inhaled:`) and it will bold automatically on the label.
- **Additional PPE** — leave the field blank to auto-compute from the HMIS code, or type your own value to override.
- **Clear Form** resets all fields and sets the date to today.

---

## Technical Notes

- Single-file HTML — no frameworks, no dependencies, no server, no account or sign-in
- Feature-matched to the hosted Easy SDS label tool. Facility accounts, the approval workflow, the admin console, and the restricted-chemicals list need a backend and are not part of this version.
- All data stays in your browser (localStorage) unless you connect Google Drive
- Works in Chrome, Edge, Firefox, and Safari
- Pictograms are rendered as inline SVG — no external image files needed
- The browser uses the product name as the suggested filename when saving as PDF

---

## GHS Label Requirements Reference

Per OSHA HazCom 2012 (29 CFR 1910.1200), secondary container labels must include:

- Product identifier
- Signal word
- Hazard pictogram(s)
- Hazard statement(s)
- Precautionary statement(s)
- Name, address, and phone number of the responsible party

*This tool is designed to support compliance but does not substitute for reviewing the SDS and confirming accuracy with your safety officer.*
