# Compatibility

Universal Clock Limiter (ARM) is built for **Windows 11 ARM64**.

The program relies on Windows processor power-management settings exposed through `powercfg` / PowrProf. Compatibility therefore depends on what the Windows build, OEM firmware and CPU platform expose.

## Hardware status

| Device / CPU | Status | Notes |
| --- | --- | --- |
| Microsoft Surface Laptop 7 / Snapdragon X Plus | Development platform | Used for current real-device testing |
| Snapdragon X Plus laptops from other OEMs | Expected to work | Additional validation wanted |
| Snapdragon X Elite laptops | Targeted | Real-device validation wanted |
| Other Windows 11 ARM64 systems | Experimental | Depends on exposed processor power policies |
| Windows x64 / x86 PCs | Not supported by this build | ARM64 executable only |

## Windows requirements

- Windows 11 ARM64
- Administrator privileges
- An active Windows power plan exposing the required processor power-management settings

## Policies used

Depending on what the platform exposes, the app can work with:

- `PROCFREQMAX`
- `PROCFREQMAX1`
- `PROCFREQMAX2`
- `PERFBOOSTMODE`
- `PERFAUTONOMOUS`
- workload-specific PPM profiles such as GameMode and LowLatency

Not every ARM PC exposes every setting. Missing optional settings should not be interpreted as a hardware failure.

## Snapdragon X Plus

Snapdragon X Plus is the primary development target. Current testing is being performed on a Surface Laptop 7 running Windows 11 ARM64.

Relevant search terms include:

- Snapdragon X Plus CPU frequency limiter
- Snapdragon X Plus underclock
- Snapdragon X Plus power limit
- Snapdragon X Plus battery tuning
- Surface Laptop 7 CPU limiter
- Surface Laptop 7 powercfg

## Snapdragon X Elite

Snapdragon X Elite is a target platform because it uses the same Windows 11 ARM processor power-management architecture, but compatibility should only be marked validated after real hardware testing.

Useful reports should include the exact laptop model, Snapdragon X Elite SKU, Windows build, selected frequency, benchmark result and whether Restore Stock works correctly.

## Validation

See [`TESTING.md`](TESTING.md) for the current validation procedure.

A device should only be listed as validated after repeatable policy read-back, benchmark comparison and stock-restore testing.
