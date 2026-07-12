# studio-resources

# Resources — Belmont AET

**Live URL:** https://bradwintersmusic-cloud.github.io/studio-resources/

Document and file directory for AET studio resources. Manuals, I/O guides, session templates, input sheets, and other studio documentation. Loads live from a Google Sheet populated via Tally form with Make automation handling Dropbox file routing.

---

## Overview

- List view (default) and card grid view toggle
- File type badges with color coding (PDF, Word, Excel, Pro Tools, Audio, Image)
- Download and preview link indicators per resource
- Filters: category, file type, access type, class, instructor
- Full-text search: title, category, notes, instructor
- Pinned resources appear above the main list
- Click any item to open full detail modal
- Active/inactive flag for hiding without deleting

---

## Data Source

**Google Sheet CSV** — URL defined at the top of the script in `index.html`:

```javascript
var SHEET_CSV_URL = "YOUR_GOOGLE_SHEET_CSV_URL_HERE";
```

To publish: Google Sheets → File → Share → Publish to web → select sheet tab → CSV → copy URL.

---

## Google Sheet Column Headers

Must match exactly (case-sensitive):

| Column          | Required | Notes                                                                       |
| --------------- | -------- | --------------------------------------------------------------------------- |
| Submission Date | Auto     | Written by Tally                                                            |
| Display Name    | No       | User-friendly name; falls back to Title if blank                            |
| Title           | Yes      | Actual file name or document title                                          |
| Category        | Yes      | See category list below                                                     |
| File Type       | No       | PDF, Word, Excel, Pro Tools, Audio, Image — auto-detected from URL if blank |
| Access          | Yes      | Downloadable, Preview Only, or Both                                         |
| Download URL    | No       | Dropbox `dl=1` link                                                         |
| Preview URL     | No       | Dropbox `dl=0` link or Office Online viewer URL                             |
| Instructor      | No       |                                                                             |
| Classes         | No       | Comma-separated class codes                                                 |
| Studios         | No       | Comma-separated studio names                                                |
| Notes           | No       | Description shown in modal                                                  |
| Pinned          | Manual   | TRUE = appears above main list                                              |
| Active          | Manual   | FALSE to hide; missing or TRUE = visible                                    |

---

## Categories

Manual, Equipment Guide, I/O Setup, Session Template, Input Sheet, Patch Sheet, Course Material, Directions, Studio Policy, Reference, Chart, Guide, Signal Flow Diagram, Wiring Diagram, Other

---

## File Type Badge Colors

| Type                       | Color  |
| -------------------------- | ------ |
| PDF                        | Red    |
| Word (.doc/.docx)          | Blue   |
| Excel (.xls/.xlsx)         | Green  |
| Pro Tools (.ptx/.pts/.pio) | Purple |
| Audio (.wav)               | Teal   |
| Image (.png/.jpg)          | Orange |
| Other                      | Grey   |

---

## File Hosting Workflow (Make + Dropbox)

Files are hosted on Dropbox. The Make automation scenario handles routing:

1. Submitter fills Tally form and uploads file
2. Make downloads file from Tally storage
3. Make uploads file to designated Dropbox folder
4. Make creates shared link and writes `dl=1` download URL to sheet
5. Preview URL is added manually if needed (e.g. Office Online viewer link for Word/Excel)

**Dropbox URL formats:**

- Download: change `dl=0` to `dl=1` at end of shared link
- Preview (PDF): change `dl=0` to `raw=1` for direct browser rendering
- Preview (Office): use `https://view.officeapps.live.com/op/view.aspx?src=ENCODED_DROPBOX_URL`

---

## Managing Resources

**To hide a resource:** Set `Active` to `FALSE` in the sheet.
**To pin a resource:** Set `Pinned` to `TRUE` in the sheet.
**To add a display name:** Enter a friendly name in the `Display Name` column. Leave blank to use the `Title` field.

---

## Tech Stack

- Static HTML / CSS / JS
- Google Sheets (CSV data source)
- Tally (form submissions)
- Make (Dropbox automation)
- Dropbox (file hosting)
- GitHub Pages hosting

---

## Repo

`bradwintersmusic-cloud/studio-resources`
Maintained by Brad Winters
