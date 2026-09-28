# Universal Clock Limiter (ARM)

**Windows 11 ARM64 CPU frequency limiter for Snapdragon X Plus, Snapdragon X Elite and other Windows on ARM PCs.**

Universal Clock Limiter (ARM) is a small native Windows utility that lets you set a maximum CPU frequency policy without manually editing `powercfg` settings. It is intended for Windows on ARM laptops where you may want to trade some peak CPU performance for lower power use, lower heat output and potentially better battery life during sustained CPU-heavy workloads.

The app is being developed and tested on a **Microsoft Surface Laptop 7 with Snapdragon X Plus**. Snapdragon X Elite and other Windows 11 ARM64 systems use the same Windows processor power-management framework, but hardware validation can still differ by device and firmware.

Author: **Mario Gad**  
Copyright © 2026 Mario Gad. All rights reserved.

## At a glance

- Windows 11 ARM64 only
- Snapdragon X Plus supported as the primary development platform
- Snapdragon X Elite targeted and open for additional validation
- Direct CPU limit input from **0.80 GHz to 5.00 GHz**
- Applies limits to both AC and battery operation
- Optional **Strict Cap** mode
- Handles GameMode and LowLatency processor power profiles
- One-click **Restore Stock**
- Native ARM64 executable
- Portable: no Python, .NET, VC++ Redistributable or installer required

## Why this exists

Windows on ARM already manages CPU frequency dynamically, but there are situations where a lower maximum frequency can be useful. A lower ceiling can reduce the CPU's available voltage/frequency range under load, which may reduce peak CPU power draw and heat output.

Typical use cases include:

- reducing heat during long CPU-heavy workloads
- lowering peak CPU power consumption
- experimenting with battery-efficient Snapdragon X settings
- limiting CPU frequency on a Surface Laptop 7 or another Windows on ARM laptop
- comparing performance-per-watt at different CPU limits
- testing lower-frequency profiles without editing Windows power settings by hand

This is a **CPU frequency-policy limiter**, not a direct hardware clock controller. The actual result depends on the processor, firmware, workload and Windows power-management implementation.

## Download and use

1. Download `Universal_Clock_Limiter_ARM_v3.0.exe` from this repository.
2. Run it and accept the Windows UAC prompt.
3. Enter a value between `0.80` and `5.00` GHz.
4. Leave **Strict Cap** enabled if you want the strongest Windows-side limit.
5. Press **Apply Limit**.
6. Press **Restore Stock** when you want normal Windows processor management again.

Example: entering `2.00` requests a maximum processor-frequency policy of `2000 MHz`.

## What the app changes

The application uses Windows processor power-management policies, including:

- `PROCFREQMAX`
- `PROCFREQMAX1`
- `PROCFREQMAX2` where exposed by Windows
- processor boost policy in Strict Cap mode
- autonomous CPPC / processor control where supported
- workload-specific PPM profiles including GameMode and LowLatency

The selected value is applied to both AC and battery profiles.

## Strict Cap

Strict Cap is intended for systems where Windows may temporarily request a higher performance state because of GameMode, latency-sensitive workloads or platform power management.

When enabled, the app also disables Windows processor boost policy and autonomous processor performance control where those settings are supported by the platform.

Some ARM systems may still reinterpret or ignore individual Windows policy requests at firmware level. This is why benchmark validation is more useful than relying only on a GHz number shown in Task Manager.

## Compatibility

| Platform | Status |
| --- | --- |
| Windows 11 ARM64 | Required |
| Snapdragon X Plus | Primary development and test platform |
| Microsoft Surface Laptop 7, Snapdragon X Plus | Current real-device test system |
| Snapdragon X Elite | Targeted; more independent device testing wanted |
| Other Windows on ARM processors | May work if the required Windows policies are exposed |
| Windows x64 / x86 | Not supported by this build |

See [`docs/COMPATIBILITY.md`](docs/COMPATIBILITY.md) for the current hardware notes and test matrix.

## Surface Laptop 7 / Snapdragon X testing

The main development system is a Surface Laptop 7 running Windows 11 on ARM with a Snapdragon X Plus processor.

Current testing focuses on:

- normal desktop use
- browser CPU stress
- sustained CPU benchmarks
- GameMode behavior
- Windows Start / latency-sensitive interactions
- Minecraft and other game workloads
- restoring stock Windows behavior after a custom limit

The same project is also intended for Snapdragon X Elite laptops, but those systems should be treated as hardware-validation targets until test results are available from real X Elite devices.

## Power, heat and battery life

Reducing the CPU frequency ceiling can reduce CPU power draw and heat under sustained load, but it does not guarantee a fixed watt reduction or a fixed battery-life improvement.

Total laptop power also depends on:

- display brightness and refresh rate
- GPU and NPU workload
- Wi-Fi activity
- memory and storage activity
- background processes
- OEM firmware
- how long a workload takes to finish at the lower frequency

For light tasks such as video playback or idle desktop use, the CPU may already spend much of its time in low-power states, so the benefit can be smaller than under sustained CPU load.

## This is not an overclocking tool

Entering a number above the physical maximum of the processor does not overclock the CPU.

For example, entering `5.00` on a processor whose hardware maximum is 3.4 GHz will not make it run at 5 GHz. The program only sets a Windows maximum-frequency policy. Hardware limits, firmware, thermals and Windows remain in control.

## How to verify a limit

On modern ARM / CPPC systems, the frequency shown by Task Manager or another monitoring utility is not always a reliable representation of the effective hardware clock.

For a useful validation test:

1. record a repeatable CPU benchmark at stock settings
2. apply a lower limit such as `2.00 GHz`
3. verify the Windows policy values with `powercfg`
4. run the same benchmark again
5. compare performance and behavior
6. press **Restore Stock** and confirm stock performance returns

You can inspect the current processor settings with:

```powershell
powercfg /qh SCHEME_CURRENT SUB_PROCESSOR
```

See [`docs/TESTING.md`](docs/TESTING.md) for the test procedure.

## Microsoft documentation

The app uses documented Windows processor power-management mechanisms:

- [Maximum processor frequency / MaxFrequency](https://learn.microsoft.com/en-us/windows-hardware/customize/power-settings/options-for-perf-state-engine-maxfrequency)
- [Processor power-management profiles](https://learn.microsoft.com/en-us/windows-hardware/customize/power-settings/configure-processor-power-management-options)
- [powercfg command-line options](https://learn.microsoft.com/en-us/windows-hardware/design/device-experiences/powercfg-command-line-options)

Microsoft lists MaxFrequency support for Windows 11 on ARM-based devices. Windows also supports workload-specific processor power-management profiles such as GameMode and LowLatency.

## Reporting hardware results

If you test Universal Clock Limiter on another Windows 11 ARM device, open a hardware-validation issue and include:

- device model
- CPU model
- Windows build
- selected frequency
- Strict Cap on/off
- AC or battery
- workload or benchmark used
- stock score and limited score if available
- whether Restore Stock returned performance to normal

Reports from **Snapdragon X Elite**, other **Snapdragon X Plus** laptops and non-Surface Windows on ARM devices are especially useful.

## Search terms / project scope

This project is relevant to users looking for a Windows on ARM CPU limiter, Snapdragon X frequency limiter, Snapdragon X Plus underclock utility, Snapdragon X Elite power-management tool, ARM64 CPU clock limiter, Surface Laptop 7 CPU limiter, lower-power Snapdragon X settings or Windows 11 ARM powercfg tuning.

## License

Copyright © 2026 Mario Gad. All rights reserved. See [`LICENSE.txt`](LICENSE.txt).

## Disclaimer

This software changes Windows processor power-management settings and requires Administrator privileges. Use it at your own risk. The software is provided as-is, without warranty.

Universal Clock Limiter (ARM) is an independent project and is not affiliated with Microsoft, Qualcomm or the Surface brand.
