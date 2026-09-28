# Technical Notes

## Windows MaxFrequency

Microsoft documents `MaxFrequency` / `PROCFREQMAX` as a maximum processor performance state expressed in MHz. Windows 11 ARM-based devices are listed as supported.

Official documentation:
https://learn.microsoft.com/en-us/windows-hardware/customize/power-settings/options-for-perf-state-engine-maxfrequency

## PPM profiles

Windows processor power management can use workload-specific profiles such as `LowLatency`, `LowPower`, `Constrained`, `GameMode`, and `SustainedPerf`.

Official documentation:
https://learn.microsoft.com/en-us/windows-hardware/customize/power-settings/configure-processor-power-management-options

Microsoft notes that PPM profiles are tuned by silicon vendors. The operating system or OEM firmware may therefore handle a requested policy differently across devices.

## Powercfg profile commands

Windows supports `/queryprofile`, `/setacprofileindex`, and `/setdcprofileindex` for PPM profiles.

Official documentation:
https://learn.microsoft.com/en-us/windows-hardware/design/device-experiences/powercfg-command-line-options

## Latency-sensitive behavior

Windows supports latency-sensitivity hints that can raise requested processor performance in response to user input and other latency-sensitive activity.

Official documentation:
https://learn.microsoft.com/en-us/windows-hardware/customize/power-settings/options-for-perf-state-engine-perflatencyhint

This is one reason runtime testing should include keyboard/mouse interaction and game workloads rather than only a synthetic browser stress test.
