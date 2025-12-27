
szv: https://szv.mzcr.cz/
mkn-10 se updatuje jednou rocne ke dni 1.1.
mkn-10: https://www.nzip.cz/data/2479-ciselnik-mkn-10-cz-otevrena-data
mkn-10: https://www.uzis.cz/index.php?pg=registry-sber-dat--klasifikace--mezinarodni-klasifikace-nemoci-mkn-10#publikace

```json
[
  {
    "name": "MKN-10 (Mezinárodní klasifikace nemocí, 10. revize)",
    "steward": "ÚZIS ČR (WHO authorized translation)",
    "scope": "Diagnosis codes (ICD-10-CZ) with descriptions and chapter groupings",
    "access_url": "https://mkn10.uzis.cz (online browser); CSV download via NZIP; VZP ČR ASCII file v932:contentReference[oaicite:0]{index=0}",
    "format": "CSV, ASCII (fixed-width or delimited text), PDF (tabelární část)",
    "schema": ["diag_code", "diag_name_cz", "chapter", "block", "note"],
    "update_cadence": "Infrequent (WHO updates/adaptations as needed; e.g. new codes for emerging diseases)",
    "versioning": "Czech version updated through national updates (e.g. v932 effective 1.1.2025:contentReference[oaicite:1]{index=1})",
    "licensing": "Free official classification (WHO copyright noted; Czech translation © ÚZIS)",
    "official": true
  },
  {
    "name": "Seznam zdravotních výkonů s bodovými hodnotami (SZV)",
    "steward": "Ministerstvo zdravotnictví ČR (MZ ČR)",
    "scope": "Medical service/procedure codes for reimbursement with point values and billing rules",
    "access_url": "MZČR vyhláška (law):contentReference[oaicite:2]{index=2}; Public DB of codes (MZČR ‘SZV’ portal); VZP ČR codebook PDF/CSV:contentReference[oaicite:3]{index=3}",
    "format": "Legal text (PDF); structured dataset via VZP (CSV, PDF)",
    "schema": ["procedure_code", "odbornost (specialty)", "flags/limits", "procedure_name", "points_value", "time_values", "category"],
    "update_cadence": "Multiple revisions annually (major update Jan 1; minor updates mid-year by MZ decrees:contentReference[oaicite:4]{index=4})",
    "versioning": "Issued by decree (e.g. Vyhláška 482/2021 Sb.:contentReference[oaicite:5]{index=5}); VZP internal version numbering (e.g. 01453 for Oct 2025:contentReference[oaicite:6]{index=6})",
    "licensing": "Mandated for use in insurance billing (public law); full datasets freely available to contracted partners:contentReference[oaicite:7]{index=7}, others via paid agreement:contentReference[oaicite:8]{index=8}",
    "official": true
  },
  {
    "name": "CZ-DRG Classification System",
    "steward": "MZ ČR (Národní DRG Centrum, ÚZIS)",
    "scope": "Diagnosis-Related Groups for inpatient cases (grouper definitions, relative weights, markers)",
    "access_url": "MZČR website (distribution package download):contentReference[oaicite:9]{index=9}; CZ-DRG grouper software/API for hospitals",
    "format": "ZIP package (documentation PDFs, CSV/XLS tables, software executables)",
    "schema": ["drg_code", "drg_description", "base_rate_weight", "MDC", "logic_rules", "DRG_markers", "critical_procedures"],
    "update_cadence": "Yearly version releases (e.g. CZ-DRG v6.0 for 2024, v7.0 for 2025):contentReference[oaicite:10]{index=10}:contentReference[oaicite:11]{index=11}; minor revisions if needed",
    "versioning": "Versioned by year (e.g. 6.0, 7.0); change logs provided (differences from previous version):contentReference[oaicite:12]{index=12}",
    "licensing": "Free with registration/acceptance of license terms (MZ ČR sub-license for DRG software/data):contentReference[oaicite:13]{index=13}",
    "official": true
  },
  {
    "name": "VZP Číselníky (General Health Insurance Code Lists)",
    "steward": "VZP ČR (largest insurer)",
    "scope": "Comprehensive billing code lists and control tables for claims: incl. diagnoses, procedures, drugs, medical devices, care types, specialty codes, etc.",
    "access_url": "VZP provider portal (latest versions in PDF/CSV):contentReference[oaicite:14]{index=14}:contentReference[oaicite:15]{index=15}; full datasets via VZP Point (authenticated) or on request:contentReference[oaicite:16]{index=16}",
    "format": "CSV, PDF (human-readable); full data as ASCII text (variable-length, delimiter-separated):contentReference[oaicite:17]{index=17}",
    "schema": "Varies per list (see “Datové rozhraní číselníků” spec:contentReference[oaicite:18]{index=18}); generally code, label, attributes (e.g. prices, validity dates, flags)",
    "update_cadence": "Ongoing — main lists updated ~monthly (effective each 1st of month):contentReference[oaicite:19]{index=19}; some quarterly or yearly. Archives of last published versions online.",
    "versioning": "Each list has its own version number and validity date (e.g. Diagnoses v932:contentReference[oaicite:20]{index=20}, Procedures v1453:contentReference[oaicite:21]{index=21}); changes and replacement noted for each version",
    "licensing": "Latest versions freely downloadable (for reference):contentReference[oaicite:22]{index=22}; complete/current data available to contracted software partners (cost-recovery per vyhláška 418/2003 Sb.):contentReference[oaicite:23]{index=23}",
    "official": "Semi-official: Based on national classifications, with VZP-specific enhancements for internal use"
  },
  {
    "name": "SZP ČR Číselníky (Association of Insurers Code Lists)",
    "steward": "Svaz zdravotních pojišťoven ČR (SZP ČR)",
    "scope": "Shared code lists for member insurers (ČPZP, OZP, ZPMV, RBP, ZPŠ, etc.): largely mirror national/VZP lists for drugs, devices, etc., with insurer-specific entries and validations",
    "access_url": "SZP ČR website (download pages per list – e.g. Hromadně vyráběné LP, ZP):contentReference[oaicite:24]{index=24}:contentReference[oaicite:25]{index=25}; updates also via insurers’ portals",
    "format": "Text (CSV-like .txt), Excel (.xls), plus change logs (xls with diffs):contentReference[oaicite:26]{index=26}",
    "schema": "Aligns with VZP data structure (uses the same field definitions and formats):contentReference[oaicite:27]{index=27}; each list file contains records with code and attributes analogous to VZP’s format",
    "update_cadence": "Regular – typically monthly, effective same dates as VZP updates (e.g. 1st of month):contentReference[oaicite:28]{index=28}. Sync’d with legislative changes and VZP catalog releases",
    "versioning": "Version encoded by date (e.g. HVLP250901 = 1 Sep 2025 release):contentReference[oaicite:29]{index=29}; changes documented in “Změny” files. Methodology v3.2 (2023) governs version control:contentReference[oaicite:30]{index=30}",
    "licensing": "Free to download from SZP ČR site for reference; intended for use by member insurers and their providers. Data largely derived from SÚKL and VZP sources:contentReference[oaicite:31]{index=31}:contentReference[oaicite:32]{index=32}",
    "official": "Authoritative for SZP ČR insurers (parallel to VZP’s lists; built on official data with minor variations)"
  }
]

```