# Scene Blueprints

Complete, copy-paste-ready implementations for every scene template and custom scene pattern. These are the actual production-tested layouts — adapt the brand imports and content for your project.

All blueprints use these generic imports — replace with your brand's equivalents:

```tsx
// Adapt these imports to your brand
import { BRAND_COLORS, BRAND_GRADIENT } from '../brand';   // or '../../brand'
import { BrandBackground } from '../components/BrandBackground';
import { GradientText } from '../components/GradientText';
import { brandFont, FONT_WEIGHTS } from '../fonts';
```

---

## Template 1: FullScreenTitleQuestion

Badge pill + large question text, centered. Scene openers and transitions.

```tsx
import React from 'react';
import {
  AbsoluteFill,
  useCurrentFrame,
  useVideoConfig,
  spring,
  interpolate,
} from 'remotion';
import { BRAND_COLORS } from '../../brand';
import { BrandBackground } from '../../components/BrandBackground';
import { brandFont, FONT_WEIGHTS } from '../../fonts';

export type FullScreenTitleQuestionProps = {
  badge: string;
  question: string;
};

export const FullScreenTitleQuestion: React.FC<FullScreenTitleQuestionProps> = ({
  badge,
  question,
}) => {
  const frame = useCurrentFrame();
  const { fps } = useVideoConfig();

  const badgeEntrance = spring({ frame, fps, delay: 5, config: { damping: 200 } });
  const badgeOpacity = interpolate(badgeEntrance, [0, 1], [0, 1]);
  const badgeScale = interpolate(badgeEntrance, [0, 1], [0.8, 1]);

  const textEntrance = spring({ frame, fps, delay: 12, config: { damping: 200 } });
  const textOpacity = interpolate(textEntrance, [0, 1], [0, 1]);
  const textY = interpolate(textEntrance, [0, 1], [30, 0]);

  return (
    <AbsoluteFill style={{ fontFamily: brandFont }}>
      <BrandBackground aurora="bottom" animated={false} />
      <AbsoluteFill
        style={{
          display: 'flex',
          flexDirection: 'column',
          alignItems: 'center',
          justifyContent: 'center',
          gap: 40,
          padding: '0 120px',
        }}
      >
        {/* Badge */}
        <div
          style={{
            opacity: badgeOpacity,
            transform: `scale(${badgeScale})`,
            padding: '10px 28px',
            borderRadius: 100,
            border: '1px solid rgba(255,255,255,0.25)',
            backgroundColor: 'rgba(255,255,255,0.08)',
            fontSize: 18,
            fontWeight: FONT_WEIGHTS.medium,
            color: BRAND_COLORS.offWhite,
            letterSpacing: 1.5,
            textTransform: 'uppercase',
          }}
        >
          {badge}
        </div>

        {/* Question */}
        <div
          style={{
            opacity: textOpacity,
            transform: `translateY(${textY}px)`,
            fontSize: 54,
            fontWeight: FONT_WEIGHTS.heading,
            color: BRAND_COLORS.white,
            textAlign: 'center',
            lineHeight: 1.3,
            maxWidth: 1100,
          }}
        >
          {question}
        </div>
      </AbsoluteFill>
    </AbsoluteFill>
  );
};
```

**Duration**: 3-6s

---

## Template 2: FullScreenCallOut

Dark card with title + bullet points that unblur in sequence.

```tsx
import React from 'react';
import {
  AbsoluteFill,
  useCurrentFrame,
  useVideoConfig,
  spring,
  interpolate,
} from 'remotion';
import { BRAND_COLORS, BRAND_GRADIENT } from '../../brand';
import { BrandBackground } from '../../components/BrandBackground';
import { brandFont, FONT_WEIGHTS } from '../../fonts';

export type CallOutItem = {
  icon: string;
  text: string;
};

export type FullScreenCallOutProps = {
  title: string;
  items: CallOutItem[];
};

export const FullScreenCallOut: React.FC<FullScreenCallOutProps> = ({
  title,
  items,
}) => {
  const frame = useCurrentFrame();
  const { fps } = useVideoConfig();

  const titleEntrance = spring({ frame, fps, delay: 5, config: { damping: 200 } });
  const titleOpacity = interpolate(titleEntrance, [0, 1], [0, 1]);

  return (
    <AbsoluteFill style={{ fontFamily: brandFont }}>
      <BrandBackground aurora="bottom" animated={false} />
      <AbsoluteFill
        style={{
          display: 'flex',
          alignItems: 'center',
          justifyContent: 'center',
          padding: '40px 50px',
        }}
      >
        <div
          style={{
            width: '100%',
            maxWidth: 1600,
            backgroundColor: BRAND_COLORS.darkCard,
            borderRadius: 20,
            border: '1px solid rgba(255,255,255,0.08)',
            padding: '50px 56px',
          }}
        >
          {/* Title */}
          <div
            style={{
              opacity: titleOpacity,
              fontSize: 42,
              fontWeight: FONT_WEIGHTS.heading,
              color: BRAND_COLORS.white,
              marginBottom: 40,
            }}
          >
            {title}
          </div>

          {/* Bullets */}
          {items.map((item, i) => {
            const bulletDelay = Math.round((3 + i * 2.5) * fps);
            const entrance = spring({
              frame,
              fps,
              delay: bulletDelay,
              config: { damping: 200 },
            });
            const opacity = interpolate(entrance, [0, 1], [0, 1]);
            const blur = interpolate(entrance, [0, 1], [6, 0]);

            return (
              <div
                key={i}
                style={{
                  display: 'flex',
                  alignItems: 'center',
                  gap: 24,
                  padding: '16px 0',
                  opacity,
                  filter: `blur(${blur}px)`,
                }}
              >
                {/* Number badge */}
                <div
                  style={{
                    width: 44,
                    height: 44,
                    borderRadius: '50%',
                    background: BRAND_GRADIENT.css,
                    display: 'flex',
                    alignItems: 'center',
                    justifyContent: 'center',
                    fontSize: 20,
                    fontWeight: FONT_WEIGHTS.bold,
                    color: BRAND_COLORS.white,
                    flexShrink: 0,
                  }}
                >
                  {i + 1}
                </div>

                <div
                  style={{
                    fontSize: 28,
                    fontWeight: FONT_WEIGHTS.regular,
                    color: BRAND_COLORS.offWhite,
                    lineHeight: 1.4,
                  }}
                >
                  {item.text}
                </div>
              </div>
            );
          })}
        </div>
      </AbsoluteFill>
    </AbsoluteFill>
  );
};
```

**Duration**: 4-15s depending on bullet count

---

## Template 3: Quote

Gradient quotation marks + centered quote text + optional attribution.

```tsx
import React from 'react';
import {
  AbsoluteFill,
  useCurrentFrame,
  useVideoConfig,
  spring,
  interpolate,
} from 'remotion';
import { BRAND_COLORS, BRAND_GRADIENT } from '../../brand';
import { BrandBackground } from '../../components/BrandBackground';
import { brandFont, FONT_WEIGHTS } from '../../fonts';

export type QuoteProps = {
  quote: string;
  attribution?: string;
};

export const Quote: React.FC<QuoteProps> = ({ quote, attribution }) => {
  const frame = useCurrentFrame();
  const { fps } = useVideoConfig();

  const markEntrance = spring({
    frame, fps, delay: 3,
    config: { damping: 14, stiffness: 80 },
  });
  const markScale = interpolate(markEntrance, [0, 1], [0.6, 1]);
  const markOpacity = interpolate(markEntrance, [0, 1], [0, 0.9]);

  const textEntrance = spring({ frame, fps, delay: 12, config: { damping: 200 } });
  const textOpacity = interpolate(textEntrance, [0, 1], [0, 1]);
  const textY = interpolate(textEntrance, [0, 1], [20, 0]);

  const attrEntrance = spring({ frame, fps, delay: 22, config: { damping: 200 } });
  const attrOpacity = interpolate(attrEntrance, [0, 1], [0, 1]);

  return (
    <AbsoluteFill style={{ fontFamily: brandFont }}>
      <BrandBackground aurora="bottom-right" animated={false} />
      <AbsoluteFill
        style={{
          display: 'flex',
          flexDirection: 'column',
          alignItems: 'center',
          justifyContent: 'center',
          padding: '0 100px',
          gap: 20,
        }}
      >
        {/* Quotation Mark */}
        <svg
          width="60"
          height="48"
          viewBox="0 0 60 48"
          style={{
            opacity: markOpacity,
            transform: `scale(${markScale})`,
          }}
        >
          <defs>
            <linearGradient id="quoteGrad" x1="0%" y1="0%" x2="100%" y2="100%">
              <stop offset="0%" stopColor={BRAND_COLORS.primary} />
              <stop offset="50%" stopColor={BRAND_COLORS.secondary} />
              <stop offset="100%" stopColor={BRAND_COLORS.tertiary} />
            </linearGradient>
          </defs>
          <text
            x="0"
            y="48"
            fill="url(#quoteGrad)"
            fontSize="72"
            fontFamily={brandFont}
            fontWeight="700"
          >
            &ldquo;
          </text>
        </svg>

        {/* Quote Text */}
        <div
          style={{
            opacity: textOpacity,
            transform: `translateY(${textY}px)`,
            fontSize: 42,
            fontWeight: FONT_WEIGHTS.heading,
            color: BRAND_COLORS.white,
            textAlign: 'center',
            lineHeight: 1.4,
            maxWidth: 1100,
          }}
        >
          {quote}
        </div>

        {/* Attribution */}
        {attribution && (
          <div
            style={{
              opacity: attrOpacity,
              fontSize: 22,
              fontWeight: FONT_WEIGHTS.regular,
              color: BRAND_COLORS.lightGray,
              marginTop: 12,
            }}
          >
            — {attribution}
          </div>
        )}
      </AbsoluteFill>
    </AbsoluteFill>
  );
};
```

**Duration**: 3-8s

---

## Template 4: SplitScreenCallOut

Left panel with icon/headline/body items, staggered reveal.

```tsx
import React from 'react';
import {
  AbsoluteFill,
  useCurrentFrame,
  useVideoConfig,
  spring,
  interpolate,
} from 'remotion';
import { BRAND_COLORS, BRAND_GRADIENT } from '../../brand';
import { BrandBackground } from '../../components/BrandBackground';
import { brandFont, FONT_WEIGHTS } from '../../fonts';

export type SplitScreenItem = {
  icon: string;
  headline: string;
  body: string;
};

export type SplitScreenCallOutProps = {
  items: SplitScreenItem[];
};

export const SplitScreenCallOut: React.FC<SplitScreenCallOutProps> = ({ items }) => {
  const frame = useCurrentFrame();
  const { fps } = useVideoConfig();

  return (
    <AbsoluteFill style={{ fontFamily: brandFont }}>
      <div style={{ display: 'flex', width: '100%', height: '100%' }}>
        {/* Left Panel — Content */}
        <div
          style={{
            width: '40%',
            backgroundColor: BRAND_COLORS.darkBg,
            display: 'flex',
            flexDirection: 'column',
            justifyContent: 'center',
            padding: '60px 50px',
            gap: 48,
            position: 'relative',
            overflow: 'hidden',
          }}
        >
          {/* Subtle aurora in left panel */}
          <div style={{
            position: 'absolute',
            bottom: '-20%',
            right: '-30%',
            width: '80%',
            height: '60%',
            background: `radial-gradient(ellipse, ${BRAND_COLORS.primary}20 0%, transparent 70%)`,
            filter: 'blur(60px)',
            pointerEvents: 'none',
          }} />

          {items.map((item, i) => {
            const delay = Math.round((3 + i * 5) * fps);
            const entrance = spring({ frame, fps, delay, config: { damping: 200 } });
            const opacity = interpolate(entrance, [0, 1], [0, 1]);
            const blur = interpolate(entrance, [0, 1], [6, 0]);

            return (
              <div key={i} style={{ opacity, filter: `blur(${blur}px)` }}>
                <div style={{ display: 'flex', alignItems: 'center', gap: 16, marginBottom: 12 }}>
                  <div style={{
                    width: 40,
                    height: 40,
                    borderRadius: '50%',
                    background: BRAND_GRADIENT.css,
                    display: 'flex',
                    alignItems: 'center',
                    justifyContent: 'center',
                    fontSize: 18,
                    fontWeight: FONT_WEIGHTS.bold,
                    color: BRAND_COLORS.white,
                  }}>
                    {i + 1}
                  </div>
                  <div style={{
                    fontSize: 28,
                    fontWeight: FONT_WEIGHTS.heading,
                    color: BRAND_COLORS.white,
                  }}>
                    {item.headline}
                  </div>
                </div>
                <div style={{
                  fontSize: 20,
                  color: BRAND_COLORS.lightGray,
                  lineHeight: 1.5,
                  paddingLeft: 56,
                }}>
                  {item.body}
                </div>
              </div>
            );
          })}
        </div>

        {/* Right Panel — Brand background */}
        <div style={{ width: '60%', position: 'relative' }}>
          <BrandBackground aurora="center" animated={false} />
        </div>
      </div>
    </AbsoluteFill>
  );
};
```

**Duration**: 10-18s

---

## Template 5: PromptDisplay

Auto-sizing prompt card with scroll for long content.

```tsx
import React from 'react';
import {
  AbsoluteFill,
  useCurrentFrame,
  useVideoConfig,
  spring,
  interpolate,
  Easing,
} from 'remotion';
import { BRAND_COLORS, BRAND_GRADIENT } from '../../brand';
import { BrandBackground } from '../../components/BrandBackground';
import { brandFont, FONT_WEIGHTS } from '../../fonts';

export type PromptDisplayProps = {
  prompt: string;
};

export const PromptDisplay: React.FC<PromptDisplayProps> = ({ prompt }) => {
  const frame = useCurrentFrame();
  const { fps, durationInFrames } = useVideoConfig();

  const cardEntrance = spring({ frame, fps, delay: 5, config: { damping: 200 } });
  const cardOpacity = interpolate(cardEntrance, [0, 1], [0, 1]);
  const cardScale = interpolate(cardEntrance, [0, 1], [0.98, 1]);

  const textEntrance = spring({ frame, fps, delay: 12, config: { damping: 200 } });
  const textOpacity = interpolate(textEntrance, [0, 1], [0, 1]);

  const lines = prompt.split('\n');
  const lineHeight = 34;
  const totalHeight = lines.length * lineHeight;
  const maxVisible = 940;
  const needsScroll = totalHeight > maxVisible;

  // Smooth scroll with ease-in/out at boundaries
  const scrollDistance = Math.max(0, totalHeight - maxVisible + 40);
  const easeStart = 0.05;
  const easeEnd = 0.95;
  const rawProgress = interpolate(
    frame,
    [30, durationInFrames - 15],
    [0, 1],
    { extrapolateLeft: 'clamp', extrapolateRight: 'clamp' }
  );

  let scrollProgress = rawProgress;
  if (rawProgress < easeStart) {
    scrollProgress = Easing.in(Easing.cubic)(rawProgress / easeStart) * easeStart;
  } else if (rawProgress > easeEnd) {
    const t = (rawProgress - easeEnd) / (1 - easeEnd);
    scrollProgress = easeEnd + Easing.out(Easing.cubic)(t) * (1 - easeEnd);
  }
  const scrollY = needsScroll ? -scrollProgress * scrollDistance : 0;

  return (
    <AbsoluteFill style={{ fontFamily: brandFont }}>
      <BrandBackground aurora="bottom-right" animated={false} />
      <AbsoluteFill style={{
        display: 'flex',
        alignItems: 'center',
        justifyContent: 'center',
        padding: '40px 50px',
      }}>
        <div style={{ width: '100%', maxWidth: 1600 }}>
          <div style={{
            backgroundColor: BRAND_COLORS.darkCard,
            borderRadius: 20,
            border: '1px solid rgba(255,255,255,0.08)',
            opacity: cardOpacity,
            transform: `scale(${cardScale})`,
            overflow: 'hidden',
            position: 'relative',
            height: needsScroll ? maxVisible : 'auto',
            maxHeight: maxVisible,
          }}>
            {/* Gradient left border */}
            <div style={{
              position: 'absolute',
              left: 0,
              top: 0,
              bottom: 0,
              width: 3,
              background: BRAND_GRADIENT.cssVertical,
              borderRadius: '3px 0 0 3px',
            }} />

            {/* Top fade */}
            {needsScroll && (
              <div style={{
                position: 'absolute',
                top: 0,
                left: 0,
                right: 0,
                height: 60,
                background: `linear-gradient(180deg, ${BRAND_COLORS.darkCard} 0%, transparent 100%)`,
                zIndex: 2,
                pointerEvents: 'none',
              }} />
            )}

            {/* Prompt text */}
            <div style={{
              padding: '44px 56px',
              opacity: textOpacity,
              transform: `translate3d(0, ${scrollY}px, 0)`,
              willChange: 'transform',
            }}>
              {lines.map((line, i) => (
                <div key={i} style={{
                  color: BRAND_COLORS.offWhite,
                  fontSize: 22,
                  fontWeight: FONT_WEIGHTS.regular,
                  lineHeight: 1.55,
                  minHeight: line === '' ? 16 : undefined,
                }}>
                  {line || '\u00A0'}
                </div>
              ))}
            </div>

            {/* Bottom fade */}
            {needsScroll && (
              <div style={{
                position: 'absolute',
                bottom: 0,
                left: 0,
                right: 0,
                height: 80,
                background: `linear-gradient(0deg, ${BRAND_COLORS.darkCard} 0%, transparent 100%)`,
                zIndex: 2,
                pointerEvents: 'none',
              }} />
            )}
          </div>
        </div>
      </AbsoluteFill>
    </AbsoluteFill>
  );
};
```

**Duration**: Match to voiceover length

---

## Template 6: HighlightedPrompt

All text visible, walking highlight synced to voiceover. The most sophisticated template.

```tsx
import React from 'react';
import {
  AbsoluteFill,
  Audio,
  Sequence,
  useCurrentFrame,
  useVideoConfig,
  spring,
  interpolate,
  staticFile,
} from 'remotion';
import { BRAND_COLORS, BRAND_GRADIENT } from '../../brand';
import { BrandBackground } from '../../components/BrandBackground';
import { brandFont, FONT_WEIGHTS } from '../../fonts';

export type PromptSection = {
  id: string;
  lines: string[];
  headers?: string[];     // Lines to bold (matched by startsWith)
  startSec: number;
  endSec: number;
};

export type HighlightedPromptProps = {
  sections: PromptSection[];
};

const SectionBlock: React.FC<{
  section: PromptSection;
  frame: number;
  fps: number;
}> = ({ section, frame, fps }) => {
  const highlightIn = spring({
    frame: Math.max(0, frame - section.startSec * fps),
    fps,
    config: { damping: 20, stiffness: 80 },
  });
  const highlightOut = frame > section.endSec * fps
    ? spring({
        frame: frame - section.endSec * fps,
        fps,
        config: { damping: 20, stiffness: 80 },
      })
    : 0;

  const highlight = Math.max(0, highlightIn - highlightOut);
  const textOpacity = interpolate(highlight, [0, 1], [0.2, 1]);
  const barOpacity = interpolate(highlight, [0, 1], [0, 0.8]);

  const headers = section.headers || [];
  const isHeader = (line: string) => headers.some((h) => line.startsWith(h));

  return (
    <div style={{
      position: 'relative',
      padding: '2px 0 2px 20px',
      marginLeft: -56,      // Extend bar to card edge
      paddingLeft: 76,
      borderRadius: 8,
    }}>
      {/* Gradient left bar */}
      <div style={{
        position: 'absolute',
        left: 0,
        top: 2,
        bottom: 2,
        width: 3,
        background: BRAND_GRADIENT.cssVertical,
        borderRadius: 2,
        opacity: barOpacity,
      }} />

      {section.lines.map((line, i) => {
        if (line === '') return <div key={i} style={{ height: 14 }} />;
        return (
          <div key={i} style={{
            fontFamily: brandFont,
            color: BRAND_COLORS.offWhite,
            fontSize: 22,
            fontWeight: isHeader(line) ? FONT_WEIGHTS.heading : FONT_WEIGHTS.regular,
            lineHeight: 1.7,
            opacity: textOpacity,
          }}>
            {line}
          </div>
        );
      })}
    </div>
  );
};

export const HighlightedPrompt: React.FC<HighlightedPromptProps> = ({ sections }) => {
  const frame = useCurrentFrame();
  const { fps } = useVideoConfig();

  const cardEntrance = spring({ frame, fps, delay: 5, config: { damping: 200 } });
  const cardOpacity = interpolate(cardEntrance, [0, 1], [0, 1]);
  const cardScale = interpolate(cardEntrance, [0, 1], [0.98, 1]);

  const textEntrance = spring({ frame, fps, delay: 12, config: { damping: 200 } });
  const textOpacity = interpolate(textEntrance, [0, 1], [0, 1]);

  return (
    <AbsoluteFill style={{ fontFamily: brandFont }}>
      <BrandBackground aurora="bottom-right" animated={false} />

      {/* Swoosh sound on each section transition */}
      {sections.slice(1).map((section) => (
        <Sequence key={`swoosh-${section.id}`} from={Math.round(section.startSec * fps)}>
          <Audio src={staticFile('audio/Swoosh.mp3')} volume={0.15} />
        </Sequence>
      ))}

      <AbsoluteFill style={{
        display: 'flex',
        alignItems: 'center',
        justifyContent: 'center',
        padding: '40px 50px',
      }}>
        <div style={{ width: '100%', maxWidth: 1600 }}>
          <div style={{
            backgroundColor: BRAND_COLORS.darkCard,
            borderRadius: 20,
            border: '1px solid rgba(255,255,255,0.08)',
            opacity: cardOpacity,
            transform: `scale(${cardScale})`,
            overflow: 'hidden',
          }}>
            <div style={{ padding: '44px 56px', opacity: textOpacity }}>
              {sections.map((section) => (
                <SectionBlock
                  key={section.id}
                  section={section}
                  frame={frame}
                  fps={fps}
                />
              ))}
            </div>
          </div>
        </div>
      </AbsoluteFill>
    </AbsoluteFill>
  );
};
```

**Usage**:
```tsx
<HighlightedPrompt
  sections={[
    { id: 'intro', lines: ['Build a dashboard with...', 'competitor cards'], headers: ['Build'], startSec: 0, endSec: 5 },
    { id: 'detail', lines: ['For each competitor...', 'AI battle cards'], headers: ['For each'], startSec: 5, endSec: 12 },
  ]}
/>
```

---

## Custom Scene: Pro Tip

Standalone scene — not a template. Badge + gradient-highlighted tip.

```tsx
import React from 'react';
import {
  AbsoluteFill,
  useCurrentFrame,
  useVideoConfig,
  spring,
  interpolate,
} from 'remotion';
import { BRAND_COLORS, BRAND_GRADIENT } from '../../brand';
import { BrandBackground } from '../../components/BrandBackground';
import { brandFont, FONT_WEIGHTS } from '../../fonts';

export const ProTipScene: React.FC = () => {
  const frame = useCurrentFrame();
  const { fps } = useVideoConfig();

  const badgeEntrance = spring({ frame, fps, delay: 5, config: { damping: 14, stiffness: 80 } });
  const badgeScale = interpolate(badgeEntrance, [0, 1], [0.6, 1]);
  const badgeOpacity = interpolate(badgeEntrance, [0, 1], [0, 1]);

  const textEntrance = spring({ frame, fps, delay: 15, config: { damping: 200 } });
  const textOpacity = interpolate(textEntrance, [0, 1], [0, 1]);
  const textY = interpolate(textEntrance, [0, 1], [20, 0]);

  return (
    <AbsoluteFill style={{ fontFamily: brandFont }}>
      <BrandBackground aurora="bottom" animated={false} />
      <AbsoluteFill style={{
        display: 'flex',
        flexDirection: 'column',
        alignItems: 'center',
        justifyContent: 'center',
        gap: 40,
        padding: '0 120px',
      }}>
        {/* Semi-transparent badge (NOT gradient-filled) */}
        <div style={{
          opacity: badgeOpacity,
          transform: `scale(${badgeScale})`,
          padding: '10px 28px',
          borderRadius: 100,
          border: '1px solid rgba(255,255,255,0.25)',
          backgroundColor: 'rgba(255,255,255,0.08)',
          fontSize: 22,
          fontWeight: FONT_WEIGHTS.medium,
          color: BRAND_COLORS.offWhite,
          letterSpacing: 1.5,
          textTransform: 'uppercase',
        }}>
          Pro Tip
        </div>

        {/* Tip text with gradient key phrase */}
        <div style={{
          opacity: textOpacity,
          transform: `translateY(${textY}px)`,
          fontSize: 54,
          fontWeight: FONT_WEIGHTS.heading,
          color: BRAND_COLORS.white,
          textAlign: 'center',
          lineHeight: 1.3,
          maxWidth: 1100,
        }}>
          Think of your prompt as a{' '}
          <span style={{
            background: BRAND_GRADIENT.css,
            WebkitBackgroundClip: 'text',
            WebkitTextFillColor: 'transparent',
          }}>
            product requirements doc
          </span>
        </div>
      </AbsoluteFill>
    </AbsoluteFill>
  );
};
```

**Duration**: 6-12s

---

## Custom Scene: Pain Points / Scattered Cards

Cards fly in, float, scatter, punchline appears.

```tsx
import React from 'react';
import {
  AbsoluteFill,
  useCurrentFrame,
  useVideoConfig,
  spring,
  interpolate,
  Easing,
} from 'remotion';
import { BRAND_COLORS, BRAND_GRADIENT } from '../../brand';
import { BrandBackground } from '../../components/BrandBackground';
import { brandFont, FONT_WEIGHTS } from '../../fonts';

const SOURCES = [
  { icon: '📧', label: 'Google Alerts', sublabel: 'Noisy & irrelevant', fromX: -500, fromY: -200, x: -280, y: -60, rotate: -8, delay: 15 },
  { icon: '💬', label: 'Slack threads', sublabel: 'Lost in scroll', fromX: 500, fromY: -300, x: 220, y: -80, rotate: 6, delay: 45 },
  { icon: '🔍', label: 'Manual searches', sublabel: 'Time-consuming', fromX: -400, fromY: 300, x: -100, y: 80, rotate: -4, delay: 75 },
  { icon: '📱', label: 'Social media', sublabel: 'Fragmented', fromX: 600, fromY: 200, x: 160, y: 60, rotate: 7, delay: 105 },
];

const SCATTER_START = 360;   // Frame when cards scatter
const PUNCHLINE_START = 400; // Frame when punchline appears

export const PainPointsScene: React.FC = () => {
  const frame = useCurrentFrame();
  const { fps } = useVideoConfig();

  // Scatter animation
  const scatterProgress = interpolate(
    frame, [SCATTER_START, SCATTER_START + 45], [0, 1],
    { extrapolateLeft: 'clamp', extrapolateRight: 'clamp', easing: Easing.in(Easing.cubic) }
  );

  // Punchline
  const punchEntrance = spring({ frame, fps, delay: PUNCHLINE_START / fps * fps, config: { damping: 20, stiffness: 80 } });
  const punchOpacity = frame >= PUNCHLINE_START ? interpolate(punchEntrance, [0, 1], [0, 1]) : 0;
  const punchY = frame >= PUNCHLINE_START ? interpolate(punchEntrance, [0, 1], [30, 0]) : 30;

  return (
    <AbsoluteFill style={{ fontFamily: brandFont }}>
      <BrandBackground aurora="bottom" animated={false} />
      <AbsoluteFill style={{
        display: 'flex',
        alignItems: 'center',
        justifyContent: 'center',
      }}>
        {/* Cards */}
        {SOURCES.map((src, i) => {
          const entrance = spring({
            frame, fps, delay: src.delay,
            config: { damping: 14, stiffness: 60, mass: 1.1 },
          });

          const x = interpolate(entrance, [0, 1], [src.fromX, src.x]);
          const y = interpolate(entrance, [0, 1], [src.fromY, src.y]);
          const rotate = interpolate(entrance, [0, 1], [src.rotate * 3, src.rotate]);
          const scale = interpolate(entrance, [0, 1], [0.5, 1]);
          const opacity = interpolate(entrance, [0, 0.4], [0, 1], { extrapolateRight: 'clamp' });

          // Idle float
          const t = frame / fps;
          const floatY = Math.sin(t * 1.2 + i * 2) * 6;
          const floatX = Math.cos(t * 0.8 + i * 3) * 4;

          // Scatter
          const scatterX = scatterProgress * src.fromX * 2;
          const scatterY = scatterProgress * src.fromY * 2;
          const scatterRotate = scatterProgress * src.rotate * 3;
          const scatterOpacity = 1 - scatterProgress;

          return (
            <div key={i} style={{
              position: 'absolute',
              transform: `translate(${x + floatX + scatterX}px, ${y + floatY + scatterY}px) rotate(${rotate + scatterRotate}deg) scale(${scale})`,
              opacity: opacity * scatterOpacity,
              willChange: 'transform, opacity',
            }}>
              <div style={{
                width: 260,
                padding: '24px 20px',
                backgroundColor: BRAND_COLORS.darkCard,
                border: '1px solid rgba(255,255,255,0.08)',
                borderRadius: 16,
                display: 'flex',
                alignItems: 'center',
                gap: 16,
                boxShadow: '0 12px 40px rgba(0,0,0,0.5)',
              }}>
                <div style={{ fontSize: 32, flexShrink: 0 }}>{src.icon}</div>
                <div>
                  <div style={{ fontSize: 20, fontWeight: FONT_WEIGHTS.heading, color: BRAND_COLORS.white }}>
                    {src.label}
                  </div>
                  <div style={{ fontSize: 15, color: BRAND_COLORS.lightGray }}>
                    {src.sublabel}
                  </div>
                </div>
              </div>
            </div>
          );
        })}

        {/* Punchline */}
        <div style={{
          position: 'absolute',
          opacity: punchOpacity,
          transform: `translateY(${punchY}px)`,
          textAlign: 'center',
        }}>
          <div style={{ fontSize: 48, fontWeight: FONT_WEIGHTS.heading, color: BRAND_COLORS.white }}>
            Replace all of it with
          </div>
          <div style={{
            fontSize: 54,
            fontWeight: FONT_WEIGHTS.heading,
            background: BRAND_GRADIENT.css,
            WebkitBackgroundClip: 'text',
            WebkitTextFillColor: 'transparent',
          }}>
            a single hub
          </div>
        </div>
      </AbsoluteFill>
    </AbsoluteFill>
  );
};
```

**Duration**: 17-22s

---

## Custom Scene: Competitor Cards + Questions

3 brand cards slam in + question pills animate below.

```tsx
import React from 'react';
import {
  AbsoluteFill,
  Audio,
  Sequence,
  useCurrentFrame,
  useVideoConfig,
  spring,
  interpolate,
  Img,
  staticFile,
} from 'remotion';
import { BRAND_COLORS } from '../../brand';
import { BrandBackground } from '../../components/BrandBackground';
import { brandFont, FONT_WEIGHTS } from '../../fonts';

const COMPETITORS = [
  { name: 'Competitor A', logo: staticFile('brand/competitor-a.png'), fromX: -800, fromY: -100, rotate: -6 },
  { name: 'Competitor B', logo: staticFile('brand/competitor-b.png'), fromX: 0, fromY: -600, rotate: 2 },
  { name: 'Competitor C', logo: staticFile('brand/competitor-c.png'), fromX: 800, fromY: -100, rotate: 5 },
];

const QUESTIONS = [
  'What are they launching?',
  'What promotions are they running?',
  "What's in the news?",
  'What does it mean for us?',
];

export const CompetitorCardsScene: React.FC = () => {
  const frame = useCurrentFrame();
  const { fps } = useVideoConfig();

  return (
    <AbsoluteFill style={{ fontFamily: brandFont }}>
      <BrandBackground aurora="bottom" animated={false} />

      {/* Button alert on each card entrance */}
      {COMPETITORS.map((_, i) => (
        <Sequence key={`alert-${i}`} from={12 + i * 17}>
          <Audio src={staticFile('audio/Button Alert.mp3')} volume={0.15} />
        </Sequence>
      ))}

      <AbsoluteFill style={{
        display: 'flex',
        flexDirection: 'column',
        alignItems: 'center',
        justifyContent: 'center',
        gap: 60,
      }}>
        {/* Cards row */}
        <div style={{ display: 'flex', gap: 40, alignItems: 'center', justifyContent: 'center' }}>
          {COMPETITORS.map((comp, i) => {
            const entrance = spring({
              frame, fps,
              delay: 12 + i * 17,
              config: { damping: 14, stiffness: 60, mass: 1.1 },
            });

            const x = interpolate(entrance, [0, 1], [comp.fromX, 0]);
            const y = interpolate(entrance, [0, 1], [comp.fromY, 0]);
            const rotate = interpolate(entrance, [0, 1], [comp.rotate * 3, comp.rotate]);
            const scale = interpolate(entrance, [0, 1], [0.6, 1]);
            const opacity = interpolate(entrance, [0, 0.4], [0, 1], { extrapolateRight: 'clamp' });

            const t = frame / fps;
            const floatY = Math.sin(t * 1.2 + i * 2) * 6;

            return (
              <div key={i} style={{
                transform: `translate(${x}px, ${y + floatY}px) rotate(${rotate}deg) scale(${scale})`,
                opacity,
                willChange: 'transform, opacity',
              }}>
                <div style={{
                  width: 400,
                  padding: '48px 32px',
                  backgroundColor: BRAND_COLORS.darkCard,
                  border: '1px solid rgba(255,255,255,0.08)',
                  borderRadius: 24,
                  display: 'flex',
                  flexDirection: 'column',
                  alignItems: 'center',
                  gap: 24,
                  boxShadow: '0 20px 50px rgba(0,0,0,0.5)',
                }}>
                  {/* Logo circle */}
                  <div style={{
                    width: 120,
                    height: 120,
                    borderRadius: '50%',
                    backgroundColor: BRAND_COLORS.white,
                    display: 'flex',
                    alignItems: 'center',
                    justifyContent: 'center',
                    padding: 20,
                    boxShadow: '0 12px 30px rgba(0,0,0,0.3)',
                  }}>
                    <Img src={comp.logo} style={{ width: '100%', height: '100%', objectFit: 'contain' }} />
                  </div>
                  <div style={{
                    color: BRAND_COLORS.white,
                    fontSize: 34,
                    fontWeight: FONT_WEIGHTS.heading,
                  }}>
                    {comp.name}
                  </div>
                </div>
              </div>
            );
          })}
        </div>

        {/* Question pills */}
        <div style={{ display: 'flex', gap: 20, flexWrap: 'wrap', justifyContent: 'center', maxWidth: 1200 }}>
          {QUESTIONS.map((q, i) => {
            const entrance = spring({
              frame, fps,
              delay: 114 + i * 30,
              config: { damping: 20, stiffness: 50 },
            });
            const opacity = interpolate(entrance, [0, 1], [0, 1]);
            const y = interpolate(entrance, [0, 1], [20, 0]);

            return (
              <div key={i} style={{
                opacity,
                transform: `translateY(${y}px)`,
                padding: '16px 32px',
                borderRadius: 100,
                border: '1px solid rgba(255,255,255,0.15)',
                backgroundColor: 'rgba(255,255,255,0.06)',
                color: BRAND_COLORS.offWhite,
                fontSize: 24,
                fontWeight: FONT_WEIGHTS.regular,
                whiteSpace: 'nowrap',
                backdropFilter: 'blur(10px)',
              }}>
                {q}
              </div>
            );
          })}
        </div>
      </AbsoluteFill>
    </AbsoluteFill>
  );
};
```

**Duration**: 16s

---

## Custom Scene: Side-by-Side with Focus States

Two cards that alternate highlighting based on voiceover timeline.

```tsx
import React from 'react';
import {
  AbsoluteFill,
  useCurrentFrame,
  useVideoConfig,
  spring,
  interpolate,
  Img,
  staticFile,
} from 'remotion';
import { BRAND_COLORS } from '../../brand';
import { BrandBackground } from '../../components/BrandBackground';
import { GradientText } from '../../components/GradientText';
import { brandFont, FONT_WEIGHTS } from '../../fonts';

const CONNECTORS = [
  { name: 'Tool A', logo: staticFile('brand/tool-a.png'), tagline: 'Web scraping', description: 'Pulls URLs and announcements', color: BRAND_COLORS.primary },
  { name: 'Tool B', logo: staticFile('brand/tool-b.png'), tagline: 'AI search', description: 'Generates competitive summaries', color: BRAND_COLORS.tertiary },
];

export const SideBySideScene: React.FC = () => {
  const frame = useCurrentFrame();
  const { fps } = useVideoConfig();

  // Focus timeline (adjust to voiceover)
  const focusAStart = 80;
  const focusBStart = 220;
  const focusBothStart = 380;

  return (
    <AbsoluteFill style={{ fontFamily: brandFont }}>
      <BrandBackground aurora="bottom" animated={false} />
      <AbsoluteFill style={{
        display: 'flex',
        flexDirection: 'column',
        alignItems: 'center',
        justifyContent: 'center',
        gap: 100,
      }}>
        {/* Title */}
        <div style={{ fontSize: 48, fontWeight: FONT_WEIGHTS.heading, color: BRAND_COLORS.white, textAlign: 'center' }}>
          Two connectors for <GradientText>live intel</GradientText>
        </div>

        {/* Cards */}
        <div style={{ display: 'flex', alignItems: 'center', gap: 80 }}>
          {CONNECTORS.map((conn, i) => {
            const entrance = spring({ frame, fps, delay: i * 15, config: { damping: 16, stiffness: 70 } });
            const entranceOpacity = interpolate(entrance, [0, 1], [0, 1]);
            const entranceY = interpolate(entrance, [0, 1], [40, 0]);

            // Focus state logic
            const focusA = interpolate(frame, [focusAStart, focusAStart + 20], [0, 1], { extrapolateLeft: 'clamp', extrapolateRight: 'clamp' });
            const focusB = interpolate(frame, [focusBStart, focusBStart + 20], [0, 1], { extrapolateLeft: 'clamp', extrapolateRight: 'clamp' });
            const focusBoth = interpolate(frame, [focusBothStart, focusBothStart + 20], [0, 1], { extrapolateLeft: 'clamp', extrapolateRight: 'clamp' });

            let currentScale = 1;
            let currentOpacity = 1;
            let currentBlur = 0;

            if (i === 0) {
              currentScale = 1 + (focusA * 0.05) - (focusB * 0.1) + (focusBoth * 0.05);
              currentOpacity = 1 - (focusB * 0.6) + (focusBoth * 0.6);
              currentBlur = (focusB * 4) - (focusBoth * 4);
            } else {
              currentScale = 1 - (focusA * 0.05) + (focusB * 0.1) - (focusBoth * 0.05);
              currentOpacity = 1 - (focusA * 0.6) + (focusB * 0.6);
              currentBlur = (focusA * 4) - (focusB * 4);
            }

            const isHighlighted = (frame >= focusAStart && frame < focusBStart && i === 0) ||
                                   (frame >= focusBStart && frame < focusBothStart && i === 1);

            return (
              <div key={i} style={{
                width: 440,
                height: 350,
                backgroundColor: BRAND_COLORS.darkCard,
                border: `1px solid ${isHighlighted ? conn.color : 'rgba(255,255,255,0.08)'}`,
                borderRadius: 24,
                padding: '40px 32px',
                display: 'flex',
                flexDirection: 'column',
                alignItems: 'center',
                gap: 20,
                boxShadow: isHighlighted ? `0 20px 60px ${conn.color}20` : '0 16px 48px rgba(0,0,0,0.4)',
                opacity: entranceOpacity * currentOpacity,
                transform: `translateY(${entranceY}px) scale(${currentScale})`,
                filter: `blur(${currentBlur}px)`,
                willChange: 'transform, opacity, filter',
              }}>
                {/* Logo */}
                <div style={{
                  width: 72, height: 72, borderRadius: '50%',
                  background: `linear-gradient(135deg, ${conn.color}20, rgba(255,255,255,0.05))`,
                  border: `1px solid ${conn.color}40`,
                  display: 'flex', alignItems: 'center', justifyContent: 'center',
                  padding: 16, overflow: 'hidden',
                }}>
                  <Img src={conn.logo} style={{ width: '100%', height: '100%', objectFit: 'contain' }} />
                </div>

                <div style={{ textAlign: 'center' }}>
                  <div style={{ fontSize: 32, fontWeight: FONT_WEIGHTS.heading, color: BRAND_COLORS.white, marginBottom: 8 }}>
                    {conn.name}
                  </div>
                  <div style={{
                    display: 'inline-block', fontSize: 18, fontWeight: FONT_WEIGHTS.semibold,
                    color: conn.color, letterSpacing: 0.5, textTransform: 'uppercase',
                    padding: '5px 14px', borderRadius: 100, backgroundColor: `${conn.color}15`, marginBottom: 16,
                  }}>
                    {conn.tagline}
                  </div>
                  <div style={{ fontSize: 20, lineHeight: 1.4, color: BRAND_COLORS.lightGray }}>
                    {conn.description}
                  </div>
                </div>
              </div>
            );
          })}
        </div>
      </AbsoluteFill>
    </AbsoluteFill>
  );
};
```

**Duration**: 15-18s

---

## Custom Scene: Notification Card

Slack-style alert with channel, badge, and message body.

```tsx
import React from 'react';
import {
  AbsoluteFill,
  useCurrentFrame,
  useVideoConfig,
  spring,
  interpolate,
} from 'remotion';
import { BRAND_COLORS } from '../../brand';
import { BrandBackground } from '../../components/BrandBackground';
import { brandFont, FONT_WEIGHTS } from '../../fonts';

export const NotificationScene: React.FC = () => {
  const frame = useCurrentFrame();
  const { fps } = useVideoConfig();

  const cardEntrance = spring({ frame, fps, delay: 3, config: { damping: 16, stiffness: 80 } });
  const cardOpacity = interpolate(cardEntrance, [0, 1], [0, 1]);
  const cardY = interpolate(cardEntrance, [0, 1], [40, 0]);

  const contentEntrance = spring({ frame, fps, delay: 10, config: { damping: 200 } });
  const contentOpacity = interpolate(contentEntrance, [0, 1], [0, 1]);

  return (
    <AbsoluteFill style={{ fontFamily: brandFont }}>
      <BrandBackground aurora="bottom-right" animated={false} />
      <AbsoluteFill style={{
        display: 'flex',
        alignItems: 'center',
        justifyContent: 'center',
        padding: '40px 50px',
      }}>
        <div style={{
          width: '100%',
          maxWidth: 900,
          backgroundColor: BRAND_COLORS.darkCard,
          borderRadius: 16,
          border: '1px solid rgba(255,255,255,0.08)',
          padding: '36px 44px',
          opacity: cardOpacity,
          transform: `translateY(${cardY}px)`,
          boxShadow: '0 16px 48px rgba(0,0,0,0.5)',
        }}>
          <div style={{ opacity: contentOpacity }}>
            {/* Channel header */}
            <div style={{
              display: 'flex',
              alignItems: 'center',
              gap: 12,
              marginBottom: 20,
            }}>
              <span style={{ color: BRAND_COLORS.lightGray, fontSize: 20, fontWeight: FONT_WEIGHTS.semibold }}>
                # competitive-intel
              </span>
              <span style={{ color: 'rgba(255,255,255,0.3)', fontSize: 16 }}>
                9:00 AM
              </span>
            </div>

            {/* Divider */}
            <div style={{ height: 1, backgroundColor: 'rgba(255,255,255,0.06)', marginBottom: 20 }} />

            {/* Alert badge */}
            <div style={{
              display: 'inline-block',
              padding: '6px 16px',
              borderRadius: 8,
              backgroundColor: `${BRAND_COLORS.primary}15`,
              color: BRAND_COLORS.primary,
              fontWeight: FONT_WEIGHTS.semibold,
              fontSize: 16,
              textTransform: 'uppercase',
              letterSpacing: 0.5,
              marginBottom: 16,
            }}>
              COMPETITOR ALERT
            </div>

            {/* Message body */}
            <div style={{
              fontSize: 24,
              lineHeight: 1.5,
              color: BRAND_COLORS.offWhite,
            }}>
              Competitor A announced a new promotion at $6.99 — undercutting
              our value menu.{' '}
              <span style={{ color: BRAND_COLORS.tertiary }}>
                See the full analysis
              </span>
            </div>
          </div>
        </div>
      </AbsoluteFill>
    </AbsoluteFill>
  );
};
```

**Duration**: 4-19s

---

## Custom Scene: Animated Gradient Background

Breathing gradient blobs for B-roll. No content — just atmosphere.

```tsx
import React from 'react';
import { AbsoluteFill, useCurrentFrame, useVideoConfig } from 'remotion';
import { BRAND_COLORS } from '../../brand';

export const AnimatedBackground: React.FC = () => {
  const frame = useCurrentFrame();
  const { fps } = useVideoConfig();
  const t = frame / fps;

  // Three breathing blobs at different positions and speeds
  const blobs = [
    {
      color: BRAND_COLORS.primary,
      cx: '30%', cy: '70%', w: '50%', h: '45%',
      scaleFreq: 0.25, opacityFreq: 0.18,
      baseScale: 1, scaleAmp: 0.08, baseOpacity: 0.22, opacityAmp: 0.06, phase: 0,
    },
    {
      color: BRAND_COLORS.secondary,
      cx: '70%', cy: '30%', w: '45%', h: '40%',
      scaleFreq: 0.3, opacityFreq: 0.22,
      baseScale: 1, scaleAmp: 0.06, baseOpacity: 0.18, opacityAmp: 0.05, phase: 2,
    },
    {
      color: BRAND_COLORS.tertiary,
      cx: '50%', cy: '55%', w: '55%', h: '50%',
      scaleFreq: 0.2, opacityFreq: 0.15,
      baseScale: 1, scaleAmp: 0.1, baseOpacity: 0.15, opacityAmp: 0.04, phase: 4,
    },
  ];

  return (
    <AbsoluteFill style={{ backgroundColor: BRAND_COLORS.darkBg }}>
      {blobs.map((blob, i) => {
        const scale = blob.baseScale + Math.sin(t * blob.scaleFreq * Math.PI * 2 + blob.phase) * blob.scaleAmp;
        const opacity = blob.baseOpacity + Math.sin(t * blob.opacityFreq * Math.PI * 2 + blob.phase + 1) * blob.opacityAmp;

        return (
          <div key={i} style={{
            position: 'absolute',
            left: blob.cx, top: blob.cy,
            width: blob.w, height: blob.h,
            transform: `translate(-50%, -50%) scale(${scale})`,
            transformOrigin: 'center center',
            background: `radial-gradient(ellipse at center, ${blob.color}40 0%, transparent 70%)`,
            filter: 'blur(80px)',
            opacity,
            pointerEvents: 'none',
          }} />
        );
      })}
    </AbsoluteFill>
  );
};
```

**Duration**: 60s+ (render in 15s chunks, concatenate with ffmpeg)

---

## Using These Blueprints

1. **Copy the template** into your `src/templates/` directory
2. **Replace brand imports** with your project's equivalents
3. **For custom scenes**, copy into `src/scenes/your-video/` and customize content
4. **Register** in `Root.tsx` with the appropriate duration
5. **Test** in Remotion Studio (`npm start`)
