# LabX

[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](LICENSE)
[![Android](https://img.shields.io/badge/Platform-Android%208.0%2B%20(API%2026%2B)-green.svg)](https://developer.android.com)
[![Kotlin](https://img.shields.io/badge/Kotlin-1.9.22-purple.svg)](https://kotlinlang.org)
[![Compose](https://img.shields.io/badge/Jetpack%20Compose-Material%203-4285F4.svg)](https://developer.android.com/jetpack/compose)
[![Offline](https://img.shields.io/badge/Network-100%25%20Offline-success.svg)](#privacy--offline-first)

**LabX** is an open-source, offline-first scientific workbench and laboratory calculator suite for Android. Designed for molecular biologists, biochemists, and life scientists, it replaces spreadsheets and disparate web tools with 27 rigorous, peer-reviewed calculators right at the laboratory bench.

---

## 🔒 100% Offline & Private

**LabX operates completely offline.**
- **No Internet Permission**: The app does not request or require Android's `android.permission.INTERNET`.
- **Zero Telemetry**: No tracking, ads, third-party analytics, or background telemetry.
- **Your Data Stays on Device**: All calculations, protocols, notes, and datasets are stored locally in an encrypted-at-rest SQLite database (Room v10) and Android DataStore.

---

## 🧪 Dashboard Categories & Modules

The dashboard is structured into **5 categories** hosting **27 offline modules**:

### 1. Solutions & Math
- **Calculator**: Comprehensive scientific calculator with operator precedence, trigonometric functions, logarithms, and calculation history.
- **Dilution Calculator**: Simple ($C_1 V_1 = C_2 V_2$), serial, and fold dilution series, plus weight/volume percent ($w/v, v/v, w/w$) preparation.
- **Buffer Preparation**: Molar mass calculations, Henderson-Hasselbalch pH modeling, and standard recipes (Tris, PBS, TAE, TBE, RIPA, HEPES).
- **Mass-Molarity Converter**: 4-way reactive solver connecting mass, moles, volume, and molarity with an integrated IUPAC periodic table and overshoot volume recovery.
- **Unit Conversion Hub**: Bidirectional converter across 8 scientific measurement domains (mass, volume, concentration, temperature, pressure, length, time, energy).
- **Reaction Setup Calculator**: Biochemical pipetting matrix with master mix scaling and excess factor compensation.

### 2. Nucleic Acids
- **Oligo Analyzer**: Thermodynamic primer melting temperatures ($T_m$ via SantaLucia & Xia nearest-neighbor, Wallace, Marmur-Doty), exact molecular weight, GC content, and extinction coefficient ($\epsilon_{260}$).
- **DNA/RNA Molarity**: Bidirectional concentration $\leftrightarrow$ molarity conversions using NEB exact single/double-strand standards, copy number ($N_A$) calculation, and sequence parser.
- **NEB Calculators**: dsDNA/ssDNA/ssRNA mass-to-moles converters and molar vector:insert ligation ratio optimizer.
- **PCR Calculations**: PCR Master Mix setup with $\mu\text{L}$-first workflows, collapsible concentration rows, reagent catalogue, thermocycling protocols, and DNA polymerase reference.
- **Spectroscopy & Purity**: Beer-Lambert law ($A = \epsilon c l$), $A_{260}$ nucleic acid concentration with background turbidity subtraction ($A_{320}$), and $A_{260}/A_{280}$ & $A_{260}/A_{230}$ purity indices.

### 3. Sequence & Analysis
- **Pairwise Alignment**: Needleman-Wunsch global sequence alignment (EMBOSS Needle) with affine gap penalties and BLOSUM62 / EDNAFULL substitution matrices.
- **Plasmid Viewer (.dna)**: Binary parser for GSL Biotech SnapGene `.dna` files to inspect plasmid sequences, features, primer binding sites, and circular/linear maps.
- **Molecular Cloning**: In silico restriction digest (REBASE database), Gibson assembly junction overlap $T_m$ analyzer, and primer design with self-dimerization checks.
- **Biodiversity & Ecology**: Ecological community metrics including Species Richness ($S$), Total Abundance ($N$), Shannon Diversity ($H'$), Pielou Evenness ($J'$), Simpson Dominance ($D$), and Berger-Parker index ($d$).

### 4. Proteins & Assays
- **ProtParam**: Protein physicochemical profiling: molecular weight, theoretical isoelectric point ($pI$ via Bjellqvist), extinction coefficient ($\epsilon_{280}$ via Pace), instability index, aliphatic index, and GRAVY score.
- **Protein Calculator**: Photometric $A_{280}$ protein concentration, ordinary least squares (OLS) linear standard curves ($R^2$), and ammonium sulfate saturation & volume expansion calculations.
- **SDS-PAGE Load**: Optimal sample lane loading volume from $A_{280}$ measurements and $OD_{600}$ whole-cell lysate pellet normalization across expression induction timepoints.
- **Biophysical Assays**: Levenberg-Marquardt non-linear curve fitting with standard errors and 95% confidence intervals for EMSA (Hill equation), MST, FP (quadratic binding), and ITC (Wiseman isotherm).
- **Antibody Dilution**: Volumetric antibody mixture calculations ($1:D$ ratios) for primary and secondary western blot/immunofluorescence assays.

### 5. Microscopy & Lab Tools
- **Cell Culture Calculator**: Culture vessel surface area library, cell seeding density requirements, doubling time ($t_d$), and yield projections.
- **Microscopy Scale**: Sensor pixel pitch to physical scale calibration, downsampling compensation, 1-2-5 rounded scale bars, and publication print DPI sizing.
- **Laboratory Timers**: Multi-channel foreground timer service running up to 8 independent bench timers simultaneously, custom presets, and stopwatch.
- **Quick Notes**: Markdown experiment notes, protocol checklists, and outcome logs organized in nested folders.
- **Reference Database**: Searchable database for amino acids, nucleotides, laboratory reagents, R scripts, electrophoresis buffer recipes, and DNA/protein ladders.
- **Protocol Planner**: Protocol timeline scheduler with automated overnight incubation logic and live step checkboxes.
- **Experiment Checklist**: Two-phase bench checklist tracking independent reagent preparation and reaction pipetting stages.

---

## 🛠 Technology Stack

- **Language**: [Kotlin](https://kotlinlang.org/) (JVM 17 target)
- **UI Framework**: [Jetpack Compose](https://developer.android.com/jetpack/compose) with [Material 3](https://m3.material.io/) design system
- **Dependency Injection**: [Dagger Hilt 2.50](https://dagger.dev/hilt/)
- **Local Persistence**:
  - [Room 2.6.1](https://developer.android.com/training/data-storage/room) (SQLite Schema Version 10)
  - [Jetpack DataStore Preferences](https://developer.android.com/topic/libraries/architecture/datastore) (reactive UI state)
- **Asynchronous Execution**: Kotlin Coroutines & Flow
- **Export Utilities**: iTextPDF & Apache Commons CSV

---

## 🏗 Building from Source

### Prerequisites
- **Android Studio**: Hedgehog (2023.1.1) or newer
- **JDK**: Java Development Kit 17
- **Android SDK**: API 34 (compileSdk)
- **Minimum Android Version**: Android 8.0 (Oreo, API 26)

### Build Instructions

1. Clone the repository:
   ```bash
   git clone https://github.com/your-username/LabX.git
   cd LabX
   ```

2. Run the test suite:
   ```bash
   ./gradlew test
   ```

3. Build the debug APK:
   ```bash
   ./gradlew assembleDebug
   ```
   The compiled APK will be generated at:
   ```
   app/build/outputs/apk/debug/app-debug.apk
   ```

4. Alternatively, build a signed release bundle:
   ```bash
   ./gradlew bundleRelease
   ```

---

## 📦 Downloads & Releases

Pre-compiled APKs are published with every tagged release:
- Visit [**GitHub Releases**](../../releases) to download the latest `LabX-vX.Y.Z.apk`.
- Sideload onto any Android device running Android 8.0 or higher.

---

## 📚 Technical Documentation

Comprehensive architectural and scientific documentation is maintained in [`docs/`](docs/):

- 📖 [**Module Directory (`docs/modules.md`)**](docs/modules.md) — Detailed catalog of all 27 modules, routes, and features.
- 📐 [**Formula Sources & References (`docs/formulas.md`)**](docs/formulas.md) — Mathematical equations, algorithmic derivations, and literature citations.
- 🗄️ [**Room Database Schema (`docs/room_schema.md`)**](docs/room_schema.md) — Complete specification of all 18 database tables, columns, indexes, and DAOs.
- 🗺️ [**Navigation Architecture (`docs/navigation_map.md`)**](docs/navigation_map.md) — NavHost routing graph, arguments, and inter-module deep links.

---

## 🤝 Contributing

Contributions are welcome! Please review our [**Contributing Guidelines**](CONTRIBUTING.md) and check out our [**Bug Report**](.github/ISSUE_TEMPLATE/bug_report.md) and [**Feature Request**](.github/ISSUE_TEMPLATE/feature_request.md) templates before submitting pull requests.

---

## 📄 License

LabX is licensed under the **Apache License 2.0**. See the [**LICENSE**](LICENSE) file for the full license text.
