## **Arx: A Monolithic BSD Native Desktop Environment**

When a proof of concept begins, it represents more than a simple experiment, it is the seed of a vision. **Arx** emerges from the desire to move beyond loosely assembled components toward a truly monolithic BSD native desktop environment. At this stage, the focus is on mapping the terrain, identifying the disciplines required, outlining the foundational components, and understanding how they must interlock to form a seamless and integrated whole. It is a deliberate shift from coexistence to cohesion, from compatibility to purpose built harmony.

---

### **Overview**

**Arx** is a fully integrated desktop environment for FreeBSD and GhostBSD, written entirely in **Odin** and designed exclusively for **Wayland**. Inspired by the system cohesion of macOS but grounded in the clarity, control, and simplicity that define BSD, Arx is built natively for BSD from the kernel outward.

This is not a rebranded collection of tools nor a port of Linux assumptions. Arx is a clean slate: purpose built, tightly integrated, and developed with the BSD architecture and philosophy in mind.

---

### **Design Goals**

* Native to BSD with no dependence on Linux-specific subsystems
* Pure Wayland display architecture with no X11 fallback
* Session management via FreeBSD `rc.conf` or `greetd`, with no `elogind`, `dbus`, or layered init services
* Written entirely in Odin for performance, memory safety, and direct system access
* Unified user interface stack, with cohesive components designed as one system
* Centralized configuration using TOML or JSON under `~/.config/arx/`
* Minimal resource usage, fast startup, and clear runtime behavior

---

### **Architecture**

#### Core Layers

* **Compositor**: Stacking window manager built in Odin using `wlroots` via FFI
* **Renderer**: Direct drawing of windows and UI using OpenGL, Pixman, or internal raster routines
* **Panel and Shell**: Layer shell interface written in Odin
* **Launcher**: Odin-based graphical launcher for applications
* **Notifications**: Wayland native popup system
* **Settings Manager**: GUI for configuring user and system settings
* **UI Toolkit**: Minimal Odin-native widget library, optionally wrapping `libui`, `raygui`, or lightweight alternatives

#### System Components

* **Session Initialization**: Uses FreeBSD `rc.conf` or `greetd`, without `elogind`, `dbus`, or system-level daemons from Linux
* **IPC**: Unix domain sockets with no reliance on D-Bus
* **Configuration Store**: Unified settings tree under `~/.config/arx/`
* **Theming and Fonts**: Applied globally from configuration files for consistent visual behavior
* **Audio Subsystem**: PipeWire and WirePlumber
* **Terminal Emulator**: `foot` or an Odin-native terminal
* **File Manager**: Optional, with support for Thunar, PCManFM Qt, or a future Arx-native implementation

---

### **What Arx Intentionally Excludes**

* X11
* GTK and Qt
* systemd, elogind, dbus, polkit, and related service layers
* Themed tool mashups or environments composed from unrelated toolkits
* Linux compatibility layers and abstractions

Arx is not built for general compatibility. It is built for BSD consistency.

---

### **How Arx Differs from KDE and GNOME**

* **Native to BSD**: Arx is built specifically for the BSD operating system, not adapted from Linux desktops
* **Integrated by Design**: Components are developed as a single, unified system
* **Direct IPC**: Uses native BSD mechanisms instead of Linux daemons and bus protocols
* **Deterministic and Transparent**: Designed for predictable behavior, maintainability, and clarity

KDE and GNOME are expansive, multi-platform desktops that assume Linux. Arx assumes BSD and embraces its design principles.

---

### **Project Status**

* Core architecture is defined
* Component specifications are underway
* `wlroots` bindings in Odin are in active development
* First prototypes are focused on the compositor, panel, and launcher

---

### **Future Goals**

* Publish Arx as a FreeBSD Ports collection
* Develop a standalone Odin UI toolkit for native applications
* Establish a BSD-native application framework for developers
* Implement clipboard handling, screenshot utilities, and full session lifecycle integration
* Explore support for jails-aware desktop utilities and accessibility frameworks

---

### **License**

**BSD 2 Clause**

---

### **Community and Philosophy**

**Arx** is a community led project grounded in BSD values: simplicity, transparency, auditability, and freedom. It is not a derivative of Linux, nor an adaptation of existing desktop conventions. It is a declaration that BSD systems deserve an environment as principled and coherent as their kernel.

Arx is built not to mimic, but to lead. If you believe BSD should stand on its own terms, we invite you to help shape what comes next.

