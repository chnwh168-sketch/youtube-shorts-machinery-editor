# YouTube Shorts Machinery Editor

A Codex skill for turning local construction-machinery and industrial-equipment footage into short-form videos with matching YouTube, Instagram, and LinkedIn publishing copy.

## What It Enforces

- Clear, stable source footage at 720p or higher, with 1080p preferred.
- No reuse of source time ranges recorded in the material-use CSV files.
- One product subtype per video and product-focused close-ups when useful.
- Orientation-aware 1080 output, H.264 video, AAC audio, and 15-45 second duration.
- A visible one-second English cover starting at timestamp zero.
- Pale-yellow `#FFF7C7` 80px cover titles on a centered translucent black panel.
- Intermittent English captions in the safe area without caption backgrounds.
- No background music and silent AAC by default for batch work.
- A Word publishing-copy document and exact source-range CSV for every batch.

## Install

Place this repository at:

```text
~/.codex/skills/youtube-shorts-machinery-editor
```

Restart Codex after installation so the skill is rediscovered.

## Local Configuration

This is a personalized operational skill. Before using it on another machine, update the local material, output, cover-preset, and font paths in `SKILL.md`. The current configuration expects the video workspace at `/Volumes/video`.

## Requirements

- Codex desktop or CLI with local filesystem access
- FFmpeg and FFprobe
- A Word-document generation environment for `.docx` publishing copy
