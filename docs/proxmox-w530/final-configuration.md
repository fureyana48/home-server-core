# Proxmox W530 — Final Configuration Reference

## Core Server v1.0

**Platform:** Lenovo ThinkPad W530  
**Core platform:** Proxmox VE  
**Core role:** Virtualization-focused server / homelab core  
**Boot:** UEFI-only  
**Partitioning:** GPT  
**Status:** COMPLETE / FROZEN

## 1. Hardware Baseline

| Item | Verified baseline |
|---|---|
| Platform | Lenovo ThinkPad W530 |
| CPU | Intel Core i7-3520M, 2 cores / 4 threads, 2.9 GHz |
| RAM | 16 GB (2 × 8 GB) |
| GPU | NVIDIA Quadro K1000M, 2 GB DDR3 |
| Display | 15.6-inch, 1600×900 |
| Boot | UEFI-only |
| Partitioning | GPT |

## 2. Storage

The authoritative retained W530 inventory contains **exactly three storage devices**:

| Capacity | Device | Project role |
|---:|---|---|
| 128 GB | mSATA SSD | Windows 11 Pro for Workstations storage |
| 500 GB | Seagate FireCuda SSHD, 5400 RPM, 8 GB cache | Linux/server storage; historical Ubuntu Server use |
| 1 TB | HGST HDD, 7200 RPM | ISO / Ventoy storage |

No fourth storage device belongs to the authoritative inventory.

## 3. Core Role

The W530 is the dedicated **Proxmox VE virtualization core** of Home Server Core.

The Core Layer provides the stable foundation for:

- virtual machines
- containers
- virtual networking
- virtual storage
- server workloads
- learning and homelab experiments

## 4. Layering Principle

```text
Higher Layers
  VMs / Containers / Services / Experiments
                 │
                 ▼
Proxmox VE Core
                 │
                 ▼
ThinkPad W530 Hardware
```

Higher-layer workloads may evolve without routinely modifying the Core.

## 5. Network / Management Boundary

The W530 is intended to be remotely managed through the Proxmox web interface.

Permanent static addressing was explicitly deferred from v1.0. Future candidates discussed were `192.168.1.23` or `192.168.1.33`; these are **not v1.0 final values**.

## 6. Backup Boundary

Raw configuration captures are kept separate from public documentation. Credentials, private keys, tokens and other sensitive data must not be published.

Exact live command output, package versions, network values, VM inventories and storage identifiers should only be taken from the authoritative W530 audit/master capture; this document intentionally does not invent missing values.

## 7. Deferred Work

- permanent static IP
- final web-console IP/banner update
- additional workloads
- server-side GitHub synchronization
- future Core revisions

## 8. Final Declaration

**The Lenovo ThinkPad W530 Proxmox VE Core Server configuration is declared COMPLETE / FROZEN for Home Server Core v1.0.**

Future changes to the Core itself should be documented as a new revision such as v1.1.
