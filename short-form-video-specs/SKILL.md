---
name: short-form-video-specs
description: Safe zones in pixels, length limits, caption limits and script word counts for vertical video on TikTok, YouTube Shorts, Instagram Reels and Facebook Reels. Use when placing captions, titles, logos or faces in a 9:16 frame, sizing a script to a length, or writing a title or caption for one of these apps.
---

# Short-Form Video Specs

Tells Claude where each app draws its buttons, captions and account name over a vertical video, so text, faces and logos stay
readable on TikTok, YouTube Shorts, Instagram Reels and Facebook Reels. It also gives each app's length and caption limits and
how many words fit a given length. Every figure is in pixels on a 1080 x 1920 frame; for another 9:16 size, scale x by
width / 1080 and y by height / 1920.

## When to Use This Skill

- Placing captions, a title card, a logo or a face in a vertical video built in Remotion, HyperFrames, ffmpeg or an editor
- Checking whether a layout is covered by an app's buttons before export
- Sizing a voiceover script to 15, 30 or 60 seconds
- Writing a title, caption or hashtags within each app's limits

## What This Skill Does

1. **Safe zones**: the area each app leaves clear, from each app's published 9:16 ad guidance, and the box inside all four at once.
2. **Layout rules**: the widest centred caption above and below the button column.
3. **Limits**: length, title, caption and hashtag limits, with the route each applies to (the app or its API).
4. **Script length**: words that fit a length at three measured speaking rates.

## The figures

Inside all four apps at once, keep text, faces and logos:

- between y = 288 and y = 1248 (288 px from the top, 672 px from the bottom)
- between x = 120 and x = 888 (120 px from the left, 192 px from the right)
- below y = 840, no further right than x = 780 (TikTok's like and share column)

| App | Clear box (left, top, right, bottom) | Button column |
|---|---|---|
| TikTok (In-Feed, standard, left to right) | 120, 240, 960, 1260 | from y = 840 down, x 780 and right of it is covered |
| YouTube Shorts | 48, 288, 888, 1248 | inside the right margin |
| Instagram Reels, Facebook Reels | 65, 269, 1015, 1248 | not modelled: Meta gives only percentages (14% top, 35% bottom, 6% sides) |

These are the apps' published presets, not a guarantee: overlays also change with the placement, the caption's length and the
app version. Reels show icons on the lower right that the figures do not model; keep text away from them.

A caption centred on the frame can be 696 px wide above y = 840 (x 192 to 888) and 480 px wide below it (x 300 to 780).

Length:
- YouTube Shorts: square or vertical uploads up to 3 minutes.
- Instagram Reels: up to 20 minutes made in the app; over 3 minutes is not recommended to new audiences. 3 seconds to 15 minutes
  through the publishing API.
- Facebook Reels: no length limit in the app; the Page Reels API takes 3 to 90 seconds.
- TikTok: no single published figure; its posting API returns each account's own maximum.

Titles and captions:
- YouTube: title up to 100 characters, description up to 5,000; more than 60 hashtags and all are ignored.
- TikTok: caption up to 2,200 UTF-16 runes through the Content Posting API.
- Instagram: caption up to 2,200 through Meta's publishing API; up to 5 hashtags on a post or reel in the app.

Script length: words = seconds x words a minute / 60, at about 150, 183 or 196 words a minute. 30 seconds holds 75 to 98 words,
60 seconds 150 to 196, and a 3 second opening line 7 to 9.

## How to Use

### Basic Usage

```
Where can I put the title so TikTok and Shorts don't cover it?
```

### Advanced Usage

```
In this Remotion composition at 720 x 1280, move every caption into the area that is clear on all four apps, centred, and keep the subtitle block under 480 px wide below the button line.
```

## Example

**User**: "How many words fit a 45 second voiceover, and where do the captions go?"

**Output**:
```
At 150, 183 and 196 words a minute: 112, 137 or 147 words.
Captions: centred, bottom edge at or above y 1248 on a 1080 x 1920 frame; below y 840 keep them within x 300 to 780 (480 px wide) to clear TikTok's button column.
```

**Credit:** Figures, sources and dates from [viewgum/short-form-video-specs](https://github.com/viewgum/short-form-video-specs) (CC BY 4.0, ViewGum), which also has PNG overlay templates, a JavaScript module and a CLI.

## Tips

- If a current screenshot of the app disagrees with a figure, follow the screenshot.
- Backgrounds and motion can fill the whole frame; only what the viewer must read needs the clear box.
- Use 150 words a minute when the voice is slow or the script is dense with numbers.

## Common Use Cases

- Caption and title placement in programmatic video (Remotion, HyperFrames, ffmpeg drawtext)
- Pre-export checks of a frame against each app's overlays
- Script planning for Shorts, Reels and TikTok
