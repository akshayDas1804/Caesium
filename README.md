# 🗜️ Caesium Image Compressor

**Caesium** is an open-source, cross-platform image compressor that optimizes JPEG, PNG, and WebP images using both lossy and lossless techniques. Designed for speed, privacy, and usability — Caesium is perfect for batch compression without sending your files to the cloud.

<p align="center">
  <img src="https://img.shields.io/github/stars/Lymphatus/caesium-image-compressor?style=social" />
  <img src="https://img.shields.io/github/workflow/status/Lymphatus/caesium-image-compressor/Build" />
  <img src="https://img.shields.io/github/license/Lymphatus/caesium-image-compressor" />
</p>

---
# UI/UX of Caesium Website
![image alt](https://github.com/akshayDas1804/Caesium/blob/main/UI%20Photo.png?raw=true)

---
## ❓ What is Caesium?

Caesium is a native image compression tool that reduces image size while preserving quality. Unlike cloud-based compressors like TinyPNG or Squoosh, Caesium works entirely offline — no uploads, no data collection.

### ✅ Key Features:
- 🖥 **Cross-platform GUI** built with **Qt (C++)**
- ⚙️ **Rust backend (libcaesium)** for fast, safe compression
- 📂 **Batch processing** with drag-and-drop support
- 🌍 **Multilingual UI** (18+ languages)
- 🔐 **Privacy-first**: No cloud uploads, works fully offline

---

## 📚 Table of Contents

- [GitHub Config Files](#github-config-files)
- [IDE Configuration (.idea)](#ide-configuration-idea)
- [Resources Folder](#resources-folder)
- [Core Source Code (src)](#core-source-code-src)
- [Test Suite](#test-suite)
- [Build & Installer Scripts](#build--installer-scripts)
- [Data Structures Overview](#data-structures-overview)
- [Why Qt and Not STL?](#why-qt-and-not-stl)
- [Compression Modes](#compression-modes)
- [CompressorService Logic Walkthrough](#compressorservice-logic-walkthrough)
- [Performance & Optimization](#performance--optimization)
- [Internationalization (i18n)](#internationalization-i18n)
- [Trade-offs & Design Decisions](#trade-offs--design-decisions)
- [Future Scope](#future-scope)
- [File-Level Summary (src)](#file-level-summary-src)
- [Installation](#installation)
- [Contributors](#contributors)
- [License](#license)

---

## 🔧 GitHub Config Files

- `.github/FUNDING.yml` – Enable GitHub Sponsors / PayPal
- `.github/workflows/build-qt.yml` – CI setup for Windows/Linux builds
- `.github/ISSUE_TEMPLATE/` – Templates for bug reports and feature requests

---

## 🧠 IDE Configuration (.idea)

JetBrains IDE configs (optional) for formatting, Clang-Tidy, VCS settings, Qt path management, etc.

---

## 📁 Resources Folder

| Path               | Description                           |
|--------------------|---------------------------------------|
| `i18n/`            | `.ts` translation files               |
| `icons/`           | App icons (.svg, .ico)                |
| `resources.qrc`    | Qt resource bundler                   |
| `style.manifest`   | Windows styles                        |
| `icons.rc`         | Windows icon linker                   |

---

## 🧩 Core Source Code (src)

### 📌 Top-Level
- `main.cpp` – App entry point
- `MainWindow.cpp/h` – Core UI logic

### 📁 dialogs/
- `AboutDialog`, `PreferencesDialog` – GUI settings & info

### 📁 exceptions/
- `FileException` – Error handling class

### 📁 filters/
- `ExtensionFilter.cpp` – Filters unsupported files

### 📁 models/
- `FileListModel.cpp` – Tracks file list + status

### 📁 network/
- `Updater.cpp` – Checks for new versions

### 📁 services/
- `CompressorService.cpp` – Interfaces with Rust backend

### 📁 utils/
- `FileUtils.cpp` – Filesystem and permission helpers

### 📁 widgets/
- `ImagePreview.cpp` – UI component for side-by-side views

### 📁 delegates/
- `FileItemDelegate.cpp` – Custom renderer for table/list

### 📁 updater/
- `SparkleUpdater.mm` – macOS auto-updates (Sparkle)

---

## 🧪 Test Suite

Includes:
- ✅ Unit tests for core services
- 🔁 Integration tests (UI + backend)
- 🧪 GUI tests for widgets

---

## ⚙️ Build & Installer Scripts

| Script/File        | Role                            |
|--------------------|----------------------------------|
| `CMakeLists.txt`   | Build setup (Qt + Rust)          |
| `libcaesium.conf`  | Rust build config                |
| `qt.conf`          | Portable Qt path helper          |
| `Info.plist`       | macOS bundle info                |
| `setup.iss`        | Inno Setup script for Windows    |

---

## 🧱 Data Structures Overview

### Qt (Frontend)
| Type | Use |
|------|-----|
| `QList<CImage>` | Image list for batch processing |
| `QSettings` | User preferences |
| `QFuture<void>` | Multithreaded compression |
| `QMap`, `QStandardItemModel` | UI tables and filters |

### Rust (Backend)
- `Vec<T>`, `HashMap<K,V>`
- FFI types: `c_char`, `c_int`
- Core function:
```rust
#[no_mangle]
pub extern "C" fn caesium_compress_image(input: *const c_char, output: *const c_char, quality: c_int) -> bool;
```

---

## 🔎 Why Qt and Not STL?

**Qt** is used instead of STL in many places due to:
- Native GUI widget integration
- `signals/slots` for real-time updates
- Easier internationalization
- Implicit data sharing (memory-efficient)

**STL** is still used in performance-critical sections.

---

## 📉 Compression Modes

| Mode     | Formats    | Description                      |
|----------|------------|----------------------------------|
| Lossless | PNG, WebP  | No data loss, perfect quality    |
| Lossy    | JPEG, WebP | Adjustable compression quality   |

---

## 🔍 CompressorService Logic Walkthrough

1. **Gathers input** – file paths, output dir, user settings
2. **Builds parameter struct** – converts Qt → C-compatible types
3. **Calls Rust FFI function** – invokes `caesium_compress_image()`
4. **Handles errors** – if false return, emits UI signal
5. **Reports progress** – updates UI via signals/slots

---

## 🚀 Performance & Optimization

| Feature | Description |
|--------|-------------|
| **Multithreading** | QtConcurrent avoids UI freezing |
| **Zero-copy Rust** | Efficient parsing where possible |
| **Speed Benchmarks** | ~12s for 100x 4MB images |
| **Memory Efficiency** | Only stores necessary buffers |

---

## 🌐 Internationalization (i18n)

| Step | Tool |
|------|------|
| Extract strings | `lupdate` |
| Edit translations | Qt Linguist (`.ts` files) |
| Compile to binary | `lrelease` produces `.qm` |
| Add language | Copy + translate `.ts` file |

---

## ⚖️ Trade-offs & Design Decisions

### Rust vs. C++
| Aspect | Rust | C++ |
|--------|------|-----|
| Memory safety | ✅ | ❌ (manual) |
| Performance | ✅ | ✅ |
| Build simplicity | ❌ (Cargo) | ✅ (CMake-only) |
| Error handling | `Result<>` | Unchecked exceptions |

### Qt vs. Other GUI Tools

| Framework | Pros | Cons |
|----------|------|------|
| **Qt** | Native feel, stability | Heavier binaries |
| Electron | Dev familiarity | High RAM usage |
| Flutter | Fast UI dev | Less native integration |

---

## 🧠 Future Scope

### 💻 Developers
- AVIF/HEIC support
- GPU compression (OpenCL/Vulkan)
- Plugin system (e.g., export to Imgur)

### 🖼 UI/UX
- Live before/after preview
- Smart tooltips, sliders
- Right-click integration

### ☁️ Cloud / Scripting
- HTML reports (size diff + visuals)
- Auto-sync to cloud (S3, Firebase)
- CLI & scheduled jobs

### 🧪 Experimental
- AI-assisted compression
- Realtime screenshot compression

---

## 📂 File-Level Summary (src)

| File | Role |
|------|------|
| `main.cpp` | Starts app + translations |
| `MainWindow.cpp` | GUI controller |
| `CompressorService.cpp` | Compression logic |
| `FileListModel.cpp` | List of compressed files |
| `ImagePreview.cpp` | Shows previews |
| `FileItemDelegate.cpp` | Renders rows |
| `Updater.cpp` | Checks online for updates |
| `SparkleUpdater.mm` | Handles macOS updates |

---

## 🛠 Installation

### Windows
1. Download installer from [Releases](https://github.com/Lymphatus/caesium-image-compressor/releases)
2. Run the `.exe`

### macOS
1. Download `.dmg` and drag to Applications

### Linux
```bash
git clone https://github.com/Lymphatus/caesium-image-compressor.git
cd caesium-image-compressor
cmake -B build
cmake --build build --config Release
```

---
# Demonstration Of Image Compression
# Original Photo
![image alt](https://github.com/akshayDas1804/Caesium/blob/main/Original%20Photo.png?raw=true)

# Lossy Compressed Photo
![image alt](https://github.com/akshayDas1804/Caesium/blob/main/Lossy%20Compression.png?raw=true)

# Lossless Compressed Photo
![image alt](https://github.com/akshayDas1804/Caesium/blob/main/Lossless%20Compression.png?raw=true)
---

## Summary
Caesium is a powerful, offline image compression tool that offers both lossless and lossy optimization for formats like JPEG, PNG, and WebP. Its lightweight design and fast performance make it ideal for everyday image compression without compromising quality. Unlike cloud-based solutions, Caesium runs entirely on your system, ensuring full privacy and data control.We personally used Caesium extensively to optimize images for online form submissions, where reduced image size significantly improved upload times and compatibility with various portals. It proved to be an essential utility for managing photo size efficiently and securely.
---

## 👥 Contributors


- Aaditya Kaushik – 202401001  
- Akshay Das – 202401011  
- Darsh Valand – 202401045  
- Harshit Goyal – 202401065  

---

## 📄 License

Licensed under the MIT License. See [LICENSE](./LICENSE) for more info.

---

## 🔗 Links

- 🌐 [Official Website](https://caesium.app)  
- 🧑‍💻 [GitHub Repo](https://github.com/Lymphatus/caesium-image-compressor)
