---
name: ai-voice-production
description: Select and evaluate TTS voices, normalize narration scripts, generate audio, validate pronunciation with ASR, and align subtitles or visuals to audio. Use for News Radio experiments and narrated video workflows.
---

# AI Voice Production

## Principles
- Audio first: finalize narration before timing subtitles, visuals or animations.
- Prefer a consistent natural built-in voice; shortlist using language, style, pace, pitch and recognition results, then let the user choose by listening.
- Keep the TTS backend interchangeable. Use API automation where appropriate; retain local TTS as a baseline. Do not purchase services without approval.

## Workflow
1. Preserve the original display script. Create a separate voice script that normalizes numbers, dates, abbreviations, mixed-language terms and ambiguous pronunciations without changing meaning.
2. Select 3–4 voices using identical representative text. Compare naturalness, pronunciation, pacing, pauses and consistency. Save approved voice ID, model, speed and settings.
3. Generate complete narration or coherent segments for long scripts. Preserve segment ordering; avoid discontinuities.
4. Transcribe generated audio with ASR and compare against the normalized script. Flag omissions, substitutions, numbers and names. ASR agreement is not proof of pronunciation quality; listen to samples.
5. If alignment is required, prefer TTS-returned character/word timestamps; otherwise use a dedicated forced aligner with known text and audio. ASR subtitle timing is a fallback, not equivalent to forced alignment. Map normalized text to display text carefully.
6. For video, derive captions and visual cue times from the final audio. Specify visual composition, assets, colors and cue words explicitly. Render frames deterministically, then mux audio; verify duration and sync.

## News Radio pilot
- Inspect existing pipeline and configuration first. Preserve production schedules, output paths and retention behavior.
- Use an identical short Chinese news script and a mixed Chinese/English script for baseline and candidates.
- Baseline: current Kokoro configuration. Candidate: ElevenLabs built-in voice via API if credentials and spending are approved. Other candidates may include Qwen3-TTS, MiniMax or IndexTTS after verifying hardware/API suitability.
- Keep experimental audio and reports separate from production and Jellyfin library. No changes to live systemd timer, production voice, retention or deployment without approval.
- Compare naturalness, names, numbers, English terms, pauses, fatigue during longer listening, duration, generation latency, failures, and actual cost per minute (if available).
- Capture ASR transcript, discrepancies and manual listening notes. Record model/voice/settings and test date.
- For audio-only News Radio, prioritize pronunciation and listening quality. Alignment is optional unless needed for diagnostics, captions or later video reuse.
- Progress from short sample to one complete bulletin only after user approves a voice. Recommend adoption only after comparison; retain rollback to baseline.

## Security and reproducibility
Store API credentials in environment variables or an ignored local .env file, never in repository or logs. Check model licensing, commercial usage, API parameters, current costs and hardware requirements before implementation. Do not claim tests passed unless executed.

## Provenance
Derived from user-provided transcript of 亚里-科技 AI 分享, “AI 配音怎么选？我用的是哪家：原理、选择、实操全流程” (2026-10-27). The News Radio pilot, security and acceptance criteria are adaptations, not claims that the original video tested them. Provider claims and rankings are not independently verified.
