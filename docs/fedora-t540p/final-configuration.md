# Fedora T540p — Final Configuration

## Core Server v1.0

**Platform:** Lenovo ThinkPad T540p  
**Operating System:** Fedora Linux 44 Server Edition  
**Hostname:** `t540p.fedora-server`  
**Architecture:** x86-64  
**Kernel:** `7.1.7-200.fc44.x86_64`  
**Server Role:** Fedora Core Server  
**Configuration Status:** FROZEN  
**Baseline:** Core Server v1.0

---

## 1. System Identity

| Item | Final Configuration |
|---|---|
| Hostname | `t540p.fedora-server` |
| Pretty Hostname | `T540p - Fedora Server` |
| OS | Fedora Linux 44 Server Edition |
| Architecture | x86-64 |
| Hardware | Lenovo ThinkPad T540p |
| Firmware | GMET91WW (2.39) |
| Boot Target | `multi-user.target` |
| Kernel | `7.1.7-200.fc44.x86_64` |
| Timezone | `Asia/Jakarta (WIB, UTC+7)` |
| NTP | Active / synchronized |

---

## 2. Network

### Primary Interface

| Item | Configuration |
|---|---|
| Interface | `wlp4s0` |
| Type | Wi-Fi |
| Connection | `Blues 1` |
| SSID | `Blues` |
| IPv4 | `192.168.1.28/24` |
| Gateway | `192.168.1.1` |
| DNS | `118.98.115.69`, `118.98.115.70` |
| NetworkManager | Active |

### Additional Network Devices

- `docker0`
- `br-0af954c5d3e6`
- `lo`
- `p2p-dev-wlp4s0`
- `enp0s25`

### Network Status

- LAN connectivity: PASS
- Internet connectivity: PASS
- Hostname resolution: PASS
- Wi-Fi connection: ACTIVE

> Note: The current Core Server v1.0 configuration uses DHCP-assigned IPv4 addressing. Permanent server IP assignment is intentionally deferred to a future Core Server revision.

---

## 3. Firewall

### Firewalld

**Status:** Active  
**Default Zone:** `FedoraServer`

### Active Interface

```text
wlp4s0
````

### Enabled Services

```text
cockpit
dhcpv6-client
http
https
ssh
```

### Open Ports

```text
53/tcp
53/udp
80/tcp
3000/tcp
8080/tcp
8081/tcp
8096/tcp
9090/tcp
9443/tcp
```

### Docker Zone

Docker networking uses its own firewalld zone:

```text
docker
```

with:

```text
br-0af954c5d3e6
docker0
```

### Runtime / Permanent Consistency

Runtime and permanent firewall configurations were verified as matching.

---

## 4. SSH

### Service

```text
sshd.service
```

**Status:** Active
**Enabled:** Yes

### Effective Configuration

```text
Port 22
ListenAddress [::]:22
ListenAddress 0.0.0.0:22
UsePAM yes
ClientAliveInterval 0
ClientAliveCountMax 3
PermitRootLogin yes
PubkeyAuthentication yes
PasswordAuthentication yes
KbdInteractiveAuthentication no
X11Forwarding yes
AllowTcpForwarding yes
```

SSH configuration was reloaded and verified during finalization.

---

## 5. Cockpit

### Service

```text
cockpit.socket
```

**Status:** Active
**Enabled:** Yes

### Web Interface

```text
Port 9090
```

Cockpit is part of the Core Server management layer.

---

## 6. Docker

### Docker Engine

```text
Docker Engine: 29.6.2
Storage Driver: overlayfs
Logging Driver: json-file
Cgroup Driver: systemd
Cgroup Version: 2
Docker Root: /var/lib/docker
```

### Docker Service

```text
docker.service
docker.socket
containerd.service
```

Docker is enabled as part of the server core stack.

---

## 7. Docker Containers

The following containers were present during the Core Server v1.0 audit:

| Container     | Image                           | Status            |
| ------------- | ------------------------------- | ----------------- |
| `web-server`  | `nginx:alpine`                  | Running           |
| `jellyfin-tv` | `jellyfin/jellyfin:latest`      | Exited            |
| `homer`       | `b4bz/homer:latest`             | Running / Healthy |
| `jellyfin`    | `jellyfin/jellyfin:latest`      | Running / Healthy |
| `adguardhome` | `adguard/adguardhome:latest`    | Running           |
| `portainer`   | `portainer/portainer-ce:2.19.5` | Running           |

### Published Ports

```text
web-server
8083 -> 80/tcp

homer
8080 -> 8080/tcp

portainer
9000 -> 9000/tcp
9443 -> 9443/tcp
```

Container workloads are considered **above the Core Server layer** and may be modified independently without redefining the Core Server baseline.

---

## 8. Docker Configuration

Docker does not use a conventional:

```text
/etc/docker/
```

configuration directory on this installation.

Docker configuration was therefore captured through:

* Docker daemon information
* Docker systemd unit
* Docker repository configuration
* Docker networking configuration
* Firewalld Docker policies
* Container state
* Images
* Networks
* Volumes

The Docker root directory is:

```text
/var/lib/docker
```

---

## 9. Virtualization / KVM

### QEMU / KVM

Hardware virtualization was verified successfully.

```text
VMX: PASS
/dev/kvm: PASS
/dev/kvm accessible: PASS
/dev/vhost-net: PASS
/dev/net/tun: PASS
```

Required cgroup controllers were also detected successfully.

### IOMMU

```text
WARN
```

No ACPI DMAR table was detected.

This is recorded as a hardware/platform limitation and does not invalidate basic KVM virtualization capability.

### Secure Guest Support

```text
WARN
```

No SEV, SEV-ES, SEV-SNP, or TDX support was detected.

This does not invalidate the Core Server baseline.

---

## 10. Libvirt

Libvirt and QEMU/KVM packages are installed and captured as part of the virtualization layer.

### Installed Virtualization Stack

* libvirt
* libvirt-client
* libvirt-daemon
* libvirt-daemon-kvm
* libvirt-daemon-driver-qemu
* QEMU/KVM
* Cockpit Machines

### Virtual Machine

The Core configuration capture identified:

```text
Fyde_OS
```

as the configured libvirt virtual machine.

### Storage Pools

Captured libvirt storage configuration includes:

```text
images
ntfs-pool
```

Libvirt configuration was captured with elevated permissions to preserve otherwise unreadable configuration files.

---

## 11. SELinux

### Status

```text
enabled
```

### Policy

```text
targeted
```

### Current Mode

```text
permissive
```

### Configuration Mode

```text
permissive
```

SELinux is therefore enabled but intentionally operating in permissive mode in Core Server v1.0.

This state is documented as part of the baseline and is not changed during the freeze period.

---

## 12. Systemd

### Failed Units

```text
0 loaded units listed.
```

No failed systemd units were detected during the final audit.

### Important Enabled Services

```text
chronyd.service
cockpit.socket
containerd.service
docker.service
docker.socket
firewalld.service
fstrim.timer
irqbalance.service
libvirtd.service
NetworkManager.service
NetworkManager-wait-online.service
smartd.service
sshd.service
thermald.service
tuned.service
tuned-ppd.service
virtqemud.service
```

The server boots into:

```text
multi-user.target
```

---

## 13. Time Configuration

```text
Timezone: Asia/Jakarta
NTP: Active
System Clock: Synchronized
```

### RTC

The system currently uses:

```text
RTC in local TZ: yes
```

This produces a system warning.

The recommended future configuration is:

```bash
timedatectl set-local-rtc 0
```

However, this change is intentionally deferred from the frozen Core Server v1.0 baseline.

---

## 14. Kernel

Current running kernel:

```text
7.1.7-200.fc44.x86_64
```

Additional installed kernels were retained as part of the Fedora package state.

---

## 15. Core Management Stack

The Core Server v1.0 management stack includes:

* NetworkManager
* Firewalld
* OpenSSH
* Cockpit
* Docker Engine
* QEMU/KVM
* Libvirt
* SELinux
* systemd
* smartmontools
* thermald
* tuned

---

## 16. Configuration Backup

The authoritative Core Server configuration capture is stored locally at:

```text
/data/core-master/fedora-t540p
```

The captured configuration contains:

```text
system/
network/
firewall/
ssh/
docker/
virtualization/
storage/
packages/
boot/
```

The master capture includes configuration snapshots, service states, package inventories, networking information, firewall state, Docker state, virtualization configuration, storage information, and system information.

The master capture was repaired and revalidated using elevated permissions for protected Libvirt configuration.

---

## 17. Core Configuration Principle

The Core Server follows a layered architecture.

### Core Layer

The following components form the stable Core Server baseline:

* Operating system
* Kernel
* Network configuration
* Firewall
* SSH
* Cockpit
* Docker engine
* Virtualization stack
* Storage configuration
* systemd services
* Security configuration
* Hardware/platform configuration

### Workload Layer

Workloads above the core may be changed independently, including:

* Docker containers
* Docker Compose applications
* Virtual machines
* Media services
* Web applications
* Network services
* Experimental workloads

Changes to the workload layer should not require modification of the frozen Core Server baseline unless the Core itself is intentionally revised.

---

## 18. Core Server v1.0 Freeze

The Fedora T540p Core Server configuration was audited and captured as a stable baseline.

### Final Status

```text
CORE SERVER: T540p Fedora Server
CORE VERSION: v1.0
AUDIT STATUS: PASS
CONFIGURATION STATUS: COMPLETE
MASTER CAPTURE: COMPLETE
FAILED SYSTEMD UNITS: 0
NETWORK: OPERATIONAL
FIREWALL: OPERATIONAL
SSH: OPERATIONAL
COCKPIT: OPERATIONAL
DOCKER: OPERATIONAL
KVM: OPERATIONAL
```

### Freeze Policy

The Core Server configuration is considered **FROZEN** after the v1.0 release.

No further Core configuration changes are required for the v1.0 baseline.

Future modifications should be released as a new Core Server revision.

Examples:

```text
v1.1
v1.2
v2.0
```

rather than silently modifying the v1.0 baseline.

---

## 19. Future Deferred Changes

The following items are intentionally outside the Core Server v1.0 freeze:

* Permanent static IP assignment
* Login/banner customization
* Web console banner/IP information updates
* Additional workload deployment
* GitHub synchronization from the server
* Further service/application configuration
* Security hardening beyond the current baseline
* RTC conversion from local time to UTC

These changes belong to future revisions or workload-layer development.

---

## 20. Final Declaration

The Lenovo ThinkPad T540p Fedora Server Core configuration has completed its audit, repair, verification, and master configuration capture process.

**The Fedora T540p Core Server v1.0 baseline is hereby declared COMPLETE and FROZEN.**

Further development is intended to occur **above the Core Server layer**, without unnecessarily modifying the established v1.0 baseline.

---

**Project:** Home Server Core
**Server:** Lenovo ThinkPad T540p
**Core:** Fedora Server
**Release:** v1.0
**Status:** COMPLETE / FROZEN
