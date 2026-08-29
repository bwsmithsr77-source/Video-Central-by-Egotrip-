# Video Central — by Egotrip

A browser-based video editor for cutting music videos, commercial ads, and podcast episodes — no upload, no install, no account. Everything runs client-side in the browser using ffmpeg.wasm.

**Live app:** _add your GitHub Pages link here once Pages is enabled_

Full setup instructions for getting this live on GitHub Pages are in [SETUP.md](SETUP.md).

## What it does

- **Projects** — create a project as a Music Video, Commercial Ad, or Podcast; each one keeps its own clips, audio, timeline, and settings
- **Clip library** — upload MP4, WebM, MOV, AVI, or MKV clips; auto-generated thumbnails; trim in/out points per clip
- **Audio system** — upload MP3, WAV, OGG, FLAC, or AAC; tag tracks as music, voiceover, speech, or SFX; adjust volume and start offset; layer multiple tracks
- **Timeline** — drag clips to reorder; cycle transitions (cut / fade / dissolve) between clips
- **Type-specific presets**
  - Music Video: beat-synced cut toggle
  - Commercial Ad: 15s / 30s / 60s duration presets, brand text overlay
  - Podcast: waveform visualization for audio-only projects
- **Export** — renders to 854×480 MP4 (H.264 + AAC) entirely in your browser and downloads directly to your device

## How to use it

1. Open the live app link (or `index.html` locally in a browser)
2. Create a new project and pick a type
3. Upload clips and/or audio
4. Trim clips, drag them into the timeline in order, set transitions
5. Add audio tracks and set volume/offset
6. Hit **Export** — it renders locally and gives you a download

## Notes / current limitations

- Everything lives in the browser tab. Nothing is uploaded to a server, but that also means projects aren't saved between sessions — treat each visit as one editing sitting.
- Fade/dissolve transitions render as a quick fade-in/out on each clip rather than a true crossfade blend, to keep rendering fast and reliable in-browser.
- Brand text overlays (Commercial Ad preset) show live in the preview but are not yet burned into the exported MP4.
- Export time scales with clip length and count — longer projects take longer to render since it's all happening on-device.

## Tech

Single-file HTML/CSS/JS app. Video/audio decoding and export handled by [ffmpeg.wasm](https://github.com/ffmpegwasm/ffmpeg.wasm), loaded from CDN. No backend, no build step — deployable as static files anywhere (GitHub Pages, Netlify, S3, etc.).

## Roadmap ideas

- Burn brand text overlays into the exported video
- True crossfade transitions
- Save/restore projects (would need a persistence layer, since raw video files can't be stored in-browser long term)
- Beat-detection for auto-syncing cuts to music
