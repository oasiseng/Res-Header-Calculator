# Residential Header & Beam Sizing Calculator

NDS 2018 / IRC 2021 — Allowable Stress Design (ASD)

A browser-based structural engineering calculator that sizes residential headers and beams per the National Design Specification for Wood Construction (NDS 2018) and the International Residential Code (IRC 2021). Generates downloadable PDF spec sheets suitable for permit applications.

## Features

### Lumber Support
- **Sawn dimensional lumber**: 8 species groups (Douglas Fir-Larch, Hem-Fir, Southern Pine, Spruce-Pine-Fir, Redwood, and regional variants), Select Structural through #3 grades
- **LVL** (Laminated Veneer Lumber): 1.9E, 2.0E, 2.1E products
- **PSL** (Parallel Strand Lumber): 1.8E, 2.0E Parallam products
- **LSL** (Laminated Strand Lumber): 1.35E, 1.55E TimberStrand products
- **Glulam**: 24F-V4, 24F-V8, 20F-V7, 16F-V2 combinations
- Custom value entry for all engineered lumber types

### Calculation Engine
- Full NDS beam design: bending, shear, deflection, and bearing checks
- Design span per NDS 3.2.1 (clear span + bearing length adjustment)
- ASD load combinations per IBC 1605.3.1
- Load duration factor (C_D) per NDS 2.3.2.1 — shortest duration load in combination governs
- Size factor (C_F) per NDS Supplement Table 4A (not applied to Southern Pine)
- Volume/depth factor (C_V) for glulam (NDS 5.3.6, x=10 Western / x=20 Southern Pine) and SCL (NDS 8.3.6)
- Lesser of C_L or C_V used for glulam and SCL per code — never both
- C_r = 1.0 for all headers (built-up headers are not repetitive members per NDS 4.3.9)
- Long-term deflection with creep factor K_cr = 1.5 per NDS 3.5.2
- Serviceability deflection uses unreduced transient loads per IBC Table 1604.3
- Optional shear reduction at d from support face per NDS 3.4.3.1
- Bearing check included in pass/fail determination
- Jack stud count derived from bearing demand, not span rules of thumb

### Two Calculation Modes
- **IRC Prescriptive**: Select load case (roof only, one floor + roof, two floors + roof), building width, eave overhang, snow load, and floor live load. Tributary widths and loads calculated automatically.
- **NDS Engineering**: Full custom input for dead load, floor live, roof live, snow, tributary width, additional uniform loads, C_D override, and deflection limit selection.

### Output
- Pass/fail banner with governing load combination
- Five structural checks with utilization bars (bending, shear, transient deflection, total deflection with creep, bearing)
- Complete load combination analysis table
- NDS adjusted design values with all applicable factors
- Bearing and framing requirements (jack studs, king studs, connection hardware with Simpson Strong-Tie references)
- SVG framing diagram
- PE seal and signature block
- Downloadable PDF spec sheet with Oasis Engineering letterhead
- Browser print fallback with clean print stylesheet

## Usage

### Quick Start
Open `header-calc.html` in a browser. No build step, no dependencies to install — it's a single self-contained HTML file.

For local development (recommended for PDF generation):
```bash
python3 -m http.server 8000
# then open http://localhost:8000/header-calc.html
```

The PDF download requires the jsPDF library loaded from CDN. If testing via `file://` protocol, use the "Print to PDF" fallback button or serve the file locally as shown above.

### Embedding
The calculator is a single HTML file that can be embedded via `<iframe>` or included directly in a website. The print/PDF output automatically hides navigation, site headers/footers, and other wrapper elements.

## Engineering Notes

- All sawn lumber reference design values are from NDS 2018 Supplement Table 4A
- Southern Pine uses size-specific F_b values (Table 4B treatment) with C_F = 1.0
- Engineered lumber values are generic/typical — users should verify against the manufacturer's ICC-ES Evaluation Service Report (ESR) for the specific product
- The depth factor exponents for engineered lumber (LVL: 0.136, PSL: 0.111, LSL: 0.143) are representative of common manufacturer standards; verify against specific ESR
- Load assumptions in IRC mode: roof DL = 12 psf, ceiling DL = 5 psf, floor DL = 10 psf, wall DL = 7 plf per foot of height, roof LL = 20 psf, ground snow converted at 0.7 factor
- Eave overhang adds to roof tributary width only, not floor tributary width

## Limitations

- Simple span, uniformly distributed loads only — no point loads, cantilevers, or continuous spans
- Lateral bracing assumed adequate (C_L = 1.0) — no unbraced length analysis
- Dry service (C_M = 1.0) and normal temperature (C_t = 1.0) only
- Does not address lateral/wind/seismic loads on the wall or opening
- Does not check axial loads (F_t, F_c) — bending, shear, deflection, and bearing only
- Notching and hole effects not considered

## License

Proprietary — Oasis Engineering. All rights reserved.
