Updated todo list

Ran terminal command:  cd /Users/mcfatem/GitHub/gccb-Reunion-2026 && python3 -c "
import csv

# Read re26-metadata.csv - get original_file_name values
re26 = []
with open('_data/re26-metadata.csv', newline='', encoding='utf-8-sig') as f:
    reader = csv.DictReader(f)
    for row in reader:
        val = row.get('original_file_name', '').strip()
        if val:
            re26.append(val)

# Read Metadata_DC - Reunion2026.csv - get file_name_1 values
dc = []
with open('Metadata_DC - Reunion2026.csv', newline='', encoding='utf-8-sig') as f:
    reader = csv.DictReader(f)
    for row in reader:
        val = row.get('file_name_1', '').strip()
        if val:
            dc.append(val)

re26_set = set(re26)
dc_set = set(dc)

matches = sorted(re26_set & dc_set)
only_re26 = sorted(re26_set - dc_set)
only_dc = sorted(dc_set - re26_set)

print(f'=== COUNTS ===')
print(f're26-metadata.csv original_file_name: {len(re26)} rows ({len(re26_set)} unique)')
print(f'Metadata_DC file_name_1: {len(dc)} rows ({len(dc_set)} unique)')
print()
print(f'=== MATCHES ({len(matches)}) ===')
for m in matches:
    print(f'  {m}')
print()
print(f'=== ONLY IN re26-metadata.csv ({len(only_re26)}) ===')
for m in only_re26:
    print(f'  {m}')
print()
print(f'=== ONLY IN Metadata_DC - Reunion2026.csv ({len(only_dc)}) ===')
for m in only_dc:
    print(f'  {m}')
"


Here's the summary:

---

**Counts**
- `re26-metadata.csv` `original_file_name`: 155 unique values
- `Metadata_DC - Reunion2026.csv` `file_name_1`: 148 unique values
- **Matches: 113**

---

**Only in `re26-metadata.csv` (42 values not in DC)**

Mostly modern JPGs (2016–2021 event photos) plus a few TIFs:
- All the `2016…`, `2019…`, `2020…`, `2021…`, `BOT…`, `winter20BOT…` JPGs (37 files)
- `Commmencement-1977-Photograph_28.tif` (note: extra `.tif` extension)
- `Election Night Party_1962..tif` (double dot)
- `ISOreal-5.jpg` (vs `ISOreal-5` without extension in DC)
- `Latin American Marimba Ensemble in Concert 001.tif`
- `New Student Days-1972-Photograph5.tif` and `…_6.tif`
- `Womens Officers-1961-Photograph_1.tif` / `…_2.tif` (no apostrophe)

---

**Only in `Metadata_DC - Reunion2026.csv` (35 values not in re26)**

- `Commmencement-1977-Photograph_28` — missing `.tif` extension
- `Election Night Party_1962.tif` — single dot (vs double dot in re26)
- `ISOreal-5` — missing `.jpg` extension
- `New Student Days-1972-Photograph_5.tif` (vs `Photograph5.tif` in re26)
- `New Student Days-1972-Photograph_6.tiff` (double-t extension)
- `Student Activities-1993.tif`, `Student Life Photographs-1994_001–006.tif`, `Student Life Photographs-1997.tif`, `Student Life, Music-1994.tif` — 8 files not in re26
- `Student_Activities_Slides_001–011.tif` — 11 files not in re26
- `Town-College-and Community-Photograph_1–6.tif` — 6 files not in re26
- `Women's Officers-1961-Photograph_1–2.tif` (with apostrophe, vs `Womens Officers` in re26)
- `diwali-18.jpg`, `diwali-5.jpg`

---

**Notable near-misses (likely the same file with typos/extension differences):**

| re26 | DC |
|---|---|
| `Commmencement-1977-Photograph_28.tif` | `Commmencement-1977-Photograph_28` (no ext) |
| `Election Night Party_1962..tif` (double dot) | `Election Night Party_1962.tif` |
| `ISOreal-5.jpg` | `ISOreal-5` (no ext) |
| `New Student Days-1972-Photograph5.tif` | `New Student Days-1972-Photograph_5.tif` (missing underscore) |
| `New Student Days-1972-Photograph_6.tif` | `New Student Days-1972-Photograph_6.tiff` (double-t) |
| `Womens Officers-1961-Photograph_1.tif` | `Women's Officers-1961-Photograph_1.tif` (apostrophe) |