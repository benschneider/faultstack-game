# Faultstack

**A systems-engineering puzzle game about stabilizing a fragile quantum machine**

🎮 **[Play the Demo](https://benschneider.github.io/faultstack-game)**

## What is Faultstack?

Faultstack is a browser-based puzzle game where you build and scale the classical control stack around a fault-tolerant quantum computer. Your job is to bring a fragile quantum system online by routing the right information through the right hardware—while managing bandwidth, latency, and feedback deadlines.

## Core Gameplay

- **Component Placement** – Arrange control-stack components on the board
- **Cable Routing** – Connect compatible ports with cables of varying capacity and speed
- **Controller Configuration** – Set up roles and supporting hardware
- **Runtime Observation** – Watch packet flow, diagnose bottlenecks, and fix failures
- **System Scaling** – Unlock better infrastructure and tackle more demanding workloads

## What You'll Learn

Faultstack teaches three things simultaneously:

1. **System-level reasoning** – Diagnose bottlenecks, make tradeoffs, and understand why architectures succeed or fail
2. **Quantum hardware architecture** – Learn about control stacks, syndrome extraction, decoding loops, and correction paths
3. **Performance and scaling intuition** – Understand how distance, traffic, contention, and deadlines affect system behavior

## Game Structure

The game features a campus map with six buildings:

- **Mission Control** – Browse and accept missions
- **Systems Lab** – Build and test your control stack designs
- **QPU Lab** – Design quantum processing unit packages
- **Research Center** – Unlock new capabilities and hardware
- **Supply Depot** – Acquire components and cables
- **Workbench** – Calibration and build workflows

Progress through training missions to learn the basics, then take on contracts that challenge you with real engineering constraints.

## Built With

- **Rust** – Core game logic and simulation
- **WebAssembly** – Browser runtime
- **Macroquad** – Lightweight game UI framework

## Development Status

Faultstack is actively in development. Current focus:

- Expanding mission content around repetition-code QPU architectures
- Building deeper quantum error correction teaching mechanics
- Improving cable routing and timing pressure gameplay
- Enhancing the visual language for hardware components

## License

See [LICENSE](LICENSE) for details.
