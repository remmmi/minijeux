# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

"Cadenas" is a collection of 4 interactive mini-games built with vanilla HTML/CSS/JavaScript. Each game is self-contained in its own directory with an `index.html` file.

## Project Structure

```
cadenas/
├── cryptex/          # Game 1: Cryptex puzzle (password: CYBER)
│   └── index.html
├── couleurs/         # Game 2: Color sequence lock (sequence: Bleu, Jaune, Vert, Rouge)
│   ├── index.html
│   └── modal.html
├── clavnum/          # Game 3: Numeric keypad lock (code: 1234)
│   ├── index.html
│   └── modal.html
└── [game4]/          # Game 4: TBD
```

## Running the Games

Each game is standalone and can be opened directly in a browser:
```bash
# Open in default browser (Linux)
xdg-open cryptex/index.html

# Or simply open the HTML files in any browser
```

## Development Guidelines

- Each game is self-contained in a single HTML file (HTML + CSS + JavaScript)
- No build process or dependencies required
- Games use vanilla JavaScript (no frameworks)
- All styling is embedded in `<style>` tags
- All logic is embedded in `<script>` tags

## Design Principles (established by Cryptex)

Use these principles as a template for all mini-games:

### 1. Configuration Centralisée
Place all game parameters at the TOP of the `<script>` section in a `CONFIG` object:
```javascript
const CONFIG = {
    password: 'SOLUTION',        // Easy to find and modify
    modalTitle: 'SUCCESS!',
    modalContent: `...`,         // Inline option
    // modalContentFile: 'modal.html',  // External file option
    // ... other game-specific settings
};
```

**Why**: Non-technical users can easily modify the game without touching complex code.

### 2. Modal avec Contenu Externe
Every game should support loading reward/hint content from external files:
- Use `fetch()` to load HTML from external files
- Support both inline (`modalContent`) and external (`modalContentFile`) options
- Create a companion `modal.html` file with examples
- Modal should support: text, images, videos, iframes, custom HTML

**Template**:
```javascript
async function loadModalContent() {
    if (CONFIG.modalContentFile) {
        const response = await fetch(CONFIG.modalContentFile);
        const content = await response.text();
        modalBody.innerHTML = content;
    } else {
        modalBody.innerHTML = CONFIG.modalContent;
    }
}
```

### 3. Style Visuel Cohérent
All games share a consistent dark, modern aesthetic:
- **Background**: Dark gradient (`#1a1a2e` → `#16213e`)
- **Primary color**: Cyan/Green glow effects (`#00ffff`, `#00ff00`)
- **Typography**: Clean sans-serif, white text with glows
- **Borders**: Subtle rgba borders with transparency
- **Animations**: Smooth transitions (0.2s - 0.5s ease)
- **Effects**:
  - Text shadows with glow (`text-shadow: 0 0 20px rgba(...)`)
  - Border glow (`box-shadow: 0 0 50px rgba(...)`)
  - Hover effects with scale transform
  - Pulse animations for success states

**Color palette**:
```css
--bg-dark: #1a1a2e;
--bg-medium: #16213e;
--accent-cyan: #00ffff;
--accent-green: #00ff00;
--text-primary: #fff;
--text-secondary: rgba(255,255,255,0.6);
--border: rgba(255,255,255,0.3);
```

### 4. Qualité Perçue (Polish)
Elements that make the game feel premium:

**Interactions fluides**:
- Cursor changes (`grab`, `grabbing`, `pointer`)
- Hover states with visual feedback
- Smooth animations (use `transition`, `@keyframes`)
- Snap-to-grid for discrete values
- Audio feedback (optional but recommended)

**Visual feedback**:
- Active/inactive states clearly differentiated
- Loading states if needed
- Success animations (pulse, glow, scale)
- Error states with visual cues

**Responsive design**:
- Works on desktop and mobile
- Touch events for mobile (`touchstart`, `touchmove`, `touchend`)
- Responsive sizing (`max-width`, `vh/vw` units)

**Modal quality**:
- Backdrop blur/darkening
- Slide-in animation
- Multiple close methods (X button, click outside, ESC key)
- Scrollable content for long hints
- Centered and responsive

### 5. Code Structure Template
Follow this structure for consistency:

```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Game Name - Mini Jeu</title>
    <style>
        /* Reset */
        * { margin: 0; padding: 0; box-sizing: border-box; }

        /* Base styles */
        body { /* dark gradient background */ }

        /* Game-specific styles */

        /* Modal styles (reusable) */
    </style>
</head>
<body>
    <!-- Game HTML -->

    <!-- Modal (standard structure) -->
    <div id="modal" class="modal">
        <div class="modal-content">
            <button class="close-btn" onclick="closeModal()">&times;</button>
            <div class="modal-header"><h2>...</h2></div>
            <div class="modal-body" id="modalBody"></div>
        </div>
    </div>

    <script>
        // ============================================
        // CONFIGURATION
        // ============================================
        const CONFIG = { /* ... */ };

        // ============================================
        // GAME CODE
        // ============================================

        // Modal functions (standard)
        async function loadModalContent() { /* ... */ }
        function showModal() { /* ... */ }
        function closeModal() { /* ... */ }

        // Initialization
        async function init() {
            await loadModalContent();
            // Initialize game...
        }
        init();
    </script>
</body>
</html>
```

### 6. User Experience Patterns

**Progressive disclosure**:
- Start simple (show only game interface)
- Reveal success modal only when puzzle is solved
- Provide subtle hints in UI (placeholder text, icons)

**Error prevention**:
- Validate inputs gracefully
- No breaking errors for user actions
- Fallback content if external files fail to load

**Accessibility**:
- Keyboard support where applicable
- Clear visual feedback for all interactions
- Readable font sizes (minimum 16px for body text)

### 7. Game-Specific Settings
Each game should allow easy customization:
- **Difficulty**: Adjustable challenge level
- **Password/Solution**: Clearly labeled and easy to change
- **Timing**: If timed, configurable duration
- **Content**: Separable reward/hint content
- **Sensitivity**: For drag/input interactions

### 8. File Organization
For each game in `[game-name]/`:
```
game-name/
├── index.html          # Main game file (self-contained)
├── modal.html          # Optional external modal content
└── assets/             # Optional: images, videos, etc.
    ├── hint-image.jpg
    └── reward-video.mp4
```

## Game Details

### Cryptex
- Location: `cryptex/index.html`
- Type: Puzzle game with rotating letter wheels
- Default password: CYBER
- Interaction:
  - Click up/down arrows to rotate one letter at a time
  - Drag wheels with mouse/touch for smooth rotation
  - Wheels snap to discrete letter positions
- Success condition: Align all wheels to spell the correct password

#### Configuration
All configuration is at the top of `cryptex/index.html` in the `CONFIG` object:

```javascript
const CONFIG = {
    password: 'CYBER',              // The secret combination
    modalTitle: '🎉 DÉVERROUILLÉ ! 🎉',  // Modal header text
    modalContent: `<p>...</p>`,     // Inline HTML content for modal
    // OR
    modalContentFile: 'modal.html', // External file to load (uncomment to use)
    dragSensitivity: 1.5            // Drag sensitivity (1.0 = normal)
};
```

#### Modal Content Options
1. **Inline HTML**: Set `modalContent` with HTML string
2. **External file**: Set `modalContentFile` to load from `modal.html` (or any HTML file)
   - Supports text, images, videos, iframes, etc.
   - See `cryptex/modal.html` for examples

### Couleurs (Color Lock)
- Location: `couleurs/index.html`
- Type: Memory and pattern recognition game with color sequences
- Default sequence: Bleu → Jaune → Vert → Rouge
- Interaction:
  - Click color buttons in order to build a sequence
  - Selected colors appear in the display area above
  - Reset button clears the current sequence
  - Validate button checks if the sequence is correct
- Success condition: Enter all colors in the exact order
- Visual feedback:
  - Selected colors pulse briefly when clicked
  - Error sequences trigger a shake animation
  - Success triggers an unlock animation and displays modal

#### Configuration
All configuration is at the top of `couleurs/index.html` in the `CONFIG` object:

```javascript
const CONFIG = {
    // The correct color sequence (easy to modify!)
    correctSequence: ['Bleu', 'Jaune', 'Vert', 'Rouge'],

    // Modal title and content
    modalTitle: '🎉 DÉVERROUILLÉ ! 🎉',
    modalContent: `<p>...</p>`,          // Inline HTML content for modal
    // OR
    // modalContentFile: 'modal.html',   // External file to load (uncomment to use)
};
```

#### Available Colors
The game includes 12 colors arranged in a 3x4 grid:
- **Row 1**: Rouge, Orange, Jaune
- **Row 2**: Vert, Bleu, Violet
- **Row 3**: Indigo, Rose, Marron
- **Row 4**: Gris, Noir, Blanc

#### Modal Content Options
1. **Inline HTML**: Set `modalContent` with HTML string
2. **External file**: Set `modalContentFile: 'modal.html'` (uncomment in config)
   - Supports text, images, videos, iframes, etc.
   - See `couleurs/modal.html` for examples with styled color display

### Clavnum (Numeric Keypad)
- Location: `clavnum/index.html`
- Type: Numeric code entry game with keypad interface
- Default code: 1234
- Interaction:
  - Click number buttons (0-9) to enter code
  - Numbers appear in display area at the top
  - Physical keyboard support (0-9, Enter, Backspace, Escape)
  - Reset button clears the entered code
  - Validate button checks if the code is correct
- Success condition: Enter the exact numeric code
- Visual feedback:
  - Keys pulse when pressed (mouse or keyboard)
  - Monospace display with cyan glow for entered digits
  - Error codes trigger a shake animation
  - Success triggers an unlock animation and displays modal
- Features:
  - Optional code masking (show • instead of digits)
  - Configurable maximum code length
  - Full keyboard support for accessibility

#### Configuration
All configuration is at the top of `clavnum/index.html` in the `CONFIG` object:

```javascript
const CONFIG = {
    // The correct numeric code (easy to modify!)
    correctCode: '1234',

    // Maximum code length (prevents overly long entries)
    maxLength: 6,

    // Hide code display (true = show •, false = show digits)
    hideCode: false,

    // Modal title and content
    modalTitle: '🎉 DÉVERROUILLÉ ! 🎉',
    modalContent: `<p>...</p>`,          // Inline HTML content for modal
    // OR
    // modalContentFile: 'modal.html',   // External file to load (uncomment to use)
};
```

#### Keyboard Controls
- **0-9**: Enter digits
- **Enter**: Validate code
- **Backspace**: Delete last digit
- **Escape**: Reset/clear code
- **ESC** (when modal open): Close modal

#### Modal Content Options
1. **Inline HTML**: Set `modalContent` with HTML string
2. **External file**: Set `modalContentFile: 'modal.html'` (uncomment in config)
   - Supports text, images, videos, iframes, etc.
   - See `clavnum/modal.html` for examples with styled code display
