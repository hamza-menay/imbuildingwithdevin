# imbuildingwithdevin

An automated demo recorder for software demos. It turns a single recorded pass through a web app into a narrated demo video, and checks the result before export.

## What works today

- Records one continuous pass through a web app with deterministic frame capture. Every frame is hashed, and the encoder holds each frame for a whole number of output frames.
- Places generated narration over the recording and aligns it to the voice timing.
- Checks the export before delivery:
  - Audio: compares the movie audio with the source narration waveform, per narration span.
  - Frames: flags single-frame flashes by comparing each frame with its neighbours.
  - Media: confirms one video and one audio stream, the frame count, a clean decode, and no unexpected silence.
- Writes a report when a check fails.

## Planned: repair loop

When a check fails, an agent would:

1. Identify the failing chapter.
2. Apply one fix from a fixed set: shift a timing span, rewrite one narration line, or reopen a UI panel.
3. Rerun from that chapter's checkpoint.
4. Stop after a fixed number of tries and leave a report.

The repair loop is not built yet. Today the checks run by hand, and a failed check stops the run.
