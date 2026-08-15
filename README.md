````markdown
# Home Server Core

**Core Server v1.0 — Portfolio Release**

A documented homelab core-server setup built around two physical server hosts:

- **Lenovo ThinkPad T540p** — Fedora Server
- **Lenovo ThinkPad W530** — Proxmox VE

This repository documents the finalized **Core Layer**: the stable host foundation on which higher-level applications, services, virtual machines, containers, and future experiments can be built without unnecessarily modifying or destabilizing the core.

---

## Project Status

**Core Server v1.0: COMPLETE / FROZEN**

The core configuration and finalization work for both server hosts has been completed and frozen as the baseline for the v1.0 release.

**Public release target:** 17 August 2026

Work above the Core Layer will continue separately after the v1.0 baseline is released.

---

## Architecture

```text
Home Server Core v1.0
│
├── Fedora Server — ThinkPad T540p
│   └── Core host + Docker + Cockpit + KVM/libvirt foundation
│
└── Proxmox VE — ThinkPad W530
    └── Core virtualization host
````

## Core Layer Principle

The Core Layer is treated as the stable foundation of the homelab.

Changes to applications, containers, virtual machines, services, experiments, and other higher-level workloads should not unnecessarily modify or destabilize the Core Layer.

```text
                    ┌─────────────────────────────┐
                    │        HIGHER LAYERS         │
                    │ Applications / Containers    │
                    │ VMs / Services / Experiments│
                    └──────────────┬──────────────┘
                                   │
                    ┌──────────────▼──────────────┐
                    │       CORE SERVER LAYER      │
                    │ Stable host configuration    │
                    │ Networking / Security / Base │
                    │ Virtualization foundation    │
                    └──────────────┬──────────────┘
                                   │
                    ┌──────────────▼──────────────┐
                    │          HARDWARE            │
                    │ ThinkPad T540p / W530       │
                    └─────────────────────────────┘
```

The purpose of this separation is to allow higher-level workloads to evolve while keeping the underlying server foundation predictable, documented, and recoverable.

---

## Repository Structure

```text
.
├── README.md
├── LICENSE
├── CHANGELOG.md
│
├── docs/
│   ├── fedora-t540p/
│   │   ├── audit-report.md
│   │   ├── final-configuration.md
│   │   └── completion-statement.md
│   │
│   └── proxmox-w530/
│       ├── audit-report.md
│       ├── final-configuration.md
│       └── completion-statement.md
│
├── architecture/
│   └── overview.md
│
├── inventory/
│   └── core-server-hardware.md
│
└── release/
    └── v1.0/
        └── release-notes.md
```

---

# Server Hosts

## Fedora Server — ThinkPad T540p

**Primary role:**

* Fedora Server core host
* Docker container platform
* Cockpit management
* KVM/libvirt virtualization foundation
* Network and firewall foundation
* Headless/server-oriented operation

The finalized configuration was audited and captured as the **Fedora T540p Core baseline**.

### Core Components

* Fedora Server
* NetworkManager
* firewalld
* OpenSSH
* Docker Engine
* Cockpit
* KVM/QEMU
* libvirt
* SELinux
* systemd

The host is designed to provide a stable server foundation while allowing containers, virtual machines, and other services to operate above the Core Layer.

---

## Proxmox VE — ThinkPad W530

**Primary role:**

* Proxmox VE core virtualization host
* Virtual machine management
* Core hypervisor platform
* Dedicated virtualization foundation

The finalized configuration was audited and captured as the **Proxmox W530 Core baseline**.

The W530 is treated as the dedicated virtualization-oriented host within the Core Server architecture.

---

# Documentation

Documentation is maintained separately for each physical server.

## Fedora T540p

* [Audit Report](docs/fedora-t540p/audit-report.md)
* [Final Configuration](docs/fedora-t540p/final-configuration.md)
* [Completion Statement](docs/fedora-t540p/completion-statement.md)

## Proxmox W530

* [Audit Report](docs/proxmox-w530/audit-report.md)
* [Final Configuration](docs/proxmox-w530/final-configuration.md)
* [Completion Statement](docs/proxmox-w530/completion-statement.md)

## Architecture

* [Architecture Overview](architecture/overview.md)

## Hardware

* [Core Server Hardware Inventory](inventory/core-server-hardware.md)

## Release

* [Core Server v1.0 Release Notes](release/v1.0/release-notes.md)

---

# Configuration Backups

Raw configuration captures and backup artifacts are kept separate from the public documentation layer.

Before any backup artifact is published, it must be reviewed for:

* passwords
* private keys
* API tokens
* credentials
* personal information
* sensitive network information
* other data that should not become public

Large raw system backups and filesystem-level configuration archives are not intended to be published directly as part of the public repository.

The repository documents the architecture, configuration, audit results, and reproducibility of the Core Layer rather than acting as a raw backup dump.

---

# Release Model

## v1.0 — Core Baseline

The v1.0 release represents the finalized and frozen Core Layer baseline.

The baseline includes:

* audited host configuration
* documented server architecture
* finalized core services
* networking foundation
* firewall configuration
* SSH configuration
* virtualization foundation
* storage configuration
* system configuration
* hardware inventory
* configuration capture
* completion documentation

**Status: COMPLETE / FROZEN**

---

## v1.x — Controlled Core Maintenance

Future v1.x releases may contain controlled changes to the Core Layer itself.

Examples may include:

* infrastructure corrections
* security improvements
* compatibility changes
* documented configuration updates
* hardware-related changes
* maintenance required by future system updates

Changes to the Core Layer should be intentional and documented.

---

## Higher Layers

Applications, containers, virtual machines, services, experiments, and other workloads are developed above the frozen Core Layer.

Higher-layer development does not automatically constitute a change to the Core Server baseline.

This separation allows the homelab to evolve without unnecessarily rebuilding the underlying infrastructure.

---

# Project Scope

This project focuses on:

* homelab infrastructure
* Linux server administration
* virtualization
* containerization
* network services
* server management
* configuration management
* documentation
* reproducibility
* technical learning
* portfolio development

This is a personal homelab and technical portfolio project.

---

# Design Philosophy

The project follows a simple principle:

> **Build the foundation once. Document it properly. Freeze it. Then build on top of it.**

The Core Layer is therefore treated as infrastructure rather than an experimental playground.

Higher-level workloads may change frequently.

The Core Layer should change deliberately.

---

# Current Status

| Component         | Status             |
| ----------------- | ------------------ |
| Fedora T540p Core | **COMPLETE**       |
| Proxmox W530 Core | **COMPLETE**       |
| Core Layer        | **FROZEN**         |
| Core Server v1.0  | **COMPLETE**       |
| Public Release    | **17 August 2026** |

---

# Portfolio

Home Server Core is a personal homelab infrastructure project created to document practical experience with:

* Linux server administration
* Fedora Server
* Proxmox VE
* Docker
* Cockpit
* KVM/QEMU
* libvirt
* networking
* firewalld
* SSH
* SELinux
* systemd
* virtualization infrastructure
* configuration auditing
* infrastructure documentation
* reproducible server configuration

The project is intended to serve both as a functional homelab foundation and as a technical portfolio demonstrating hands-on infrastructure work.

---

## License

See [LICENSE](LICENSE) for the applicable license.

```
