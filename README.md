# Syllabus — from clutter to a single spine

One competency spine that can hold Maharashtra State Board and CBSE without
flattening either. Board textbooks and frameworks are *views* over it; the
concept and the competency are the units, never the chapter.

## Layout

```
PLAN.md                      architecture, layers, possibilities
docs/
  NCFSE-FRAMEWORK.md         what NCF-SE 2023 settles + implications for alignment
  DATASET.md                 NCF-SE dataset: schema, method, limitations
  SCF-DATASET.md             Maharashtra SCF Foundational Stage dataset + alignment
  HPC-DATASET.md             Holistic Progress Card sources (cards + guides)
  SETU-DATASET.md            Setu Abhyas 2026-27 text + image extraction
  TEXTBOOKS-MAH-DATASET.md   Std 3 state textbooks: text, images, renders
  TEXTBOOKS-STD4-DATASET.md  Std 4 state textbooks: text, images, renders
data/
  sources.json               source registry (L0, built from source_manifest.json)
  source_manifest.json       editable metadata for every registered source
  ncfse/                     NCF-SE corpus, section tree, competency spine
  scf/                       SCF corpus, section tree, CGs, competencies,
                             Annexure 1 learning outcomes
  hpc/                       Holistic Progress Card cards + guides (page-anchored)
  setu/                      Setu Abhyas extraction: text, images, page renders
  textbooks/                 Std 3 + Std 4 state textbooks: text, images, renders
  bridge_2026_27/            Setu Abhyas source PDFs (Marathi/English/Urdu)
  alignment/                 SCF ↔ NCF-SE register with difference taxonomy
files/                       source PDFs (as provided)
scripts/                     extraction, index, alignment, validation
requirements.txt             pdfplumber, pymupdf, pypdfium2, pillow
```

## Current state

| Layer | State |
|---|---|
| L0 sources | 71 registered, checksummed: NCF-SE 2023, SCF Foundational 2024, 6 HPC cards/guides, 13 Setu Abhyas books (8 extracted; 5 Urdu await OCR), 42 Std 3 + 8 Std 4 textbooks (2026-27) |
| L1 atoms | NCF-SE 22,907 lines / 227k words; SCF 9,618 lines / 83k words; Setu 19,556 lines / 114,574 words + 986 images; Std 3 textbooks 114,615 lines / 710,967 words + 3,252 unique images (40 extracted; 2 blocked); Std 4 textbooks 20,576 lines / 122,518 words + 2,222 unique images (7 extracted; 1 blocked) |
| L2 concepts | not started (Std 3 textbooks are now in L0/L1) |
| L3 competencies | NCF-SE 205 CGs → 601 competencies; SCF 13 CGs → 68 competencies → 127 outcome rows |
| L4 structures | NCF-SE stages + 8 areas; SCF 192-section tree; board trees pending |
| L5 assessment | principles in `docs/NCFSE-FRAMEWORK.md` §5; HPC cards/guides ingested, descriptor mapping pending |
| L6 generation | not started |
| Alignment | SCF ↔ NCF-SE Foundational: 69 pairs, 12 divergences recorded |

## What the alignment already shows

Maharashtra's Foundational Stage is a close adaptation of NCF-SE: 57 of 68
competencies are the same statement, and the CG numbering coincides. The
differences are small in number and large in consequence:

- safety awareness replaced by movement ease (C-1.5);
- work at school/home narrowed to physical labour for others (C-5.1);
- counting in 5s dropped (C-8.3);
- word problems dropped from addition and subtraction (C-8.6);
- shapes' observable properties and spatial relations dropped (C-8.8);
- the dispositional mathematics competency (C-8.14) has no SCF counterpart.

The full register is `data/alignment/SCF-NCFSE.md`. Annexure 1 adds the
outcome layer beneath the competencies: 68 milestone tables, 127 sub-aspect
rows, five columns अ–इ, page-anchored to the printed SCF.

## Commands

```bash
python3 scripts/show_section.py NCFSE.PA.C03.S04   # read an NCF-SE section
python3 scripts/validate.py                        # NCF-SE invariants
python3 scripts/extract_scf_competencies.py        # SCF CGs + competencies
python3 scripts/extract_scf_grid.py                # Annexure 1 table rules (needs pdfplumber)
python3 scripts/extract_scf_outcomes.py            # Annexure 1 outcome tables
python3 scripts/build_alignment.py                 # SCF ↔ NCF-SE register
python3 scripts/validate_scf.py                    # SCF invariants
python3 scripts/extract_pdf_source.py ...          # any new text PDF -> page corpus
python3 scripts/extract_setu.py --book all         # Setu text + images + page renders
python3 scripts/build_registry.py                  # rebuild data/sources.json
python3 scripts/validate_sources.py                # L0 registry + page corpora
python3 scripts/extract_textbooks.py --all         # Std 3 textbooks: text + images + renders
python3 scripts/extract_textbooks.py --family textbooks_std4 --all   # Std 4 textbooks
python3 scripts/validate_textbooks.py              # textbook page/image invariants
python3 scripts/validate_textbooks.py --family textbooks_std4
```

Re-extraction is documented in `docs/DATASET.md`, `docs/SCF-DATASET.md`,
`docs/HPC-DATASET.md` and `docs/SETU-DATASET.md`.

## The one rule

Every claim resolves to a page. No provenance, no claim.
# syllabus
