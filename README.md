**BSD-Native Graphics System: Arx Architecture and Implementation Plan**

**Overview:**
When a proof of concept begins, it represents more than a simple experiment, it is the seed of a vision. **Arx** emerges from the desire to move beyond loosely assembled components toward a truly monolithic BSD-native desktop environment. At this stage, the focus is on mapping the terrain, identifying the disciplines required, outlining the foundational components, and understanding how they must interlock to form a seamless and integrated whole. It is a deliberate shift from coexistence to cohesion, from compatibility to purpose-built harmony.

**Arx** is a secure, fully integrated desktop environment and graphics system for BSD systems. Written in **Odin** and scripted in **Wren**, it is designed to replace legacy display systems like X11 and avoid Linux-origin technologies such as Wayland, in favor of a native protocol inspired by Arcan.

---

**Core Principles:**

* Entirely BSD-native, free from Linux-specific APIs and daemons
* Secure by design: capsicum, jails, sandboxed graphical clients
* Unified architecture integrating graphics, input, audio, and session layers
* Minimalist dependencies: excludes dbus, PAM, systemd, pulseaudio
* Supports remote operation with a built-in display protocol (non-X11, non-VNC)
* Fully implemented in Odin, with Wren for scripting and customization

---

**Component Breakdown:**

1. **Kernel Interface Layer**

   * Interfaces with vt, DRM, or BSD-native kernel graphics drivers
   * Input sourced through devd events (not udev)
   * Framebuffer fallback for older systems

2. **Display Server Core**

   * Compositor and scene manager in Odin
   * Security isolation for each client
   * Rendering via OpenGL, Pixman, or internal rasterizer

3. **Input System**

   * Native handling of keyboard, mouse, touch, gamepad
   * Event parsing from devd
   * Per-client routing of input events

4. **Window Protocol**

   * Custom BSD-native protocol modeled after Arcan or 9P concepts
   * Uses direct IPC (sockets or memory channels)
   * Lightweight, auditable, and deterministic

5. **Audio System (Optional)**

   * Minimal statically linked backend
   * Native interface for PCM and mixing
   * Optional PipeWire support with modular integration

6. **Session and Resource Manager**

   * Client lifecycle management and system state
   * Wren-powered scripting layer for behavior control
   * ZFS snapshot support for session rollback

7. **Client Toolkit SDK**

   * Lightweight UI toolkit written in Odin
   * Native widgets for internal tools
   * Optional bindings to SDL or Nuklear for developer use

8. **Legacy Compatibility (Optional)**

   * X11/Wayland support is optional via isolated compatibility layer
   * Designed for containment in jails, not core integration

9. **Remote Access Layer**

   * Direct protocol-level display streaming
   * Remote login and interaction over SSH or secure tunnel

---

**Security Design:**

* All graphical clients run with restricted privileges
* Sandboxing through jails and capsicum
* No global clipboard or shared surfaces unless explicitly configured
* Event-driven, asynchronous IPC model

---

**Deployment Strategy:**

**Stage 1: Foundation Development**

* Define core protocol and sandbox rules
* Create base compositor, renderer, and input stack
* Implement IPC and Wren scripting bridge

**Stage 2: Shell and UI**

* Develop internal panel, launcher, and settings UI
* Integrate configuration manager and theme engine
* Provide base SDK for native apps

**Stage 3: System Integration**

* Session startup via rc.conf or greetd
* ZFS support and devd integration
* Logging, crash reporting, and test suite

**Stage 4: Application Ecosystem**

* File manager, terminal, and editor tools
* Clipboard, screenshot, and power menu support
* Developer documentation and SDK release

**Stage 5: Optional Extensions**

* Compatibility sandbox for legacy apps
* Remote desktop support
* Accessibility and internationalization

---

**Advantages Over KDE, GNOME, and Wayland:**

* BSD-native design from kernel to UI
* Free of layered IPC daemons and Linux system services
* Secure by default and coherent in architecture
* Predictable behavior, low resource footprint, and fast startup
* Offers first-class support for jail and ZFS integration

---

**Project Status:**

* Design and architecture planning complete
* Compositor and IPC prototypes in progress
* Input and session lifecycle components under definition

---

**Future Goals:**

* Provide full desktop stack in BSD ports tree
* Deliver SDK and documentation for Odin-native apps
* Build out localization, onboarding, and accessibility systems
* Establish remote control and display features for network use

---

**License:**
**BSD 2-Clause**

---

**Community and Philosophy:**
Arx is a declaration that BSD users deserve a desktop environment built to match the principles of their operating system: simplicity, control, clarity, and technical integrity. It is not adapted from Linux, nor based on external paradigms. Arx is an independent, auditable, and forward-looking environment where BSD is not a platform target, but the foundation.

If you believe in a native BSD future, Arx welcomes your contribution.
