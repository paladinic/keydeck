# Contributing to keydeck

Thanks for taking a look. keydeck is small enough that one person can hold all
of it in their head, and the goal is to keep it that way.

## The one hard rule

**keydeck is a single self-contained `index.html` with no dependencies and no
build step.** Portability is the product, not an implementation detail. A change
that is excellent in every other way will still be declined if it breaks this.

Concretely, a pull request must not add:

- an npm package, a CDN `<script>`, a web font, or any other external resource
- a bundler, transpiler, minifier, preprocessor, or any other build step
- a second file that `index.html` needs in order to run
- a network request of any kind
- cookies, `localStorage`, or anything else written to the user's machine
  without them choosing to save

If you need a helper function, write it inline. If you need an icon, draw it as
inline SVG — that is how every existing icon works.

Everything else is open for discussion: new instruments, new engines, editing
tools, better timing, accessibility, bug fixes.

## How the file is laid out

Roughly 3,300 lines in three parts: styles, markup, then script. The script is
divided by banner comments, so the fastest way to navigate is to search for
them. Line numbers below are for v0.9.5 and will drift — the banners won't.

```
     1   <style>          Win95 chrome: bevels, menus, toolbars, dialogs
   243   <body>           menu bar, toolbars, workspace, piano, modals
   571   <script>
   576     audio engine        oscillator + FM voices, drums, reverb
   836     state               tracks, notes, project state
  1002     undo                snapshot stack
  1034     transport           clock, playback scheduling, click, count-in
  1165     note input          note on/off, held-note recording
  1241     external MIDI       Web MIDI in/out, latency compensation
  1423     computer keyboard   QWERTY key map, global shortcuts
  1526     clipboard           copy / cut / paste
  1568     menus               menu bar actions
  1623     transport UI        play/stop/record buttons, tempo, loop
  1734     tracks UI           track headers, arm, mute, solo
  1832     canvas              piano roll, ruler, gutter drawing and hit-testing
  2336     paint loop          requestAnimationFrame render
  2389     on-screen piano     clickable keyboard
  2444     file i/o            project JSON, MIDI export
  2636     MIDI import         standard MIDI file parser
  2774     wav export          OfflineAudioContext render + WAV encoder
  2879     instrument editor   patch editing, waveform scopes
  3234     boot                startup
```

A few things worth knowing before you edit:

- **Time is measured in beats**, as floating-point quarter notes from the start
  of the song. Pixels and seconds are derived from beats, never the reverse.
- **Playback is scheduled ahead of the audio clock**, not driven by
  `setInterval`. If you add a sound, schedule it against `ctx.currentTime`.
- **Recording is latency-compensated.** Incoming notes are stamped earlier by a
  measured offset so that what you played lands where you heard it. Anything
  that timestamps notes needs to go through the same path.
- **Undo is snapshot-based.** Call `snapshot()` *before* mutating state, not after.
- **The project format is versioned** (`v: 6`). If you change what gets saved,
  bump the version and keep the loader able to read older files.

## Testing a change

There is no test suite — the app is the test. Before opening a pull request,
open the file and confirm at least this much still works:

1. Add a track, record a few bars from the QWERTY keyboard, play it back.
2. Draw, drag, resize, and right-click-erase a note in the piano roll.
3. Undo and redo both of those.
4. Loop a range with the click and count-in on.
5. Export a `.mid` and open it in something else (a DAW, or re-import it).
6. Export a `.wav` and listen to it.
7. Save a project, reload the page, and open it again.
8. Open the instrument editor, change a parameter, and hear it apply.

If your change touches MIDI hardware, test it over `http://localhost` — Web MIDI
is blocked on `file://`.

Please check it in more than one browser if you can. Chrome and Firefox differ
in useful ways, particularly around audio timing.

## Style

Match what's already there rather than importing habits from elsewhere:

- 2-space indent, semicolons, double quotes
- Plain browser JavaScript — no modules, no TypeScript, no JSX
- Short comments that explain *why*, not *what*
- Keep the Win95 look. The bevels, the 11px Verdana, the square corners and the
  LCD readout are the point, not an accident.

## Reporting bugs

Open an issue with your browser and OS, what you did, what happened, and what
you expected. If it involves MIDI hardware, name the device. If it involves a
specific project, attach the saved `.json` — it's plain text and small.

## Pull requests

Keep them focused: one change per pull request. Say what you changed and how
you tested it. Since there's no CI to catch regressions, a short note on what
you exercised by hand is genuinely useful.
