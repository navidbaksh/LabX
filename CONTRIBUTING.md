# Contributing to LabX

Thank you for your interest in contributing to LabX! This document provides guidelines for contributing to the project.

## Getting Started

1. **Fork the repository** and clone it locally
2. Set up your development environment (Android Studio Hedgehog or newer)
3. Make sure you can build the project: `./gradlew assembleDebug`
4. Run the tests: `./gradlew test`

## How to Contribute

### Reporting Bugs

- Use the **Bug Report** issue template
- Include steps to reproduce, expected behaviour, and actual behaviour
- Include your Android version and device model
- Attach screenshots if applicable

### Suggesting Features

- Use the **Feature Request** issue template
- Describe the use case — what scientific workflow does this help with?
- If you have a specific formula or reference, include it

### Submitting Code

1. Create a feature branch from `main`: `git checkout -b feature/your-feature`
2. Follow the existing code style (Kotlin, Jetpack Compose, Material 3)
3. Add unit tests for any new calculations or formulas
4. Ensure all tests pass: `./gradlew test`
5. Ensure the APK builds cleanly: `./gradlew assembleDebug`
6. Submit a pull request with a clear description

## Code Style

- **Language**: Kotlin
- **UI**: Jetpack Compose with Material 3
- **Architecture**: ViewModel + Repository pattern with Hilt DI
- **Formatting**: Follow standard Kotlin conventions
- **Naming**: Screen files end in `Screen.kt`, ViewModels end in `ViewModel.kt`
- **Tests**: Place unit tests in `app/src/test/`, instrument tests in `app/src/androidTest/`

## Adding a New Calculator Module

1. Create the screen composable in `ui/screens/YourModuleScreen.kt`
2. If it needs a ViewModel, create `ui/screens/YourModuleViewModel.kt`
3. Place calculation logic in `util/YourModuleCalculator.kt`
4. Add a navigation route in `MainActivity.kt`
5. Add a dashboard tile in `DashboardScreen.kt` under the appropriate category
6. Add unit tests in `src/test/` covering the formula
7. Document the formula and its source in `docs/formulas.md`

## Formula References

Every calculator in LabX should reference the formula or algorithm it implements. When adding or modifying a calculation:

- Cite the textbook, paper, or standard the formula comes from
- Add the reference to `docs/formulas.md`
- Include edge cases and assumptions in code comments

## Code of Conduct

Be respectful and constructive. We're building tools for scientists — accuracy and clarity matter more than speed.

## Questions?

Open a Discussion or an Issue. We're happy to help.
