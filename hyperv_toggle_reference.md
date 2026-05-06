# Hyper-V Toggle Reference

Switching between Docker Desktop (needs Hyper-V) and VirtualBox (wants Hyper-V off) on Windows 11.

Each switch requires a **full reboot**.

---

## Disable Hyper-V (for VirtualBox / Kali)

Open **PowerShell as Administrator**, then run:

```powershell
bcdedit /set hypervisorlaunchtype off

Disable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V-All -NoRestart
Disable-WindowsOptionalFeature -Online -FeatureName VirtualMachinePlatform -NoRestart
Disable-WindowsOptionalFeature -Online -FeatureName HypervisorPlatform -NoRestart
```

Some commands may report the feature isn't present — ignore.

**Reboot the machine.** Hyper-V doesn't fully unload until restart.

After reboot, Docker Desktop and WSL2 will not start until Hyper-V is re-enabled. That's expected.

---

## Re-enable Hyper-V (for Docker / WSL2)

Open **PowerShell as Administrator**, then run:

```powershell
bcdedit /set hypervisorlaunchtype auto

Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V-All -NoRestart
Enable-WindowsOptionalFeature -Online -FeatureName VirtualMachinePlatform -NoRestart
Enable-WindowsOptionalFeature -Online -FeatureName HypervisorPlatform -NoRestart
```

**Reboot the machine.**

After reboot, Docker Desktop and WSL2 will work normally. VirtualBox will still run but with degraded performance (NEM / "snail mode") until Hyper-V is disabled again.

---

## Verify current state

Open PowerShell (admin not required) and run:

```powershell
systeminfo | findstr /i "hyper-v"
```

**Hyper-V is OFF** when you see lines like:

```
Hyper-V Requirements: VM Monitor Mode Extensions: Yes
                      Virtualization Enabled In Firmware: Yes
                      Second Level Address Translation: Yes
                      Data Execution Prevention Available: Yes
```

**Hyper-V is ON** when you see:

```
Hyper-V Requirements: A hypervisor has been detected. Features required for Hyper-V will not be displayed.
```

If you disabled Hyper-V but still see "A hypervisor has been detected," a Windows feature didn't fully turn off — usually `VirtualMachinePlatform`. Re-run the disable commands and reboot again.

---

## Quick mental model

- `bcdedit /set hypervisorlaunchtype off` → tells Windows boot loader not to start the hypervisor
- The `Disable-WindowsOptionalFeature` commands → turn off the Windows components that would otherwise re-enable it
- Need both, and a reboot, for VirtualBox to get native VT-x access
- Reverse all three (set to `auto`, `Enable-WindowsOptionalFeature`, reboot) for Docker

---

## What breaks while Hyper-V is OFF

- Docker Desktop
- WSL2 (any Linux distro under `wsl`)
- Windows Sandbox
- Hyper-V Manager VMs (if any)
- Windows Defender Application Guard

Save your work in any of those before disabling.
