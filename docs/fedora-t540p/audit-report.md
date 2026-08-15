# Fedora T540p Core Server — Audit Report

**Project:** Home Server Core  
**Host:** Lenovo ThinkPad T540p  
**Operating System:** Fedora Linux Server  
**Core Role:** Primary Fedora Server Core  
**Audit Status:** COMPLETE  
**Configuration Status:** FROZEN  
**Release Target:** Core Server v1.0

---

## 1. Purpose

This document records the audit and validation process performed on the Lenovo ThinkPad T540p running Fedora Server.

The purpose of the audit was to verify that the server core layer was operational, internally consistent, documented, and ready to be frozen as the baseline configuration for Core Server v1.0.

The audit was performed as a read-only validation process wherever possible.

The objective was **not** to optimize or expand the server stack, but to establish a stable and reproducible core baseline before higher-layer services and projects are developed on top of it.

---

## 2. System Identity

Final validated system identity:

- Hostname: `t540p.fedora-server`
- Pretty hostname: `T540p - Fedora Server`
- Hardware: Lenovo ThinkPad T540p
- Architecture: x86-64
- Operating system: Fedora Linux 44 Server Edition
- Kernel: `7.1.7-200.fc44.x86_64`
- Boot target: `multi-user.target`
- Firmware: `GMET91WW (2.39)`
- Firmware date: 2021-06-03

The system successfully operates as a headless/server-oriented Fedora installation.

---

## 3. Network Audit

### Wireless Interface

Primary network interface:

- Interface: `wlp4s0`
- Type: Wi-Fi
- Connection: `Blues 1`
- SSID: `Blues`
- State: Connected

Final active IPv4 configuration observed during the audit:

- Address: `192.168.1.28/24`
- Gateway: `192.168.1.1`
- DNS:
  - `118.98.115.69`
  - `118.98.115.70`

The server successfully maintained network connectivity through Wi-Fi.

### Network Validation

Gateway connectivity:

- `192.168.1.1` — reachable
- Packet loss: 0%

Internet connectivity:

- `1.1.1.1` — reachable
- Packet loss: 0%

Hostname connectivity:

- `fedoraproject.org` — successfully resolved and reachable

### DNS Incident During Audit

The initial DNS diagnostic using `resolvectl` failed because `systemd-resolved` was not active/present as the DNS resolver service:

```text
Could not activate remote peer 'org.freedesktop.resolve1'
unknown unit
````

This did **not** indicate loss of network connectivity.

Direct IP connectivity remained operational, and hostname resolution through the active networking stack was subsequently verified successfully by resolving and pinging `fedoraproject.org`.

Therefore, the incident was classified as a diagnostic-method mismatch rather than a network failure.

---

## 4. Firewall Audit

Firewall service:

* `firewalld`: active
* Default zone: `FedoraServer`
* Network interface: `wlp4s0`

The active FedoraServer zone contains the required server services and ports.

Validated services include:

* Cockpit
* SSH
* HTTP
* HTTPS
* DHCPv6 client

Validated ports include:

* `22/tcp`
* `53/tcp`
* `53/udp`
* `80/tcp`
* `3000/tcp`
* `8080/tcp`
* `8081/tcp`
* `8096/tcp`
* `9090/tcp`
* `9443/tcp`

Docker maintains its own firewall zone and bridge interfaces.

Runtime and permanent firewall configurations were verified to be consistent for the audited ports.

Firewall status was therefore classified as **healthy**.

---

## 5. SSH Audit

SSH service:

* Service: `sshd`
* Status: active
* Enabled: yes
* Port: `22`

Effective configuration validated:

* `ListenAddress 0.0.0.0:22`
* `ListenAddress [::]:22`
* PAM authentication: enabled
* Public-key authentication: enabled
* Password authentication: enabled
* Root login: permitted
* X11 forwarding: enabled
* TCP forwarding: enabled

During the audit, a systemd notice indicated that the SSH unit configuration had changed on disk.

A systemd daemon reload was subsequently performed and SSH status was captured again.

The SSH service remained operational.

---

## 6. Cockpit Audit

Cockpit:

* Service/socket: active
* Enabled: yes
* Listening port: `9090`

Cockpit was successfully identified as the primary web-based administration interface for the Fedora server core.

---

## 7. Docker Audit

Docker Engine:

* Version: `29.6.2`
* Storage driver: `overlayfs`
* Logging driver: `json-file`
* Cgroup driver: `systemd`
* Cgroup version: `2`
* Docker root directory: `/var/lib/docker`

Docker service was active and operational.

### Containers observed during final audit

| Container     | Image                           | State             |
| ------------- | ------------------------------- | ----------------- |
| `web-server`  | `nginx:alpine`                  | Running           |
| `jellyfin-tv` | `jellyfin/jellyfin:latest`      | Exited            |
| `homer`       | `b4bz/homer:latest`             | Running / healthy |
| `jellyfin`    | `jellyfin/jellyfin:latest`      | Running / healthy |
| `adguardhome` | `adguard/adguardhome:latest`    | Running           |
| `portainer`   | `portainer/portainer-ce:2.19.5` | Running           |

The stopped `jellyfin-tv` container was recorded as an application-layer state and did not invalidate the core server configuration.

---

## 8. Docker Configuration Capture

The initial master configuration capture attempted to copy `/etc/docker`, but the directory was not present:

```text
cp: cannot stat '/etc/docker': No such file or directory
```

This was investigated rather than treated as a failure.

Docker configuration was subsequently captured through the actual active configuration and system locations.

Validated Docker-related locations included:

* `/var/lib/docker`
* Docker systemd service definitions
* Docker repository configuration
* Docker/firewalld integration files

The repaired master capture successfully recorded Docker configuration information.

---

## 9. Libvirt / KVM Audit

Virtualization support was validated successfully.

Hardware virtualization:

* VMX: PASS
* `/dev/kvm`: present
* `/dev/kvm`: accessible
* `/dev/vhost-net`: present
* `/dev/net/tun`: present
* Required cgroup controllers: PASS

IOMMU:

* Warning: no ACPI DMAR table detected

Secure guest support:

* Warning: SEV / SEV-ES / SEV-SNP / TDX unavailable

These warnings are hardware/platform capability limitations and do not invalidate normal CPU-based virtualization.

Libvirt and QEMU configuration were captured, including:

* libvirt configuration
* QEMU configuration
* network definitions
* storage pool definitions
* nwfilter definitions
* VM definitions

A virtual machine definition for `Fyde_OS` was present in the captured configuration.

---

## 10. Systemd Audit

Final failed-unit check:

```text
0 loaded units listed.
```

No failed systemd units were present during the final audit.

Important enabled services included:

* NetworkManager
* firewalld
* sshd
* docker
* cockpit
* chronyd
* smartd
* thermald
* tuned
* libvirt / virtualization services

Systemd state was therefore classified as **healthy**.

---

## 11. SELinux Audit

SELinux status:

* Enabled: yes
* Policy: targeted
* Current mode: permissive
* Configured mode: permissive

The permissive state was intentionally recorded as the final baseline configuration.

No SELinux failure was detected during the audit.

---

## 12. Storage and System State

Storage configuration was captured as part of the master configuration archive.

Captured information includes:

* `lsblk`
* `findmnt`
* `/etc/fstab`
* filesystem mount information

The master capture also includes system uptime and kernel information.

---

## 13. Time and Boot Configuration

Boot target:

```text
multi-user.target
```

Time zone:

```text
Asia/Jakarta (WIB, UTC+07:00)
```

System clock:

* synchronized: yes
* NTP service: active

The system reported that the RTC was configured to use local time.

This configuration was recorded as a known system warning and was not changed during the finalization process.

---

## 14. Kernel and Package Inventory

Final running kernel:

```text
7.1.7-200.fc44.x86_64
```

Package inventory was captured.

Total installed package count at the audit stage:

```text
1933
```

The inventory included the complete server stack, including:

* Cockpit
* Docker Engine
* Docker Compose
* firewalld
* NetworkManager
* OpenSSH
* libvirt
* QEMU/KVM
* SELinux policy
* smartmontools
* thermald
* tuned

---

## 15. Master Configuration Capture

The final master configuration was stored under:

```text
/data/core-master/fedora-t540p
```

The capture contains configuration and audit data covering:

* system identity
* network
* firewall
* SSH
* Docker
* Docker systemd integration
* libvirt/KVM
* storage
* systemd
* package repositories
* package inventory
* SELinux
* boot and time configuration
* kernel parameters
* installed services

The repaired master capture successfully resolved the initial permission and configuration-capture issues.

Final master capture size:

```text
868K
```

---

## 16. Master Capture Validation

The master directory was checked for unreadable files.

The final capture completed without unresolved unreadable-file errors.

The previously encountered libvirt permission issue was corrected by performing the required root-level capture.

The final validation confirmed that the expected configuration files were present in the master archive.

---

## 17. Final Health Check

Final health state:

| Component      | Result                  |
| -------------- | ----------------------- |
| NetworkManager | ACTIVE                  |
| Firewall       | ACTIVE                  |
| SSH            | ACTIVE                  |
| Docker         | ACTIVE                  |
| Cockpit        | ACTIVE                  |
| SELinux        | PERMISSIVE              |
| Failed units   | 0                       |
| Boot target    | multi-user.target       |
| Kernel         | `7.1.7-200.fc44.x86_64` |
| Hostname       | `t540p.fedora-server`   |

---

## 18. Audit Conclusion

The Fedora T540p core server successfully passed the final configuration audit.

All major core components required for the current server baseline were verified:

* operating system
* networking
* firewall
* SSH
* web administration
* Docker
* virtualization
* systemd
* SELinux
* storage
* kernel
* time synchronization
* package inventory
* configuration capture

Known warnings were documented rather than ignored:

* `systemd-resolved` diagnostic mismatch
* RTC configured in local time
* IOMMU unavailable
* secure guest virtualization unavailable
* SELinux permissive mode

None of these findings prevented the server from fulfilling its defined Core Server role.

---

## 19. Final Status

**AUDIT RESULT: PASS**

**CORE CONFIGURATION: COMPLETE**

**MASTER CONFIGURATION CAPTURE: COMPLETE**

**CORE SERVER STATUS: FROZEN**

**CORE SERVER v1.0 BASELINE: APPROVED**

The Fedora T540p core configuration is therefore declared **COMPLETE and FROZEN** for the Core Server v1.0 baseline.

Further development should occur above the established core layer and should not modify the frozen baseline unless a controlled future core revision is intentionally created.

---

## 20. Next Revision Policy

Future core modifications should be released as a new configuration revision.

Example:

```text
Core Server v1.0
    |
    |-- frozen baseline
    |
    +-- higher-layer development
    |
    +-- controlled core changes
             |
             v
        Core Server v1.1
```

A future revision may include changes such as:

* permanent server IP configuration
* updated console/banner information
* corrected web-console URLs
* updated master configuration capture

Such changes should be documented separately and must not silently overwrite the v1.0 baseline.

---

**Document status:** FINAL
**Host:** Lenovo ThinkPad T540p
**Core Role:** Fedora Server Core
**Baseline:** Core Server v1.0
**Audit:** PASSED
**Configuration:** FROZEN
