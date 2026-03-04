# Wayback Policy Scraper

A desktop GUI tool for collecting historical **Terms of Service**, **Privacy Policies**, and other policy documents from the **Internet Archive Wayback Machine**, saving both raw HTML and cleaned text versions locally in a structured format.

 **This tool is currently under active development. Features may change and bugs may exist.**

---

# Overview

Wayback Policy Scraper allows users to:

- Select a platform (e.g., Facebook, TikTok, Discord, etc.)
- Select specific policy types (Terms of Service, Privacy Policy, Community Guidelines, etc.)
- Choose a date range
- Automatically retrieve archived snapshots from the Wayback Machine
- Download and save:
  - Raw HTML
  - Cleaned plain-text version


---

## Structured Output

Each snapshot is saved as:

```
output/
 └── platform/
      └── policy/
           └── YYYYMMDD_HHMMSS/
                ├── raw.html
                └── 20230510123000.txt
```

Additionally, each platform generates a **mastersheet CSV**:

```
platform_mastersheet.csv
```

The CSV contains:

| Column | Description |
|------|------|
| Date Saved | Local timestamp when snapshot was downloaded |
| Platform | Platform name |
| Page Type | Type of policy |
| Snapshot Timestamp | Wayback timestamp |
| Wayback Link | Link to archived page |
| Local Path | Local directory path |

## Resume Support

If a snapshot folder already exists, the program automatically **skips it**.

This allows interrupted downloads to **resume safely without duplicating work**.

## Custom Target Support

Users can add new platforms and policy pages through the GUI.

Custom entries are stored in:

```
custom_targets.json
```

---

# Installation

## 1. Clone the Repository

```bash
git clone https://github.com/yourusername/wayback-policy-scraper.git
cd wayback-policy-scraper

```
## 2. Python Version

```Requires:

Python 3.9+


```
## 3. Install Required Packages


Run:

```bash
pip install requests customtkinter tkcalendar
```

Optional (recommended for improved text extraction):

```bash
pip install readability-lxml lxml
```

---

# How to Run

From the project directory:

```bash
python wayback_gui.py
```

The GUI window will open.

---

# Resume Logic

Before downloading a snapshot, the program checks whether the folder already exists:

```
out/platform/page/YYYYMMDD_HHMMSS/
```

If the directory exists:

- The snapshot is skipped
- The download continues with the next item

This allows interrupted downloads to resume.

---

# Adding Custom Targets

In the GUI:

1. Enter:
   - Platform Name
   - Policy Type
   - Original URL
2. Click **Save Target**

These entries are stored in:

```
custom_targets.json
```

When the program starts:

- Default targets are loaded
- Custom targets are merged automatically

---

# Known Limitations

- Limited rate control beyond a fixed delay between downloads
- Single-threaded download worker
- No automatic policy comparison between versions
- No structured export formats beyond CSV
- Large date ranges may take significant time

---

# Example Output

Example directory structure:

```
out/facebook/terms-of-service/20230510_123000/
```

Files inside:

```
raw.html
20230510123000.txt
```

Plus the platform CSV:

```
facebook_mastersheet.csv
```


# Important Notes

- Internet connection is required.
- Wayback Machine availability may affect performance.
- Large date ranges may produce many snapshots.
- Please respect Internet Archive usage policies.

---

