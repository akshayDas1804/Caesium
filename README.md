# 🖼️ Caesium Image Compressor

[![Build Status](https://img.shields.io/github/actions/workflow/status/Lymphatus/caesium-image-compressor/build-qt.yml?branch=master)](https://github.com/Lymphatus/caesium-image-compressor/actions)
[![License](https://img.shields.io/github/license/Lymphatus/caesium-image-compressor)](LICENSE)
[![Platforms](https://img.shields.io/badge/platform-Windows%20%7C%20macOS%20%7C%20Linux-blue)](https://github.com/Lymphatus/caesium-image-compressor/releases)
[![Web Demo](https://img.shields.io/badge/Demo-caesium.app-brightgreen)](https://caesium.app)
[![Contributors](https://img.shields.io/github/contributors/Lymphatus/caesium-image-compressor)](https://github.com/Lymphatus/caesium-image-compressor/graphs/contributors)

![Caesium UI Screenshot](https://raw.githubusercontent.com/Lymphatus/caesium-image-compressor/master/resources/screenshots/main_window.png)

---

## ❓ What is Caesium?

Caesium is an open-source image compressor designed to reduce file size without compromising quality. It supports batch processing, drag-and-drop UI, and both lossy/lossless modes for formats like JPEG, PNG, and WebP.

- Cross-platform GUI built in **C++ with Qt**
- Rust backend using **libcaesium** for high-performance compression
- Supports **translations, custom icons, persistent settings**, and native integration with macOS and Windows

---

## 📚 Table of Contents

- [GitHub Config Files](#-github-config-files)
- [IDE Configuration (.idea)](#-ide-configuration-idea)
- [Resources Folder](#resources-folder)
- [Core Source Code (src)](#core-source-code-src)
- [Test Suite](#test-suite)
- [Build & Installer Scripts](#build--installer-scripts)
- [Data Structures Overview](#data-structures-overview)
- [Why Qt and Not STL?](#why-qt-and-not-stl)
- [CompressorService Logic Walkthrough](#compressorservice-logic-walkthrough)
- [Compression Modes](#compression-modes)
- [Developer & Power User Ideas](#developer--power-user-ideas)
- [Future Scope](#future-scope)
- [File-Level Summary (src)](#file-level-summary-src)
- [Summary](#summary)
- [Contributors](#contributors)

---

## 🔧 GitHub Config Files

### `.github/FUNDING.yml`
- Enables GitHub Sponsors or custom donation links

### `.github/workflows/build-qt.yml`
- GitHub Actions CI for Windows and Linux builds

### `.github/ISSUE_TEMPLATE`
- Templates for bugs, features, and general issues

---

## 🧠 IDE Configuration (.idea)

| File | Purpose |
|------|---------|
| Project_Default.xml | Clang-Tidy inspection |
| codeStyleConfig.xml | C++/Markdown formatting |
| editor.xml | Severity control |
| QtSettings.xml | Qt path setup |
| vcs.xml | VCS integration |
| modules.xml, .iml | JetBrains project data |
| misc.xml | CMake & Python config |

---

## 📁 Resources Folder

| File/Folder | Description |
|-------------|-------------|
| `i18n/` | Multilingual translations (.ts) |
| `icons/` | App icons (.svg, .ico) |
| `resources.qrc` | Qt resource bundler |
| `icons.rc` | Windows icon bundler |

---

## 🧩 Core Source Code (src)

- `main.cpp`: App entry
- `MainWindow.cpp/h`: UI logic

### Dialogs
- `AboutDialog`, `PreferencesDialog`

### Services
- `CompressorService.cpp`: Calls Rust

### Models/Utils
- `FileListModel`, `FileUtils.cpp`, `ImagePreview`

### Delegates
- `FileItemDelegate`: Custom table views

### Updaters
- `Updater.cpp`, `SparkleUpdater.mm`

---

## 🧪 Test Suite

- Unit, integration, and GUI tests using Qt Test

---

## ⚙️ Build & Installer Scripts

| File | Role |
|------|------|
| `CMakeLists.txt` | Core build logic |
| `libcaesium.conf` | Rust lib caching |
| `Info.plist` | macOS metadata |
| `qt.conf` | Qt portable build |
| `setup.iss` | Windows installer |

---

## 🧱 Data Structures Overview

### Qt Types

| Qt | STL | Use |
|----|-----|-----|
| `QVector`, `QList` | `vector`, `list` | File lists |
| `QMap`, `QHash` | `map`, `unordered_map` | Mapping settings |
| `QSettings` | — | Persistent configs |
| `QStandardItemModel` | — | Model/View UI |

### Rust Types
- `Vec<T>`, `HashMap<K, V>`, structs for compression params

---

## 🔎 Why Qt and Not STL?

Qt offers signals/slots, `.qrc` asset bundling, implicit sharing, and native GUI rendering. STL is used where direct performance is needed.

---

## 📉 Compression Modes

| Mode | Formats | Description |
|------|---------|-------------|
| Lossless | PNG, WebP | Exact match compression |
| Lossy | JPEG, WebP | Adjustable quality |

---

## 🔍 CompressorService Logic Walkthrough

1. Collect user input (paths, settings)
2. Create struct with compression params
3. Convert to FFI-safe types for Rust
4. Call `caesium_compress_image()` via FFI
5. Emit progress + error signals to UI

---

## 💡 Developer & Power User Ideas

- AVIF/HEIC support
- GPU acceleration (OpenCL, Vulkan)
- CLI support, scheduled compression
- Preset-based automation
- Plugin system

---

## 🖼 Screenshots

![Screenshot](https://raw.githubusercontent.com/Lymphatus/caesium-image-compressor/master/resources/screenshots/preferences_dialog.png)

---

## 🧪 Future Scope

- AI-powered compression
- Live side-by-side preview
- Web-based comparison reports
- Integration with CDN/cloud

---

## 📂 File-Level Summary (src)

| File | Role |
|------|------|
| `main.cpp` | App entry |
| `MainWindow.cpp` | GUI logic |
| `CompressorService.cpp` | Compression |
| `FileListModel.cpp` | File state |
| `FileItemDelegate.cpp` | Custom rendering |
| `Updater.cpp`, `SparkleUpdater.mm` | Update system |

---

## ✅ Summary

Caesium brings together:
- Qt for cross-platform UI
- Rust for fast, safe compression logic
- CMake + Cargo for flexible builds

---

## 👥 Contributors

- Aaditya Kaushik - 202401001  
- Akshay Das - 202401011  
- Darsh Valand - 202401045  
- Harshit Goyal - 202401065  

---

**GitHub**: [github.com/Lymphatus/caesium-image-compressor](https://github.com/Lymphatus/caesium-image-compressor)  
**Web Demo**: [caesium.app](https://caesium.app)
