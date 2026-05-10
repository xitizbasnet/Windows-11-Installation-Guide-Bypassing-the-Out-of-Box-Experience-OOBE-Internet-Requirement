# Windows 11 Offline Installation Guide

## Bypassing OOBE Internet & TPM Requirements

> **Document Type:** IT Administration Manual
> **Platform:** Windows 11
> **Audience:** System Administrators, IT Support Technicians, Deployment Teams
> **Purpose:** Install Windows 11 without an internet connection and bypass TPM-related setup restrictions.

---

# 📖 Overview

During a standard Windows 11 installation, Microsoft requires:

* An active internet connection
* A Microsoft account
* TPM (Trusted Platform Module) compatibility checks

In environments such as:

* Offline deployments
* Virtual machines
* Test environments
* Legacy hardware
* Lab systems

these requirements may prevent installation from continuing.

This guide explains two supported workaround methods:

| Method                              | Purpose                                                   |
| ----------------------------------- | --------------------------------------------------------- |
| **LabConfig Registry Modification** | Bypass TPM requirement checks                             |
| **OOBE\BYPASSNRO Command**          | Bypass internet requirement and allow local account setup |

---

# ⚠️ Important Notes

> **Use Responsibly**
> These procedures should only be used in authorized IT environments and according to your organization’s deployment policies.

> **Compatibility Notice**
> Installing Windows 11 on unsupported hardware may limit future updates or support from Microsoft.

---

# 🧰 Prerequisites

Before starting, ensure the following requirements are met:

* Windows 11 bootable installation media (USB/DVD)
* Keyboard access during installation
* Basic familiarity with Windows Setup
* Backup of important data (recommended)

---

# 🚀 Installation Procedure

---

# Step 1 — Boot From Windows Installation Media

1. Insert the Windows 11 installation media.
2. Boot the computer from the USB/DVD.
3. Wait for the Windows Setup screen to load.

> ℹ️ If you are already on the **“Let’s connect you to a network”** screen, skip directly to **Step 6**.

---

# Step 2 — Configure Initial Setup

When the Windows Setup dialog appears:

1. Select your preferred:

   * Language
   * Time and currency format
   * Keyboard layout

2. Click **Next**.

3. Select **Install Now**.

---

# Step 3 — Product Key Activation

You will be prompted to enter a Windows product key.

## Available Options

### Option A — Enter a Product Key

Input your valid Windows 11 license key.

### Option B — Continue Without a Product Key

Click:

```text
I don't have a product key
```

> 💡 Systems previously activated with Windows 10 or Windows 11 may automatically reactivate using the digital license linked to the hardware.

---

# Step 4 — Select Windows Edition

If prompted:

1. Choose the Windows 11 edition to install.
2. Accept the Microsoft license terms.
3. Click **Next**.

Select the installation type:

```text
Custom: Install Windows only (Advanced)
```

---

# Step 5 — Select Installation Drive

1. Choose the target drive or partition.
2. Click **Next**.
3. Windows installation will begin.

The system will:

* Copy files
* Install features
* Restart automatically

After reboot:

1. Select your:

   * Region
   * Keyboard layout

---

# Step 6 — Open Command Prompt During OOBE

At the following screens:

```text
Let's connect you to a network
```

or

```text
This PC can’t run Windows 11
```

press the following keyboard shortcut:

```text
Shift + F10
```

This opens the Windows Command Prompt.

---

# 🛠️ Method 1 — TPM Bypass Using Registry Editor

This method bypasses TPM-related installation checks.

---

## Open Registry Editor

In Command Prompt, type:

```cmd
regedit
```

Press **Enter**.

---

## Navigate to Setup Registry Path

Go to:

```text
Computer\HKEY_LOCAL_MACHINE\SYSTEM\Setup
```

---

## Create the `LabConfig` Registry Key

1. Right-click the `Setup` folder.
2. Select:

```text
New → Key
```

3. Name the key:

```text
LabConfig
```

---

## Create TPM Bypass DWORD

Inside the `LabConfig` key:

1. Right-click in the right panel.
2. Select:

```text
New → DWORD (32-bit) Value
```

3. Name the value:

```text
ByPassTPMCheck
```

4. Set the value data to:

```text
1
```

5. Click **OK**.

---

## Exit Registry Editor

1. Close Registry Editor.
2. Return to Command Prompt.
3. Type:

```cmd
exit
```

4. Press **Enter**.

---

## Restart Installation

1. Close the Windows Setup screen.
2. Restart the Windows installation process.

> ✅ TPM compatibility checks should now be bypassed successfully.

---

# 🌐 Method 2 — Bypass Internet Requirement Using `OOBE\BYPASSNRO`

This method removes the mandatory internet connection requirement during setup.

---

## Launch Command Prompt

At the network requirement screen:

```text
Let's connect you to a network
```

press:

```text
Shift + F10
```

---

## Execute Bypass Command

In Command Prompt, enter:

```cmd
oobe\bypassnro
```

Press **Enter**.

---

## Automatic Restart

The system will:

* Restart automatically
* Reload the Out-of-Box Experience (OOBE) setup wizard

---

## Continue Without Internet

When returned to the network setup screen:

1. Click:

```text
I don't have internet
```

2. On the next screen, select:

```text
Continue with limited setup
```

---

# 👤 Create a Local User Account

You can now complete Windows 11 setup using a local account instead of a Microsoft online account.

Configure:

* Username
* Password
* Security questions
* Privacy settings

---

# ✅ Installation Complete

Windows 11 should now install successfully without:

* Internet connectivity
* Microsoft account sign-in
* TPM enforcement restrictions

---

# 📌 Quick Reference Commands

## Open Command Prompt During Setup

```text
Shift + F10
```

---

## Open Registry Editor

```cmd
regedit
```

---

## Bypass Internet Requirement

```cmd
oobe\bypassnro
```

---

# 🧪 Common Use Cases

These methods are commonly used in:

* Enterprise deployment labs
* Virtual machine environments
* Air-gapped systems
* Hardware testing
* Legacy hardware installations
* Offline workstation provisioning

---

# 🔒 Security & Compliance Considerations

Before deploying systems using these methods:

* Verify compliance with organizational IT standards
* Confirm endpoint security requirements
* Review Microsoft licensing policies
* Ensure systems remain properly patched and secured

---

# 📚 Troubleshooting

## Command Prompt Does Not Open

Ensure you press:

```text
Shift + F10
```

during the OOBE/setup phase.

---

## `oobe\bypassnro` Command Not Working

Possible causes:

* Incorrect command syntax
* Unsupported Windows image
* Modified installation media

Verify the command is entered exactly as:

```cmd
oobe\bypassnro
```

---

## Installation Still Requires TPM

Confirm the following registry value exists:

```text
Computer\HKEY_LOCAL_MACHINE\SYSTEM\Setup\LabConfig
```

DWORD:

```text
ByPassTPMCheck = 1
```

---

# 🏁 Conclusion

Using the methods outlined above, IT administrators can successfully deploy Windows 11 in offline or unsupported hardware environments while bypassing:

* Internet connectivity requirements
* Microsoft account enforcement
* TPM setup restrictions

This approach is especially useful for controlled deployment scenarios, lab environments, and legacy system provisioning.

---
