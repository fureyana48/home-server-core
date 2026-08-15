# Home Server Core

**Core Server v1.0 — Portfolio Release**

A documented homelab core-server setup built around two physical server hosts:

- **Lenovo ThinkPad T540p** — Fedora Server
- **Lenovo ThinkPad W530** — Proxmox VE

This repository documents the finalized **Core Layer**: the stable host foundation on which higher-level applications, services, virtual machines, containers, and future experiments can be built without unnecessarily changing the core.

---

## Project Status

**Core Server v1.0: COMPLETE / FROZEN**

The core configuration and finalization work for both hosts has been completed and frozen as the baseline for the v1.0 release.

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

```## Core Layer Principle

The Core Layer is treated as the stable foundation of the homelab.

Changes to applications, containers, virtual machines, services, experiments, and other higher-level workloads should not unnecessarily modify or destabilize the Core Layer.

                    ┌─────────────────────────────┐
                    │       Applications           │
                    │ Containers / VMs / Services │
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
                    │          HARDWARE             │
                    │ ThinkPad T540p / W530        │
                    └─────────────────────────────┘
Repository Structure
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
Server Hosts
Fedora Server — ThinkPad T540p

Primary role:

Fedora Server core host
Docker container platform
Cockpit management
KVM/libvirt virtualization foundation
Network and firewall foundation
Headless/server-oriented operation

The finalized configuration was audited and captured as the Fedora T540p Core baseline.

Proxmox VE — ThinkPad W530

Primary role:

Proxmox VE core virtualization host
Virtual machine management
Core hypervisor platform
Dedicated virtualization foundation

The finalized configuration was audited and captured as the Proxmox W530 Core baseline.

Configuration Backups

Raw configuration captures and backup artifacts are kept separate from the public documentation layer.

Before any backup artifact is published, it must be reviewed for:

passwords
private keys
API tokens
credentials
personal information
sensitive network information
other data that should not become public

Large raw system backups and filesystem-level configuration archives are not intended to be published directly as part of the public repository.

The repository documents the architecture, configuration, audit results, and reproducibility of the Core Layer rather than acting as a raw backup dump.

Release Model
v1.0

Finalized and frozen Core Layer baseline.

v1.x

Controlled maintenance or changes to the Core Layer itself.

Higher Layers

Applications, containers, virtual machines, services, experiments, and other workloads are developed above the frozen Core Layer.

Documentation

Documentation for each server is maintained separately:

Fedora T540p Core
Proxmox W530 Core

Architecture documentation:

Architecture Overview

Hardware inventory:

Core Server Hardware

Release documentation:

Core Server v1.0
Project Scope

This project focuses on:

homelab infrastructure
Linux server administration
virtualization
containerization
network services
server management
configuration management
documentation
reproducibility
technical learning
portfolio development

This is a personal homelab and technical portfolio project.

Status

Core Server v1.0

T540p Fedora Server Core — COMPLETE

W530 Proxmox VE Core — COMPLETE

Core Layer — FROZEN

Public Release Target — 17 August 2026

---
