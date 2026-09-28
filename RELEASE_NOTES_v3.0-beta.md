# v3.0 Beta

First public beta of Universal Clock Limiter (ARM).

## Changes

- Replaced the old slider with direct GHz input.
- Input range is now 0.80 to 5.00 GHz.
- A value is only applied after pressing **Apply Limit**.
- Added **Restore Stock**.
- Added **Strict Cap** mode.
- Added handling for workload-specific Windows PPM profiles including GameMode and LowLatency.
- Native Windows 11 ARM64 build.
- Portable single EXE with no Python, .NET runtime, VC++ Redistributable, or installer dependency.
- Added read-back checks for the main Windows processor-policy values.

This release is still a beta because Windows-on-ARM firmware behavior can differ between devices. Hardware test reports are welcome, especially from Snapdragon X Elite systems.

Author: Mario Gad  
Copyright © 2026 Mario Gad. All rights reserved.
