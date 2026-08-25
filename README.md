<div align="center">

# Moodly

**A desktop widget that watches the rhythm you work at, and wears the result.**

It counts *how many* keys and clicks happen. It never sees *which* ones.

[![Download](https://img.shields.io/github/v/release/Poseidonas/moodly?label=download&style=for-the-badge)](https://github.com/Poseidonas/moodly/releases/latest)
[![Licence](https://img.shields.io/badge/licence-MIT-blue?style=for-the-badge)](LICENSE)

</div>

---

## The idea

You already know when you have had a good hour. You rarely know *why*, and you
almost never notice the hour you spent switching between things without
settling into any of them.

Moodly sits quietly in a corner of your screen and notices the shape of your
work — steady, bursty, or absent — without knowing anything about the work
itself.

| | | |
| :-: | --- | --- |
| 👀 | **learning** | working out what your normal looks like |
| 😌 | **calm** | your usual pace |
| 🔥 | **god mode** | well above it, and steady with it |
| 😬 | **stressed** | working in fits and starts |
| 😤 | **irritated** | hard bursts separated by dead stops |
| 😴 | **away** | not at the machine |

## What it counts, and what it cannot see

This is the part worth reading carefully.

Moodly reads the counters the operating system already keeps: how many key
presses, clicks, scrolls and trackpad gestures have occurred. **Those counters
carry no content.** There is no keystroke log, because there is nothing to log.

That is not a promise about restraint — it is the shape of the thing:

- On macOS it uses `CGEventSourceCounterForEventType`, which returns a number
  and nothing else. The app asks for **no Accessibility permission**, because
  reading content would require one and it never reads content.
- Mouse *movement* is deliberately ignored: it is noise, not intent.
- Nothing is sent anywhere. There is no account, no server, no telemetry.
- Your settings live in one plain JSON file you can read, edit or delete.

## The baseline is yours

Nothing is compared against an average.

Moodly learns what half an hour of *your* ordinary work looks like, and reports
how far the present sits from that. The same reading means different things for
different people, which is the point: someone who types all day and someone who
mostly reads and clicks each get an honest picture of their own rhythm.

It also refuses to read too much into quiet. Reading a long document produces
very little input with long gaps in it — mathematically that looks wildly
uneven, and an earlier version of this widget called it stress. Below half of
your normal activity, unevenness is ignored: quiet is simply quiet.

## It does not flicker

Working rhythm is naturally uneven. A widget that reacted to every second of it
would change six times a minute and tell you nothing.

A mood has to hold for **25 seconds** before it is shown, and once shown it
stays for at least **two minutes**. The exception is walking away, which is
reported at once — there is nothing to deliberate about.

## Install

Download the file for your system from the
[latest release](https://github.com/Poseidonas/moodly/releases/latest):

| System | File |
| --- | --- |
| macOS (Apple silicon) | `Moodly_x.y.z_aarch64.dmg` |
| macOS (Intel) | `Moodly_x.y.z_x64.dmg` |
| Windows | `Moodly_x.y.z_x64-setup.exe` |
| Linux | `moodly_x.y.z_amd64.AppImage` or `.deb` |

**macOS:** open the `.dmg` and drag Moodly to Applications. The first launch
needs right-click → Open, because the build is not signed with a paid Apple
developer certificate.

**Windows:** run the installer. SmartScreen may warn about an unknown
publisher, for the same reason.

## Settings

Right-click the widget, or use the menu bar icon:

- **launch at login** — starts quietly when you sign in
- **show in the Dock** — off by default; it lives in the menu bar instead
- **display and corner** — which screen, which corner, how far from the edges
- **opacity when quiet** — how faint it goes when nothing notable is happening
- **language** — Ελληνικά or English

Drag the widget anywhere and it stays there, across restarts. If that display
is later disconnected, it returns to its corner rather than sitting off-screen
where you cannot reach it.

## What it will not claim

It does not know how you feel.

Typing fast can mean flow or panic; typing little can mean thinking or
giving up. No counter can tell those apart, and a program that says otherwise
is guessing at you.

What Moodly can honestly say is how you are working, and when that changes —
which is the part you can actually act on.

## Built with

[Tauri](https://tauri.app) and Rust, so the whole thing is a few megabytes and
stays out of the way while it runs.

## Licence

MIT © [George Vasiliades](https://github.com/Poseidonas)
