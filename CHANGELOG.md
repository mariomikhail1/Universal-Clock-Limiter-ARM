# Changelog

## v3.0

- Replaced the frequency slider with a direct GHz input field.
- Input range changed to 0.80–5.00 GHz.
- Frequency changes occur only after pressing APPLY LIMIT.
- Added separate RESTORE STOCK action.
- Added Strict Cap toggle.
- Added PPM-profile handling for GameMode, LowLatency, SustainedPerf, Multimedia, Background, EntryLevelPerf, Constrained, LowPower, EcoQos, and UtilityQos.
- Uses documented `powercfg /setacprofileindex` and `/setdcprofileindex` where available, with a runtime-override fallback.
- Added base-policy writes and read-back verification through PowrProf APIs.
- Restore Stock resets the base frequency cap to Windows-controlled behavior and restores backed-up PPM runtime overrides.
- Reworked the UI and branding for Windows 11 ARM64.
