# Video Production Skill

Portable skill for creating branded video content with Remotion + sound design + voiceover. Captures proven patterns from production experience — scene templates, animation language, component architecture, and end-to-end workflow.

## Quick Start: New Project Setup

When starting a new video project for a brand:

1. **Scaffold the repo** — [rules/project-setup.md](rules/project-setup.md)
2. **Define the brand** — [rules/brand-system.md](rules/brand-system.md)
3. **Build components** — [rules/components.md](rules/components.md)
4. **Create templates** — [rules/templates.md](rules/templates.md)
5. **Compose scenes** — [rules/scene-patterns.md](rules/scene-patterns.md) + [rules/scene-blueprints.md](rules/scene-blueprints.md)
6. **Animate** — [rules/animation.md](rules/animation.md)
7. **Add sound** — [rules/sound-design.md](rules/sound-design.md)
8. **Generate voiceover** — [rules/voiceover.md](rules/voiceover.md)
9. **Render & deliver** — [rules/rendering.md](rules/rendering.md)

## What This Skill Covers

| Area | What You Get |
|------|-------------|
| **Project scaffold** | Directory structure, Root.tsx, brand.ts, fonts, asset pipeline |
| **Brand system** | Colors, gradients, typography, surfaces — parameterized for any brand |
| **Components** | Background, GradientText, Logo, PillBadge, AnimatedText |
| **9 Scene Templates** | Title cards, callouts, quotes, prompts, split-screen, headlines |
| **Scene Patterns** | Pro tips, pain points, competitor cards, notifications, side-by-side |
| **Scene Blueprints** | Copy-paste-ready implementations for all templates + custom scenes |
| **Animation Language** | Spring physics, staggered entrances, highlight walking, idle float |
| **Sound Design** | SFX categories, music beds, mixing with FFmpeg, volume envelopes |
| **Voiceover** | Eleven Labs integration for AI narration |
| **Rendering** | Single scene, batch, chunk rendering for long scenes, ffmpeg concat |

## End-to-End Workflow

See [rules/workflow.md](rules/workflow.md) for the full production pipeline from transcript to final deliverable.

## Adapting for a New Brand

The brand system is fully parameterized. To adapt:

1. Replace colors in `brand.ts` with the new brand palette
2. Replace font files in `public/fonts/` and update `fonts.ts`
3. Replace logo assets in `public/brand/`
4. Update gradient definitions to match brand direction
5. All components and templates automatically inherit the new brand

No template code needs to change — everything references the brand constants.
