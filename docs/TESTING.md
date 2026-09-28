# Hardware Testing Guide

This file defines the minimum validation procedure before calling a device or CPU tested.

## Test matrix

| Device | CPU | Windows build | Status |
| --- | --- | --- | --- |
| Surface Laptop 7 | Snapdragon X Plus | Add exact build after test | Validation pending |
| Other Windows-on-ARM PC | Snapdragon X Elite | Add exact build after test | Validation pending |

## Test procedure

1. Reboot into the Balanced power plan.
2. Record the stock benchmark result.
3. Apply a 2.00 GHz limit with Strict Cap enabled.
4. Confirm `PROCFREQMAX`, `PROCFREQMAX1`, and `PROCFREQMAX2` where present.
5. Confirm `PERFBOOSTMODE=0` and `PERFAUTONOMOUS=0` where supported.
6. Run a CPU benchmark and compare it with stock.
7. Test normal desktop use, browser CPU stress, Start/menu input, a Game Mode workload, and a non-Game-Mode workload.
8. Restore Stock and verify normal performance returns.

## Useful commands

```powershell
powercfg /qh SCHEME_CURRENT SUB_PROCESSOR
```

```powershell
powercfg /queryprofile SCHEME_CURRENT PROFILE_GAMEMODE
```

```powershell
powercfg /queryprofile SCHEME_CURRENT PROFILE_LOWLATENCY
```

## Pass criteria

A device should only be marked validated when the requested policy values are written and read back successfully, benchmark performance changes consistently with the requested limit, Restore Stock returns behavior to baseline, and repeated tests remain stable after reboot.

Task Manager GHz readouts alone are not sufficient proof of the effective hardware clock on modern ARM/CPPC systems. Pair policy read-back with a repeatable performance test.
