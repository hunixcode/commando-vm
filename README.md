<div align="center">
    <img src="Images/commando-readme.png" alt="CommandoVM" width="450"/>
</div>

# CommandoVM

Complete Mandiant Offensive VM — a customizable Windows-based security distribution for penetration testing and red teaming. CommandoVM packages a wide array of offensive tools that highlight the effectiveness of Windows as an attack platform, complementing what you'd find in [Kali Linux](https://www.kali.org/).

## Requirements

| Component | Minimum | Recommended |
|-----------|---------|-------------|
| OS | Windows 10 | Windows 10 22H2 |
| Storage | 60 GB | 80+ GB |
| RAM | 2 GB | 4+ GB |
| Network | 1 adapter | 2 adapters |

> Insider Preview editions of Windows are not supported.

## Install

### 1. Deploy a Windows VM

Download a Windows 10 virtual machine from the [official source](https://www.microsoft.com/en-us/software-download/windows10ISO).

> You should never install CommandoVM on your host machine. It makes irreversible changes that cannot be uninstalled.

### 2. Disable Windows Defender

Tamper Protection must be disabled **first**, otherwise Group Policy settings are ignored.

1. Open **Windows Security** → **Virus & threat protection** → **Manage settings**
2. Switch **Tamper Protection** to **Off**
3. Open **Local Group Policy Editor** (`gpedit`)
4. Navigate to `Computer Configuration` → `Administrative Templates` → `Windows Components` → `Microsoft Defender Antivirus` → `Real-time Protection`
5. Enable **Turn off real-time protection**
6. **Reboot**
7. Navigate to `Computer Configuration` → `Administrative Templates` → `Windows Components` → `Microsoft Defender Antivirus`
8. Enable **Turn off Microsoft Defender Antivirus**
9. **Reboot**

> It is not necessary to change any other setting (Real Time Protection, etc.). Tamper Protection must be disabled before changing Group Policy settings.

### 3. Run the Installer

```powershell
Set-ExecutionPolicy Unrestricted -Force
cd ~/Downloads/commando-vm
Get-ChildItem .\ -Recurse | Unblock-File
.\install.ps1               # GUI install
.\install.ps1 -cli          # Command-line install
```

Installation may take over an hour and will restart your machine multiple times. You are done when your background changes to the CommandoVM logo.

## Profiles

CommandoVM offers several installation profiles under the [`Profiles/`](Profiles/) directory. You can select one during the GUI install or pass it via `-customProfile`:

```powershell
.\install.ps1 -cli -customProfile .\Profiles\Default.xml -noPassword
```

See the [Customization](Docs/Customization.md) docs for the XML profile format.

## Troubleshooting

Refer to the [Troubleshooting Guide](Docs/Troubleshooting.md) for detailed install help, including pre-install checks, Boxstarter password prompts, and common failure modes.

## Quickstart Guide

New to the project? The [CommandoVM Quickstart Guide](Docs/Commando_Quickstart_Guide.md) walks you through the architecture, the VM-Packages ecosystem, and how to start contributing.

## Contributing

CommandoVM is built from two interconnected repositories:

- **commando-vm** (this repo) — installer, profiles, and documentation
- **[VM-Packages](https://github.com/mandiant/VM-Packages)** — the tool packages and their install logic

### How to help

- Submit new tool packages or report package issues on the [VM-Packages issue tracker](https://github.com/mandiant/VM-Packages/issues)
- Read the [VM-Packages wiki](https://github.com/mandiant/VM-Packages/wiki) for contribution guides
- Check the [Quickstart Guide](Docs/Commando_Quickstart_Guide.md) to go from zero to contributor

## Credits

- Jake Barteaux @day1player
- Blaine Stancill @MalwareMechanic
- Nhan Huynh @htnhan
- Drew Farber @0xFarbs
- Alex Tselevich @nos3curity
- George Litvinov @geo-lit
- Dennis Tran @Menn1s
- Joseph Clay @skollr34p3r
- Ana Martinez Gomez @anamma_06
- Moritz Raabe
- Derrick Tran @dumosuku
- Mandiant Red Team
- Mandiant FLARE

## License

This configuration script is provided under the [Apache 2.0 License](License.txt). Installation and use of this script is subject to the license terms of each downloaded/installed package. By proceeding with installation, you accept the license terms of each package and acknowledge that your use will be subject to its respective terms.
