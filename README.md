<div align="center">

# Lenovo Legion Go 1 — AMD Adrenalin 26.10.2 Toolkit

### Public Beta v6.0 — Original Legion Go Z1 Extreme

![Release](https://img.shields.io/badge/release-Public%20Beta%20v6.0-2EA44F?style=for-the-badge)
![AMD](https://img.shields.io/badge/AMD-26.10.2-ED1C24?style=for-the-badge)
![Audit](https://img.shields.io/badge/final%20audit-78%2F78-2EA44F?style=for-the-badge)
![Platform](https://img.shields.io/badge/platform-Windows%2011-0078D4?style=for-the-badge)
![License](https://img.shields.io/badge/license-MIT-blue?style=for-the-badge)

**Automatically build, install and verify AMD Adrenalin 26.10.2 for the original Legion Go Z1 Extreme.**

[Releases](../../releases) · [Installation and checksums](docs/AMD-26.10.2-GO1.md) · [Report an issue](../../issues)

</div>

---

> [!IMPORTANT]
> Public Beta v6.0 targets **only the original Lenovo Legion Go 1 Z1 Extreme**. The driver installation was physically validated on one device using Beta r3, followed by a successful RC1 persistence audit of 78/78 checks. The release retains the RC1 executable payload.

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
| AMD Adrenalin | 26.10.2 |
| Display driver | `32.0.32015.12012` |
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

## Download and install

Download the following two files from [GitHub Releases](../../releases):

- `LegionGo-AMD-26.10.2-V5-Derived-RC1.zip`
- `Start-LegionGo-AMD-26.10.2-RC1.ps1`

Also obtain the official AMD installer independently:

`whql-amd-software-adrenalin-edition-26.10.2-win11-c.exe`

Place all three files in Downloads. Do not rename or manually extract the toolkit ZIP. Verify their hashes using the [installation guide](docs/AMD-26.10.2-GO1.md). Use Windows PowerShell 5.1 on the supported device:

```powershell
powershell.exe -NoProfile -ExecutionPolicy Bypass -File "$env:USERPROFILE\Downloads\Start-LegionGo-AMD-26.10.2-RC1.ps1"
```

Administrator access and disabled Secure Boot are required. AC power is recommended. Accept the initial confirmation prompts and let the managed workflow handle the stages and restarts.

## Validation results

| Check | Result |
|---|---|
| Physical installation | Passed (Beta r3) |
| RC1 final persistence audit | **78/78 PASS** |
| Failed checks / warnings | 0 / 0 |
| GPU problem code | 0 |
| Display driver | `32.0.32015.12012` |
| TESTSIGNING / nointegritychecks | OFF / OFF |
| Local and official catalog coverage | 14/14 each |
| AMD Software installation | Passed |
| Workflow stage | Complete |
| Package manifest integrity | 21/21 |
| Secure Boot | Disabled |

A fresh RC1 installation, rollback, gaming performance, sleep behavior and additional configurations remain unverified. This is a public beta, not an official AMD or Lenovo driver release.

## Troubleshooting

Do not manually run numbered stages, edit workflow state, or toggle boot signing during an active installation. If the console enters Select mode, press Esc. Stop at a hard failure and preserve the installer logs instead of forcing another attempt. Report problems through [GitHub Issues](../../issues) and redact personal information before sharing evidence.

## Independence and license

This independent community project is not endorsed or supported by AMD, Lenovo or Microsoft. Original project code and documentation are distributed under the [MIT License](LICENSE). Third-party software and trademarks remain subject to their own terms; see [Third-Party Notices](THIRD-PARTY-NOTICES.md).
