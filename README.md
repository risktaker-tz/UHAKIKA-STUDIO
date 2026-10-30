# UHAKIKA STUDIO
All-in-one, fully-free AI video generation studio — one prompt in, professional video out
(documentaries, animations, explainers) in any language, at $0 software cost.

This monorepo contains **18 upstream projects merged with their full git history**
(via `git subtree`) — every file, every commit, every branch, every tag preserved.

## Studio map
| Directory | Engine | Role in the studio |
|---|---|---|
| `core/video-agent` | MoneyPrinterTurbo fork | Core pipeline engine: script -> TTS -> subtitles -> visuals -> FFmpeg assembly |
| `engines/tts-kokoro` | Kokoro-82M | Fast CPU narration, 8 languages (Apache-2.0) |
| `engines/tts-cosyvoice` | CosyVoice 3 | Zero-shot voice cloning (3 s) + emotion control (Apache-2.0) |
| `engines/tts-chatterbox` | Chatterbox V3 | Expressive multilingual TTS, 23 languages (MIT) |
| `engines/tts-gptsovits` | GPT-SoVITS | Few-shot signature narrator training (MIT) |
| `engines/tts-piper` | Piper | Ultra-light 35+ language TTS fallback (MIT) |
| `engines/music-acestep` | ACE-Step v1.5 | Music generation from prompt, 50+ language lyrics (Apache-2.0) |
| `engines/sfx-stableaudio` | Stable Audio Open | SFX, ambience, loops (Community License) |
| `engines/video-wan22` | Wan 2.2 | Text/image-to-video animation of shots (Apache-2.0) |
| `engines/video-ltx2` | LTX-2 | Open-weights video+audio generation (conditional) |
| `engines/anim-manim` | Manim CE | Code-driven math/explainer animations (MIT) |
| `engines/anim-motioncanvas` | Motion Canvas | Code-driven motion graphics (MIT) |
| `engines/image-flux` | FLUX.1-schnell | Fast AI stills (Apache-2.0) |
| `engines/image-qwen-image` | Qwen-Image | AI stills with multilingual in-image text (Apache-2.0) |
| `engines/gpu-comfyui` | ComfyUI | GPU worker hub (Kaggle/Colab free tier) (GPL-3.0) |
| `engines/asr-whisperx` | WhisperX | Word-level subtitle alignment + diarization (BSD-4) |
| `engines/asr-fasterwhisper` | faster-whisper | 99-language ASR, CPU (MIT) |
| `engines/edit-autoeditor` | auto-editor | Automatic rough-cut editing (public domain) |

## Pipeline
```
PROMPT -> Studio Brain (LLM script + shot list, any language)
       -> Visuals:  stock APIs + FLUX/Qwen stills + Wan2.2 motion + Manim explainers
       -> Voice:    language router: Kokoro / CosyVoice / Chatterbox / Piper
       -> Audio:    ACE-Step score + Stable Audio SFX + FFmpeg ducking/loudnorm
       -> Text:     WhisperX word-level -> styled ASS subtitles
       -> Edit:     auto-editor + FFmpeg/MoviePy assembly -> QC -> final MP4
```

## Ref conventions
- Each engine keeps its **full commit history** (21,000+ commits total): find an engine's merge with `git log --grep "UHAKIKA: merge"` then browse its original history with `git log <merge-commit>^2`
- Original feature branches: `legacy/<engine>/<branch>`
- Original tags: `<engine>/<tag>`
- License per directory: see `LICENSES.md` and each directory's LICENSE file.
