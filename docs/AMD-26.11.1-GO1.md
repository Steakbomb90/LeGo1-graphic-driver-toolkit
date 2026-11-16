# Public Beta v6.1 — AMD Adrenalin 26.11.1

**Scope: original Lenovo Legion Go 1 Z1 Extreme only.** Download the two toolkit assets from [Public Beta v6.1](../../releases/tag/public-beta-v6.1).

## Compatibility and prerequisites

- Exact display hardware ID: `PCI\VEN_1002&DEV_15BF&SUBSYS_381217AA&REV_04`.
- Windows 11 x64; use Windows PowerShell 5.1.
- Administrator access, saved work, independent recovery option and AC power recommended. Preserve BitLocker/device-encryption recovery information before changing Secure Boot.
- Secure Boot must already be disabled. Installation temporarily changes Test Signing and certificate trust, modifies the Driver Store, installs AMD Software and restarts Windows.
- No mandatory Lenovo recovery driver download. Direct upgrade from the previous public beta was validated; clean installations and rollback remain unverified.

## Release asset identities

Keep the exact hardware-tested RC1 filenames unchanged. Verify SHA-256 hashes before executing the bootstrap.

| File | SHA-256 |
| --- | --- |
| `LegionGo-AMD-26.11.1-Public-Beta-v6.1-RC1.zip` | `939A81D9C693B4DE39ACA13B4433CEC6DD08B4C0355D7EB3385A04C18BD064DC` |
| `Start-LegionGo-AMD-26.11.1-RC1.ps1` | `FACAC4704481D8E78F7E913138767C982E8601DE87E1E97C44285BB3DDD58FB0` |

Obtain the official AMD installer separately from AMD. It is not bundled.

```text
amd-software-adrenalin-edition-26.11.1-win11-c.exe
Length: 1780861240 bytes
FileVersion: 26.11.1.0
SHA-256: 5A2B7A334D3E91E0B278F45CAD981CE5C0DFE610311DC7E5F2CA0D6D87119211
```

## Installation

Place both toolkit files and exactly one matching official AMD EXE in Downloads. Do not manually extract the toolkit ZIP. After checking the file hashes, run this command in Windows PowerShell 5.1 on the supported Legion Go:

```powershell
powershell.exe -NoProfile -ExecutionPolicy Bypass -File "$env:USERPROFILE\Downloads\Start-LegionGo-AMD-26.11.1-RC1.ps1" -Install
```

The explicit `-Install` parameter is required. The bootstrap verifies the package and installer, and the managed workflow handles extraction, deterministic driver construction, local catalog signing, installation, reboots, AMD Software and the final persistence audit. Follow the initial confirmation prompts. Do not manually run numbered stages or edit workflow state. If the console enters Select mode, press Esc.

For read-only desktop validation, use `-GateOnly` instead of `-Install`. Never use installation mode on unsupported hardware.

## Validation

On November 16, 2026, the exact RC1 package passed desktop preflight and completed a physical direct upgrade on an original Legion Go Z1 Extreme.

| Check | Result |
| --- | --- |
| Windows PowerShell preflight | 38/38 PASS |
| Package integrity | 21/21 PASS |
| Final persistence audit | 78/78 PASS |
| Failed checks / warnings | 0 / 0 |
| GPU | AMD Radeon(TM) 780M |
| Display driver | 32.0.32015.16001 |
| GPU problem code | 0 |
| Workflow stage | Complete |
| Test Signing / nointegritychecks | OFF / OFF |
| Critical catalog coverage | 14/14 local and 14/14 official |
| AMD Software runtime verification | 7/7 |
| Secure Boot | Disabled |

Deterministic modified driver identities:

```text
INF SHA-256: 6A42395E39DBD5ACC91B937472806375B9FA659E3183747396AF4227097D3208
DAT SHA-256: 7986B5DC0CB3C2207ECE857D0060475A603B5342649D146874850C0D4A2509CA
```

Clean installations, rollback and broader gaming, sleep and performance testing remain unverified. Secure Boot remains disabled and the local public signing certificate remains trusted. Raw device evidence is not included.

Independent community project; not endorsed by AMD, Lenovo or Microsoft. See [MIT License](../LICENSE) and [Third-Party Notices](../THIRD-PARTY-NOTICES.md).
