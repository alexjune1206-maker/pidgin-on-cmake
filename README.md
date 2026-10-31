# WARNING! COMPILING WILL FAIL BECAUSE THERE ARE MISSING CMAKELISTS! I AM WORKING ON IT! YOU CAN HELP TOO!

# Pidgin (CMake Migration)

![CMake Version](https://img.shields.io/badge/CMake-3.16%2B-blue)
![License](https://img.shields.io/github/license/alexjune1206-maker/pidgin-on-cmake)

This repository contains a modernized build system migration for **Pidgin** and **libpurple** (version 2.14.14). The original build infrastructure has been completely migrated from the legacy GNU Autotools (`configure`, `Makefile.am`) over to a clean, native, and maintainable **CMake** configuration.

---

## 🚀 Features Mapped

- **Modern CMake Architecture:** Clear targets, scoped properties, and native dependency lookup via `PkgConfig`.
- **System Checks Integration:** Replaced custom shell-based macros with standard CMake verification routines (`CheckIncludeFile`, `CheckFunctionExists`, `CheckStructHasMember`).
- **Feature Toggles:** Easy compilation switches to build with or without specific user interfaces (GTK+ UI, Console UI) or features (D-Bus, GStreamer, Voice and Video).

---

## 🛠️ Prerequisites

Before building the project, ensure you have a compiler supporting C/C++ and the following developer tools installed on your system:

- **CMake** (v3.16 or newer)
- **Pkg-config**
- **GLib 2.0** development headers (>= 2.16.0)
- **LibXML2** development headers (>= 2.6.0)

### Optional Dependencies (Based on Build Flags)
- **GTK+ 2.0** & **Pango** (For the graphical interface)
- **LibGNT** & **ncurses** (For the Finch console user interface)
- **D-Bus** & **Python 3** (For IPC interface generation)
- **GStreamer 1.0** & **Farstream 0.2** (For Voice/Video & audio sound effects)

On Ubuntu/Debian systems, you can install the core dependencies via:
```bash
sudo apt update
sudo apt install build-essential cmake pkg-config libglib2.0-dev libxml2-dev
```

---

## 🏗️ Building and Installing

We use a standard out-of-source build layout to keep the source tree clean. Follow these simple steps in your terminal:

### 1. Configure the Project
Create a build directory and run the configuration generation:
```bash
cmake -B build -S .
```

### 2. Compile the Code
Compile all project targets using the generated build files:
```bash
cmake --build build --parallel \$(nproc)
```

### 3. Install
Install the compiled binaries, headers, and shared resources to your system path:
```bash
sudo cmake --install build
```

---

## ⚙️ Available Configuration Options

You can customize your build parameters by passing `-D<OPTION>=ON|OFF` during the configuration step. 

| Option | Default | Description |
| :--- | :--- | :--- |
| `ENABLE_GTKUI` | `ON` | Compile the graphical Pidgin user interface (requires GTK+ 2.0). |
| `ENABLE_CONSOLEUI` | `ON` | Compile the terminal/console Finch user interface (requires GNT). |
| `ENABLE_DBUS` | `ON` | Enable D-Bus IPC service integration & code generation. |
| `ENABLE_GSTREAMER` | `ON` | Enable multimedia sound and audio events support via GStreamer. |
| `ENABLE_VV` | `ON` | Enable experimental Voice and Video features. |
| `ENABLE_DEBUG` | `OFF` | Build with strict debugging definitions active. |
| `ENABLE_I18N` | `ON` | Build and install localized system translation arrays. |

*Example of configuring a Headless / Console-only build:*
```bash
cmake -B build -S . -DENABLE_GTKUI=OFF -DENABLE_CONSOLEUI=ON
```

---

## 📄 License

This project is licensed under the **GNU General Public License v2.0 (GPL-2.0)**. See the [LICENSE](LICENSE) file for the full legal text.
