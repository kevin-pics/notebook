# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is Kevin's Cornell Notes collection website - a static HTML site showcasing learning notes organized using the Cornell Note-taking System. The site features an interactive index page with filtering and sorting capabilities.

## Architecture

**Static Site Structure:**
- `index.html` - Main index page with Vue 3 SPA that lists all notes
- `cornell/` - Individual Cornell note HTML files (self-contained with inline styles)
- `css/index.css` - Shared styles for the index page
- No build process - pure HTML/CSS/JavaScript

**Index Page (index.html):**
- Vue 3 application (loaded via CDN)
- AirDatepicker for date filtering (single date selection only)
- Data is hardcoded in the Vue data() section as a `notes` array
- Each note object structure:
  ```javascript
  {
    id: number,           // Sequential integer
    title: string,        // Note title
    url: string,          // Relative path to HTML file in cornell/
    tags: string[],       // Array of tags
    date: string,         // Format: 'YYYY-MM-DD HH:mm'
    dateOnly: string      // Format: 'YYYY-MM-DD'
  }
  ```

**Cornell Note Files:**
- Self-contained HTML files with inline CSS
- Follow Cornell Note-taking System format (cue column, notes column, summary)
- Use consistent styling defined in inline `<style>` tags
- Responsive design with mobile support

## Critical Workflow: Adding New Notes

**When a new Cornell note HTML file is added to `cornell/` directory, you MUST update `index.html`:**

1. **Extract metadata from the new note:**
   - Title: Extract from the `<h1>` tag in the note file
   - Tags: Infer from content or ask the user
   - Date: Use current timestamp in format `YYYY-MM-DD HH:mm`

2. **Update the Vue data section in index.html:**
   - Add new note object to the `notes` array
   - Assign next sequential `id` (current max + 1)
   - Set `url` to relative path: `cornell/filename.html`
   - Set both `date` and `dateOnly` fields
   - Update `lastUpdate` field to current date (YYYY-MM-DD)

3. **Verify the update:**
   - Ensure note appears in the index
   - Check filtering and sorting work correctly

## Git Workflow

- This is a GitHub Pages repository (kevin-pics/notebook)
- Always commit changes after updating the index
- Use descriptive commit messages
- `.DS_Store` files are ignored
- `.editorconfig` exists to prevent unwanted formatting changes

## UI/UX Notes

- Date picker uses AirDatepicker (not flatpickr) with Chinese locale
- Filter info displays: "X notes on YYYY-MM-DD" when filtered
- Filter info displays: "X notes in total" when not filtered
- Sort button toggles between ascending/descending date order
- Responsive design: mobile layout adjusts for smaller screens
