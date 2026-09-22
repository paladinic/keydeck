# keydeck

**A multitrack MIDI recorder and piano-roll sequencer in a single HTML file.**

Type on your computer keyboard, record to as many tracks as you like, edit the
notes in a piano roll, and export a standard `.mid` or a rendered `.wav`.

[![License: MIT](https://img.shields.io/badge/License-MIT-black.svg)](LICENSE)
![No dependencies](https://img.shields.io/badge/dependencies-0-black.svg)
![Single file](https://img.shields.io/badge/files-1-black.svg)
![No build step](https://img.shields.io/badge/build%20step-none-black.svg)

**[▶ Try it now](https://paladinic.github.io/keydeck/)** — or
**[download `index.html`](https://raw.githubusercontent.com/paladinic/keydeck/main/index.html)**
(right-click → Save as) and double-click it. That's the whole install.

---

## Portability is the feature

keydeck is one file. Not "one file plus a bundler that produces one file" — the
file in this repository is the file that runs. Open it in an editor and you can
read every byte that executes.

| | |
|---|---|
| **Dependencies** | None. No npm, no CDN, no framework, no font, no icon pack. |
| **Build step** | None. What you clone is what you run. |
| **Network** | Never. There is no `fetch`, no `XMLHttpRequest`, no remote `src`. Turn off your Wi-Fi. |
| **Storage** | None. No cookies, no `localStorage`. Nothing is left on the machine. |
| **Telemetry** | None. |
| **Install** | Double-click the file. |

Everything is inline: the synthesiser, the sequencer, the MIDI file writer, the
WAV encoder, the SVG icons, even the favicon. Mail it to yourself, put it on a
USB stick, drop it in a locked-down corporate browser, run it on a plane, keep
it on a Raspberry Pi with no internet. It works the same everywhere.

> **One caveat:** connecting a **hardware** MIDI keyboard needs the Web MIDI
> API, and browsers only expose that on a secure page. Opened straight from
> disk (`file://`) everything else works — the QWERTY keyboard, the piano roll,
> playback, and both exports — but hardware input stays greyed out. Use the
> [hosted version](https://paladinic.github.io/keydeck/), or serve the folder
> locally: `python -m http.server` then open `http://localhost:8000`.

---

## What it does

**Input**
- Play notes on the QWERTY keyboard — two full octaves laid out like a piano
- Draw, drag, and resize notes directly in the piano roll
- Record from a hardware MIDI keyboard, sustain pedal included
- Import an existing `.mid` file

**Sequencing**
- Unlimited tracks, each with its own instrument, colour, volume, mute and solo
- Metronome click and count-in
- Loop range, snap/quantize (1/16 through bar, plus triplets)
- Time signatures from 2/4 to 12/8, tempo 40–240 BPM
- Select, copy, cut, paste, quantize a selection, undo/redo

**Sound**
- A built-in synthesiser with two engines: additive/subtractive **oscillators**
  and **FM**
- Ten instruments out of the box — piano, electric piano, marimba, organ,
  plucked guitar, sub bass, strings, warm pad, synth lead, and a drum kit
- A full instrument editor with live waveform and envelope scopes: oscillator
  stacks, ADSR, resonant low-pass filter with key tracking and envelope sweep,
  vibrato, reverb send
- Send to external gear over MIDI out instead of, or alongside, the internal synth

**Output**
- Export a standard MIDI file, whole song or a bar range
- Render to WAV offline at 44.1 or 48 kHz, faster than real time
- Save and reload the whole project as plain JSON, custom instruments included

---

## The keyboard

Two rows, one octave apart. The lower row starts at the current octave; the
upper row starts one octave above it.

```
   black:   2   3       5   6   7       9   0
   white: Q   W   E   R   T   Y   U   I   O   P     ← octave + 1

   black:   S   D       G   H   J       L   ;
   white: Z   X   C   V   B   N   M   ,   .   /     ← current octave
```

| Key | Action |
|---|---|
| `Space` | Play / stop |
| `Enter` | Record |
| `Esc` | Stop |
| `Home` | Go to start |
| `Shift` (hold) | Sustain pedal |
| `-` / `=` | Octave down / up |
| `↑` / `↓` | Arm previous / next track |
| `Ctrl`+`Z` / `Ctrl`+`Shift`+`Z` | Undo / redo |
| `Ctrl`+`C` / `X` / `V` | Copy / cut / paste at cursor |
| `Ctrl`+`A` / `Ctrl`+`D` | Select all in track / deselect |
| `Del` | Delete selection |
| `Alt`+`F` / `T` / `P` / `H` | Open the File / Track / Transport / Help menu |

In the piano roll: **drag** to move a note, **shift+drag** to select an area,
**right-click** to erase, **Ctrl+wheel** to zoom.

---

## Getting started

1. Open keydeck.
2. **Track → Add track** and pick an instrument.
3. Press **Record** (or `Enter`), wait for the count-in, and play.
4. Press `Space` to hear it back. Fix anything by dragging notes in the roll.
5. **File → Export MIDI** or **Export WAV**.

Your work is never saved automatically — keydeck writes nothing to your disk
unless you ask. Use **File → Save project** to keep a `.json` you can reopen later.

---

## Browser support

Chrome, Edge, Firefox and Safari all run keydeck. It relies on the Web Audio
API for sound and `OfflineAudioContext` for WAV rendering, both of which have
been standard for years.

Web MIDI (hardware keyboards and MIDI out) works in Chrome, Edge and Firefox,
on a secure page. Safari does not implement Web MIDI; everything else still works.

---

## Contributing

Issues and pull requests are welcome. The one rule that shapes everything else:
**it stays a single file with no dependencies and no build step.** See
[CONTRIBUTING.md](CONTRIBUTING.md) for how the file is laid out and how to test
a change.

---

## License

[MIT](LICENSE) © Claudio Paladini
