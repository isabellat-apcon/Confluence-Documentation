# First-Time Setup: ThreatGuard on WSL

Windows alternative to the VirtualBox Alma VM guide. Run Malcolm / ThreatGuard in **AlmaLinux 9 (WSL 2)** with **Docker Desktop**.

The product UI is **`https://127.0.0.1`** (accept the cert). That is not Angular `ng serve` in VS Code (`localhost:4200`) — that is frontend-only development.

---

## What to download (workflow)

| When | Get | Why |
| --- | --- | --- |
| **First install** | Latest **`network-security.*.full.tar`** | Loads the full Malcolm image set. Required once on a new machine. |
| **Later upgrades** | **partial** (or RPM / `upgradeLatest.sh`) | Smaller; skips re-downloading images you already have when Malcolm’s version is unchanged. |

Full packages are heavy, so CI publishes a new **full** only about every **3rd** build (or on a manual run). Always start from the newest **full**, then move to the latest **partial** if you need to catch up.

Get artifacts from the team’s current **GitHub Actions / object-storage browse page** (replacing Jenkins). Prefer the `latest` full pointer for a first install.

---

## Prerequisites

1. Docker Desktop for Windows — leave it **running**.
2. AlmaLinux 9 from the Microsoft Store.
3. ~16 GB+ RAM recommended; tens of GB free disk for images.
4. On the corp network: install APCON TLS CAs in WSL if `dnf`/`curl` fail with self-signed cert errors (`GoWebServer/cert_*.crt` → `/etc/pki/ca-trust/source/anchors/`, then `sudo update-ca-trust extract`).

From **cmd** / PowerShell:

```bat
wsl -l -v
wsl --set-default AlmaLinux-9
wsl --set-default-version 2
```

To wipe and restart: `wsl --unregister AlmaLinux-9`, then reinstall from the Store.

---

## Install

1. Open Docker Desktop, then open the AlmaLinux-9 terminal. Create user **`apcon`** (admin) with the lab password from internal docs when prompted.

2. Copy the **full** tarball into Linux (not only `/mnt/c`) and extract:

```bash
mkdir -p /malcolm && cd /malcolm
cp /mnt/c/Users/<you>/Downloads/network-security.*.full.tar .
tar -xvf network-security.*.full.tar
```

3. Edit **`setupAlma9.sh`** for WSL:
   - Comment out the two **`firewall-cmd`** lines.
   - Comment out the final **`reboot`**.
   - If the script dies right after `NEW_DISKS=`, change that line to end with `|| true` (WSL has no NVMe disks).

4. Run setup, then install (both take a while):

```bash
sudo ./setupAlma9.sh
sudo ./apcon_install.sh
```

Optional (PCAP paths): `sudo ./setup_vm_capture.sh` if you have that script (`util/setup_vm_capture.sh` in this repo).

5. Start and check:

```bash
sudo /opt/apcon/sbin/start.sh
/opt/apcon/malcolm/scripts/status
```

6. Browser: **`https://127.0.0.1`** → accept cert → log in. Classic Malcolm page: `/malcolm.html`.

---

## Day-to-day

| Script | Use |
| --- | --- |
| `/opt/apcon/sbin/start.sh` | Start |
| `/opt/apcon/sbin/die.sh` | Stop |
| `/opt/apcon/sbin/upgradeLatest.sh` | Upgrade (picks partial vs full when it can) |
| `/opt/apcon/sbin/rollback.sh` | Previous install |

Keep **one** Docker engine in play (Docker Desktop per the original WSL notes). If ports `443`/`9200` are busy after a failed start, stop with `die.sh`, free orphaned proxies if needed, then `start.sh` again.

---

## Checklist

- [ ] Docker Desktop running; AlmaLinux-9 = WSL 2 default  
- [ ] CAs trusted (if SSL errors)  
- [ ] **Full** tar under `/malcolm`, extracted  
- [ ] `setupAlma9.sh` patched; `setupAlma9.sh` → `apcon_install.sh`  
- [ ] `start.sh`; UI at `https://127.0.0.1`  

Packaging cadence detail: [RFC-0005](rfcs/0005-build-artifact-object-storage.md).
