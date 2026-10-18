# Windows shutdown returned to sign-in instead of powering off

**Status:** Resolved and retested by the user on 2026-10-18.

## Symptom

Selecting Start > Power > Shut down blacked out the display for a few seconds, then returned to the Windows sign-in screen. A normal Restart took roughly 50 seconds. The user had checked the hardware wiring and believed it was correct.

## Relevant system details

- Windows registry reported ProductName `Windows 10 Pro`, EditionID `Professional`, DisplayVersion `26H2`, build `26300.9711`.
- Microsoft identifies the 26300 build series as Windows 11, version 26H2. The ProductName string therefore did not reliably identify the installed Windows generation. The available evidence cannot establish whether the installation was Tiny11 or another modified image.
- Motherboard: MSI PRO Z890-S WIFI (MS-7E54); BIOS 1.A80, dated 2025-06-20.
- Active power plan: High performance.

## Evidence collected

Before the fix:

- The Start menu power-button action was Sleep on AC and DC (`UIBUTTON_ACTION` index 0).
- Fast Startup was enabled (`HiberbootEnabled=1`).
- Automatic restart after a system failure was enabled (`AutoReboot=1`).
- The System log recorded Event 1074 from `StartMenuExperienceHost.exe` with shutdown type `power off` for the failed attempt. The log had no subsequent Event 6006 (Event Log stopped) or Kernel-General Event 13 (OS shutting down), and the latest boot event remained earlier. This showed Windows received a power-off request, but that attempt did not complete as a clean shutdown.
- No matching Event 41, 1001, or 6008 was found for that attempt, so the available log evidence did not establish a bugcheck or unexpected reboot.

## Changes made

1. Changed the Start menu power-button action from Sleep to Shut down for both AC and DC power. Verified with `powercfg /query SCHEME_CURRENT SUB_BUTTONS` (current indices 2 and 2).
2. Disabled Fast Startup by setting `HKLM\SYSTEM\CurrentControlSet\Control\Session Manager\Power\HiberbootEnabled` to DWORD `0`. Verified the registry value after the elevated change.
3. Issued one normal Windows shutdown test. The user then retested and confirmed that Shut down now displays the expected Windows shutdown message, takes a few seconds, and powers the PC off. No forced app closure was used.

## Conclusion and caveat

The shutdown problem is resolved in the user's retest. The repair changed both the Start menu power-button action and Fast Startup before the successful test, so the evidence does not isolate which setting was individually causal. Fast Startup's hybrid shutdown path was a strong suspect, and the original Sleep action was a confirmed misconfiguration. There is no evidence tying the fault to Tiny11 or to the nationality of an image creator.

## References

- Microsoft, Fast Startup and shutdown troubleshooting: https://learn.microsoft.com/en-us/troubleshoot/windows-client/setup-upgrade-and-drivers/fast-startup-causes-system-hibernation-shutdown-fail
- Microsoft, Windows 11 release information: https://learn.microsoft.com/en-us/windows/release-health/windows11-release-information
- Microsoft, Tiny11 Builder repository (for identifying the known NTDEV project, not as evidence this PC used it): https://github.com/ntdevlabs/tiny11builder

