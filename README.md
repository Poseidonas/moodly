<div align="center">

# Moodly

**A desktop widget that watches the rhythm you work at, and wears the result.**

</div>

---

## What it does

Moodly sits quietly in a corner of your screen. It notices how you are working
— steadily, in bursts, or not at all — and shows it, without ever knowing what
you are working on.

| | |
| --- | --- |
| 👀 | learning what your normal looks like |
| 😌 | working at your usual pace |
| 🔥 | well above it, and steady with it |
| 😬 | working in fits and starts |
| 😤 | hard bursts separated by dead stops |
| 😴 | away from the machine |

## What it counts, and what it cannot see

Moodly counts **how many** keys and clicks happen. It never sees **which** ones.

This is not a promise about restraint — it is how the program is built. macOS
publishes per-event-type counters that any process may read, and those counters
carry no content. There is no keystroke log because there is nothing to log,
and the app asks for no accessibility permission at all.

Nothing is sent anywhere. Everything stays on your machine, in a plain JSON
file you can read or delete.

## The baseline is yours

Nothing is measured against an average. Moodly learns what half an hour of
*your* ordinary work looks like and reports how far the present sits from that.
Someone who types all day and someone who mostly reads and clicks each get an
honest reading of their own rhythm.

A mood has to hold for twenty-five seconds before it appears, and stays for at
least two minutes afterwards. Working rhythm is naturally uneven; a widget that
reacted to every second of it would flicker rather than tell you anything.

## What it will not claim

It does not know how you feel. It knows how you work, and when that changes.

## Install

Download the latest release below, open the `.dmg`, and drag Moodly to
Applications.

Windows and Linux builds are planned.

## Settings

Right-click the widget, or use the menu bar icon:

- launch at login
- which display and corner it sits in, and how far from the edges
- how faint it goes when nothing notable is happening
- language — Ελληνικά or English

Drag it anywhere and it stays there, across restarts. If that display is later
disconnected, it returns to its corner rather than sitting off-screen.

## Licence

MIT © [George Vasiliades](https://github.com/Poseidonas)
