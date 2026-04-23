---
schema: 1
type: note
name: "Apple Health Card"
tagline: "Apple Health Style Datacore Card"
description: |
  This is a Datacore script and CSS snippet that creates a dashboard similar to Apple Health's activity rings.
  
  ## Features
  
  - Displays daily activity rings for move, exercise, and stand goals.
  - Shows a heart rate chart for the last 6 days.
  - Summarizes daily and historical health data.
  
  ## How to Use
  
  1.  **Enable Plugins**: Make sure you have the [Datacore](https://github.com/blacksmithgu/obsidian-dataview) plugin installed and enabled in your Obsidian vault.
  
  2.  **Add CSS Snippet**:
      *   Create a new file in your vault's snippet folder (`.obsidian/snippets/`) named `health-card.css`.
      *   Copy the CSS content below into the `health-card.css` file.
      *   Enable the snippet in Obsidian's settings (`Settings > Appearance > CSS Snippets`).
  
  3.  **Create the Datacore Note**:
      *   Create a new note in your vault.
      *   Copy the Datacore script below into the note.
  
  4.  **Health Data**:
      *   The script queries for notes in a folder named `Health`.
      *   Each note in the `Health` folder should have the following frontmatter properties:
  
          ```yaml
          ---
          date: YYYY-MM-DD
          move: 100
          move_goal: 500
          exercise: 10
          exercise_goal: 30
          stand: 2
          stand_goal: 12
          hr_low: 60
          hr_avg: 80
          hr_high: 120
          hr_resting: 57
          ---
          ```
author: Maws7140
categories:
  - tracker
tags:
  - apple
  - health
screenshots:
  - https://i.ibb.co/G359mZ22/59cbdab83c06.png
plugins:
  - id: datacore
    name: "Datacore"
    version: "0.1.29"
attached_snippets:
  - path: "snippets/health-card-new.css"
    name: "health-card-new"
environment:
  obsidian_version: "unknown"
  theme: "default"
  os: "Win32"
files:
  - path: "Misc/Apple health dashboard.md"
    type: md
    size: 6531
---

# Apple Health Card

Apple Health Style Datacore Card

## Description

This is a Datacore script and CSS snippet that creates a dashboard similar to Apple Health's activity rings.

## Features

- Displays daily activity rings for move, exercise, and stand goals.
- Shows a heart rate chart for the last 6 days.
- Summarizes daily and historical health data.

## How to Use

1.  **Enable Plugins**: Make sure you have the [Datacore](https://github.com/blacksmithgu/obsidian-dataview) plugin installed and enabled in your Obsidian vault.

2.  **Add CSS Snippet**:
    *   Create a new file in your vault's snippet folder (`.obsidian/snippets/`) named `health-card.css`.
    *   Copy the CSS content below into the `health-card.css` file.
    *   Enable the snippet in Obsidian's settings (`Settings > Appearance > CSS Snippets`).

3.  **Create the Datacore Note**:
    *   Create a new note in your vault.
    *   Copy the Datacore script below into the note.

4.  **Health Data**:
    *   The script queries for notes in a folder named `Health`.
    *   Each note in the `Health` folder should have the following frontmatter properties:

        ```yaml
        ---
        date: YYYY-MM-DD
        move: 100
        move_goal: 500
        exercise: 10
        exercise_goal: 30
        stand: 2
        stand_goal: 12
        hr_low: 60
        hr_avg: 80
        hr_high: 120
        hr_resting: 57
        ---
        ```

## Required Plugins

| Plugin | Version | Link |
|--------|---------|------|
| Datacore | 0.1.29 | [GitHub](https://github.com/search?q=Datacore%20obsidian) |

## Attached Snippets

- `snippets/health-card-new.css` — health-card-new

## Installation

1. Download the `.md` file(s) from this repo
2. Place them in your vault
3. Copy the attached CSS snippet files into `.obsidian/snippets/`
4. Enable them in Settings > Appearance > CSS Snippets
5. Install the required plugins listed above

---
*Published via [Vault Hub](https://obsidianvaulthub.com)*
