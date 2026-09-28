# Universal Clock Limiter (ARM)

Universal Clock Limiter is a small native Windows 11 ARM64 utility for setting a maximum CPU frequency policy without installing extra runtimes.

I built it for Windows on ARM laptops where I wanted an easy way to trade some peak CPU performance for lower power use and less heat during sustained workloads. Instead of editing `powercfg` settings by hand, you enter a GHz limit, press **Apply Limit**, and the app writes the relevant Windows processor power-management settings for AC and battery use.

Author: **Mario Gad**  
Copyright © 2026 Mario Gad. All rights reserved.

## Current status

This is an early public beta.

Initial development and testing is being done on a **Surface Laptop 7 with Snapdragon X Plus**. Snapdragon X Elite uses the same Windows 11 ARM power-management framework, but I am not marking X Elite as fully validated until I have independent hardware test results.

The app is Windows 11 ARM64 only.

## What it does

- Direct frequency input from **0.80 GHz to 5.00 GHz**
- Nothing changes until **Apply Limit** is pressed
- Applies the requested policy to both AC and battery operation
- Handles `PROCFREQMAX`, `PROCFREQMAX1`, and `PROCFREQMAX2` where Windows exposes them
- Optional **Strict Cap** mode disables boost policy and autonomous processor control where supported
- Also applies limits to workload-specific Windows PPM profiles such as GameMode and LowLatency
- **Restore Stock** removes the manual frequency cap and returns processor control to Windows
- Native ARM64 executable
- No Python, .NET runtime, VC++ Redistributable, or installer required

## Why lower the maximum frequency?

A lower CPU frequency ceiling can reduce the voltage/frequency range used under load. On supported hardware this can lower peak CPU power draw and heat output. On a laptop that can also help battery life during sustained CPU-heavy work.

The exact result depends on the workload. A browser tab, a video, a game, and a full CPU render do not stress the system in the same way. Display brightness, GPU load, Wi-Fi, memory, storage, background tasks, and firmware behavior also affect total system power.

This tool does not promise a fixed watt reduction or a fixed battery-life gain.

## Download and use

1. Download `Universal_Clock_Limiter_ARM_v3.0.exe` from this repository.
2. Run it and accept the Windows UAC prompt.
3. Enter a value between `0.80` and `5.00`.
4. Leave **Strict Cap** enabled if you want the strongest Windows-side limit.
5. Press **Apply Limit**.
6. Press **Restore Stock** when you want normal Windows processor management again.

Example: entering `2.00` requests a 2000 MHz maximum processor-frequency policy.

## Important: this is not an overclocking tool

Entering a number above the physical maximum of the CPU does not make the processor run faster than its hardware limit.

For example, entering `5.00` on a CPU that tops out at 3.4 GHz does not overclock it to 5 GHz. The application sets a Windows maximum-frequency policy. Hardware limits, firmware, thermals, OEM policy, and the Windows processor power manager still decide what the CPU can actually do.

## Compatibility

| Platform | Status |
| --- | --- |
| Windows 11 ARM64 | Required |
| Snapdragon X Plus | Primary development / test platform |
| Snapdragon X Elite | Expected to work, validation wanted |
| Other Windows 11 ARM64 processors | May work if the required Windows policies are exposed |
| Windows x64 / x86 | Not supported by this build |

## How it works

Windows exposes processor power-management settings through `powercfg` and the PowrProf API. The main frequency policy is `PROCFREQMAX`, expressed in MHz. Newer heterogeneous systems can also expose additional efficiency-class variants such as `PROCFREQMAX1` and `PROCFREQMAX2`.

Strict Cap also changes boost and autonomous performance policies when the platform exposes them. The application additionally covers workload-specific PPM profiles because Windows can use separate policies for GameMode, LowLatency, sustained performance, low-power workloads, and QoS classes.

Microsoft documentation:

- MaxFrequency: https://learn.microsoft.com/en-us/windows-hardware/customize/power-settings/options-for-perf-state-engine-maxfrequency
- Processor power-management profiles: https://learn.microsoft.com/en-us/windows-hardware/customize/power-settings/configure-processor-power-management-options
- powercfg command-line options: https://learn.microsoft.com/en-us/windows-hardware/design/device-experiences/powercfg-command-line-options

## A note about reported GHz values

On modern ARM/CPPC systems, the GHz number shown by Task Manager or another monitoring tool is not always a perfect representation of the effective hardware clock. Windows and the platform firmware can use abstract performance states and workload-specific policies.

For that reason, the best way to validate a limit is to combine:

1. policy read-back with `powercfg`, and
2. a repeatable CPU benchmark before and after applying the limit.

See [`docs/TESTING.md`](docs/TESTING.md) for the current test procedure.

## Restore / recovery

If a limit behaves unexpectedly, open the app and press **Restore Stock**. A reboot is also recommended after unusual power-policy behavior.

You can inspect the active processor policy manually with:

```powershell
powercfg /qh SCHEME_CURRENT SUB_PROCESSOR
```

## Reporting hardware results

If you test it on another Windows 11 ARM device, open a hardware-validation issue and include:

- device model
- CPU model
- Windows build
- selected frequency
- Strict Cap on/off
- AC or battery
- workload / benchmark used
- stock score and limited score if available
- whether Restore Stock returned performance to normal

This is especially useful for Snapdragon X Elite systems.

## License

Copyright © 2026 Mario Gad. All rights reserved. See [`LICENSE.txt`](LICENSE.txt).

## Disclaimer

This software changes Windows processor power-management settings and requires Administrator privileges. Use it at your own risk. The software is provided as-is, without warranty.

Universal Clock Limiter (ARM) is an independent project and is not affiliated with Microsoft, Qualcomm, or the Surface brand.
