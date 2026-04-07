---
name: pencildev-to-figma
description: Import Pencil.dev (.pen) design files into Figma. Use when migrating designs from Pencil.dev to Figma, converting .pen files, or bridging Pencil and Figma workflows. Handles screens, components, images, fonts, auto-layout, effects, and rich text.
version: "1.0.0"
license: See LICENSE in repository
metadata:
  homepage: "https://github.com/gui-uxdoccom/pencildev-to-figma"
  openclaw:
    emoji: "🎨"
    homepage: "https://github.com/gui-uxdoccom/pencildev-to-figma"
    requires:
      bins:
        - node
        - npm
---

# Pencil.dev to Figma

A Figma plugin that imports `.pen` design files from Pencil.dev into Figma, preserving the complete design structure without manual rebuilding.

## What It Does

Reads Pencil.dev JSON files (.pen v2.9+) and recreates the full design in Figma:
- All screen frames with proper sizing and positioning
- Auto-layout (horizontal/vertical with gap, padding, alignment)
- Groups, rectangles, ellipses, lines, polygons, paths, and text nodes
- Reusable components become Figma Components with proper instances
- Fills: solid, image, linear/radial/angular gradients
- Strokes, effects (shadows, blur), corner radius, opacity, rotation
- Rich text with per-segment formatting
- Variable resolution (`$varName` references)

## Setup

```bash
git clone https://github.com/gui-uxdoccom/pencildev-to-figma.git
cd pencildev-to-figma
npm install
npm run build
```

Then in Figma: Plugins > Development > Import plugin from manifest > select `manifest.json`.

## Usage

1. Run the plugin from Figma's Plugins menu
2. Upload a `.pen` file (optionally select a folder with local images)
3. Select which screens to import
4. Review and remap any missing fonts
5. Plugin creates pages with imported screens and a components page

## Key Features

- **Font remapping**: Scans for required fonts, suggests fallbacks for missing ones
- **Image handling**: Loads local images, fetches remote URLs, converts SVG/WebP to PNG automatically
- **Component support**: Reusable nodes become Figma Components on a dedicated page; instances link back
- **Progress feedback**: Real-time updates during import with post-import summary

## Architecture

Uses Figma's dual-runtime:
- **UI iframe** (React): File parsing, image fetching, font scanning
- **Plugin sandbox**: Creates Figma nodes, applies styles, manages pages

Communication via `postMessage` between runtimes.

## When to Use This Skill

- Migrating a design library from Pencil.dev to Figma
- Converting `.pen` prototypes for Figma-based collaboration
- Batch importing multiple Pencil screens into Figma
- Preserving component relationships during migration
