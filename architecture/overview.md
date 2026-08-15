# Home Server Core — Architecture Overview

## Core Server v1.0

```text
HIGHER LAYERS
  VMs / Containers / Applications / Services / Experiments
                         │
                         ▼
CORE SERVER LAYER
  Fedora Server T540p + Proxmox VE W530
                         │
                         ▼
HARDWARE
  ThinkPad T540p + ThinkPad W530
```

### T540p

Fedora Server core host with Docker, Cockpit, KVM/QEMU, libvirt, NetworkManager, firewalld, OpenSSH, SELinux and systemd.

### W530

Proxmox VE virtualization-focused core host with UEFI-only/GPT baseline.

## Core Principle

Build the foundation, document it, freeze it, then build above it.

Higher-layer workloads may change frequently. The Core Layer should change deliberately and through documented revisions.
