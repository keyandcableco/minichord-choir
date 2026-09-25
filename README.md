# Minichord choir

A browser page that plays each chord voice of the [minichord](https://github.com/BenjaminPoilve/minichord) through its own instrument, using the minichord's MPE output. One chord button, four timbres: a voice-led line keeps its instrument while it glides.

**Open it:** https://keyandcableco.github.io/minichord-choir/

## What it does

- **A sampled choir.** Recorded "aah" and "ooh" choirs from three free soundfonts (Musyng Kite, FatBoy and FluidR3), looped seamlessly, with the vowel menu crossfading between them. See [samples/README.md](samples/README.md) for sources and licenses.
- **Synthesized singers.** Choir section, solo singer and monk voices built from five-formant bass, tenor, alto and soprano vowel tables, with a glottal source, a few singers per section slightly out of step, pitch drift, a scoop into each note and breath. Pick the vowel, or sing "Kyrie eleison" one syllable per chord.
- **Four voices, four instruments.** Each MPE member channel (2 to 5 on the chord port) gets its own timbre, level and pan. Voices can also be assigned by pitch, lowest note to highest.
- **A live pitch trace** draws each voice as its own line, so glides and voice leading are visible.
- **Device controls over sysex:** MPE output, voice leading and its range, glide time and temperament, read back from the minichord so the page shows its real state. Changes are live; save the preset in [Sound Lab](https://keyandcableco.github.io/minichord-soundlab/) to keep them.
- **Voice motion readout:** how far each voice moved at the last chord change, with a running average, to compare voice leading on and off.
- **MPE MIDI recorder:** saves what the minichord sends as a MIDI file with every per-voice bend intact, for an MPE-aware host.
- **Test buttons** that play a chord and a voice-led glide without a minichord attached.
- **Two looks:** Scriptorium, a chant-book page with rubric staff lines and square neumes, and Workbench, a plain one. Plus a cathedral reverb, since it's a choir.

## Requirements

- Chrome, Edge or Opera on a computer or Android. Safari and iOS browsers have no Web MIDI.
- Allow MIDI access, including system-exclusive messages, when the browser asks. Without sysex the page still plays but can't change settings on the minichord.
- Firmware with MPE output (address 110). Voice leading (111 and 112) and the 19- and 31-EDO temperaments need the unofficial `test-allFeatures` build from [keyandcableco/minichord](https://github.com/keyandcableco/minichord).

## Running it locally

It's a static page. Serve the folder and open it (the choir samples won't load from a plain file):

```
python3 -m http.server 8000
```

then visit http://localhost:8000/.

## Notes

- The page listens to the minichord's chord port (Port 1) by default. The harp port declares its own MPE zone on the same channel numbers, so mixing both ports would put harp strings into the chord voices.
- Any sysex write marks a controller as connected, which pauses the minichord's autosave of knob moves until it is unplugged, the same as with Sound Lab.
- If audio stutters on an older computer, choose "Light" in the performance menu, and turn the reverb down.
