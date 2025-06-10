# deepsleep-docx
# SilentCore

Minimal kernel-level trickery to let your Windows box enter a **deep sleep** state that’s not quite suspend, not quite hibernate. Just off enough to kill noise, just on enough to bounce back in under 200ms.

## What It Does

- Hooks `NtSetSystemPowerState()` without wrecking things
- Drops all non-vital HAL threads
- Compresses RAM snapshot to temp RAMDisk
- Turns off GPU context, keeps RTC ticking
- Halts background schedulers, telemetry gets ghosted
- Keeps machine “asleep” without fans, disk, or net activity (except ping)

## Why

Because Sleep and Hibernate suck. One’s too light, the other’s molasses. This hits the sweet spot for power users, coders, weirdos who work at 3AM and want the machine back before their coffee brews.

## Requirements

- Windows 10/11 with Secure Boot off
- VT-x / AMD-V enabled
- Rust toolchain (driver-side)
- WDK + custom-signed driver (yeah, annoying, deal with it)
- 8GB+ RAM or it’ll choke

## How To Use (kinda)

You build the driver, load it (manually, obviously), and run the provided control script. There’s no UI. If you need UI, this ain’t for you.

## Risks

- It’s kernel stuff. Don’t cry if your machine reboots sideways.
- Probably voids your laptop warranty.
- Not tested on anything but 3 personal builds, so..

## Why It’s Called SilentCore

Because that’s what it does. Strips Windows down to its silent bones while keeping just enough alive to come back like nothing happened.



No PRs unless you know what IRQL is and why Deferred Procedure Calls exist.

