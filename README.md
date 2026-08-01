# A Curated Comprehensive Dataset of Asymmetric Organocatalytic Mannich Reactions

This repository accompanies the paper *"A curated comprehensive dataset of asymmetric organocatalytic Mannich reaction"* and contains the dataset, curation scripts, and figures described therein.

## Project summary

Asymmetric organocatalytic Mannich reactions are a cornerstone method for the stereoselective construction of C–C bonds and nitrogen-containing stereocenters. Despite the large body of literature, reaction data remain scattered across publications in heterogeneous formats, which limits their reuse for data-driven and machine-learning studies.

This dataset addresses that gap. It contains **4,015 asymmetric organocatalytic Mannich reactions** collected from **153 primary publications** and **manually curated** — structures, conditions, and stereochemical outcomes were verified against the original sources rather than automatically extracted. Each entry includes the reaction components as SMILES, the catalyst and its class, reaction conditions, and the reported stereochemical outcome (*ee*, and where available, *dr*). The dataset comprises 468 unique organocatalysts, 538 unique nucleophiles, and 578 unique electrophiles (imines).

> **Note.** The number of unique organocatalyst SMILES may be smaller than 468: atropisomeric BINOL-derived catalysts can share an identical SMILES string (since standard SMILES does not encode axial chirality) while representing distinct catalysts that differ only in the `axial_configuration` column (*R* or *S*). Such cases are counted as separate organocatalysts.

The dataset is intended as a reusable, machine-readable foundation for enantioselectivity prediction, and broader cheminformatics work on organocatalysis.

## Dataset

The dataset is provided in `mannich_dataset/` as `mannich_dataset.csv` (UTF-8). Each row corresponds to a single reaction entry with the following columns:

| Column | Description |
| --- | --- |
| `paper_doi` | DOI of the source publication |
| `electrophile` | Electrophile / imine component (SMILES) |
| `nucleophile` | Nucleophile component (SMILES) |
| `organocatalyst` | Organocatalyst structure (SMILES) |
| `axial_configuration` | Axial chirality descriptor (*R* or *S*) for atropisomeric (e.g. BINOL-type) catalysts, recorded separately because standard SMILES `@`/`@@` encodes only point chirality |
| `organocatalyst_3d_sdf` | Name of the SDF file containing the 3D structure of the organocatalyst |
| `organocatalyst_class` | Catalyst class |
| `organocatalyst_concentration(mol%)` | Catalyst loading (mol % relative to the limiting reagent) |
| `product` | Reaction product (SMILES) |
| `ee` | Enantiomeric excess (%) |
| `ddG_kcal_mol` | Absolute free-energy difference \|ΔΔG‡\| derived from *ee* (kcal/mol); magnitude only, sign not assigned |
| `dr` | Diastereomeric ratio, where reported |
| `syn/anti` | Relative configuration of the major diastereomer (*syn* or *anti*) |
| `yield` | Isolated / reported yield (%) |
| `solvent` | Reaction solvent |
| `temperature` | Reaction temperature (°C) |
| `time` | Reaction time (h) |
| `acid_additive` | Acidic additive, if used |
| `acid_additive_concentration(mol%)` | Loading of the acidic additive (mol % relative to the limiting reagent) |
| `base_additive` | Basic additive, if used |
| `base_additive_concentration(mol%)` | Loading of the basic additive (mol % relative to the limiting reagent) |
| `additive` | Other additive, if used |
| `additive_concentration(mol%)` | Loading of the other additive (mol % relative to the limiting reagent) |
| `water_additive_equiv` | Added water, in equivalents |
| `electrophile/nucleophile` | Molar ratio of electrophile to nucleophile |
| `two_or_three_components` | Whether the reaction is run as a two- or three-component variant (preformed imine vs. in situ from amine + carbonyl), encoded as `0` = two-component and `1` = three-component |
| `molecular_sieves` | Presence of molecular sieves, encoded as `1` = present and `0` = absent |

**Note on stereochemistry.** Tetrahedral stereocenters are encoded with standard SMILES `@`/`@@` notation. Axial chirality of atropisomeric (BINOL-type) catalysts cannot be captured this way and is therefore recorded explicitly in the `axial_configuration` column as a flag (`R`, `S`, or `none`); the corresponding three-dimensional structure is provided as an SDF file whose name is given in the `organocatalyst_3d_sdf` column.

## Scripts

The `scripts/` folder contains the Jupyter notebooks used to generate the catalyst structures and the figures in the paper:

- `scripts/generate_catalysts_sdfs.ipynb` — generates the 3D organocatalyst structures from the catalyst SMILES and axial configuration; the resulting SDF files are written to `mannich_dataset/organocatalysts_sdfs.zip/`.
- `scripts/figures/` — notebooks that reproduce the figures reported in the paper (`figure_02.ipynb`–`figure_04.ipynb`, `figure_06.ipynb`, `figure_07.ipynb`), one notebook per figure.

## Citation

A manuscript describing this dataset is in preparation. Citation details will be added here once it is available. In the meantime, if you use this dataset, please link to this repository.

## License

The dataset is released under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/); code is released under the MIT License (see [`LICENSE`](LICENSE)).
