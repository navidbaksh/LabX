# LabX — Module Directory

LabX provides **27 offline tools** organized across **5 categories** on the dashboard. Every module is self-contained, reactive, and requires zero network access.

---

## 1. Solutions & Math (`solutions_math`)

| Module | Route | Description | Key Features |
| :--- | :--- | :--- | :--- |
| **Calculator** | `scientific_calc` | Standard & scientific arithmetic calculator | Expression parser, trig functions, powers, logarithms, calculation history |
| **Dilution Calculator** | `dilution` | Solution dilution preparation | Simple $C_1 V_1 = C_2 V_2$, serial dilutions, fold dilution series, % $(w/v, v/v, w/w)$ |
| **Buffer Preparation** | `buffer_prep` | Molar buffer recipe and salt calculations | Dry chemical mass, stock dilution, Henderson-Hasselbalch, standard recipes (Tris, PBS, TAE, TBE, RIPA, HEPES) |
| **Mass-Molarity Converter** | `mass_molarity` | Interconvert mass, moles, molarity, and volume | 4-way reactive solver, built-in IUPAC periodic table formula MW, overshoot mass volume correction |
| **Unit Conversion Hub** | `unit_conversion` | Multi-domain scientific unit converter | 8 categories: mass, volume, concentration, temperature, pressure, length, time, energy |
| **Reaction Setup Calculator** | `reaction_setup` | Scalable reaction pipetting planner | Protein ($A_{280}$), RNA, and small-molecule reactions with master mix excess factor compensation |

---

## 2. Nucleic Acids (`nucleic_acids`)

| Module | Route | Description | Key Features |
| :--- | :--- | :--- | :--- |
| **Oligo Analyzer** | `nucleic_acid` | Oligonucleotide parameter analysis | SantaLucia/Xia nearest-neighbor $T_m$, Wallace rule, Marmur-Doty, salt adjustment, exact MW, $\epsilon_{260}$, OD quantitation |
| **DNA/RNA Molarity** | `dna_rna_molarity` | Bidirectional concentration $\leftrightarrow$ molarity | NEB exact MW equations for dsDNA, ssDNA, ssRNA, dsRNA, copy number calculation ($N_A$), volume section |
| **NEB Calculators** | `neb_calculators` | Mass-to-moles and cloning ligation ratio | dsDNA/ssDNA/ssRNA mass $\leftrightarrow$ moles, vector-to-insert molar ratio ligation optimizer |
| **PCR Calculations** | `pcr_hub` | PCR master mix and thermocycling setup | Reagent catalogue bottom sheet, $\mu\text{L}$-first collapsible concentration rows, polymerase database, extension rates |
| **Spectroscopy & Purity** | `spectroscopy` | Photometric analysis & nucleic acid purity | Beer-Lambert law ($A = \epsilon c l$), $A_{260}$ nucleic acid quantitation, $A_{260}/A_{280}$ & $A_{260}/A_{230}$ purity checks |

---

## 3. Sequence & Analysis (`sequence_analysis`)

| Module | Route | Description | Key Features |
| :--- | :--- | :--- | :--- |
| **Pairwise Alignment** | `needle_alignment` | EMBOSS Needle pairwise sequence alignment | Needleman-Wunsch algorithm with affine gap penalty, BLOSUM62 (protein) & EDNAFULL (nucleic acid) matrices |
| **Plasmid Viewer (.dna)** | `plasmid_viewer` | Binary SnapGene `.dna` file reader | Standalone binary parser for features, primer binding sites, linear/circular plasmid rendering |
| **Molecular Cloning** | `cloning` | In silico molecular biology suite | Restriction digest simulation (REBASE enzymes), Gibson assembly junction overlap $T_m$, primer design & self-dimer check |
| **Biodiversity & Ecology** | `ecology` | Ecological community metrics | Species richness ($S$), abundance ($N$), Shannon diversity ($H'$), Pielou evenness ($J'$), Simpson dominance ($D$), Berger-Parker index |

---

## 4. Proteins & Assays (`proteins_assays`)

| Module | Route | Description | Key Features |
| :--- | :--- | :--- | :--- |
| **ProtParam** | `protparam` | Protein physicochemical characterization | MW, theoretical $pI$ (Bjellqvist), extinction coefficient $\epsilon_{280}$ (Pace), instability index (Guruprasad), aliphatic index, GRAVY score |
| **Protein Calculator** | `protein` | Protein concentration & precipitation | $A_{280}$ spectrophotometric calculation, OLS linear regression standard curve ($R^2$), $(NH_4)_2SO_4$ saturation salt mass & volume expansion |
| **SDS-PAGE Load** | `sds_page_load` | Gel lane loading normalization | Purified protein load volume from $A_{280}$, $OD_{600}$ whole-cell lysate pellet normalization across induction timepoints |
| **Biophysical Assays** | `biophysical_assay` | Non-linear binding curve regression | Levenberg-Marquardt solver with parameter errors and 95% CI: EMSA (Hill equation), MST, FP (quadratic binding), ITC (Wiseman isotherm) |
| **Antibody Dilution** | `antibody_dilution` | Immunoassay reagent dilution | Primary and secondary antibody volumetric ratios ($1:D$) with target buffer volumes |

---

## 5. Microscopy & Lab Tools (`microscopy_tools`)

| Module | Route | Description | Key Features |
| :--- | :--- | :--- | :--- |
| **Cell Culture Calculator** | `cell_culture` | Hemocytometer and culture flask planner | Seeding density, vessel surface areas (dishes, multi-well plates, T-flasks), doubling time ($t_d$), yield projection |
| **Microscopy Scale** | `microscopy_scale` | Micrograph scale calibration & scale bars | Pixel size and coupler magnification calibration, downsampling compensation, 1-2-5 rounded scale bars, print DPI sizing |
| **Laboratory Timers** | `lab_timers` | Multi-timer bench utility | Android Foreground Service, up to 8 independent concurrent timers, custom presets, stopwatch |
| **Quick Notes** | `lab_notebook` | Bench experiment logbook | Markdown editor, protocol notes, experiment outcome logs, folder organization, Room persistence |
| **Reference Database** | `reference_db` | Laboratory reference encyclopaedia | Amino acids (properties, pKa), nucleotides, chemical reagents, R scripts, DNA/protein molecular weight ladders, electrophoresis buffer recipes |
| **Protocol Planner** | `protocol_planner` | Multi-step timeline scheduler | Sequential protocol builder, overnight pause logic, active run tracker with checkboxes |
| **Experiment Checklist** | `experiment_checklist` | Two-phase bench checklist | Independent Prep & Pipetting phase tracking, master mix multiplier ($N$), custom reagent rows |
