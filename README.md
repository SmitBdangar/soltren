# Soltren Enterprise Raycaster

A robust, enterprise-grade 3D Raycaster engine built entirely in Rust. It renders a 2D map into a First-Person 3D perspective directly inside your terminal using ASCII characters and the Digital Differential Analysis (DDA) algorithm. 

This project aims to demonstrate clean architecture, strong typing, and robust panic/error handling within a terminal application context.

## Features
- **DDA Algorithm**: Highly efficient ray vector math to calculate wall distances and fix fisheye distortion.
- **Terminal Rendering**: A custom, double-buffered frame (`crossterm`) allows for flicker-free rendering at high framerates.
- **Directional Lighting**: Walls automatically dim based on distance to the camera and orientation (N/S vs E/W).
- **Strong Typing**: Core engine uses a custom `Vector2D` library and strongly typed `Material` enums for physical map layouts.

---

## 🚀 Building & Running

Ensure you have Rust and Cargo installed via rustup.

### ⚠️ Windows Requirements
Because the engine uses `crossterm` to interface directly with the low-level Windows Console API (switching to Raw Mode to accept unbuffered keyboard input), **you must have a C++ linker installed to compile the `winapi` bindings.**

If you get a `linker "link.exe" not found` error during compilation:
1. Download [Visual Studio Build Tools](https://visualstudio.microsoft.com/visual-cpp-build-tools/).
2. Run the installer and check the box for **"Desktop development with C++"**.
3. Finish the installation and **Restart your terminal** path context.

### Run Command
```bash
cargo run --release
```

---

## 🎮 Controls
* **W / Up Arrow**: Move Forward
* **S / Down Arrow**: Move Backward
* **A / Left Arrow**: Rotate Camera Left
* **D / Right Arrow**: Rotate Camera Right
* **Esc / Q**: Quit the engine cleanly

## Architecture Breakdown
* `src/engine.rs`: The core fixed-timestep game loop preventing CPU melting.
* `src/map.rs`: A strongly typed Material grid.
* `src/player.rs`: The entity holding geometric position, direction, and camera plane vectors.
* `src/math.rs`: Provides the `Vector2D` foundation for smooth DDA math.
* `src/raycaster.rs`: Decoupled pure math DDA ray generation.
* `src/renderer/*.rs`: Handles OS-level API calls, frame buffering, color handling, and a custom Panic Hook to prevent the terminal from permanently locking up on a crash.
