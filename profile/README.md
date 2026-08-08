# IT-Kuny

Infrastructure, automation, and self-hosting with a strong bias towards privacy, control, and Linux-first solutions.

- 🇨🇭 Located in Switzerland
- Focus: AI Agent agnostic private (like-a-ISP & NOC) data center infrastructure, Proxmox, kernel hardening, hardware-aware tooling and more
- Philosophy: sustainable, vendor-independent IT with re-use of existing hardware where it makes sense
- Security: defense-in-depth, CVE tracking, SIEM, kernel-level mitigation — because "it works" isn't good enough

**Website:** https://it-kuny.ch
**Self-hosted Git:** https://git.it-kuny.ch *(currently not exposed to the public)*

---

## About IT-Kuny

IT-Kuny is primarily a one-person operation in cooperation with self trained AI agent called Jarvis.

The work sits somewhere between previously homelab, nowadays private data center engineering and NOC/ISP,  (and maybe further...) and real-world support:

- Fixing everyday issues for friends, family, and close contacts (smartphones, PCs, tablets, NAS, Gaming consoles, TVs, TV Box's, Router/Modem, Security cameras etc.)
- Acting as a consultant and "second brain" for new systems, network redesigns, and infrastructure overhauls
- Building tools and workflows when existing solutions are too heavy, opaque, or vendor-locked

Most tooling here started as _"we have a real problem to solve right now"_ and was later cleaned up and published.

---

## What you'll find here

This organization collects tools and configurations that help you:

- Run self-hosted infrastructure (Proxmox, Linux, containers)
- Automate repetitive operational tasks
- Harden systems and reduce attack surface
- Make hardware behaviour more predictable (IOMMU, iLO fans, kernel profiles)
- Recover broken systems quickly (chroot, storage detection, bootfix)

Most of the daily-driver projects live on a self-hosted Forgejo instance on a private distributed server farm.
GitHub is used for public tooling, kernels, and upstream collaboration (and sometimes for experiments that are useful to others).

---

## Key repositories

### Core tooling

| Repository | Description |
| ---------- | ----------- |
| [`chrooty`](https://github.com/IT-Kuny/chrooty) | Rescue and chroot utility that automates recovery workflows. Handles LVM, ZFS, Btrfs subvolumes, EFI mounts, logging, and a plugin-driven hook system for pre/post-chroot actions. Designed for "fix this system now" scenarios on modern Linux distributions. |
| [`Proxmox-Sync-Wildcard`](https://github.com/IT-Kuny/Proxmox-Sync-Wildcard) | Bash automation to securely pull a wildcard TLS certificate from a remote CA / reverse proxy host and deploy it into a Proxmox VE cluster. Includes full store backup, atomic replacement, permission fixes, and minimal service impact (reloads only `pveproxy`). |
| [`dnf-pkgsync`](https://github.com/IT-Kuny/dnf-pkgsync) | Helper script to export and restore package sets between DNF-based systems (migration/bootstrap use-cases). |

These projects are designed to be dropped into real environments: rescue media, Proxmox clusters, and automation pipelines.

---

### Infrastructure & Automation

| Repository | Description |
| ---------- | ----------- |
| [`PDC-stack`](https://github.com/IT-Kuny/PDC-stack) | Self-hosted DevOps monorepo for private data center operations. Bundles 9 services (n8n, Grafana + InfluxDB, Zabbix, Wazuh, nginx ECH, UPS Dashboard, WGDashboard, Falco, Akvorado + ClickHouse) with shared networks, volumes, and documentation. Designed for Proxmox/Debian hosts with ZFS storage. |
| [`ThinClient-For-Proxmox`](https://github.com/IT-Kuny/ThinClient-For-Proxmox) | Thin client orchestration for Proxmox VE environments. Multi-user capable with OOBE, boot-wait phases, SPICE connect, and PAM-based SSO via the companion `pam_proxmox` module. Currently in active development. *(private)* |
| [`AISec`](https://github.com/IT-Kuny/AISec) | AI-powered network guardian for firewalls — detects known threats, anomalous behaviour, and blocks attackers automatically. Four-layer defense: signature matching, ML anomaly detection, pattern recognition, automatic response. *In active development, source code not yet published.* |

These projects target real virtualization environments — from single-host Proxmox to multi-node clusters with monitoring, SIEM, and automation pipelines.

> **Collaboration note:** The community network backbone (LIXP fleet — FreeBSD/FRR routing, VyOS/IPSec) is designed and operated by a community partner. IT-Kuny hosts its own WireGuard overlay on top of it and the monitoring/NOC stack (Akvorado, Grafana, Zabbix) that runs on top. The fleet itself is not an IT-Kuny product.

---

### Hardware- and platform-specific work

| Repository | Scope | Focus |
|-----------|-------|-------|
| [`Thinkpad-P16S-Kernel`](https://github.com/IT-Kuny/Thinkpad-P16S-Kernel) | Opinionated Linux kernel profile for the Lenovo ThinkPad P16s Gen4. Keeps NVMe-only internal storage, USB BOT/UAS disks, USB4/TB4, graphics, audio, camera, LAN, WLAN, BT, and trims unused SATA/SAS/FC/iSCSI paths to reduce complexity and attack surface. | Hardware-specific kernel config, IOMMU, VFIO, modern workstation hardening. |
| [`HPE-G8-G9-Fan-Controller`](https://github.com/IT-Kuny/HPE-G8-G9-Fan-Controller) | Fan controller stack for modded iLO4 servers on HPE Gen8/Gen9 platforms. | Practical fan control UI/service for homelab ProLiant systems. |
| [`HPE-Proliant-G8-G9-Autofan-Controller`](https://github.com/IT-Kuny/HPE-Proliant-G8-G9-Autofan-Controller) | Standalone thermal controller for HPE ProLiant Gen8/Gen9 with per-sensor curves and adaptive cooling logic. | Autonomous thermal management for quiet but safe operation. |
| [`UGREEN-DXP-FAN-NAS-Driver`](https://github.com/IT-Kuny/UGREEN-DXP-FAN-NAS-Driver) | Kernel driver for the system fan controller on UGREEN DXP NAS devices. Enables proper fan speed management under Linux where no official driver exists. | Hardware driver, NAS platform support, Linux kernel integration. |

This is not a generic "one size fits all" kernel - it is a documented profile for a very specific platform and threat model.

---

### Upstream collaboration & forks

| Repository | Origin | Purpose |
|-----------|--------|---------|
| [`IOMMU-Report`](https://github.com/IT-Kuny/IOMMU-Report) | Fork of `mkoreneff/iommu_info_generate` | Curses-based TUI to inspect local platform details and submit IOMMU topology data to [iommu.info](https://iommu.info). Includes API health checks, vendor probes, board existence checks, chunked upload flow, and throttling that respects `Retry-After`. |
| [`HPE-G8-G9-Fan-Controller`](https://github.com/IT-Kuny/HPE-G8-G9-Fan-Controller) | Fork/continuation in the iLO4 fan-control ecosystem | Next.js UI and Dockerized service to control fan speeds on modded iLO4-based HPE Gen8/Gen9 servers. Talks to iLO4 over SSH, exposes presets and dynamic fan layouts, and is homelab-friendly when paired with an auth proxy. |
| [`pvekclean`](https://github.com/IT-Kuny/pvekclean) | Fork of `jordanhillis/pvekclean` | Proxmox VE kernel cleanup tool. Consolidates community PRs and fixes 6 open upstream issues: ZFS `/boot` support, UEFI/systemd-boot detection, complete header removal, metapackage filtering, and stale dpkg state after purge. Added semantic version comparison for update checks (PR #2). v2.1.0. |

These forks are kept close to upstream while adding homelab-centric operational experience.

---



## Communities

- **Nosial (n64.cc)** — Member, infrastructure contributor
- **Neternels** — Contributor to custom kernel builds for Kali NetHunter
- **Private Security Research Group** — knowledge sharing with industry practitioners, including Kali NetHunter Core Team members

---

## Scope & support model

IT-Kuny is not a large service provider. It is mainly:

- Best-effort support for friends, family, and close contacts and for those who want to get in touch with
- Help for small environments that share the same philosophy (primarly focused on privacy-focused, realistic budgets) and other environment obviously too

Typical support activities include:

- **End-user systems & apps**
  Fixing issues with Apps (e.g. Google Play, Samsung Browser, iOS App sideloading via XCode, Wireguard), mail clients, office suites, and everyday desktop workflows on Windows, macOS, and Linux. And also for iOS/iPadOS and Android/HarmonyOS.

- **Client devices**
  Troubleshooting and setting up smartphones and tablets (Android, iOS/iPadOS), including accounts, apps, backups, and security and privacy.

- **Storage & NAS systems**
  Deploying and maintaining NAS devices (e.g. Synology, UGREEN and similar), ACL permissions, shared folders, remote access, and backup strategies.

- **Networks & small infra**
  Designing or restructuring small networks (home and small office), including Wi-Fi, routing, VPN, DNS, remote access, and pragmatic security baselines.

- **Consulting & planning**
  Acting as a sounding board for new systems, hardware refreshes, or complete infrastructure overhauls - from "_What should I buy?_" to "_How do we migrate without losing data and while being live?_".

Language-wise:

- 🇨🇭 Swissgerman - native
- 🇩🇪 German - native
- 🇬🇧 English - fluent

There is **no 24/7 SLA** and **no marketing team**. **Expect** _honest answers_, _conservative designs_, and solutions **you** can actually maintain yourself.

---

## Technology focus

Typical stack and domains represented across these projects:

- **Operating systems:** Linux (Fedora, Debian, Proxmox), with a focus on server and workstation use-cases
- **Infrastructure:** Proxmox VE, containers, homelab automation, backup and recovery workflows
- **Security & hardening:** Kernel configuration, IOMMU/VFIO, TLS automation, reduced attack surface
- **Scripting & tooling:** Bash, Python, TypeScript/Next.js, plus packaging for Debian/RPM where useful
- **Hardware:** ThinkPad platforms, HPE ProLiant Gen8, **3× Synology NAS, 1× UGREEN NAS**, IOMMU-capable boards and virtualization hosts

If you care about owning your infrastructure, keeping control over your data, and understanding what your hardware is actually doing, you are in the right place.

---

## Contributions & upstream work

### Merged upstream contributions

| Project | Stars | Contribution |
|---------|-------|-------------|
| [`Lissy93/dashy`](https://github.com/Lissy93/dashy) | ⭐ 26k+ | Synology NAS deployment guide ([PR #567](https://github.com/Lissy93/dashy/pull/567)) |
| [`louislam/uptime-kuma`](https://github.com/louislam/uptime-kuma) | ⭐ 90k+ | Swiss German (de-CH) translation via Weblate |
| [`Core-2-Extreme/Video_player_for_3DS`](https://github.com/Core-2-Extreme/Video_player_for_3DS) | — | German language support ([PR #85](https://github.com/Core-2-Extreme/Video_player_for_3DS/pull/85)) |
| [`kaisenlinux/kaisen-menu`](https://github.com/kaisenlinux/kaisen-menu) | — | German language string updates |

### Open upstream contributions

| Project | Contribution |
|---------|-------------|
| [`jordanhillis/pvekclean`](https://github.com/jordanhillis/pvekclean) | [PR #23](https://github.com/jordanhillis/pvekclean/pull/23) — ZFS boot support, systemd-boot detection, header cleanup, metapackage filter (fixes 6 open issues) |

### Compliance & security reports

| Project | Contribution |
|---------|-------------|
| [`swiss/trustbroker.swiss`](https://github.com/swiss/trustbroker.swiss) | [Issue #1](https://github.com/swiss/trustbroker.swiss/issues/1) — AGPL licensing report: missing project license header adaptation |

### Original projects (AI-Assisted, Owner-Approved)

| Project | Description |
|---------|-------------|
| [`0n1cOn3/LinuxDOOM`](https://github.com/0n1cOn3/LinuxDOOM) | DOOM port for Linux using OSS audio — vibeported under Hx guidance |
| [`0n1cOn3/mumble-iphoneos-swift`](https://github.com/0n1cOn3/mumble-iphoneos-swift) | Swift-based Mumble client for iOS — vibeported from upstream |
| [`IT-Kuny/HPE-G8-G9-Fan-Controller`](https://github.com/IT-Kuny/HPE-G8-G9-Fan-Controller) | Next.js UI + Dockerized fan control for HPE Gen8/Gen9 with modded iLO4 — vibeforked and enhanced |
| [`IT-Kuny/HPE-Proliant-G8-G9-Autofan-Controller`](https://github.com/IT-Kuny/HPE-Proliant-G8-G9-Autofan-Controller) | Standalone thermal controller with per-sensor curves and adaptive cooling — vibeforked and enhanced |

---

## Personal GitHub

**[@0n1cOn3](https://github.com/0n1cOn3)** — Security tools, spyware IOC blocklists (NSO/Intellexa/Paragon/Candiru — AI-Assisted Research), and more.

Additional internal tools, Ansible roles, and more live on the self-hosted Git:

- 🔗 **Forgejo:** https://git.it-kuny.ch *(currently internal-only; public exposure under evaluation)*

Issues and pull requests are welcome on the public repositories here on GitHub.
For anything security-sensitive, please use a private contact channel instead of opening a public issue.

---

## Tools, platforms & ecosystem

Tools and technologies I work with - some daily, some project-based:

<br clear="both">
<div align="center">
  <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/fedora/fedora-original.svg" height="30" alt="fedora logo"  />
  <img width="12" />
  <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/centos/centos-original.svg" height="30" alt="centos logo"  />
  <img width="12" />
  <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/debian/debian-original.svg" height="30" alt="debian logo"  />
  <img width="12" />
  <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/ubuntu/ubuntu-plain.svg" height="30" alt="ubuntu logo"  />
  <img width="12" />
  <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/docker/docker-original.svg" height="30" alt="docker logo"  />
  <img width="12" />
  <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/github/github-original-wordmark.svg" height="30" alt="github logo"  />
  <img width="12" />
  <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/gitlab/gitlab-plain-wordmark.svg" height="30" alt="gitlab logo"  />
  <img width="12" />
  <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/markdown/markdown-original.svg" height="30" alt="markdown logo"  />
  <img width="12" />
  <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/podman/podman-original-wordmark.svg" height="30" alt="podman logo"  />
  <img width="12" />
  <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/nginx/nginx-original.svg" height="30" alt="nginx logo"  />
  <img width="12" />
  <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/filezilla/filezilla-plain.svg" height="30" alt="filezilla logo"  />
</div>

###

<br clear="both">

<div align="center">
  <img src="https://skillicons.dev/icons?i=cloudflare" height="30" alt="cloudflare logo"  />
  <img width="12" />
  <img src="https://skillicons.dev/icons?i=bash" height="30" alt="bash logo"  />
  <img width="12" />
  <img src="https://skillicons.dev/icons?i=git" height="30" alt="git logo"  />
  <img width="12" />
  <img src="https://skillicons.dev/icons?i=powershell" height="30" alt="powershell logo"  />
  <img width="12" />
  <img src="https://skillicons.dev/icons?i=py" height="30" alt="python logo"  />
  <img width="12" />
  <img src="https://skillicons.dev/icons?i=cmake" height="30" alt="cmake logo"  />
  <img width="12" />
  <img src="https://skillicons.dev/icons?i=cpp" height="30" alt="cplusplus logo"  />
  <img width="12" />
  <img src="https://skillicons.dev/icons?i=ruby" height="30" alt="ruby logo"  />
  <img width="12" />
  <img src="https://skillicons.dev/icons?i=rust" height="30" alt="rust logo"  />
  <img width="12" />
  <img src="https://skillicons.dev/icons?i=swift" height="30" alt="swift logo"  />
  <img width="12" />
  <img src="https://skillicons.dev/icons?i=perl" height="30" alt="perl logo"  />
  <img width="12" />
  <img src="https://skillicons.dev/icons?i=gradle" height="30" alt="gradle logo"  />
  <img width="12" />
  <img src="https://skillicons.dev/icons?i=java" height="30" alt="java logo"  />
  <img width="12" />
  <img src="https://skillicons.dev/icons?i=mysql" height="30" alt="mysql logo"  />
  <img width="12" />
  <img src="https://skillicons.dev/icons?i=postgres" height="30" alt="postgresql logo"  />
  <img width="12" />
  <img src="https://skillicons.dev/icons?i=html" height="30" alt="html5 logo"  />
  <img width="12" />
  <img src="https://skillicons.dev/icons?i=css" height="30" alt="css logo"  />
  <img width="12" />
  <img src="https://skillicons.dev/icons?i=js" height="30" alt="javascript logo"  />
  <img width="12" />
  <img src="https://skillicons.dev/icons?i=php" height="30" alt="php logo"  />
  <img width="12" />
  <img src="https://skillicons.dev/icons?i=electron" height="30" alt="electron logo"  />
  <img width="12" />
  <img src="https://skillicons.dev/icons?i=redis" height="30" alt="redis logo"  />
  <img width="12" />
  <img src="https://skillicons.dev/icons?i=nodejs" height="30" alt="nodejs logo"  />
  <img width="12" />
  <img src="https://skillicons.dev/icons?i=ansible" height="30" alt="ansible logo"  />
  <img width="12" />
  <img src="https://skillicons.dev/icons?i=vscode" height="30" alt="vscode logo"  />
  <img width="12" />
  <img src="https://skillicons.dev/icons?i=wordpress" height="30" alt="wordpress logo"  />

---

</div>

###

<div align="center">
  <img src="https://img.shields.io/badge/Linux-FCC624?logo=linux&logoColor=black&style=for-the-badge" height="40" alt="linux logo"  />
  <img width="12" />
  <img src="https://img.shields.io/badge/Windows-0078D6?logo=windows&logoColor=white&style=for-the-badge" height="40" alt="windows logo"  />
  <img width="12" />
  <img src="https://img.shields.io/badge/Apple-000000?logo=apple&logoColor=white&style=for-the-badge" height="40" alt="apple logo"  />
  <img width="12" />
  <img src="https://img.shields.io/badge/Android-3DDC84?logo=android&logoColor=black&style=for-the-badge" height="40" alt="android logo"  />
</div>

---

## Contact

🌐 Website:

https://it-kuny.ch

💬 Telegram:
<br clear="both">
<div align="left">
  <a href="https://t.me/h_2_o0" target="_blank">
    <img src="https://img.shields.io/static/v1?message=Telegram&logo=telegram&label=&color=2CA5E0&logoColor=white&labelColor=&style=for-the-badge" height="35" alt="telegram logo"  />
  </a>
</div>

---

For project-specific bugs or feature requests, please use the respective GitHub issue tracker.
