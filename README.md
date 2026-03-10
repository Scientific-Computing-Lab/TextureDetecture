# Detecture

<table>
  <tr>
    <td align="center">
      <strong>Browse the live Detecture website</strong><br/>
      Open the published ADE20K site or jump straight to the review gallery.<br/><br/>
      <a href="https://scientific-computing-user.github.io/ade20k-texture-miner-site/">
        <img alt="Browse Detecture Website" src="https://img.shields.io/badge/Browse-Detecture%20Website-0f3c75?style=for-the-badge" />
      </a>
      <a href="https://scientific-computing-user.github.io/rwtd-texture-miner-site/review/">
        <img alt="Open Review Gallery" src="https://img.shields.io/badge/Open-Review%20Gallery-1f8d57?style=for-the-badge" />
      </a>
    </td>
  </tr>
</table>

Detecture is a standalone texture-structure scoring project that asks a narrow question:

"How texturized is this image for real-world texture segmentation?"

It answers that question with a `0-100` score driven primarily by:

- region fragmentation and balance
- texture occupancy
- boundary coherence
- penalties for object-heavy or ambiguous scenes
- optional CLIP and VLM correction layers

This private repository was extracted on `2026-03-10` from a broader mixed workspace so the Detecture scoring project can live as its own code-and-data artifact.

## What This Repository Contains

- Detecture source code under `rwtd_miner/`
- run scripts and configuration under `scripts/`, `configs/`, and `config.yaml`
- a large static review bundle under `docs/review/` with manifests, thumbnails, originals, masks, and overlays
- a private raw ADE20K benchmark copy under `data/raw/ade20k/ADEChallengeData2016/`
- a preserved ADE20K-only website export under `site_exports/ade20k_texture_miner_site/`
- progress diagnostics and audit files under `progress/`
- legacy operational notes copied from the source repo so historical execution context is not lost

Important: the internal Python package name remains `rwtd_miner` for stability. The branding is `Detecture`, but the implementation was extracted without a risky package-wide rename.

## Quick Start

```bash
cd /path/to/Detecture
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

Run the ADE20K Detecture pipeline using the included raw benchmark copy:

```bash
bash scripts/run_detecture_ade20k.sh \
  --out /path/to/detecture_ade20k_eval \
  --ade_root /path/to/Detecture/data/raw/ade20k/ADEChallengeData2016 \
  --skip_download
```

Generic CLI entrypoint:

```bash
bash scripts/detecture_cli.sh ade20k_full \
  --out /path/to/detecture_ade20k_eval \
  --ade_root /path/to/Detecture/data/raw/ade20k/ADEChallengeData2016 \
  --skip_download
```

Open the bundled review website locally:

```bash
xdg-open docs/review/index.html
```

## Included Documentation

- `SCIENTIFIC_README.md`: problem statement, score definition, pipeline design, evaluation logic, and limitations
- `DATA_README.md`: included data inventory, provenance, benchmark terms, and reproduction notes
- `REQUEST_AND_DESIGN.md`: what was requested, how Detecture was separated into its own repo, and the extraction decisions
- `RANKING_EXPLANATION.txt`: concise formula-level explanation of the ranking stack

## Repository Layout

- `rwtd_miner/`: implementation, adapters, scoring stages, utilities
- `scripts/`: operational scripts and Detecture-branded wrappers
- `configs/`: reusable profiles and dataset registry files
- `docs/review/`: repo-resident review bundle for local inspection
- `data/raw/ade20k/ADEChallengeData2016/`: private benchmark copy used for Detecture evaluation
- `site_exports/ade20k_texture_miner_site/`: preserved export of the ADE20K-only project website
- `progress/`: progress board, audits, diagnostics, and prior review summaries

## Detecture Scope

This repository is intentionally narrower than the earlier mixed workspace.

Detecture includes:

- the `1-100` texture suitability scoring system
- ADE20K-based evaluation and review artifacts
- the exported website snapshot that presented this project
- the code paths that generate those outputs

Detecture does not include:

- `.venv` or machine-local dependency installs
- the external `/home/galoren/rwtd_runs` cache tree from the broader multi-dataset workspace
- unrelated existing work under `/home/galoren/Detecture/`

That boundary keeps this repository focused on the scoring project itself and makes a private GitHub repo feasible.

## Provenance

- extraction source snapshot commit only: `2da18efafe8542a5b88f9d3a15b77a9daa9f1435`
- included ADE20K-only site export snapshot commit: `6d73c2a67ed41a3d455cddcea0ae4ef3a80d975e`

## Data Notes

This repository contains third-party benchmark data and generated review assets. Keep it private unless you have separately verified the redistribution terms for every included asset.

ADE20K official sources referenced by the pipeline:

- `https://sceneparsing.csail.mit.edu/`
- `https://data.csail.mit.edu/places/ADEchallenge/ADEChallengeData2016.zip`
- `https://github.com/CSAILVision/ADE20K`

Use `DATA_README.md` before copying or republishing any raw images.
