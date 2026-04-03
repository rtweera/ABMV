# ABMV - Agent-Based Modeling & Visualization (Flocking Simulation)

ABMV is a JavaFX-based boids simulation that demonstrates emergent flocking behavior using classic rules:
- **Separation** (avoid crowding),
- **Alignment** (match neighbor direction),
- **Cohesion** (move toward neighbors).

The project provides a live visualization canvas plus runtime controls for tuning simulation parameters.

## Table of Contents
- [Overview](#overview)
- [Features](#features)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [Prerequisites](#prerequisites)
- [Getting Started](#getting-started)
- [Running the App](#running-the-app)
- [Running Tests](#running-tests)
- [Usage Guide](#usage-guide)
- [Configuration & Parameters](#configuration--parameters)
- [Architecture Summary](#architecture-summary)
- [Current Work](#current-work)
- [Future Work](#future-work)
- [Known Limitations](#known-limitations)
- [Contributing](#contributing)
- [License](#license)

## Overview
This repository contains an interactive flocking simulator where each boid updates itself based on nearby boids and wraps around world boundaries. A JavaFX control panel allows modifying behavior weights and movement characteristics during runtime.

## Features
- JavaFX real-time rendering of boids as direction-aware triangles.
- Adjustable runtime controls:
  - boid speed,
  - perception radius,
  - separation weight,
  - alignment weight,
  - cohesion weight.
- Add boids dynamically.
- Reset simulation state.
- Boid count HUD shown in the canvas.
- Parallelized boid updates via Java streams.

## Tech Stack
- **Language:** Java
- **Build Tool:** Maven
- **UI:** JavaFX (`javafx-controls`)
- **Testing:** JUnit 5

## Project Structure
```text
src/main/java/com/app/
├── FlockingSimulatorApp.java         # JavaFX entry point + UI controls
├── boid/Boid.java                    # Boid behavior rules and movement
├── math/Vector2D.java                # 2D vector utilities
├── simulation/Simulation.java        # Simulation state/update loop
├── visualization/Visualizer.java     # Canvas rendering and frame updates
└── message/Message.java              # Messaging model (currently unused)

src/test/java/com/app/
└── Main32Test.java                   # Basic setup/smoke test
```

## Prerequisites
- **JDK 20** (required by current Maven compiler configuration).
- Maven 3.8+ recommended.

## Getting Started
```bash
git clone https://github.com/rtweera/ABMV.git
cd ABMV
```

## Running the App
Use the JavaFX Maven plugin:

```bash
mvn javafx:run
```

## Running Tests
```bash
mvn test
```

If you see `invalid target release: 20`, switch to JDK 20 before running Maven.

## Usage Guide
When the application starts:
1. A simulation window opens with a drawing canvas and control panel.
2. Use **Add Boid** to inject new boids.
3. Tune sliders to observe emergent behavior changes in real time.
4. Use **Reset Simulation** to clear and reinitialize boids.

## Configuration & Parameters
Defaults in current implementation:
- Initial boid count: `1`
- Canvas/simulation space: `800 x 600`
- Boid max speed: `2.0`
- Perception radius: `50`
- Separation weight: `1.5`
- Alignment weight: `1.0`
- Cohesion weight: `1.0`

## Architecture Summary
- **`FlockingSimulatorApp`**: Creates UI layout, sliders, and buttons; starts/stops simulation and rendering.
- **`Simulation`**: Owns boid collection and simulation loop (approx. 60 FPS update cadence).
- **`Boid`**: Applies separation, alignment, and cohesion forces; updates velocity/position; wraps on boundaries.
- **`Visualizer`**: Renders boids every frame with heading-based rotation.
- **`Vector2D`**: Reusable vector math operations used throughout boid logic.

## Current Work
The repository currently focuses on a functional baseline flocking simulator:
- Core boid rules are implemented and parameterized.
- Runtime tuning UI is in place and connected to simulation state.
- Rendering loop and simulation loop are integrated.
- Basic Maven/JUnit project setup exists.

## Future Work
Potential next improvements:
- Add meaningful automated tests for boid behavior and simulation invariants.
- Introduce obstacle/predator mechanics (partially hinted in commented code).
- Improve concurrency model and shared parameter handling for thread safety.
- Support pause/resume, remove-boid controls, and richer UI/UX.
- Add configuration profiles/presets and save/load simulation settings.
- Improve performance for larger boid counts (spatial partitioning like quadtrees).
- Export frames/record simulation runs.
- Add CI checks and badge/status reporting in repository metadata.

## Known Limitations
- Current test suite is minimal.
- Build is pinned to Java 20; non-20 JDKs will fail compile.
- Some classes (e.g., messaging model) are not yet integrated into active simulation flow.

## Contributing
Contributions are welcome. Suggested workflow:
1. Fork the repository.
2. Create a feature branch.
3. Make focused changes with tests/docs updates.
4. Open a pull request describing motivation and impact.

## License
No license file is currently present in this repository. Add a `LICENSE` file to define usage terms.
