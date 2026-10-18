---
name: ui-review
description: Review a UI change against the laws of UX, with a render beside each point. Use when asked to review screens, a pull request that changes UI, or a design before it's built.
---

# Reviewing a UI change

## Before you look

1. Read what the change is for and who asked. Review against that brief, not your own taste.
2. Get the real screens: renders or screenshots of each changed screen, before and after, light and dark, at the default and the largest text size. If the author didn't include them, make them (see the app-renders skill) or ask for them.
3. Find the app's own rules (a ui-rules or design-system doc, its tokens file) and review against those first.

## The checks

| Check | Law | What fails it |
|---|---|---|
| Answers within 100 ms | Doherty | A spinner while the network answers; no pressed state; a failure with no Retry |
| Hit areas | Fitts | Under 44 × 44 pt on a phone, 24 × 24 pt on a desktop; no hover state on a desktop |
| Few choices | Hick | More than five items in a menu or toolbar before a More |
| The platform's pattern | Jakob | A home-made control where Mail, Finder or Slack already has one |
| One meaning, one look | Similarity | A colour, badge or tint used for two meanings; a one-off value instead of a token |
| Red is for "needs you" | Von Restorff | Red as decoration, or for something that isn't failing or waiting on the person |
| Small rows | Miller | More than four pieces of metadata on a row |
| Nothing twice | Occam | The same fact shown twice on one screen |
| Four states | Tesler | A screen with no loading, empty, error or offline state, or one with no next step |
| No lost input | Postel | A draft lost on navigation, a pasted link or file refused |
| Undo over confirm | | "Are you sure?" on something reversible |
| Keyboard path | | A desktop action with no key, or a list without ↑/↓, Return, typing and Esc |
| Access | | An icon-only button without a label; truncation at the largest text size; missing dark mode |

## Reporting

- Lead with the verdict: approved, approved with one change, or changes needed.
- One point per finding: what fails, which check, the render that shows it, and the smallest fix.
- Ask for one specific change at a time, most important first. Approve what's good as it is.
- Say what you didn't check (a device you couldn't run, VoiceOver you didn't try).
