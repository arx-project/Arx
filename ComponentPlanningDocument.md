# Arx Desktop Environment: Component Planning Document

## Purpose

Define and document all core and supporting components required for building Arx, a monolithic BSD native desktop environment written in Odin, using Wayland and BSD base system services.

---

## Core System Components

### 1. Compositor

* Stacking window manager using wlroots (FFI bindings)
* Handles: surface lifecycle, input, focus, output layout

### 2. Renderer

* Draws window frames, shadows, backgrounds, and decorations
* Backend: OpenGL, Pixman, or internal raster engine
* Supports: anti-aliased fonts, theme-aware elements

### 3. Session Manager

* Integrates with rc.conf or greetd
* Launches compositor, panel, and applications
* Handles logout, shutdown, reboot

### 4. IPC Layer

* BSD native Unix sockets for internal communication
* Event subscription model: UI components can respond to signals

### 5. Configuration System

* Loads and saves config in TOML or JSON
* Default path: \~/.config/arx/config.toml
* Supports live reload or restart reload

---

## Graphical Components

### 6. Panel / Bar

* Layer shell protocol client
* Hosts: clock, workspaces, launcher, tray

### 7. Launcher

* Application search and execution (like dmenu or rofi)
* Reads from .desktop files or predefined list

### 8. Settings Manager

* GUI to configure themes, resolution, keybindings, sessions

### 9. Notification Daemon

* Displays Wayland native notifications
* Follows desktop notifications spec (without D-Bus)

### 10. UI Toolkit

* Minimal widget library written in Odin
* Widgets: buttons, sliders, text fields, lists
* Used by settings manager, launcher, and other internal tools

---

## Optional or Extensible Components

### 11. File Manager

* Optional integration: Thunar, PCManFM Qt, or native Odin based

### 12. Terminal Emulator

* Odin native terminal or integration with foot

### 13. Clipboard Manager

* Wayland compatible copy and paste
* Secure memory handling

### 14. Screenshot Tool

* Select region or window
* Saves to configured location

### 15. Power Menu

* Suspend, reboot, shutdown, logout
* Uses rc commands, no polkit or elogind

### 16. Accessibility (Future)

* Keyboard navigation and basic screen reader hooks

### 17. Application Framework (Future)

* APIs for native Odin applications
* Window lifecycle, input event dispatch, theme integration
* Consider app sandboxing and permissions model

### 18. User Onboarding and First Login

* Default configuration generator on first launch
* Minimal setup wizard for resolution, theme, keyboard layout

### 19. Localization and Internationalization

* Unicode support, including RTL layout support
* Language selector in settings manager
* i18n strings support in UI toolkit

### 20. Security and Privilege Separation

* Process isolation where applicable
* Drop privileges for UI daemons
* Secure defaults for clipboard, notifications, and IPC

---

## Backend Infrastructure

### 21. Logging

* Per component logging to \~/.cache/arx/\*.log
* Configurable verbosity

### 22. Theme and Font Engine

* Centralized theme system loaded from config
* Renders using internal renderer

### 23. Input Device Manager

* Mouse, touchpad, keyboard, gamepad
* Uses libinput (via wlroots)

### 24. Audio Integration

* PipeWire and WirePlumber
* Optional GUI mixer

---

## Developer and Debugging Tools

### 25. Dev Console

* Interactive log viewer and diagnostics

### 26. Crash Handling

* Logs backtraces and errors
* Optional integration with external crash reporters

### 27. Testing Framework

* Unit and integration tests for components

---

## Deliverables

* Initial proof of concept: compositor, panel, launcher
* Phase 2: notifications, settings, terminal
* Phase 3: UI toolkit, file manager, screenshots, clipboard
* Long term: accessibility, application framework, BSD ports integration

---

## Next Steps

* Define interface contracts between components
* Begin Odin bindings for wlroots and libinput
* Draft config schema and user onboarding design
* Set up build system and logging infrastructure
