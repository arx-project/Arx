**BSD-Native Graphics System: Arcan-Inspired Architecture Plan (Arx)**

**Overview:**
When a proof of concept begins, it represents more than a simple experiment, it is the seed of a vision. **Arx** emerges from the desire to move beyond loosely assembled components toward a truly monolithic BSD-native desktop environment. At this stage, the focus is on mapping the terrain, identifying the disciplines required, outlining the foundational components, and understanding how they must interlock to form a seamless and integrated whole. It is a deliberate shift from coexistence to cohesion, from compatibility to purpose-built harmony.

**Arx** is a secure, fully integrated desktop environment and graphics system for BSD systems. Written in **Odin** and scripted in **Wren**, it is designed to replace X11 and Wayland with a cleaner, simpler, and more native solution.

---

**Core Principles:**

* Fully BSD-native, no Linux-specific APIs or daemons
* Security-first, capsicum, jails, sandboxed clients
* Monolithic userland, audio, input, display, and protocol unified
* Minimal dependencies, no dbus, PAM, systemd, or pulseaudio
* Network-aware, built-in remote capability without legacy X11 baggage
* Modern implementation, written in Odin with Wren as the embedded scripting engine

---

**Component Breakdown:**

1. **Kernel Interface Layer**

   * Interface to vt, drm, or future BSD-native KMS
   * Input from devd (no udev dependency)
   * Fallback to framebuffer on unsupported GPUs

2. **Display Server Core**

   * Compositor, renderer, and scene graph manager
   * Sandbox-per-client (jail or chroot)
   * Rendering backends: software, OpenGL, Vulkan (via BSD-compatible Mesa)

3. **Input System**

   * Devd listener and event parser
   * Abstraction over keyboard, mouse, touch, gamepad
   * Secure per-client routing and filtering

4. **Window Protocol**

   * Message-passing IPC or file descriptor-based protocol
   * Clean namespace separation for each client
   * Lightweight protocol designed for simplicity and auditability

5. **Audio System (Optional but Integrated)**

   * Minimal, statically-linked audio stack
   * Support for PCM, mixing, and per-client isolation
   * ALSA-like interface, BSD-native only

6. **Session and Resource Manager**

   * Compositor scripting layer implemented in Wren
   * Resource quotas and watchdogs for clients
   * Snapshot/rollback integration with ZFS (optional)

7. **Client Toolkit SDK**

   * Native drawing API (2D and 3D)
   * BSD-specific bindings (for Odin, C3, C)
   * Backends for SDL, Nuklear, and minimalist GUI widgets

8. **Legacy Compatibility (Optional)**

   * X11/Wayland bridge layer (optional, not default)
   * Run legacy apps in jail with shimmed protocol handler

9. **Remote Access Layer**

   * Secure, efficient streaming of display state
   * Protocol-level rather than pixel-level (like VNC)
   * SSH or capsicum-secured transport

---

**Security Design:**

* Per-client jails or chroots
* Capsicum enforcement on client-server boundaries
* No global clipboard or shared memory unless explicitly permitted
* Event-driven, async messaging to avoid blocking paths

---

**Deployment Strategy:**

### Stage 1: Evaluation and Toolchain Preparation

* Audit Arcan for BSD readiness and Lua dependency boundaries
* Replace Lua scripting engine with embedded Wren interpreter
* Build Arcan and Durden on BSD, create ports or static builds

### Stage 2: Arcan-Based Shell Development

* Fork or reconfigure Durden into a BSD-native desktop shell
* Replace unnecessary features with BSD-native equivalents
* Integrate ZFS snapshotting, `bectl`, `devd`, and jails
* Develop minimal applications (launcher, terminal, settings) using Arcan client protocol

### Stage 3: BSD Desktop Integration

* Design installer integration for Arx
* Define init and session scripts for rc.d or greetd
* Provide configuration UI for shell, themes, startup apps
* Package as a complete DE under a BSD-friendly license

### Stage 4: SDK and App Ecosystem

* Release SDK for developing Arcan-native apps in Odin
* Port simple apps (file manager, image viewer, text editor)
* Provide SDL/Nuklear bindings to facilitate GUI app development

### Stage 5: Optional Compatibility and Remote Layer

* Develop optional X11/Wayland wrapper using jails
* Add secure network session protocol with encrypted transport

---

**Advantages Over KDE, GNOME, and Wayland:**

* Native to BSD from kernel to UI
* No reliance on Linux IPC daemons or service stacks
* Built as a single cohesive platform rather than a layered toolkit
* Secure by design and simple to audit
* Includes modern remote access and session control by default

---

**Project Status:**

* Core architecture is defined
* Component specifications are underway
* Arcan evaluation and Wren substitution planned
* First prototypes focused on compositor, shell, and launcher

---

**Future Goals:**

* Publish Arx as a FreeBSD Ports collection
* Develop Odin-native UI toolkit
* Expand BSD-native application framework
* Add session utilities, clipboard support, accessibility tools
* Integrate jails-aware sandboxing and optional compatibility bridges

---

**License:**
**BSD 2-Clause**

---

**Community and Philosophy:**
Arx is a community-led project grounded in BSD values: simplicity, transparency, auditability, and freedom. It is not a derivative of Linux, nor an adaptation of existing desktop conventions. It is a declaration that BSD systems deserve an environment as principled and coherent as their kernel.

Arx is built not to mimic, but to lead. If you believe BSD should stand on its own terms, we invite you to help shape what comes next.
