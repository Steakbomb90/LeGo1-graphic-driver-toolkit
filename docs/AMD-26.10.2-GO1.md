# Public Beta v6.0 — AMD Adrenalin 26.10.2

**Scope: original Lenovo Legion Go 1 Z1 Extreme only.** See [GitHub Releases](../../releases) for the published assets.

## Compatibility and prerequisites

- Exact display hardware ID: `PCI\VEN_1002&DEV_15BF&SUBSYS_381217AA&REV_04`.
- Windows 11 x64; use Windows PowerShell 5.1, not PowerShell 7.
- Administrator access, AC power, saved work, and an independent Windows recovery option. Preserve BitLocker/device-encryption recovery information before changing Secure Boot.
- Secure Boot must already be disabled. The workflow temporarily changes Test Signing and certificate trust, modifies the Driver Store, installs AMD Software, and restarts Windows.
- No mandatory Lenovo recovery-driver download. Recovery and alternate starting stacks have not been independently validated for this candidate.

## Release asset identities

The release uses the validated RC1 package and bootstrap filenames. Keep their filenames unchanged and verify their hashes before installation.

| File | SHA-256 |
|---|---|
| `LegionGo-AMD-26.10.2-V5-Derived-RC1.zip` (130972 bytes) | `9CB7D2329B5FB4E725FD461A1B659D3B1D172028FF5067107D9FED6C70739C8A` |
| `Start-LegionGo-AMD-26.10.2-RC1.ps1` | `38A503068E2DF63976FBA7D75FFBD7AD102E8222DA708152B223E7A7F442574A` |

Obtain the official AMD EXE independently. The toolkit does not bundle the AMD installer.

```text
whql-amd-software-adrenalin-edition-26.10.2-win11-c.exe
Length: 1781619344 bytes
FileVersion: 26.10.2.0
SHA-256: 2D743DE62B6732A04BCD940AF76CD2D0C1EF85E2F01A91EA235AC96BCEB42B77
```

## Installation

Place the two RC1 files directly in Downloads with exactly one matching AMD EXE under Downloads. Do not manually extract the inner toolkit ZIP. Verify the bootstrap hash against the value above before executing it. From Windows PowerShell 5.1 on the supported device:

```powershell
powershell.exe -NoProfile -ExecutionPolicy Bypass -File "$env:USERPROFILE\Downloads\Start-LegionGo-AMD-26.10.2-RC1.ps1"
```

The bootstrap validates the package and official EXE, then launches the managed workflow. The stages extract the AMD source, build the device-specific package, validate and install it, manage required reboot/resume boundaries, install AMD Software, and audit persistence. Do not manually run numbered stages or edit workflow state to force progress. If the console enters Select mode, press Esc rather than Ctrl+C. A completed r3 workflow follows the read-only audit path.

## Validation evidence

On November 16, 2026, one physical original Legion Go completed Beta r3 end to end. A subsequent RC1 read-only audit on that same installation returned:

| Check | Result |
|---|---|
| Final persistence audit | 78/78 passed |
| Failed checks / warnings | 0 / 0 |
| GPU | AMD Radeon(TM) 780M |
| Display driver | 32.0.32015.12012 |
| GPU problem code | 0 |
| Workflow stage | Complete |
| Test Signing / nointegritychecks | OFF / OFF |
| Critical catalog coverage | 14/14 local and 14/14 official |
| Secure Boot | Disabled |

The candidate toolkit passed 21/21 manifest checks. RC1 retains the tested driver stages and adds console QuickEdit protection. A fresh RC1 installation, its automatic reboot-resume behavior, rollback, gaming, sleep and performance are not yet independently validated. A retained local public certificate and disabled Secure Boot mean the final state is not equivalent to default Windows security. Raw device evidence is not included.

Independent community project; not endorsed by AMD, Lenovo or Microsoft. See [MIT License](../LICENSE) and [Third-Party Notices](../THIRD-PARTY-NOTICES.md).
