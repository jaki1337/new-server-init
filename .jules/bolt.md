## 2026-02-21 - [Spinner Efficiency]
**Learning:** Using `ps | awk | grep` in a tight loop to monitor a process in a shell script is extremely inefficient, spawning multiple processes every few milliseconds. This can consume significant CPU resources (up to 10% of a core on small VPS) just for the UI.
**Action:** Use `kill -0 $PID` to check for process existence instead, which is a much cheaper operation (often a shell builtin).

## 2026-02-21 - [Shallow Deployment]
**Learning:** Default `git clone` operations download the entire history of a repository, which is unnecessary for automated server deployments and increases bandwidth/time consumption.
**Action:** Always use `--depth 1` for deployment clones to minimize network and disk overhead.

## 2026-02-21 - [Dynamic Resource Allocation]
**Learning:** Hardcoding resource limits (like SWAP size) can lead to inefficiencies on small systems or under-utilization on large ones. Dynamic detection via `/proc/meminfo` allows for "per-system" optimization.
**Action:** Always use dynamic detection for hardware-dependent configurations to ensure optimal performance across varied environments.

## 2026-02-21 - [Script Portability]
**Learning:** `#!/usr/bin/env bash` is standard but can fail if `env` is not in its expected path or if the user invokes the script with `sh`. A robust re-exec block ensures the script always runs in its intended shell.
**Action:** Use a `#!/bin/sh` shebang with a Bash re-exec block for maximum portability of Bash scripts.

## 2026-02-21 - [Package Optimization]
**Learning:** Using `--no-install-recommends` with `apt install` significantly reduces the number of packages installed, saving both bandwidth and disk space, especially on server systems where GUI-related or optional dependencies are often pulled in by default.
**Action:** Always use `--no-install-recommends` for server provisioning scripts.

## 2026-02-21 - [Log Monitoring Efficiency]
**Learning:** On modern systemd-based Linux distributions (like Debian 12/13), the `systemd` backend for Fail2Ban is much more efficient than polling log files, as it uses the `sd-journal` API.
**Action:** Configure Fail2Ban to use `backend = systemd` on supported systems.
