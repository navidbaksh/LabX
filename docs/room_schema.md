# LabX — Room Database Schema (Version 10)

LabX uses an offline SQLite database via Android Room (`LabDatabase`).

- **Database Class**: `com.labcalcpro.app.data.local.LabDatabase`
- **File Name**: `labcalc_database`
- **Schema Version**: `10`
- **Type Converters**: `RoomTypeConverters`

---

## Entity Schema (18 Tables)

### 1. `calculation_history` (`HistoryEntity`)
Stores calculations performed across modules.
| Column | Type | Constraints | Description |
| :--- | :--- | :--- | :--- |
| `id` | `Long` (INTEGER) | PRIMARY KEY, AUTOINCREMENT | Unique ID |
| `timestamp` | `Long` (INTEGER) | NOT NULL | Epoch time (ms) |
| `moduleTag` | `String` (TEXT) | NOT NULL | Module identifier |
| `expression` | `String` (TEXT) | NOT NULL | Calculation inputs/equation |
| `result` | `String` (TEXT) | NOT NULL | Calculated output string |
| `isPinned` | `Boolean` (INTEGER) | NOT NULL (default `0`) | Pin status (pinned items bypass pruning) |

### 2. `favourites` (`FavouriteEntity`)
Stores user-pinned module configurations.
| Column | Type | Constraints | Description |
| :--- | :--- | :--- | :--- |
| `id` | `Long` (INTEGER) | PRIMARY KEY, AUTOINCREMENT | Unique ID |
| `moduleTag` | `String` (TEXT) | NOT NULL | Target module |
| `label` | `String` (TEXT) | NOT NULL | User label |
| `parameterJson` | `String` (TEXT) | NOT NULL | Serialized parameters |
| `timestamp` | `Long` (INTEGER) | NOT NULL | Epoch time (ms) |

### 3. `rotor_presets` (`RotorPresetEntity`)
Stores centrifuge rotor configurations.
| Column | Type | Constraints | Description |
| :--- | :--- | :--- | :--- |
| `id` | `Long` (INTEGER) | PRIMARY KEY, AUTOINCREMENT | Unique ID |
| `name` | `String` (TEXT) | NOT NULL | Rotor name |
| `minRadius` | `Double` (REAL) | NOT NULL | Minimum radius (mm) |
| `maxRadius` | `Double` (REAL) | NOT NULL | Maximum radius (mm) |
| `avgRadius` | `Double` (REAL) | NOT NULL | Average radius (mm) |

### 4. `timer_presets` (`TimerPresetEntity`)
Stores saved laboratory timer configurations.
| Column | Type | Constraints | Description |
| :--- | :--- | :--- | :--- |
| `id` | `Long` (INTEGER) | PRIMARY KEY, AUTOINCREMENT | Unique ID |
| `name` | `String` (TEXT) | NOT NULL | Timer preset name |
| `durationSeconds` | `Long` (INTEGER) | NOT NULL | Duration in seconds |

### 5. `quick_notes` (`NoteEntity`)
Quick bench notes within the lab notebook.
| Column | Type | Constraints | Description |
| :--- | :--- | :--- | :--- |
| `id` | `Long` (INTEGER) | PRIMARY KEY, AUTOINCREMENT | Unique ID |
| `title` | `String` (TEXT) | NOT NULL | Note title |
| `content` | `String` (TEXT) | NOT NULL | Text / markdown content |
| `timestamp` | `Long` (INTEGER) | NOT NULL | Epoch time (ms) |
| `folderId` | `Long?` (INTEGER) | NULLABLE | Foreign key to `folders.id` |

### 6. `protocols` (`ProtocolEntity`)
Reusable lab protocols written in Markdown.
| Column | Type | Constraints | Description |
| :--- | :--- | :--- | :--- |
| `id` | `Long` (INTEGER) | PRIMARY KEY, AUTOINCREMENT | Unique ID |
| `name` | `String` (TEXT) | NOT NULL | Protocol name |
| `contentMarkdown` | `String` (TEXT) | NOT NULL | Markdown protocol content |
| `isPinned` | `Boolean` (INTEGER) | NOT NULL (default `0`) | Pin status |
| `timestamp` | `Long` (INTEGER) | NOT NULL | Epoch time (ms) |
| `folderId` | `Long?` (INTEGER) | NULLABLE | Foreign key to `folders.id` |

### 7. `experiment_logs` (`ExperimentLogEntity`)
Structured experiment records with outcomes.
| Column | Type | Constraints | Description |
| :--- | :--- | :--- | :--- |
| `id` | `Long` (INTEGER) | PRIMARY KEY, AUTOINCREMENT | Unique ID |
| `title` | `String` (TEXT) | NOT NULL | Experiment title |
| `date` | `Long` (INTEGER) | NOT NULL | Date (ms) |
| `outcome` | `String` (TEXT) | NOT NULL | Outcome tag/status |
| `notes` | `String` (TEXT) | NOT NULL | Detailed observations |

### 8. `folders` (`FolderEntity`)
Hierarchical organization for notes and protocols.
| Column | Type | Constraints | Description |
| :--- | :--- | :--- | :--- |
| `id` | `Long` (INTEGER) | PRIMARY KEY, AUTOINCREMENT | Unique ID |
| `name` | `String` (TEXT) | NOT NULL | Folder name |
| `type` | `String` (TEXT) | NOT NULL | `"note"` or `"protocol"` |
| `parentFolderId` | `Long?` (INTEGER) | NULLABLE | Parent folder ID |
| `timestamp` | `Long` (INTEGER) | NOT NULL | Creation time (ms) |

### 9. `clone_sequences` (`CloneSequence`)
DNA sequences used in molecular cloning.
| Column | Type | Constraints | Description |
| :--- | :--- | :--- | :--- |
| `id` | `Long` (INTEGER) | PRIMARY KEY, AUTOINCREMENT | Unique ID |
| `name` | `String` (TEXT) | NOT NULL | Sequence name |
| `rawSequence` | `String` (TEXT) | NOT NULL | Raw nucleotide sequence |
| `isCircular` | `Boolean` (INTEGER) | NOT NULL | Circular plasmid vs linear |
| `dateCreated` | `Long` (INTEGER) | NOT NULL | Creation time (ms) |
| `notes` | `String` (TEXT) | NOT NULL | Associated notes |

### 10. `restriction_enzymes` (`RestrictionEnzyme`)
REBASE restriction enzyme database.
| Column | Type | Constraints | Description |
| :--- | :--- | :--- | :--- |
| `id` | `Long` (INTEGER) | PRIMARY KEY, AUTOINCREMENT | Unique ID |
| `name` | `String` (TEXT) | NOT NULL | Enzyme name (e.g. EcoRI) |
| `recognitionSequence` | `String` (TEXT) | NOT NULL | Recognition site (IUPAC) |
| `cutPositionTop` | `Int` (INTEGER) | NOT NULL | Cut position on top strand |
| `cutPositionBottom` | `Int` (INTEGER) | NOT NULL | Cut position on bottom strand |
| `overhangType` | `String` (TEXT) | NOT NULL | `"BLUNT"`, `"FIVE_PRIME"`, `"THREE_PRIME"` |
| `methylationSensitive` | `Boolean` (INTEGER) | NOT NULL | Methylation sensitivity |
| `isoschizomers` | `String` (TEXT) | NOT NULL | Comma-separated isoschizomers |

### 11. `constructs` (`Construct`)
In silico assembled cloning constructs.
| Column | Type | Constraints | Description |
| :--- | :--- | :--- | :--- |
| `id` | `Long` (INTEGER) | PRIMARY KEY, AUTOINCREMENT | Unique ID |
| `name` | `String` (TEXT) | NOT NULL | Construct name |
| `sequence` | `String` (TEXT) | NOT NULL | Assembled sequence |
| `strategy` | `String` (TEXT) | NOT NULL | Assembly strategy |
| `dateCreated` | `Long` (INTEGER) | NOT NULL | Creation date |
| `linkedProtocolId` | `Long?` (INTEGER) | NULLABLE | Linked protocol ID |

### 12. `protein_profiles` (`ProteinProfile`)
Saved protein extinction coefficient and molecular weight profiles.
| Column | Type | Constraints | Description |
| :--- | :--- | :--- | :--- |
| `id` | `Int` (INTEGER) | PRIMARY KEY, AUTOINCREMENT | Unique ID |
| `name` | `String` (TEXT) | NOT NULL | Protein name |
| `extinctionCoefficient` | `Double` (REAL) | NOT NULL | $\epsilon_{280}\ (\text{M}^{-1}\text{cm}^{-1})$ |
| `molecularWeight` | `Double` (REAL) | NOT NULL | Molecular weight (Da) |
| `notes` | `String?` (TEXT) | NULLABLE | Notes |
| `createdAt` | `Long` (INTEGER) | NOT NULL | Creation time (ms) |

### 13. `planner_protocols` (`PlannerProtocolEntity`)
Templates for protocol timeline scheduling.
| Column | Type | Constraints | Description |
| :--- | :--- | :--- | :--- |
| `id` | `Long` (INTEGER) | PRIMARY KEY, AUTOINCREMENT | Unique ID |
| `name` | `String` (TEXT) | NOT NULL | Protocol name |
| `stepsJson` | `String` (TEXT) | NOT NULL | Serialized steps list |
| `buffersJson` | `String` (TEXT) | NOT NULL | Serialized buffers list |
| `reagentsJson` | `String` (TEXT) | NOT NULL | Serialized reagents list |

### 14. `planner_runs` (`PlannerProtocolRunEntity`)
Active or completed protocol timeline execution runs.
| Column | Type | Constraints | Description |
| :--- | :--- | :--- | :--- |
| `id` | `Long` (INTEGER) | PRIMARY KEY, AUTOINCREMENT | Unique ID |
| `protocolId` | `Long?` (INTEGER) | NULLABLE | Source protocol ID |
| `name` | `String` (TEXT) | NOT NULL | Run name |
| `stepsJson` | `String` (TEXT) | NOT NULL | Steps with durations |
| `checkedStepsJson` | `String` (TEXT) | NOT NULL | Checked step indices |
| `startTimeMillis` | `Long` (INTEGER) | NOT NULL | Run start timestamp |
| `buffersJson` | `String` (TEXT) | NOT NULL | Buffers list |
| `reagentsJson` | `String` (TEXT) | NOT NULL | Reagents list |

### 15. `saved_buffers` (`SavedBuffer`)
Custom user-defined buffer formulations.
| Column | Type | Constraints | Description |
| :--- | :--- | :--- | :--- |
| `id` | `Long` (INTEGER) | PRIMARY KEY, AUTOINCREMENT | Unique ID |
| `name` | `String` (TEXT) | NOT NULL | Buffer recipe name |
| `components` | `String` (TEXT) | NOT NULL | Serialized component array |

### 16. `saved_reactions` (`SavedReactionEntity`)
Saved biochemical pipetting reaction setups.
| Column | Type | Constraints | Description |
| :--- | :--- | :--- | :--- |
| `id` | `Long` (INTEGER) | PRIMARY KEY, AUTOINCREMENT | Unique ID |
| `name` | `String` (TEXT) | NOT NULL | Reaction name |
| `timestamp` | `Long` (INTEGER) | NOT NULL | Timestamp |
| `totalVolume` | `Double` (REAL) | NOT NULL | Target reaction volume |
| `totalVolumeUnit` | `String` (TEXT) | NOT NULL | Unit ($\mu\text{L}$, $\text{mL}$) |
| `numReactions` | `Int` (INTEGER) | NOT NULL | Reaction count |
| `excessFactor` | `Double` (REAL) | NOT NULL | Pipetting excess fraction |
| `bufferName` | `String` (TEXT) | NOT NULL | Buffer component name |
| `componentsJson` | `String` (TEXT) | NOT NULL | Serialized reagent entries |

### 17. `checklists` (`SavedChecklist`)
Two-phase checklist state & templates.
| Column | Type | Constraints | Description |
| :--- | :--- | :--- | :--- |
| `id` | `Long` (INTEGER) | PRIMARY KEY, AUTOINCREMENT | Unique ID |
| `name` | `String` (TEXT) | NOT NULL | Checklist name |
| `date` | `String?` (TEXT) | NULLABLE | Run date |
| `isTemplate` | `Boolean` (INTEGER) | NOT NULL | Template (`1`) vs Active Run (`0`) |
| `isMasterMix` | `Boolean` (INTEGER) | NOT NULL | Master mix multiplier enabled |
| `masterMixN` | `Int` (INTEGER) | NOT NULL | Master mix reaction count |
| `rows` | `String` (TEXT) | NOT NULL | Serialized rows with prep & pipette checks |

### 18. `saved_ecology_analyses` (`SavedEcologyAnalysis`)
Ecological biodiversity sample datasets.
| Column | Type | Constraints | Description |
| :--- | :--- | :--- | :--- |
| `id` | `Long` (INTEGER) | PRIMARY KEY, AUTOINCREMENT | Unique ID |
| `siteName` | `String` (TEXT) | NOT NULL | Sample/site location |
| `date` | `String` (TEXT) | NOT NULL | Sample date |
| `notes` | `String` (TEXT) | NOT NULL | Environmental observations |
| `speciesRows` | `String` (TEXT) | NOT NULL | Serialized species & counts |
| `shannonIndex` | `Double` (REAL) | NOT NULL | Shannon $H'$ |
| `evenness` | `Double` (REAL) | NOT NULL | Pielou $J'$ |
| `simpsonDiversity` | `Double` (REAL) | NOT NULL | Simpson $D$ |
| `bergerParkerDominance` | `Double` (REAL) | NOT NULL | Berger-Parker $d$ |
| `richness` | `Int` (INTEGER) | NOT NULL | Species richness $S$ |
| `totalAbundance` | `Int` (INTEGER) | NOT NULL | Total individuals $N$ |

---

## Data Access Objects (DAOs)

1. `HistoryDao` — Manages calculation log with automatic 200-item unpinned pruning (`insertAndPrune`).
2. `FavouriteDao` — Module quick-presets and pinned parameters.
3. `PresetDao` — Centrifuge rotors and lab timers.
4. `NotebookDao` — Quick notes, markdown protocols, experiment logs, and nested folders.
5. `CloningDao` — Sequences, restriction enzymes, and recombinant constructs.
6. `ProteinProfileDao` — SDS-PAGE protein profiles ($\epsilon_{280}$, MW).
7. `PlannerDao` — Protocol scheduling templates and active execution runs.
8. `SavedBufferDao` — Reusable buffer preparation recipes.
9. `SavedReactionDao` — Scaled pipetting setups (keeps last 10 runs).
10. `ChecklistDao` — Checklist templates and active runs.
11. `EcologyDao` — Biodiversity analysis persistence.
