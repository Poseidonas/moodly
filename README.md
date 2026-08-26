<div align="center">

# Moodly

**A desktop widget that watches the rhythm you work at, and wears the result.**

It counts *how many* keys and clicks happen. It never sees *which* ones.

<br />

[![Download for macOS](https://img.shields.io/badge/Download-macOS-000000?style=for-the-badge&logo=apple&logoColor=white)](https://github.com/Poseidonas/moodly/releases/latest)
[![Download for Windows](https://img.shields.io/badge/Download-Windows-0078D4?style=for-the-badge&logo=windows&logoColor=white)](https://github.com/Poseidonas/moodly/releases/latest)
[![Download for Linux](https://img.shields.io/badge/Download-Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black)](https://github.com/Poseidonas/moodly/releases/latest)

<sub>Free · no account · nothing leaves your machine</sub>

<br />

[![Latest release](https://img.shields.io/github/v/release/Poseidonas/moodly?style=flat-square&color=0a84ff)](https://github.com/Poseidonas/moodly/releases/latest)
[![Downloads](https://img.shields.io/github/downloads/Poseidonas/moodly/total?style=flat-square&color=34c759)](https://github.com/Poseidonas/moodly/releases)
[![Licence](https://img.shields.io/badge/licence-MIT-lightgrey?style=flat-square)](LICENSE)

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
| 🤔 | **working it out** | present but slow, with real gaps — the shape of difficulty |
| 🔥 | **god mode** | well above it, and steady with it |
| 😬 | **stressed** | working in fits and starts |
| 😤 | **irritated** | hard bursts separated by dead stops |
| 😴 | **away** | not at the machine |

---

## How it reads you

Every second, Moodly asks the operating system two questions: *how many* input
events have happened in total, and *how long* since the last one. From the
difference between one second and the next it builds two numbers.

**Intensity** — how much is happening, against your own normal.
Keys count as one, a click as half, a right-click as nearly one (it is sixty
times rarer, so it carries more meaning), a scroll as a tenth, since scrolls
arrive in handfuls.

**Unevenness** — how ragged the last ten seconds were, measured as the spread
of activity divided by its average. Steady work sits near zero; alternating
full-tilt and nothing tops out around one.

Those two numbers decide the mood:

| Pattern | Reading |
| --- | --- |
| well above normal, and even with it | **god mode** |
| above normal, but in bursts with dead stops between | **irritated** |
| around normal, arriving unevenly | **stressed** |
| below half your normal, in regular light touches with gaps | **working it out** |
| below half your normal, steadily | **calm** |
| nothing for ninety seconds | **away** |

Those last two lines matter more than they look.

Reading a long document produces very little input with long gaps in it, which
is mathematically *wildly* uneven — an early version of this widget called that
stress. Below half your normal activity, unevenness is ignored entirely.

But quiet is not one thing. Cognitive-load research describes what happens when
a task gets hard: typing slows, clicking drops, pauses lengthen — and the person
is still very much there. Calling that "calm" would be reading ease into
difficulty. So the quiet is split by how the gaps fall over half a minute:
regular light contact with real gaps between is someone working something out;
steady low input is someone at ease; nothing at all is an empty chair.

### It does not flicker

Working rhythm is naturally uneven. A widget that reacted to every second of it
would change six times a minute and tell you nothing.

A mood has to **hold for 25 seconds** before it is shown, and once shown it
**stays for at least two minutes**. The exception is walking away, which is
reported at once — there is nothing to deliberate about.

### The baseline is yours

Nothing is compared against an average. Moodly learns what **half an hour** of
*your* ordinary work looks like and reports how far the present sits from that.

The same reading means different things for different people, which is the
point: someone who types all day and someone who mostly reads and clicks each
get an honest picture of their own rhythm. It also uses the median rather than
the mean, so one furious afternoon does not redefine your normal.

---

## What it counts, and what it cannot see

This is the part worth reading carefully.

**Moodly reads counters the operating system already keeps.** On macOS that is
`CGEventSourceCounterForEventType` — a function that returns *a number* and
nothing else: how many key presses have occurred since the machine started.

**There is no keystroke log, because there is nothing to log.** The interface
carries no key codes, no characters, no window titles, no clipboard. Not "we
choose not to store it" — it never arrives in the first place.

Concretely:

- **No accessibility permission is requested.** Reading what you type would
  require one on macOS. Moodly never asks, because it never reads.
- **Mouse movement is ignored** on purpose: it is noise, not intent.
- **Nothing is transmitted.** No account, no server, no telemetry, no analytics.
  The app makes exactly one network request in its life, and only when *you*
  press "Check" for updates: a call to GitHub's public releases API.
- **Your settings are one plain JSON file** in your own user folder. Open it,
  edit it, delete it.

### Verifying that for yourself

You do not have to take this on trust. On macOS:

```sh
# Every network connection the app has open — expect none while it runs
lsof -i -a -p $(pgrep -x Moodly)

# Whether it holds accessibility access — it is not in the list
sqlite3 "$HOME/Library/Application Support/com.apple.TCC/TCC.db" \
  "select client from access where service='kTCCServiceAccessibility'"
```

On Windows, Resource Monitor shows the same: no outbound connections. On Linux,
`ss -p | grep -i moodly`.

### On the legality of it

Moodly records nothing that identifies you and transmits nothing anywhere, so
there is no personal data to protect, disclose or delete — the counters it
reads are the same ones any screensaver uses to decide the machine is idle.

That said: this is a tool for watching **your own** rhythm on **your own**
machine. Installing it on someone else's computer to observe them would be a
different thing entirely, and in most places an unlawful one. It has no remote
reporting, no hidden mode and no dashboard for a third party — by design, so it
cannot become that.

---

## It stays out of the way

Measured on an idle machine, with the widget running and visible:

| | |
| --- | --- |
| **Memory** | ~22 MB |
| **CPU** | ~3.5% of one core |
| **Installer** | 3–6 MB |
| **Disk** | ~12 MB |

Built with [Tauri](https://tauri.app) and Rust, using the system's own web
view rather than shipping a browser — which is why the download is measured in
megabytes rather than hundreds of them.

It also sends nothing to itself when nothing changes: the widget is only told
about a new reading when the mood, the learning progress or the activity
actually differs from the last one.

---

## Install

**[Download the latest release](https://github.com/Poseidonas/moodly/releases/latest)**
and pick the file for your system:

| System | File |
| --- | --- |
| macOS, Apple silicon | `Moodly_*_aarch64.dmg` |
| macOS, Intel | `Moodly_*_x64.dmg` |
| Windows | `Moodly_*_x64-setup.exe` |
| Linux | `Moodly_*_amd64.AppImage` or `.deb` |

Neither build is signed with a paid certificate, so the first launch needs a
nudge: on macOS right-click the app and choose **Open**; on Windows, SmartScreen
will warn about an unknown publisher.

### Where it works today

The counters Moodly is built on are a macOS interface, so **the reading works
fully on macOS only**. The Windows and Linux builds install and run, but cannot
count activity yet — and say so plainly rather than showing a mood they have no
basis for.

Windows support means counting raw input arrivals and discarding the payload,
which keeps exactly the same guarantee. That work is ahead.

---

## Settings

Right-click the widget, or use the menu bar icon:

- **launch at login** — starts quietly when you sign in
- **show in the Dock** — off by default; it lives in the menu bar instead
- **display and corner** — which screen, which corner, how far from the edges
- **opacity when quiet** — how faint it goes when nothing notable is happening
- **language** — Ελληνικά or English

Drag it anywhere and it stays there, across restarts. If that display is later
disconnected it returns to its corner, rather than sitting off-screen where you
cannot reach it.

---

## What it will not claim

It does not know how you feel.

Typing fast can mean flow or panic; typing little can mean thinking or giving
up. No counter can tell those apart, and a program that says otherwise is
guessing at you.

What Moodly can honestly say is how you are working, and when that changes —
which is the part you can actually do something about.

---

<div align="center">

MIT © [George Vasiliades](https://github.com/Poseidonas)

</div>
