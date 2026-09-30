# Changelog

All notable changes to LabX are documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [0.1.0] — Unreleased

### Added
- **PCR Calculations** — redesigned Master Mix tab with µL-first workflow, collapsible concentration rows, reagent catalogue, table summary card, and DataStore persistence
- **Ecology tab** — biodiversity metrics (Shannon, Simpson, Pielou, Margalef, Berger-Parker), species-abundance data entry, interpretation guide
- **Experiment Checklist** — two-phase checklist (Prep / Pipette), master mix toggle, dynamic reagent rows with volume/unit fields
- **Oligo Analyzer** — upgraded with OligoCalc-style calculations: salt-adjusted Tm, nearest-neighbour Tm, molecular weight, GC%, extinction coefficient, reverse complement, self-complementarity checks
- **DNA/RNA Molarity** — bidirectional concentration ↔ molarity converter with sequence and length input modes, volume section, quick presets
- **Protocol Planner** — full experiment protocol builder with steps, timers, and export
- **SnapGene Viewer** — plasmid map viewer with feature annotations
- **Scientific Calculator** — expression evaluator with scientific functions

### Changed
- PCR Calculator Hub renamed to **PCR Calculations** across the app
- Buffer default changed from 10× to **5× stock** (5.0 µL per 25 µL reaction)
- DNA/RNA Molarity: Quick Presets now wrap with `FlowRow` instead of overflowing off-screen

### Fixed
- DNA/RNA Molarity: large gap between Quick Presets row and Input Mode toggle caused by 5 chips overflowing a non-wrapping `Row`

## [0.0.7] — 2026-06-26

### Added
- Initial release with 20+ laboratory calculator modules
- Dashboard with four categories: Solutions & Concentrations, Nucleic Acids & Cloning, Microscopy & Lab Tools, Protein & Spectroscopy
- Room database (v10) for history, lab notebook, saved reactions, and protocols
- DataStore-based persistence for calculator states
- Full offline operation — no network access required
- Dark theme with Material 3 design system

---

## Release Notes

### How to install

Download the latest APK from the [Releases](../../releases) page and sideload it on your Android device (Android 8.0+ / API 26+).

Alternatively, build from source:

```bash
git clone https://github.com/your-username/LabX.git
cd LabX
./gradlew assembleDebug
# APK is at app/build/outputs/apk/debug/app-debug.apk
```
