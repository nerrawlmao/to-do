# To-Do Notes

A modern, feature-rich To-Do application for Android built with **Kotlin** and **Jetpack Compose**.

![Kotlin](https://img.shields.io/badge/Kotlin-7F52FF?style=for-the-badge&logo=kotlin&logoColor=white)
![Jetpack Compose](https://img.shields.io/badge/Jetpack_Compose-4285F4?style=for-the-badge&logo=jetpackcompose&logoColor=white)
![Material 3](https://img.shields.io/badge/Material_3-0061FF?style=for-the-badge&logo=materialdesign&logoColor=white)
![Room](https://img.shields.io/badge/Room-003B57?style=for-the-badge&logo=sqlite&logoColor=white)
![Glance](https://img.shields.io/badge/Glance_Widget-34A853?style=for-the-badge&logo=android&logoColor=white)
![Min SDK](https://img.shields.io/badge/minSdk-26-FF6D00?style=for-the-badge&logo=android&logoColor=white)

---

## Features

### Core

- **Create Notes** — Tap the FAB to instantly create a new note with an empty todo item
- **Edit Titles** — Inline title editing with automatic save (500ms debounce)
- **Manage Todos** — Add, edit, and delete todo items within each note
- **Toggle Completion** — Tap the checkmark to mark items complete with animated strikethrough
- **Multi-Note Tabs** — Swipe between notes using a horizontal tab bar

### Advanced

- **Drag-to-Reorder Tabs** — Long-press and drag to reorder your notes — position is persisted
- **Dark Mode** — Toggle dark/light theme from the top bar; setting is saved across sessions
- **Home Screen Widget** — Glance-based widget displays your first note's todos on the home screen
- **Widget Toggle** — Mark todos complete directly from the widget without opening the app
- **Adaptive Widget** — Widget automatically adjusts background color for dark mode
- **Edge-to-Edge Display** — Full-screen experience using `enableEdgeToEdge()`

---

## Screenshots

<p float="left">
  <img src="app/src/main/res/mipmap-xhdpi/ic_banner.png" width="200" alt="App Banner" />
</p>

---

## Tech Stack

| Layer | Technology |
|---|---|
| **Language** | Kotlin 2.2.10 |
| **UI** | Jetpack Compose + Material 3 (Compose BOM 2025.06.00) |
| **Architecture** | MVVM (ViewModel + Repository + DAO) |
| **Database** | Room (SQLite) via KSP |
| **Async** | Kotlin Coroutines + StateFlow |
| **Widget** | Jetpack Glance 1.1.1 |
| **Drag & Drop** | `composereorderable` 0.9.6 |
| **Min / Target SDK** | 26 / 34 |

---

## Architecture

```
MainActivity
  └── ToDoTheme (dark/light)
       └── MainScreen
            ├── TopBar (theme toggle)
            ├── TabBar (reorderable notes)
            └── NoteContent (title + todos)

NoteViewModel ──► NoteRepository ──► NoteDao ──► Room DB
```

The app follows the **MVVM** pattern:
- **Model**: `NoteEntity` / `TodoItem` data classes + Room DAO
- **ViewModel**: `NoteViewModel` holds all UI state as `StateFlow` and handles user actions
- **View**: Composable functions in `MainScreen.kt` render state and dispatch events

---

## Data Model

```kotlin
NoteEntity(
    id: Long,                    // Auto-generated primary key
    title: String = "Untitled",
    todos: List<TodoItem>,       // Serialized as JSON
    position: Int,               // Tab ordering
    createdAt: Long              // Unix timestamp
)

TodoItem(
    text: String,
    completed: Boolean,
    uid: String                  // UUID for widget toggle targeting
)
```

---

## Getting Started

### Prerequisites

- Android Studio (latest stable)
- Android SDK 34+
- JDK 17+

### Build & Run

```bash
# Clone the repository
git clone https://github.com/your-username/notes.git
cd notes

# Build debug APK
./gradlew assembleDebug

# Install on connected device
./gradlew installDebug
```

Or open the project in **Android Studio** and run the `:app` configuration.

---

## Project Structure

```
app/
├── src/main/java/com/todo/notes/
│   ├── MainActivity.kt          # Single-activity entry point
│   ├── ToDoApp.kt               # Application class (DB singleton)
│   ├── data/
│   │   ├── db/                  # Room database, DAO, entities
│   │   └── repository/          # NoteRepository
│   ├── ui/
│   │   ├── screens/             # MainScreen composable
│   │   ├── theme/               # Color, Theme, Typography
│   │   └── viewmodel/           # NoteViewModel
│   └── widget/                  # Glance widget + receiver
├── src/main/res/
│   ├── drawable/                # Icons and widget backgrounds
│   ├── layout/                  # Widget XML layouts
│   └── xml/                     # Widget info, backup rules
└── build.gradle.kts
```

---

## Widget

The home screen widget is built with **Jetpack Glance** and supports:

- Displaying the first note's title and todo items
- Toggling todo completion directly from the widget
- Dynamic dark/light background adaptation
- Opening the app on tap

---

## Roadmap

- [ ] Search across notes and todos
- [ ] Categories / tags for organization
- [ ] Cloud sync and backup
- [ ] Due dates and reminders
- [ ] Widget customization (select which note to display)
- [ ] Data export (JSON / CSV)

---

## License

```
MIT License

Copyright (c) 2025
```
