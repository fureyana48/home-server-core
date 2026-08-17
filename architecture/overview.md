# Core Infrastructure Architecture

## Host Layer

### ThinkPad T540p
Role: Fedora Server Core host; container, management, network, and virtualization foundation.

### ThinkPad W530
Role: Proxmox VE Core virtualization host and hypervisor control plane.

## Layer Model

```text
┌──────────────────────────────────────┐
│ Higher Layer / Workloads             │
│ VMs · Containers · Applications      │
│ Services · Experiments               │
├──────────────────────────────────────┤
│ Core Infrastructure Layer            │
│ OS · Network · Firewall · Hypervisor │
│ Management · Base Runtime            │
├──────────────────────────────────────┤
│ Hardware Layer                       │
│ ThinkPad T540p · ThinkPad W530       │
└──────────────────────────────────────┘
```
