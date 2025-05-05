**BSD-Native Graphics System: Arcan-Inspired Architecture Plan (Arx)**

**Overview:**
When a proof of concept begins, it represents more than a simple experiment, it is the seed of a vision. **Arx** emerges from the desire to move beyond loosely assembled components toward a truly monolithic BSD-native desktop environment. At this stage, the focus is on mapping the terrain, identifying the disciplines required, outlining the foundational components, and understanding how they must interlock to form a seamless and integrated whole. It is a deliberate shift from coexistence to cohesion, from compatibility to purpose-built harmony.

**Arx** is a secure, fully integrated desktop environment and graphics system for BSD systems. Written in **Odin** and scripted in **Wren**, it is designed to replace X11 and Wayland with a cleaner, simpler, and truly native BSD solution.

---

**Purpose:**
Define and document all core and supporting components required for building Arx, a monolithic BSD-native desktop environment written in Odin, using BSD system services and free from Linux-specific display architectures.

---

**Core Principles:**

* Fully BSD-native, no Linux-specific APIs or daemons
* Security-first, capsicum, jails, sandboxed clients
* Monolithic userland, audio, input, display, and protocol unified
* Minimal dependencies, no dbus, PAM, systemd, or pulseaudio
* Network-aware, built-in remote capability without legacy X11 or Wayland
* Modern implementation, written in Odin with Wren as the embedded scripting engine

---

**Core System Components:**

1. **Compositor**

   * Stacking window manager written natively in Odin
   * Handles surface lifecycle, input, focus, and output layout
   * Implements its own protocol modeled after Arcan or Plan 9 concepts

2. **Renderer**

   * Draws window frames, shadows, backgrounds, and decorations
   * Backend: OpenGL, Pixman, or internal raster engine
   * Supports anti-aliased fonts, theme-aware elements

3. **Session Manager**

   * Integrates with rc.conf or greetd
   * Launches compositor, panel, and applications
   * Handles logout, shutdown, reboot

4. **IPC Layer**

   * BSD-native Unix sockets or capability-secured channels
   * Event subscription model for component interaction

5. **Configuration System**

   * Loads and saves config in TOML or JSON
   * Default path: \~/.config/arx/config.toml
   * Supports live reload or restart reload

---

**Graphical Components:**

6. **Panel / Bar**

   * Top-level UI bar for system information and control
   * Hosts clock, workspaces, launcher, tray

7. **Launcher**

   * Application search and execution
   * Reads from native manifest files or predefined list

8. **Settings Manager**

   * GUI to configure themes, resolution, keybindings, sessions

9. **Notification Daemon**

   * Displays notifications using internal protocol
   * Avoids D-Bus and external libraries

10. **UI Toolkit**

* Minimal widget library written in Odin
* Provides buttons, sliders, text fields, lists
* Used by internal tools and optionally available to third-party apps

---

**Optional or Extensible Components:**

11. **File Manager**

* Optional: Odin-native implementation

12. **Terminal Emulator**

* Odin-native terminal with minimal dependencies

13. **Clipboard Manager**

* Native copy and paste
* Secure memory handling

14. **Screenshot Tool**

* Region or window capture
* Saves to configured location

15. **Power Menu**

* Suspend, reboot, shutdown, logout
* Uses rc commands

16. **Accessibility (Future)**

* Keyboard navigation, screen reader hooks

17. **Application Framework (Future)**

* APIs for Odin apps: lifecycle, input, themes
* App sandboxing and permissions

18. **User Onboarding and First Login**

* Default configuration generator
* Minimal setup wizard

19. **Localization and Internationalization**

* Unicode and RTL support
* Language selector
* i18n support in UI toolkit

20. **Security and Privilege Separation**

* Per-component isolation
* Dropped privileges for daemons
* Secure defaults

---

**Backend Infrastructure:**

21. **Logging**

* Per-component logs in \~/.cache/arx/\*.log
* Configurable verbosity

22. **Theme and Font Engine**

* Central theme system
* Rendered via internal renderer

23. **Input Device Manager**

* Mouse, touchpad, keyboard, gamepad
* Uses devd and custom input handling, no libinput

24. **Audio Integration**

* Optional minimal audio layer
* PipeWire support can be considered modular

---

**Developer and Debugging Tools:**

25. **Dev Console**

* Interactive log viewer and diagnostics

26. **Crash Handling**

* Logs backtraces and errors
* Optional crash report integration

27. **Testing Framework**

* Unit and integration tests

---

**Deliverables:**

* Initial proof of concept: compositor, panel, launcher
* Phase 2: notifications, settings, terminal
* Phase 3: UI toolkit, file manager, screenshots, clipboard
* Long term: accessibility, application framework, BSD ports integration

---

**Next Steps:**

* Define interface contracts between components
* Begin Odin implementation of graphics protocol and input handling
* Draft config schema and user onboarding design
* Set up build system and logging infrastructure

---

**License:**
**BSD 2-Clause**

---

**Community and Philosophy:**
Arx is a community-led project grounded in BSD values: simplicity, transparency, auditability, and freedom. It is not a derivative of Linux, nor an adaptation of existing desktop conventions. It is a declaration that BSD systems deserve an environment as principled and coherent as their kernel.

Arx is built not to mimic, but to lead. If you believe BSD should stand on its own terms, we invite you to help shape what comes next.
