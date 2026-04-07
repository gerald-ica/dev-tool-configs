---
name: openscreen
description: Free open-source screen recording and editing desktop app. Use when building screen recording features, creating product demos, working with Electron video capture, or implementing timeline-based video editing. Alternative to Screen Studio.
version: "1.0.0"
license: See LICENSE in repository
metadata:
  homepage: "https://github.com/siddharthvaddem/openscreen"
  openclaw:
    emoji: "🎬"
    homepage: "https://github.com/siddharthvaddem/openscreen"
    requires:
      bins:
        - node
        - npm
---

# OpenScreen

A free, open-source desktop app for screen recording and polished product demos. A simplified alternative to Screen Studio.

## What It Does

Records screen/window capture, provides timeline-based editing with professional effects, and exports polished videos. Built with Electron + React.

## Key Features

**Recording:**
- Record specific windows or entire screen via `desktopCapturer` API
- Capture microphone and system audio
- HUD overlay for source selection

**Editing:**
- Automatic or manual zoom effects with adjustable depth
- Motion blur for smoother pan/zoom animations
- Variable segment speed (slow-mo, fast-forward)
- Video cropping and timeline-based trimming
- Text, arrow, and image annotations

**Visual Customization:**
- Multiple backgrounds: wallpapers, solid colors, gradients, custom images
- Dark theme interface

**Export:**
- Multiple aspect ratios and resolutions
- WebM format with duration correction

## Setup

```bash
git clone https://github.com/siddharthvaddem/openscreen.git
cd openscreen
npm install
npm run dev    # Development with Vite HMR
npm run build  # Production build
```

**Platform builds:**
```bash
npm run build:mac
npm run build:win
npm run build:linux
```

**macOS notes:**
- Handle Gatekeeper: `xattr -rd com.apple.quarantine /Applications/Openscreen.app`
- Grant screen recording + accessibility permissions in System Settings

## Architecture

Multi-window Electron app with URL-parameter-based routing:
- **HUD Overlay** (`windowType=hud-overlay`): Transparent overlay for recording control
- **Source Selector** (`windowType=source-selector`): Window/screen picker
- **Editor** (`windowType=editor`): Full editing interface with timeline

**Tech stack:** Electron, React, PixiJS (video preview/timeline), dnd-timeline (drag-and-drop editing), Vite, Radix UI, Vitest + Playwright for testing.

## When to Use This Skill

- Building screen recording features in Electron apps
- Creating product demo/walkthrough tooling
- Implementing timeline-based video editing UI
- Working with `desktopCapturer` API and WebM processing
- Designing multi-window Electron architectures
