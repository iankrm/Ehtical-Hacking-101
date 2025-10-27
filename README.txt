# Ethical Hacking Lab Setup Checklist
**Use this checklist to build a safe, snapshot-friendly lab for learning ethical hacking.**
**Warning/Legal:** Only test systems you own or have explicit permission to test. Do not connect lab VMs to production networks.

---

## 1) Host requirements
- Host OS: Windows / macOS / Linux (pick one)
- CPU: virtualization support (VT-x / AMD-V) **enabled in BIOS/UEFI**
- RAM: **8 GB minimum** (16 GB recommended)
- Disk: **≥ 50 GB free** (20 GB+ for each VM)
- Backup: create a host backup before installing many VMs

---

## 2) Software to install on host
- Virtual machine manager:
  - Recommended free: **VirtualBox** (https://www.virtualbox.org)
  - Alternative: **VMware Workstation Player** (free for non-commercial)
- Kali Linux ISO: download latest from https://www.kali.org/get-kali
- Optional: VirtualBox Extension Pack (for USB passthrough if needed)
- Optional: Host snapshot tool (e.g., Windows Restore Point, Time Machine on macOS)

---

## 3) Create a base Kali VM (recommended settings)
1. Open VirtualBox → New
2. Name: `kali-linux`
   - Type: Linux
   - Version: Debian (64-bit) or Other Linux (64-bit)
3. RAM: 2048 MB (min) / 4096+ recommended
4. CPUs: 1–2 (2+ recommended if host has cores)
5. Disk: VDI, dynamically allocated, 20–40 GB
6. Storage → Attach the Kali ISO to the optical drive
7. System → Boot Order: disable Floppy, keep Optical and HDD
8. Display → Video Memory: 64–128 MB
9. Network: leave Adapter 1 as NAT (or disable for full isolation)
10. Start VM and install Kali from ISO

---

## 4) Network setup & isolation (critical)
- **Internal Network (Recommended):**
  - Create an internal-only network (VirtualBox name: `labnet`) and attach it to VMs that should communicate with each other.
  - This network does NOT provide internet unless you create a gateway/NAT VM.
- **NAT (careful):**
  - Use NAT only if you need limited internet access from the VM; know that NAT can expose traffic to the host's network stack.
- **Never use Bridged mode** for vulnerable lab VMs (bridged connects VMs directly to your LAN).
- **Host-only** is another option for host↔VM comms without exposing to LAN.
- Confirm isolation: from a VM with internal-only adapters, `ping 8.8.8.8` should fail unless you explicitly enable internet.

---

## 5) Snapshots & backups
- Before any exercise, take a snapshot named `clean-install-YYYYMMDD`.
  - VirtualBox: Snapshots → Take Snapshot...
  - VMware: Snapshot → Take Snapshot...
- After major config changes, take another snapshot.
- If you need longer-term safety, export VMs as OVA/OVF backups.

---

## 6) Vulnerable VM & CTF sources (safe to use)
- TryHackMe (use lab mode or your own VM instances)
- HackTheBox (use retired/starting machines in lab environment)
- VulnHub (download intentionally vulnerable VM images)
- Metasploitable (for offline practice only)

---

## 7) Safe testing best practices
- Use **unique** credentials in lab — do not reuse work/personal passwords.
- Keep lab VMs on an internal-only network when practicing attacks.
- Avoid copying sensitive files into lab VMs.
- Log all actions and use snapshots to revert.
- If you discover a real vulnerability in a third-party product, follow **responsible disclosure** practices (report to vendor, avoid public exploit publication).

---

## 8) Quick verification commands (harmless)
- On Kali VM:
  - `ip a` — show interfaces and IPs
  - `ping <other-vm-ip>` — test internal VM communication
  - `ping 8.8.8.8` — should fail if fully isolated
- On host: confirm VirtualBox network adapters exist (VirtualBox Host-Only Network)

---

## 9) Handy tips & notes
- If installation fails, ensure VT-x/AMD-V is enabled in BIOS.
- If using Windows 10/11, disable Hyper-V if VirtualBox has trouble (or use Hyper-V compatible VMs).
- Keep a README in your lab GitHub repo with snapshots, versions, and step logs.
- Consider using a disposable VM for internet-facing tasks and keep it separate.

---

## 10) Resources & links to save in your video description
- VirtualBox: https://www.virtualbox.org
- VMware Player: https://www.vmware.com/products/workstation-player.html
- Kali Linux: https://www.kali.org/get-kali
- TryHackMe: https://tryhackme.com
- HackTheBox: https://www.hackthebox.com
- VulnHub: https://www.vulnhub.com

---

**End of checklist.**
