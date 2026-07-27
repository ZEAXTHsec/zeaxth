# ZEAXTH Micro Games Hub — Design Spec

**Date:** 2026-07-27
**Status:** Approved

## Overview

ZEAXTH is a collection of micro browser games, starting with a Wordle clone (WORDLY). The initial deliverable is a landing page hub + the Wordle game, deployed to Netlify via git.

## File Structure

```
d:\Micro Projects\games\wordle\
├── index.html          ← New: Landing page hub
├── word-guess.html     ← Existing: Wordle game (minor polish)
└── games/              ← Empty folder for future games
```

## Landing Page (`index.html`)

### Layout
1. **Header** — "ZEAXTH" centered, tagline "micro games, no downloads"
2. **Game grid** — centered grid of game cards
   - 1 column on mobile (<480px)
   - 2 columns on tablet (480-768px)
   - 3 columns on desktop (>768px)
3. **Footer** — subtle "more games coming soon" text

### Game Card Design
- Background: `#1a1a1b`, border-radius 8px, subtle border `#3a3a3c`
- Top accent bar: 4px colored strip (green `#6a9963` for Wordle)
- Game emoji/icon (🔤)
- Title: "WORDLY"
- Description: "Guess the 5-letter word in 6 tries"
- "PLAY" button with accent color
- Hover: card lifts 4px, soft glow shadow, 200ms ease transition

### Animations
- Staggered fade-in from below on page load (each card delayed 100ms more than the last)
- Hover lift + glow: 200ms ease
- Subtle pulsing glow on "more coming" placeholder card

### Design System
- Same CSS variables as word-guess.html: `--bg: #121213`, `--text: #f4f4f4`, `--green: #6a9963`, etc.
- Same font stack: 'Helvetica Neue', Arial, sans-serif
- Inline CSS (self-contained, no build step — matches existing approach)

## Wordle Game (`word-guess.html`)

### Changes from current
- Smoother tile flip easing (adjust animation curve)
- Subtle confetti particle effect on win (pure CSS, ~15 lines)
- Small "← ZEAXTH" link in header to navigate back to hub

### Preserved
- All existing CSS, JS, and HTML structure
- Word list, scoring logic, keyboard handling, toast, modal
- Dark theme, same color variables

## Deployment

- Git repo initialized in project directory
- Push to GitHub
- Netlify connected, auto-deploys on push
- Site available at: zeaxth.netlify.app

## Future

- New games added as individual HTML files
- Each new game gets a card on the landing page
- Games folder for organization
