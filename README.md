<div align="center">

# Lenovo Legion Go 1 — AMD Adrenalin 26.11.1 Toolkit

### Public Beta v6.1 — Original Legion Go Z1 Extreme

![Release](https://img.shields.io/badge/release-Public%20Beta%20v6.1-2EA44F?style=for-the-badge)
![AMD](https://img.shields.io/badge/AMD-26.11.1-ED1C24?style=for-the-badge)
![Audit](https://img.shields.io/badge/final%20audit-78%2F78-2EA44F?style=for-the-badge)
![Platform](https://img.shields.io/badge/platform-Windows%2011-0078D4?style=for-the-badge)
![License](https://img.shields.io/badge/license-MIT-blue?style=for-the-badge)

**Automatically build, install and verify AMD Adrenalin 26.11.1 for the original Legion Go Z1 Extreme.**

[Public Beta v6.1](../../releases/tag/public-beta-v6.1) · [Installation and checksums](docs/AMD-26.11.1-GO1.md) · [Report an issue](../../issues)

</div>

---

> [!IMPORTANT]
> Public Beta v6.1 targets **only the original Lenovo Legion Go 1 Z1 Extreme**. The exact released RC1 package successfully completed a direct upgrade from the previous public beta on physical hardware, followed by a 78/78 persistence audit with zero failures or warnings. RC1 filenames are intentionally retained.

> [!WARNING]
> This toolkit modifies the display driver, Driver Store, certificate trust, AMD Software, scheduled tasks and temporary Windows Test Signing configuration. Save your work, keep an independent Windows recovery option available and preserve your BitLocker or Device Encryption recovery key before changing Secure Boot. Secure Boot remains disabled and a local public signing certificate remains trusted after installation.

## Supported hardware

| Property | Required value |
|---|---|
| Device | Lenovo Legion Go 1 |
| Processor | AMD Ryzen Z1 Extreme |
| Exact display hardware ID | `PCI\VEN_1002&DEV_15BF&SUBSYS_381217AA&REV_04` |
| GPU | AMD Radeon(TM) 780M |
| OS | Windows 11 x64 |
| AMD Adrenalin | 26.11.1 |
| Display driver | `32.0.32015.16001` |
| Active DDInstall | `ati2mtag_Phoenix_LegionGo` |

All other hardware IDs are outside the supported scope.

## What's included

- Automatic extraction of the official AMD installer.
- Deterministic Legion Go-specific INF/DAT construction and local catalog signing.
- Exact hardware and SHA-256 integrity verification.
- One managed PowerShell workflow with initial confirmation prompts and automatic reboot/resume.
- Session-wide QuickEdit protection.
- AMD Software and DVR installation.
- Return to normal boot-signing policy and final 78-check persistence audit.
- No mandatory Lenovo recovery driver download.
- Explicit `-Install` mode for the supported device; `-GateOnly` enables read-only preflight without starting installation.

## Download and install

Download the following two files from [Public Beta v6.1 release](../../releases/tag/public-beta-v6.1):

- `LegionGo-AMD-26.11.1-Public-Beta-v6.1-RC1.zip`
- `Start-LegionGo-AMD-26.11.1-RC1.ps1`

Also obtain the official AMD installer independently:

`amd-software-adrenalin-edition-26.11.1-win11-c.exe`

Place all three files in Downloads. Do not rename or manually extract the toolkit ZIP. Verify their hashes using the [installation guide](docs/AMD-26.11.1-GO1.md). Use Windows PowerShell 5.1 on the supported device:

```powershell
powershell.exe -NoProfile -ExecutionPolicy Bypass -File "$env:USERPROFILE\Downloads\Start-LegionGo-AMD-26.11.1-RC1.ps1" -Install
```

Administrator access and disabled Secure Boot are required. AC power is recommended. Do not run installation mode on any unsupported system. Accept the initial confirmation prompts and let the managed workflow handle the stages and restarts.

## Validation results

| Check | Result |
|---|---|
| Physical direct upgrade | Passed (exact RC1 package) |
| Windows PowerShell preflight | **38/38 PASS** |
| RC1 final persistence audit | **78/78 PASS** |
| Failed checks / warnings | 0 / 0 |
| GPU problem code | 0 |
| Display driver | `32.0.32015.16001` |
| TESTSIGNING / nointegritychecks | OFF / OFF |
| Local and official catalog coverage | 14/14 each |
| AMD Software installation | Passed |
| Workflow stage | Complete |
| Package manifest integrity | 21/21 |
| Secure Boot | Disabled |

Clean installation, rollback, gaming performance, sleep behavior and additional configurations remain unverified. This is a public beta, not an official AMD or Lenovo driver release.

## Troubleshooting

Do not manually run numbered stages, edit workflow state, or toggle boot signing during an active installation. If the console enters Select mode, press Esc. Stop at a hard failure and preserve the installer logs instead of forcing another attempt. Report problems through [GitHub Issues](../../issues) and redact personal information before sharing evidence.

## Independence and license

This independent community project is not endorsed or supported by AMD, Lenovo or Microsoft. Original project code and documentation are distributed under the [MIT License](LICENSE). Third-party software and trademarks remain subject to their own terms; see [Third-Party Notices](THIRD-PARTY-NOTICES.md).
