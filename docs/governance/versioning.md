# Infrastructure Versioning Policy

## Core Release Family

Core infrastructure uses the `1.x` release family.

Examples:

```text
v1.0.0
v1.0.1
v1.1.0
v1.1.1
v1.2.0
v1.2.1
```

Patch releases address corrective or maintenance changes without materially changing Core architecture.

Minor releases represent intentional Core configuration evolution while preserving the architectural role of the Core Layer.

## Higher-Layer Release Family

Workload and experimentation layers use `v2.x`, `v3.x`, and later release families.

```text
v2.0.0
v2.1.0
v2.1.1
v3.0.0
```

## Principle

```text
Core Layer    = stable infrastructure boundary
Higher Layer = controlled workload evolution
```
