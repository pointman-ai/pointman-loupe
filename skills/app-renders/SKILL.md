---
name: app-renders
description: Make renders and screenshots of real app screens as evidence (SwiftUI on macOS and iOS), before and after a change, light and dark, at the largest text size. Use when a UI change needs pictures for a review or a report.
---

# Renders of real screens

Evidence is a picture of the real view, not a mockup. Make each one at the size people will see it, and look at it yourself before you post it.

## What to make

- Each changed screen, **before and after**, in **light and dark**, at the **default and the largest** text size.
- For a flow, a short screen recording beats a row of stills.
- Put them on a page beside each other with one line saying what changed, and link it in the thread.

## Before and after without touching anyone's checkout

1. `git worktree add --detach <before-dir> <base-commit>`: the base in a folder of its own.
2. Build the same render test in both folders, each with its own derived data, on the same simulator.
3. Run both with the same test names, so the pictures pair up by name.

Never stash or switch branches in a shared checkout to get a "before".

## macOS (SwiftUI)

- `ImageRenderer` leaves out ScrollView contents. Put the view in an off-screen **borderless** `NSWindow` (at x = -6000, borderless so the height isn't cut to the screen) with an `NSHostingView`, and capture it with `bitmapImageRepForCachingDisplay` + `cacheDisplay`.
- Give the root view `.background(Color(nsColor: .windowBackgroundColor))`, or dark renders come out transparent.
- In an async `@MainActor` test, wait with `try await Task.sleep`, never `RunLoop.main.run`: that blocks the view's own loading.
- Titled off-screen windows don't draw materials or glass. To capture those, grab your own window with `CGWindowListCreateImage`.
- If someone is using the Mac, don't open test windows on their screen: build a small harness app (the app's sources without its `@main`, its own bundle id, no sandbox, an accessory activation policy) that draws off screen from fixtures.

## iOS and iPadOS

- A render test that draws each screen into a `UIWindow` with `drawHierarchy` captures UIKit's own controls; `ImageRenderer` misses some.
- `xcrun simctl io <device> screenshot x.png` for a running app. A landscape iPad shot needs `sips -r 270`.
- XCUITest screenshots after a rotation come out cropped. Record instead: `xcrun simctl io <device> recordVideo --codec h264 --force x.mp4` in the background, stop it with `pkill -INT -f recordVideo`, then take stills with `ffmpeg -i x.mp4 -vf fps=2`.
- Text size: launch with `-UIPreferredContentSizeCategoryName UICTContentSizeCategoryAccessibilityXXXL` for the largest.

## UI tests

- An `.accessibilityIdentifier` on a container replaces its children's own: find children by label.
- Seed the screen's data from fixtures, not from a live service, so every state (loading, empty, error, offline) can be drawn on purpose.
