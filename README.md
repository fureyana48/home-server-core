# Home Server Core

**Core Infrastructure Documentation — Technical Template**

This repository documents the stable **Core Layer** of a personal homelab infrastructure.

## Architecture

```text
Home Server Core
├── Fedora Server — ThinkPad T540p
├── Proxmox VE — ThinkPad W530
└── Higher Layers: VMs / Containers / Applications / Services / Experiments
```

## Core Layer Policy

The Core Layer is the controlled infrastructure boundary. Changes above it should not unnecessarily modify or destabilize the host foundation.

## Documentation Lifecycle

1. Scope and role
2. Baseline configuration
3. Pre-change audit
4. Change record
5. Post-change validation
6. Backup and integrity verification
7. Release statement

## Versioning

- `v1.0.x` — patch-level Core maintenance
- `v1.1.x` — controlled Core maintenance line
- `v1.2.x` — controlled Core maintenance line
- `v2.x+` — higher-layer/workload development

See `docs/governance/versioning.md`.
