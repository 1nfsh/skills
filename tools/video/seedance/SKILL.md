---
name: seedance
description: "Generate videos with ByteDance Seedance 2.0 models via inference.sh CLI. Models: Seedance 2 T2V, Seedance 2 I2V, Seedance 2 R2V. Capabilities: text-to-video, image-to-video, reference-to-video, synchronized audio, quality/fast modes, 480p/720p. Use for: social media videos, music videos, product demos, animated content, AI video with sound. Triggers: seedance, seedance 2, bytedance video, seedance t2v, seedance i2v, seedance r2v, video with audio, seedance 2.0, bytedance seedance"
allowed-tools: Bash(belt *)
---

# Seedance 2.0 Video Generation

Generate videos with synchronized audio using ByteDance's Seedance 2.0 models via [inference.sh](https://inference.sh) CLI.

## Quick Start

> Requires inference.sh CLI (`belt`). [Install instructions](https://raw.githubusercontent.com/inference-sh/skills/refs/heads/main/cli-install.md)

```bash
belt login

belt app run falai/seedance-2-t2v --input '{
  "prompt": "a jazz band performing in a dimly lit club",
  "generate_audio": true
}'
```


## Seedance 2.0 Models

| Model | App ID | Best For |
|-------|--------|----------|
| Seedance 2 T2V | `falai/seedance-2-t2v` | Text-to-video with audio |
| Seedance 2 I2V | `falai/seedance-2-i2v` | Animate images with audio |
| Seedance 2 R2V | `falai/seedance-2-r2v` | Reference images/videos/audio to video |

All models support **quality** and **fast** modes, 480p/720p resolution, and synchronized audio generation.

## Examples

### Text-to-Video with Audio

```bash
belt app run falai/seedance-2-t2v --input '{
  "prompt": "ocean waves crashing on rocks during a storm, dramatic cinematic shot",
  "generate_audio": true,
  "duration": 10,
  "aspect_ratio": "16:9"
}'
```

### Fast Mode (Cheaper)

```bash
belt app run falai/seedance-2-t2v --input '{
  "prompt": "a butterfly landing on a flower in slow motion",
  "mode": "fast",
  "generate_audio": true
}'
```

### Image-to-Video

Animate a still image into a video:

```bash
belt app run falai/seedance-2-i2v --input '{
  "image": "https://your-image.jpg",
  "prompt": "gentle camera movement, leaves rustling in the wind",
  "generate_audio": true
}'
```

### Image-to-Video with Start and End Frames

```bash
belt app run falai/seedance-2-i2v --input '{
  "image": "https://start-frame.jpg",
  "end_image": "https://end-frame.jpg",
  "prompt": "smooth transition between scenes",
  "generate_audio": true
}'
```

### Reference-to-Video

Use reference images, videos, or audio in your prompt with `@Image1`, `@Video1`, `@Audio1` placeholders:

```bash
belt app run falai/seedance-2-r2v --input '{
  "prompt": "A person who looks like @Image1 is walking through a garden",
  "images": ["https://portrait.jpg"],
  "generate_audio": true
}'
```

### Multi-Reference

```bash
belt app run falai/seedance-2-r2v --input '{
  "prompt": "@Image1 and @Image2 are having a conversation at a cafe",
  "images": ["https://person1.jpg", "https://person2.jpg"],
  "generate_audio": true
}'
```

### Reference with Audio

```bash
belt app run falai/seedance-2-r2v --input '{
  "prompt": "A musician who looks like @Image1 is performing @Audio1",
  "images": ["https://musician.jpg"],
  "audios": ["https://music.mp3"],
  "generate_audio": true
}'
```

## Pricing

| Mode | 720p | 480p |
|------|------|------|
| Quality | ~$0.30/sec | ~$0.13/sec |
| Fast | ~$0.24/sec | ~$0.11/sec |

## Parameters (T2V)

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `prompt` | string | required | Text description of the video |
| `generate_audio` | boolean | false | Generate synchronized audio |
| `duration` | enum | - | Duration in seconds (4–10) |
| `aspect_ratio` | enum | - | 16:9, 9:16, 1:1, 4:3, 3:4 |
| `resolution` | enum | - | 480p or 720p |
| `mode` | enum | quality | quality or fast |
| `seed` | integer | random | Reproducible generation |

## Parameters (I2V)

Same as T2V plus:

| Parameter | Type | Description |
|-----------|------|-------------|
| `image` | file | Starting frame image (required) |
| `end_image` | file | Optional ending frame |

## Parameters (R2V)

Same as T2V plus:

| Parameter | Type | Description |
|-----------|------|-------------|
| `images` | array | Reference images (@Image1, @Image2, ...) |
| `videos` | array | Reference videos (@Video1, @Video2, ...) |
| `audios` | array | Reference audio (@Audio1, @Audio2, ...) |

## Search Seedance Apps

```bash
belt app list --search "seedance"
```

## Related Skills

```bash
# Full platform skill (all 250+ apps)
npx skills add inference-sh/skills@infsh-cli

# All video generation models
npx skills add inference-sh/skills@ai-video-generation

# Google Veo
npx skills add inference-sh/skills@google-veo

# Image generation (for image-to-video)
npx skills add inference-sh/skills@ai-image-generation

# AI avatars & lipsync
npx skills add inference-sh/skills@ai-avatar-video
```

Browse all video apps: `belt app list --category video`

## Documentation

- [Running Apps](https://inference.sh/docs/apps/running) - How to run apps via CLI
- [Streaming Results](https://inference.sh/docs/api/sdk/streaming) - Real-time progress updates
- [Content Pipeline Example](https://inference.sh/docs/examples/content-pipeline) - Building media workflows
