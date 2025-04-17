# 🗜️ Caesium Image Compressor

**Caesium** is an open-source, cross-platform image compressor that optimizes JPEG, PNG, and WebP images using both lossy and lossless techniques. Designed for speed, privacy, and usability — Caesium is perfect for batch compression without sending your files to the cloud.

<p align="center">
  <img src="https://img.shields.io/github/stars/Lymphatus/caesium-image-compressor?style=social" />
  <img src="https://img.shields.io/github/workflow/status/Lymphatus/caesium-image-compressor/Build" />
  <img src="https://img.shields.io/github/license/Lymphatus/caesium-image-compressor" />
</p>

---

# 🎨 UI/UX of Caesium Website

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
- [Demonstration Of Image Compression](#demonstration-of-image-compression)
- [Summary](#summary)
- [Contributors](#contributors)
- [License](#license)
- [Links](#links)

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

Detailed breakdown of project architecture including:
- UI Logic
- Rust backend integration
- Error handling
- Utilities
- Platform-specific components

---

## 🧪 Test Suite

Includes:
- ✅ Unit tests for core services
- 🔁 Integration tests (UI + backend)
- 🧪 GUI tests for widgets

---

## ⚙️ Build & Installer Scripts

Comprehensive build setup using CMake, Rust’s Cargo, and platform-specific installer scripts.

---

## 🧱 Data Structures Overview

Explains use of Qt containers and Rust data structures for performance and memory safety.

---

## 🔎 Why Qt and Not STL?

Qt’s framework offers real-time signals/slots, better internationalization support, and UI consistency across platforms.

---

## 📉 Compression Modes

| Mode     | Formats    | Description                      |
|----------|------------|----------------------------------|
| Lossless | PNG, WebP  | No data loss, perfect quality    |
| Lossy    | JPEG, WebP | Adjustable compression quality   |

---

## 🔍 CompressorService Logic Walkthrough

Outlines the full pipeline from UI input to backend Rust function calls and real-time feedback.

---

## 🚀 Performance & Optimization

Techniques like multithreading, zero-copy logic, and asynchronous operations contribute to exceptional performance.

---

## 🌐 Internationalization (i18n)

18+ languages supported via Qt’s `.ts` system — easily extendable for localization.

---

## ⚖️ Trade-offs & Design Decisions

Breaks down our reasoning for using Rust over C++, Qt over Electron, and other architectural decisions.

---

## 🧠 Future Scope

Ideas for enhancing compression capabilities, UI/UX improvements, cloud integration, and AI-based optimizations.

---

## 📂 File-Level Summary (src)

Quick reference for key files and their purpose within the codebase.

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

## 🖼 Demonstration Of Image Compression

### Original Photo
![image alt](https://github.com/akshayDas1804/Caesium/blob/main/Original%20Photo.png?raw=true)

### Lossy Compressed Photo
![image alt](https://github.com/akshayDas1804/Caesium/blob/main/Lossy%20Compression.png?raw=true)

### Lossless Compressed Photo
![image alt](https://github.com/akshayDas1804/Caesium/blob/main/Lossless%20Compression.png?raw=true)

---

## 📋 Summary

Caesium is a powerful, offline image compression tool that offers both lossless and lossy optimization for formats like JPEG, PNG, and WebP. Its lightweight design and fast performance make it ideal for everyday image compression without compromising quality.

Unlike cloud-based solutions, Caesium runs entirely on your system, ensuring full privacy and data control.

We personally used Caesium extensively to optimize images for online form submissions, where reduced image size significantly improved upload times and compatibility with various portals. It proved to be an essential utility for managing photo size efficiently and securely.

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
