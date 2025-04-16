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
- [CompressorService Logic Walkthrough](#compressorservice-logic-walkthrough)
- [Future Scope](#future-scope)
- [File-Level Summary (src)](#file-level-summary-src)
- [Summary](#summary)
- [Contributors](#contributors)
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

Qt offers:
- Native integration with GUI components
- Efficient resource handling with `.qrc`
- Implicit sharing for better memory performance
- Simplified settings and event management (e.g., `QSettings`, `signals/slots`)

STL is still used internally for isolated performance-focused logic, but Qt offers better synergy for UI development.

---

# 📂 File-Level Summary (src)

| File | Purpose |
|------|---------|
| main.cpp | Launches Qt app, sets up translation |
| MainWindow.cpp/h | Main GUI controller and events |
| CompressorService.cpp | Prepares image params, calls Rust lib, saves output |
| FileListModel.cpp | Stores and updates list of images + compression state |
| ImagePreview.cpp | Displays thumbnails or side-by-side compression preview |
| FileItemDelegate.cpp | Customizes how file list rows are rendered (e.g., progress bars) |
| Updater.cpp | Checks for version updates (used by network module) |
| SparkleUpdater.mm | macOS-specific update framework support |

---

# 🔍 CompressorService Logic Walkthrough

The `CompressorService.cpp` file is central to compression logic. Here’s how it works:

1. **Input Collection**
   - Gathers file paths, output folders, and user-defined settings (quality, resize, lossless flag).

2. **Parameter Construction**
   - Fills a `CompressorSettings` struct with image-specific compression parameters.
   - Converts Qt types (QString, QSize) to C-compatible types for FFI.

3. **Rust Backend Call**
   - Uses C-style function (from `libcaesium`) to invoke compression routine.
   - Handles FFI bridge using `extern "C"` definitions.

4. **Error Handling**
   - Checks the return value from backend call.
   - If error, emits a signal with failure info (displayed to user).

5. **Progress Reporting**
   - Emits signals during and after compression to update UI (file list model + preview).

---

# 📉 Compression Modes

Caesium supports **both** compression types:

| Mode | Formats | Description |
|------|---------|-------------|
| Lossless | PNG, WebP | Keeps all pixel data intact |
| Lossy | JPEG, WebP | Adjustable quality slider |

Compression quality can be set via UI, and preview functionality helps users see trade-offs before applying.

---

# 💡 Developer & Power User Ideas

## 💻 For Developers / Contributors

1. **Support More File Formats**: Add AVIF, HEIC via `libavif`, `libheif`
2. **Smarter Compression Suggestions**: Auto-suggest lossy/lossless based on image type
3. **Parallelism / GPU Acceleration**: Use OpenCL/Vulkan for faster batch jobs
4. **Plugin Architecture**: Add custom exporters (e.g., Imgur, Dropbox)

## 🖼 Future Scope

5. **Advanced Resize**: Smart crop, watermark, aspect-ratio locks
6. **Presets + Automation**: Save configs like "Web Export", allow batch scripting
7. **Scheduled Compression**: Like cron — auto compress on schedule

## 🌐 UI / UX Enhancements

8. **Live Preview**: Side-by-side before/after view
9. **Tooltips & Sliders**: Explain lossy/lossless visually
10. **Drag + Shell Integration**: Right-click compress with Caesium

## ☁️ Cloud & Web Features

11. **Cloud Sync/CDN Export**: Auto-upload to S3, Netlify, Firebase
12. **HTML Comparison Report**: Visual + size diff reports for sharing

## 🧪 Experimental

13. **AI Compression**: Use ML to retain perceptual detail at low sizes
14. **Real-Time Webcam/Screenshot Compression**: Auto-optimize screen captures

---

## Contributors
- Aaditya Kaushik - 202401001
- Akshay Das - 202401011
- Darsh Valand - 202401045
- Harshit Goyal - 202401065


