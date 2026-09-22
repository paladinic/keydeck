# Changelog

All notable changes to keydeck are recorded here. The format follows
[Keep a Changelog](https://keepachangelog.com/en/1.1.0/), and keydeck uses
[semantic versioning](https://semver.org/spec/v2.0.0.html).

The version is shown in the browser tab title and under **Help → About**.

## [Unreleased]

### Added
- Open-source repository scaffolding: README, MIT license, contributing guide,
  issue and pull request templates.
- A screenshot and a standalone `docs/logo.svg`, the latter drawn with exactly
  the same geometry as the inline favicon so the tab icon and the repo mark are
  one drawing.
- GitHub Pages deployment, so hardware MIDI keyboards work without setting up a
  local server.
- A CI check that fails the build if `index.html` gains an external dependency,
  a network call, browser storage, or a build step.

## [0.9.5] — 2026-09-22

First public release.

### Added
- Multitrack recording from the computer keyboard, with count-in and metronome.
- Piano-roll editing: draw, drag, resize, and erase notes; area select; copy,
  cut, paste; quantize a selection; undo and redo.
- A built-in synthesiser with two engines — oscillator stacks and FM — plus a
  resonant low-pass filter with key tracking, ADSR, vibrato, and a reverb send.
- Ten instruments: piano, electric piano, marimba, organ, plucked guitar, sub
  bass, strings, warm pad, synth lead, and a drum kit.
- An instrument editor with live single-cycle and full-note scopes.
- Web MIDI input with sustain-pedal support and measured latency compensation,
  and MIDI output with per-track channels (drums on channel 10).
- Standard MIDI file import.
- Export to standard MIDI file and to WAV, whole song or a bar range.
- Project save and load as plain JSON, including edited instruments.
- Loop range, snap from 1/16 to a bar including triplets, time signatures from
  2/4 to 12/8, and tempo from 40 to 240 BPM.

[Unreleased]: https://github.com/paladinic/keydeck/compare/v0.9.5...HEAD
[0.9.5]: https://github.com/paladinic/keydeck/releases/tag/v0.9.5
