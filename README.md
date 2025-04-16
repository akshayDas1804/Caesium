# 📦 Caesium Image Compressor – Repository Overview

Welcome to the structured overview of the **Caesium Image Compressor** GitHub repository – a Qt-based application for efficient image compression with both lossy and lossless modes. It integrates a powerful Rust backend and a cross-platform GUI frontend built with Qt.

---

# ❓ What is Caesium?

Caesium is an open-source image compressor designed to reduce file size without compromising quality. It supports batch processing, drag-and-drop UI, and both lossy/lossless modes for formats like JPEG, PNG, and WebP.

- Cross-platform GUI built in **C++ with Qt**
- Rust backend using **libcaesium** for high-performance compression
- Supports **translations, custom icons, persistent settings**, and native integration with macOS and Windows

---

# 📚 Table of Contents

- [GitHub Config Files](#github-config-files)
- [IDE Configuration (.idea)](#ide-configuration-idea)
- [Resources Folder](#resources-folder)
- [Core Source Code (src)](#core-source-code-src)
- [Test Suite](#test-suite)
- [Build & Installer Scripts](#build--installer-scripts)
- [Data Structures Overview](#data-structures-overview)
- [Why Qt and Not STL?](#why-qt-and-not-stl)

---

# 🔧 GitHub Config Files

## `.github/FUNDING.yml`
- Enables GitHub Sponsors or custom donation links (e.g., PayPal)

## `.github/workflows/build-qt.yml`
- GitHub Actions CI to build on Windows and Linux
- Installs Qt, sets up cache for libcaesium
- macOS build is commented out

## `.github/ISSUE_TEMPLATE`
- `bug_report.md`: Guide for structured bug reports
- `feature_request.md`: Template for feature suggestions
- `other-issues.md`: Open-ended report format

---

# 🧠 IDE Configuration (.idea)

| File | Purpose |
|------|---------|
| Project_Default.xml | Clang-Tidy inspection config |
| codeStyleConfig.xml, Project.xml | Formatting for C++/Markdown |
| editor.xml | Granular inspection severity controls |
| QtSettings.xml | Qt path configs for Debug/Release |
| vcs.xml | Enables Git VCS inside JetBrains IDE |
| modules.xml, .iml | JetBrains project module info |
| .name | Stores project name |
| misc.xml | Python/CMake setup, excluded folders |

---

# 📁 Resources Folder

| Subfolder/File | Description |
|----------------|-------------|
| `i18n/` | `.ts` files for multilingual support |
| `icons/` | Application icons (.svg, .png, .ico) |
| `languages.qrc`, `resources.qrc` | Qt resource files for bundling assets |
| `style.manifest`, `icons.rc` | Windows styling and resource linking |

---

# 🧩 Core Source Code (src)

### 📂 Top-Level Files
- `main.cpp`: Application entry point
- `MainWindow.cpp/h`: Main GUI logic and layout

### 📂 src/dialogs/
- `AboutDialog`, `PreferencesDialog`: UI dialogs for settings, about info

### 📂 src/exceptions/
- `FileException`: Custom error handling for I/O

### 📂 src/filters/
- `ExtensionFilter.cpp`: Filters unsupported file types

### 📂 src/models/
- `FileListModel`: Stores image paths, statuses, and progress

### 📂 src/network/
- `Updater.cpp`: Fetches updates or changelogs from the web

### 📂 src/services/
- `CompressorService.cpp`: Calls Rust backend (`libcaesium`) with parameters

### 📂 src/utils/
- `FileUtils.cpp`: Helper functions for paths, names, permissions

### 📂 src/widgets/
- `ImagePreview.cpp`: Custom Qt widget for image previews

### 📂 src/delegates/
- `FileItemDelegate.cpp`: Custom renderers for table/list view

### 📂 src/updater/
- `SparkleUpdater.mm`: Native macOS auto-update via Sparkle

---

# 🧪 Test Suite

The `tests/` folder contains automated tests using Qt’s test framework. It likely includes:
- **Unit Tests** for individual services
- **Integration Tests** for component communication
- **GUI Tests** for widget behavior

---

# ⚙️ Build & Installer Scripts

| File | Role |
|------|------|
| `CMakeLists.txt` | Builds app and links Qt + libcaesium |
| `libcaesium.conf` | Caching config for the Rust library |
| `Info.plist` | macOS bundle info and permissions |
| `qt.conf` | Helps app locate Qt runtime when portable |
| `setup.iss` | Windows installer generator (Inno Setup) |

---

# 🧱 Data Structures Overview

### Qt Containers Used

| Qt Class | STL Equivalent | Use |
|----------|----------------|-----|
| `QVector`, `QList` | `std::vector`, `std::list` | Store image list, UI entries |
| `QMap`, `QHash` | `std::map`, `std::unordered_map` | Map filenames to settings |
| `QSettings` | — | Persist user preferences |
| `QStandardItemModel` | Custom Model/View pattern | Power UI list/table views |

### Rust Backend (libcaesium)
- `Vec<T>` for dynamic collections
- `HashMap<K,V>` for mapping IDs to options
- Custom `struct` types for compression params

---

# 🔎 Why Qt and Not STL?

| Reason | Qt | STL |
|--------|-----|-----|
| GUI Integration | ✔️ Signals/slots, QML, QStrings | ❌ Manual wiring needed |
| Copy-on-Write | ✔️ Efficient sharing | ❌ Deep copies required |
| App Settings | ✔️ QSettings | ❌ No built-in alternative |
| Event Handling | ✔️ Built-in (signals) | ❌ Manual callbacks |
| Resource Bundling | ✔️ `.qrc` + icons | ❌ Not applicable |

Qt is preferred for GUI-heavy apps like Caesium because it reduces boilerplate, integrates tightly with Qt Designer, and improves developer productivity.

---

# 📉 Compression Modes

Caesium supports **both** compression types:

| Mode | Formats | Description |
|------|---------|-------------|
| Lossless | PNG, WebP | Keeps all pixel data intact |
| Lossy | JPEG, WebP | Adjustable quality slider |

Compression quality can be set via UI, and preview functionality helps users see trade-offs before applying.

---

# 🧠 Summary

Caesium Image Compressor is a Qt-powered, cross-platform GUI built for efficient image compression using a performant Rust backend. Its modular structure and strong use of Qt's features make it a powerful, developer-friendly application for real-world desktop use.

Want to dive deeper into a specific folder, view architecture diagrams, or walk through function logic in files like `CompressorService.cpp` or `MainWindow.cpp`? Let me know!

