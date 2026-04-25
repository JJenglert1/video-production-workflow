# Video Production with AI — Two Paths

This repo originally linked to a **Remotion-based** video production workflow. Since then, a second approach has emerged using **HyperFrames** — and both are worth knowing about. Use this page to pick your path.

---

## Choose Your Path

### Path 1 — Remotion (React-based)
**Best if:** You're comfortable with React, want a mature ecosystem, or your team already uses JavaScript frameworks.

> **[Video Production Workflow (this repo)](https://github.com/JJenglert1/video-production-workflow)**

Remotion is a React-based video framework that's been around for five years. It has a large community, excellent documentation, and a proven track record in production. You build videos as React components, and it renders them to MP4 using a headless Chrome-based pipeline.

### Path 2 — HyperFrames (HTML-based, newer)
**Best if:** You want a smoother editing experience, prefer HTML/CSS over React, or want tighter AI-agent integration out of the box.

> **[Media Production Kit (HyperFrames)](https://github.com/JJenglert1/media-production-kit)**

HyperFrames is a newer HTML-based platform backed by HeyGen. It works similarly to Remotion — you write animated code files that render to MP4 — but it has a better user experience within the actual editor. It's designed from the ground up for AI-assisted video production, with a live preview studio and a library of pre-built blocks.

---

## Side-by-Side Comparison

| | Remotion | HyperFrames |
|---|---|---|
| **Built on** | React (JSX/TSX) | HTML + GSAP |
| **Backed by** | Open source / Remotion GmbH | HeyGen |
| **Maturity** | ~5 years, large community | Newer, growing fast |
| **Editor experience** | Good (Remotion Studio) | Better UX in the live editor |
| **AI agent support** | Works well | Designed for AI agents |
| **Rendering** | Headless Chrome | Headless Chrome |
| **Best for** | React teams, complex logic | Quick iteration, AI-first workflows |

---

## Which video is which?

- **My original video** covers the **Remotion** workflow (this repo).
- **My latest video** covers the **HyperFrames** workflow → [Media Production Kit](https://github.com/JJenglert1/media-production-kit).

---

## Remotion Skill — Full Documentation

Everything below covers the original Remotion-based workflow.

---

A portable Claude Code skill for creating branded video content with **Remotion** (React-based video framework), **sound design**, and **voiceover**. Captures proven patterns from production — scene templates, animation language, component architecture, and end-to-end workflow.

## What's Inside

```
video-production/
├── SKILL.md                        # Skill entry point
├── README.md                       # This file
└── rules/
    ├── project-setup.md            # Scaffold a new Remotion project
    ├── brand-system.md             # Define colors, gradients, typography for any brand
    ├── components.md               # 5 reusable components (Background, GradientText, etc.)
    ├── templates.md                # 9 scene templates (titles, callouts, quotes, prompts)
    ├── scene-patterns.md           # Proven compositions (pro tips, competitor cards, etc.)
    ├── scene-blueprints.md         # Copy-paste-ready code for all templates + custom scenes
    ├── animation.md                # Spring physics, staggered entrances, highlight walking
    ├── sound-design.md             # SFX categories, music beds, FFmpeg mixing
    ├── voiceover.md                # Eleven Labs integration
    ├── rendering.md                # Single/batch/chunk rendering workflows
    └── workflow.md                 # End-to-end production pipeline
```

## Installation

### Claude Code (Global)

Copy the skill into your Claude Code skills directory:

```bash
git clone https://github.com/JJenglert1/video-production.git ~/.claude/skills/video-production
```

Claude Code automatically loads skills from `~/.claude/skills/` when referenced.

### Per-Project

Clone into your project's `.claude/skills/` directory:

```bash
cd your-project
mkdir -p .claude/skills
git clone https://github.com/JJenglert1/video-production.git .claude/skills/video-production
```

### For Other Tools (Codex, etc.)

Clone wherever your tool reads skill/instruction files from:

```bash
git clone https://github.com/JJenglert1/video-production.git ~/skills/video-production
```

## Usage

Reference the skill by name in your Claude Code prompts:

```
Using the video-production skill, set up a new Remotion project for Acme Corp
```

```
Use the video-production skill to create scenes for this transcript: [paste transcript]
```

```
Following the video-production workflow, add sound design to this video
```

You can also reference specific rule files:

```
Follow the video-production brand-system rules to define colors for my brand
```

```
Use the video-production animation patterns for these scene transitions
```

## Quick Start: New Video Project

1. **Set up the repo** → `rules/project-setup.md`
   - Scaffold Remotion project, configure brand.ts, fonts.ts, asset pipeline

2. **Define your brand** → `rules/brand-system.md`
   - Colors, gradients, typography, surfaces — swap these and everything inherits

3. **Build components** → `rules/components.md`
   - BrandBackground, GradientText, PillBadge, AnimatedText, BrandLogo

4. **Create templates** → `rules/templates.md`
   - Pick from 9 proven templates: titles, callouts, quotes, prompts, split-screen

5. **Compose scenes** → `rules/scene-patterns.md`
   - Pro tips, pain points, competitor cards, side-by-side comparisons, notifications

6. **Animate** → `rules/animation.md`
   - Spring physics, staggered entrances, highlight walking, idle float

7. **Add sound** → `rules/sound-design.md`
   - SFX on transitions, music beds, volume envelopes via FFmpeg

8. **Generate voiceover** → `rules/voiceover.md`
   - Eleven Labs integration, script timing, Remotion audio embedding

9. **Render & deliver** → `rules/rendering.md`
   - Single scene, batch, chunk rendering for long scenes

## Adapting for a New Brand

The entire system is brand-agnostic. To adapt for a new brand:

1. Replace colors in `brand.ts` with the new palette
2. Replace font files in `public/fonts/` and update `fonts.ts`
3. Replace logo assets in `public/brand/`
4. Update gradient definitions

**No template or component code needs to change** — everything references the brand constants.

## What This Skill Produces

- **Title cards** — branded motion graphics overlays for video editing
- **Scene transitions** — animated transitions between video sections
- **Prompt displays** — code/text displays with walking highlights synced to voiceover
- **Sound design** — background music with volume envelopes + SFX at key moments
- **Animated backgrounds** — gradient breathing backgrounds for B-roll
- **Complete video packages** — all of the above, assembled into a production pipeline

## Tech Stack

- [Remotion](https://www.remotion.dev/) — React-based video framework
- [FFmpeg](https://ffmpeg.org/) — Audio mixing, video concatenation, rendering
- [WaveSpeed AI](https://wavespeed.ai/) — SFX and music generation
- [Eleven Labs](https://elevenlabs.io/) — AI voiceover generation
