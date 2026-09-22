# MedLab AI: KUHS Assistant 🔬

> **Dedicated AI Study & Clinical Suite for Kerala University of Health Sciences (KUHS) B.Sc Medical Laboratory Technology (MLT) Students.**

[![Android](https://img.shields.io/badge/Platform-Android-green.svg)](https://developer.android.com)
[![Jetpack Compose](https://img.shields.io/badge/UI-Jetpack%20Compose%20(Material%203)-blue.svg)](https://developer.android.com/jetpack/compose)
[![Kotlin](https://img.shields.io/badge/Language-Kotlin-purple.svg)](https://kotlinlang.org)
[![Room DB](https://img.shields.io/badge/Database-Room%20(Offline%20First)-orange.svg)](https://developer.android.com/training/data-storage/room)
[![Gemini AI](https://img.shields.io/badge/AI-Google%20Gemini%202.5%20Flash-deepgreen.svg)](https://aistudio.google.com)

---

## 📖 Overview

**MedLab AI: KUHS Assistant** is a native Android application built using Kotlin and Jetpack Compose. It delivers an AI-augmented academic and clinical training environment tailored specifically to the syllabus, exam patterns, and practical valuation criteria of the **Kerala University of Health Sciences (KUHS)** for the Bachelor of Science in Medical Laboratory Technology (B.Sc MLT).

### Key Highlights
- **KUHS Valuation Key Engine**: Generates official university-benchmarked model answers formatted specifically for 2-Mark short answers, 5-Mark standard questions, 10-Mark essays, and 15-Mark major essays.
- **Voice-Enabled Viva Simulator**: Simulates a KUHS External Practical Examiner session with immediate feedback, scoring out of 10, confidence grades, vocabulary checks, and follow-up clinical questions.
- **Laboratory Dilution & Pipetting Calculator**: Instant $C_1 V_1 = C_2 V_2$ calculations for working standards, reagents, and serial dilutions.
- **Spaced Repetition Flashcard Vault (SM-2)**: High-yield deck covering Hematology, Clinical Biochemistry, Microbiology, Histopathology, and Blood Banking with clinical mnemonics.
- **Virtual Microscopy Atlas**: Morphological pointers, stain identification, and ideal-zone examination guidelines for peripheral smears, AFB sputum, and hemoglobinopathies.
- **Focus Soundscape Generator**: Native PCM sine-wave audio synthesizer generating laboratory centrifuge hum (110 Hz), gamma focus waves (40 Hz), and ambient air handler frequencies (60 Hz).
- **Offline-First Persistence**: Local Room database with encrypted storage for user profiles, clinical notes, custom flashcards, and exam scores.

---

## 🛠️ Architecture & Tech Stack

- **Architecture**: MVVM (Model-View-ViewModel) with Clean Repository Pattern
- **UI Framework**: Modern Jetpack Compose with Material 3 Design System
- **Asynchronous Flow**: Kotlin Coroutines & `StateFlow` / `Flow`
- **Local Database**: AndroidX Room Database 2.7.0 with Kotlin Symbol Processing (KSP)
- **Networking**: OkHttp 4.12.0 for high-performance direct Gemini API endpoints
- **AI Model**: Google Gemini 2.5 Flash via Google AI Studio
- **Audio Synthesis**: Native Android `AudioTrack` PCM streaming + Text-To-Speech (TTS)

---

## 📋 Prerequisites

Before cloning and running the project locally, ensure you have:
1. **Android Studio**: Android Studio Hedgehog (2023.1.1) or Ladybug (2024.2+) recommended.
2. **JDK**: Java Development Kit 11 or higher (OpenJDK 17 / 21 recommended).
3. **Android SDK**: Android 14+ (API level 34 or 36) installed via the Android SDK Manager.
4. **Google Gemini API Key**: Obtain a free API key from [Google AI Studio](https://aistudio.google.com/app/apikey).

---

## 🚀 Quick Start & Local Setup

### 1. Clone the Repository
```bash
git clone https://github.com/your-username/medlab-ai-kuhs-assistant.git
cd medlab-ai-kuhs-assistant
```

### 2. Configure Environment Variables
Copy the example environment file:
```bash
cp .env.example .env
```
Open `.env` in any text editor and insert your Gemini API Key:
```env
GEMINI_API_KEY=your_actual_gemini_api_key_here
```

> **Note on Security**: The `.env` file is included in `.gitignore` to prevent sensitive credentials from ever being committed to GitHub.

### 3. Open in Android Studio
1. Launch **Android Studio**.
2. Click **Open** and select the cloned project folder.
3. Allow Gradle to sync and download all dependencies.
4. *(Local machine build adjustment)* In `app/build.gradle.kts`, if building outside of the AI Studio container without `debug.keystore`, remove or comment out:
   ```kotlin
   // signingConfig = signingConfigs.getByName("debugConfig")
   ```
5. Select an Android Emulator or connected physical device running Android 7.0+ (API 24+).
6. Click **Run 'app'** (`Shift + F10`).

---

## 📦 Building via Command Line (Gradle)

To build the debug APK directly via command line:

```bash
# On Linux / macOS:
gradle :app:assembleDebug

# Or on Windows:
gradle.bat :app:assembleDebug
```

The compiled APK will be generated at:
```
app/build/outputs/apk/debug/app-debug.apk
```

---

## 📂 Project Structure

```
├── .env.example              # Sample environment template for API keys
├── .gitignore                # Git ignore rules for Android Studio & Gradle
├── README.md                 # Complete project documentation
├── build.gradle.kts          # Top-level Gradle build configuration
├── settings.gradle.kts       # Subproject modules and dependency repositories
├── gradle.properties         # JVM & Android build properties
├── metadata.json             # AI Studio platform metadata
├── gradle/
│   ├── libs.versions.toml    # Centralized Gradle Version Catalog
│   └── wrapper/
│       └── gradle-wrapper.properties
└── app/
    ├── .gitignore            # Module build ignore
    ├── build.gradle.kts      # Application dependencies & SDK configurations
    ├── proguard-rules.pro    # ProGuard / R8 minification rules
    └── src/
        └── main/
            ├── AndroidManifest.xml
            ├── java/com/example/
            │   ├── MainActivity.kt               # Navigation host & scaffolding
            │   ├── audio/
            │   │   └── SoundscapeGenerator.kt    # PCM sound synth & TTS engine
            │   ├── data/
            │   │   ├── ai/
            │   │   │   ├── GeminiService.kt      # Gemini API prompt client
            │   │   │   └── KuhsKnowledgeBase.kt  # Syllabus, slides, mnemonics
            │   │   ├── local/
            │   │   │   ├── Entities.kt           # Room entities (Notes, Scores, Cards)
            │   │   │   ├── MedLabDao.kt          # Reactive Room DAO
            │   │   │   └── MedLabDatabase.kt     # Room database configuration
            │   │   ├── model/
            │   │   │   └── Models.kt             # Domain data models
            │   │   └── repository/
            │   │       └── MedLabRepository.kt   # Repository data layer
            │   └── ui/
            │       ├── components/
            │       │   └── CommonComponents.kt   # Glassmorphic UI library
            │       ├── screens/
            │       │   ├── AuthScreen.kt         # KUHS student login & registration
            │       │   ├── DashboardScreen.kt    # Clinical hub & subject cards
            │       │   ├── FlashcardVaultScreen.kt # Spaced review, slides, mnemonics
            │       │   ├── KuhsAiChatScreen.kt   # Valuation key model answers
            │       │   ├── PomodoroNotesScreen.kt # Lab calculator, timer, audio synth
            │       │   ├── ProgressScreen.kt     # Exam readiness index & history
            │       │   ├── QuizEngineScreen.kt   # Sprint, mock, survival tests
            │       │   └── VivaSimulatorScreen.kt # Voice examiner simulation
            │       ├── theme/
            │       │   ├── Color.kt              # Deep void & neon palette
            │       │   ├── Theme.kt              # M3 dark theme configuration
            │       │   └── Type.kt               # Clean typography scale
            │       └── viewmodel/
            │           └── MedLabViewModel.kt    # Central MVVM state controller
            └── res/
                ├── drawable/                     # Launcher vector assets
                ├── mipmap-anydpi-v26/            # Adaptive icons
                ├── values/                       # Strings, colors, styles
                └── xml/                          # Backup and extraction rules
```

---

## 🔑 Environment Variables Reference

| Variable | Description | Required | Source |
|---|---|---|---|
| `GEMINI_API_KEY` | Google Gemini API key for generating valuation keys and evaluating oral viva defense | Yes (for AI features) | [Google AI Studio](https://aistudio.google.com/app/apikey) |

---

## 🧪 Testing & Verification

Run local unit tests:
```bash
gradle :app:testDebugUnitTest
```

---

## 📄 License & Academic Disclaimer

This project is developed for educational and academic study assistance aligned with the Kerala University of Health Sciences (KUHS) curriculum. It is intended to supplement academic textbooks and clinical laboratory training.
