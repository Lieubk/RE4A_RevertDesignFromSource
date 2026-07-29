# RE4A — Setup

**RE4A — Reverse Engineering for Automotive (SAD/SDD generator)**

## What's in this package

| Folder / file | Description |
|---|---|
| `RE4A\RE4A.exe` | The desktop application (start here). |
| `RE4A.Cli\RE4A.Cli.exe` | The command-line tool (for automation / CI). |
| `UserGuide.md` | Full user manual. |
| `THIRD-PARTY-NOTICES.md` | Open-source component licences. |

This build is **self-contained** — the .NET runtime is bundled, so **you do NOT need to install
.NET** on the target machine.

## Requirements

- **Windows 10 / 11, 64-bit.**
- A valid RE4A **license** (per machine — see *Activation* below).
- *Optional* — **Enterprise Architect 16 or 17 (64-bit)**: only needed to open the `.qea` export.
- *Optional* — **Java + PlantUML**: only needed to render diagrams as images in DOCX / previews.
  Without them, diagrams appear as text. (See the User Guide, "Diagram rendering tools".)

## Install & run

1. Copy this whole folder to the target PC (any location).
2. Run **`RE4A\RE4A.exe`**.

## Code signature

All RE4A binaries (`RE4A.exe`, `RE4A.Cli.exe`, `RE4A*.dll`) are **Authenticode-signed and
timestamped**, so Windows can detect any tampering after delivery. To check a file: right-click ▸
**Properties ▸ Digital Signatures**, or run
`Get-AuthenticodeSignature .\RE4A\RE4A.exe` in PowerShell.

Expected signer:

| Field | Value |
|---|---|
| Subject | `CN=RE4A Code Signing, O=RE4A` |
| SHA-1 thumbprint | `218907E441AAA36B8718D8F2390C08F9DEB40D69` |
| Signature / key | SHA-256, RSA-3072, RFC3161 timestamped |

> **Note** — this build is signed with the vendor's **own (self-signed) certificate**, not one from a
> public certificate authority. The signature still proves the files are unmodified since they were
> built, but Windows SmartScreen and some AV/EDR products will still warn on first run because the
> issuing certificate is not in the machine's trusted-root list. Confirm the thumbprint above with
> your vendor before running, and whitelist the folder in your endpoint-protection tool if needed.

## Activation (first run)

On first launch the application is **locked** until a license is installed:

1. In the red banner at the top, click **License…** (or **Options ▸ License…**).
2. Click **Copy** to copy **This machine's ID** (`XXXX-XXXX-XXXX-XXXX`) and send it to your vendor.
3. When you receive your license file, click **Import license file (.lic)…** and select it.
4. The application unlocks. The license is stored on this machine and stays active on later runs.

A license is valid on **one machine only**. See `UserGuide.md` for the full workflow and
troubleshooting.
