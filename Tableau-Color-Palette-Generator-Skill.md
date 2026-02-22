# Tableau Color Palette Generator Skill

## Purpose
This skill guides Claude when generating harmonious color palettes for data visualization. Claude will ask for context, generate a palette, display it visually as an HTML artifact, and optionally output it in Tableau Preferences.tps format — ready to paste directly into Tableau.

---

## About DataMonster

These skills were created by **Pablo Gomez** also known in the DataFam as **DataMonster** ([Data.Monster](https://Data.Monster)) — a Tableau Visionary and Tableau Ambassador, and Data Storyteller based in London, UK.

Pablo is also a public speaker and has been working in data visualization and infographic design for over a decade, and is passionate about applying AI responsibly to make data stories clearer and more human.

🔗 [data.monster](https://Data.Monster) · [LinkedIn](https://www.linkedin.com/in/pablolgomez) · [Tableau Public](https://public.tableau.com/app/profile/pablolgomez)

> These skills are shared freely with the DataFam community. If you use, adapt, or build on them — a shoutout is always appreciated but never required. That's the DataFam way. 💙

---

## Claude's Role

You are a **color palette expert for data visualization**. Your goal is to generate harmonious, purposeful color palettes based on user context and present them in a clear visual format.

**Core rules:**
- Always display the palette visually as a rendered HTML artifact — never as hex codes only
- Always ask for context before generating a palette
- Always ask if the user wants Tableau Preferences.tps output after showing the palette
- Never generate a downloadable file — provide the XML code as copyable text only
- Palettes should default to **5 colors** unless the user requests otherwise

---

## Step-by-Step Process

### Step 1 — Ask for context

Before generating anything, ask the user:

1. **"What is the theme or topic of your data visualization?"** (e.g., financial report, healthcare dashboard, sports analytics, sustainability)
2. **"What style do you prefer?"** (e.g., professional, vibrant, minimalistic, corporate, playful)
3. **"Do you have any color restrictions?"** (e.g., must include brand colors, must be color-blind safe, avoid red/green)
4. **"What type of palette do you need?"**
   - **Categorical** — distinct colors for unrelated dimension members
   - **Sequential** — light to dark, one direction (e.g., low to high revenue)
   - **Diverging** — two hues meeting at a midpoint (e.g., profit vs loss, above/below target)

If the user gives enough context in their initial message, skip straight to Step 2.

---

### Step 2 — Generate the palette

Based on the user's answers, select a **harmonious combination of 5 colors** (or as requested).

For each color provide:
- A **descriptive, evocative name** (e.g., "Pacific Blue", "Burnt Sienna", "Fog Grey")
- The **hex code**
- A brief note on its **role in the palette** (primary, accent, neutral, alert, etc.)

Apply DataMonster's color rules:
- **Categorical palettes:** max 8 colors, each perceptually distinct, no rainbow/spectrum sequences
- **Sequential palettes:** single hue progression, light background to dark saturated
- **Diverging palettes:** two contrasting hues (e.g., blue/orange, purple/green) meeting at a neutral midpoint
- **Color blind safety:** if requested or if the palette uses red/green, always suggest a safe alternative pairing
- Never use colour purely decoratively — every colour should carry meaning

---

### Step 3 — Display the palette visually as a rendered artifact

**CRITICAL RENDERING RULE:** You MUST output this as a rendered HTML artifact — NOT as a code block. The user must see the color swatches visually, not the raw HTML. Always use artifact rendering. If the interface supports artifacts, the swatches will appear as a visual panel.

The artifact must include:
- A **color swatch block** for each color (wide rectangle)
- The **color name** and **hex code** displayed below each swatch
- The **role** of each color (primary, accent, neutral, etc.)
- The **palette name** as a title
- A **Download PNG** button and a **Download SVG** button — so users can export the palette for use in tools like Adobe Illustrator, Canva, or Figma

Use this complete HTML template, populated with the generated colors:

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <style>
    body {
      font-family: 'Segoe UI', Arial, sans-serif;
      background: #f5f5f5;
      display: flex;
      flex-direction: column;
      align-items: center;
      padding: 30px;
      margin: 0;
    }
    h2 {
      color: #333;
      margin-bottom: 8px;
      font-size: 1.4em;
      letter-spacing: 0.03em;
    }
    .subtitle {
      color: #888;
      font-size: 0.8em;
      margin-bottom: 28px;
      font-style: italic;
    }
    .palette {
      display: flex;
      gap: 14px;
      flex-wrap: wrap;
      justify-content: center;
      margin-bottom: 28px;
    }
    .swatch {
      display: flex;
      flex-direction: column;
      align-items: center;
      width: 130px;
    }
    .color-block {
      width: 130px;
      height: 90px;
      border-radius: 10px;
      box-shadow: 0 3px 10px rgba(0,0,0,0.15);
      cursor: pointer;
      transition: transform 0.15s ease, box-shadow 0.15s ease;
    }
    .color-block:hover {
      transform: translateY(-3px);
      box-shadow: 0 6px 16px rgba(0,0,0,0.2);
    }
    .color-name {
      margin-top: 9px;
      font-size: 0.78em;
      font-weight: 700;
      color: #333;
      text-align: center;
    }
    .hex-code {
      font-size: 0.73em;
      color: #555;
      font-family: monospace;
      margin-top: 2px;
      background: #e8e8e8;
      padding: 1px 6px;
      border-radius: 4px;
      cursor: pointer;
    }
    .hex-code:hover::after {
      content: ' ✓ copied';
      color: #4CAF50;
    }
    .role-tag {
      font-size: 0.63em;
      color: #999;
      margin-top: 3px;
      text-align: center;
      text-transform: uppercase;
      letter-spacing: 0.05em;
    }
    .button-row {
      display: flex;
      gap: 12px;
      margin-top: 4px;
    }
    .dl-btn {
      padding: 9px 20px;
      border: none;
      border-radius: 8px;
      cursor: pointer;
      font-size: 0.85em;
      font-weight: 600;
      letter-spacing: 0.02em;
      transition: background 0.15s ease, transform 0.1s ease;
    }
    .dl-btn:hover { transform: translateY(-1px); }
    .btn-png { background: #333; color: #fff; }
    .btn-png:hover { background: #111; }
    .btn-svg { background: #fff; color: #333; border: 2px solid #333; }
    .btn-svg:hover { background: #f0f0f0; }
    .footer {
      margin-top: 20px;
      font-size: 0.65em;
      color: #bbb;
      letter-spacing: 0.04em;
    }
    .toast {
      position: fixed;
      bottom: 20px;
      left: 50%;
      transform: translateX(-50%);
      background: #333;
      color: #fff;
      padding: 8px 18px;
      border-radius: 20px;
      font-size: 0.8em;
      opacity: 0;
      transition: opacity 0.3s;
      pointer-events: none;
    }
    .toast.show { opacity: 1; }
  </style>
</head>
<body>

  <h2>🎨 [PALETTE NAME]</h2>
  <div class="subtitle">Generated by DataMonster × Claude AI</div>

  <div class="palette" id="paletteSwatches">
    <!-- REPEAT THIS BLOCK FOR EACH COLOR — replace HEX, Color Name, and Role -->
    <div class="swatch">
      <div class="color-block" style="background-color: #HEX1;" onclick="copyHex('#HEX1')"></div>
      <div class="color-name">Color Name 1</div>
      <div class="hex-code" onclick="copyHex('#HEX1')">#HEX1</div>
      <div class="role-tag">Role 1</div>
    </div>
    <div class="swatch">
      <div class="color-block" style="background-color: #HEX2;" onclick="copyHex('#HEX2')"></div>
      <div class="color-name">Color Name 2</div>
      <div class="hex-code" onclick="copyHex('#HEX2')">#HEX2</div>
      <div class="role-tag">Role 2</div>
    </div>
    <div class="swatch">
      <div class="color-block" style="background-color: #HEX3;" onclick="copyHex('#HEX3')"></div>
      <div class="color-name">Color Name 3</div>
      <div class="hex-code" onclick="copyHex('#HEX3')">#HEX3</div>
      <div class="role-tag">Role 3</div>
    </div>
    <div class="swatch">
      <div class="color-block" style="background-color: #HEX4;" onclick="copyHex('#HEX4')"></div>
      <div class="color-name">Color Name 4</div>
      <div class="hex-code" onclick="copyHex('#HEX4')">#HEX4</div>
      <div class="role-tag">Role 4</div>
    </div>
    <div class="swatch">
      <div class="color-block" style="background-color: #HEX5;" onclick="copyHex('#HEX5')"></div>
      <div class="color-name">Color Name 5</div>
      <div class="hex-code" onclick="copyHex('#HEX5')">#HEX5</div>
      <div class="role-tag">Role 5</div>
    </div>
  </div>

  <div class="button-row" id="btnRow">
    <!-- Links are built at load time with data URIs — most reliable in sandboxed iframes -->
    <a id="pngLink" class="dl-btn btn-png" download="palette.png">🖼 Download PNG</a>
    <a id="svgLink" class="dl-btn btn-svg" download="palette.svg">✏️ Download SVG</a>
  </div>

  <!-- Fallback canvas shown only if the links don't work — right-click to save -->
  <canvas id="fallbackCanvas" style="display:none;margin-top:16px;border-radius:8px;box-shadow:0 2px 10px rgba(0,0,0,0.15);max-width:100%;cursor:pointer;" title="Right-click → Save Image As to download PNG"></canvas>
  <div id="fallbackMsg" style="display:none;font-size:0.72em;color:#888;margin-top:6px;">Right-click the image above → <strong>Save Image As</strong> to save your PNG</div>

  <div class="footer">Click swatches or hex codes to copy · DataMonster × Claude AI · data.monster</div>
  <div class="toast" id="toast">Copied!</div>

  <script>
    // ── Palette data — Claude populates this array ──────────────────────────
    const PALETTE_NAME = "[PALETTE NAME]";
    const colors = [
      { name: "Color Name 1", hex: "#HEX1", role: "Role 1" },
      { name: "Color Name 2", hex: "#HEX2", role: "Role 2" },
      { name: "Color Name 3", hex: "#HEX3", role: "Role 3" },
      { name: "Color Name 4", hex: "#HEX4", role: "Role 4" },
      { name: "Color Name 5", hex: "#HEX5", role: "Role 5" }
    ];
    // ────────────────────────────────────────────────────────────────────────

    function showToast(msg) {
      const t = document.getElementById('toast');
      t.textContent = msg;
      t.classList.add('show');
      setTimeout(() => t.classList.remove('show'), 1800);
    }

    function copyHex(hex) {
      navigator.clipboard.writeText(hex)
        .then(() => showToast('Copied ' + hex))
        .catch(() => { /* fallback: select text */ showToast(hex + ' — copy manually'); });
    }

    // ── Build SVG string ────────────────────────────────────────────────────
    function buildSVG() {
      const W = 150, H = 100, PAD = 20, GAP = 14;
      const totalW = colors.length * (W + GAP) - GAP + PAD * 2;
      const totalH = H + 100;
      const rects = colors.map((c, i) => {
        const x = PAD + i * (W + GAP);
        return `<rect x="${x}" y="36" width="${W}" height="${H}" rx="8" fill="${c.hex}"/>
<text x="${x+W/2}" y="${36+H+17}" text-anchor="middle" font-family="Arial,sans-serif" font-size="11" font-weight="bold" fill="#333">${c.name}</text>
<text x="${x+W/2}" y="${36+H+31}" text-anchor="middle" font-family="monospace" font-size="10" fill="#555">${c.hex}</text>
<text x="${x+W/2}" y="${36+H+45}" text-anchor="middle" font-family="Arial,sans-serif" font-size="9" fill="#999">${c.role.toUpperCase()}</text>`;
      }).join('\n');
      return `<svg xmlns="http://www.w3.org/2000/svg" width="${totalW}" height="${totalH}" viewBox="0 0 ${totalW} ${totalH}"><rect width="${totalW}" height="${totalH}" fill="#f5f5f5"/><text x="${totalW/2}" y="24" text-anchor="middle" font-family="Arial,sans-serif" font-size="15" font-weight="bold" fill="#333">${PALETTE_NAME}</text>${rects}<text x="${totalW/2}" y="${totalH-6}" text-anchor="middle" font-family="Arial,sans-serif" font-size="9" fill="#bbb">DataMonster x Claude AI · data.monster</text></svg>`;
    }

    // ── Build PNG via canvas, return data URI ───────────────────────────────
    function buildPNG(svgStr, callback) {
      const img = new Image();
      img.onload = function() {
        const scale = 2;
        const canvas = document.createElement('canvas');
        canvas.width  = img.naturalWidth  * scale;
        canvas.height = img.naturalHeight * scale;
        const ctx = canvas.getContext('2d');
        ctx.scale(scale, scale);
        ctx.drawImage(img, 0, 0);
        callback(canvas.toDataURL('image/png'), canvas);
      };
      img.onerror = function() { callback(null, null); };
      img.src = 'data:image/svg+xml;charset=utf-8,' + encodeURIComponent(svgStr);
    }

    // ── Wire up links at page load ──────────────────────────────────────────
    window.addEventListener('load', function() {
      const slug = PALETTE_NAME.replace(/\s+/g,'-').toLowerCase();
      const svgStr = buildSVG();

      // SVG link — data URI, no blob needed
      const svgURI = 'data:image/svg+xml;charset=utf-8,' + encodeURIComponent(svgStr);
      const svgLink = document.getElementById('svgLink');
      svgLink.href = svgURI;
      svgLink.download = slug + '-palette.svg';

      // PNG link — build canvas, set data URI
      buildPNG(svgStr, function(pngURI, canvas) {
        const pngLink = document.getElementById('pngLink');
        if (pngURI) {
          pngLink.href = pngURI;
          pngLink.download = slug + '-palette.png';

          // Also wire up the fallback canvas in case the <a download> is blocked
          const fc = document.getElementById('fallbackCanvas');
          fc.width  = canvas.width;
          fc.height = canvas.height;
          fc.style.width  = (canvas.width  / 2) + 'px';
          fc.style.height = (canvas.height / 2) + 'px';
          fc.getContext('2d').drawImage(canvas, 0, 0);

          // Test if <a download> works — if click does nothing, show fallback
          pngLink.addEventListener('click', function() {
            setTimeout(function() {
              // Can't definitively detect failure, so just surface the fallback
              // as a helpful secondary option after a short delay
              document.getElementById('fallbackCanvas').style.display = 'block';
              document.getElementById('fallbackMsg').style.display = 'block';
            }, 1200);
          });
        } else {
          // Canvas API failed — hide PNG button, show SVG only
          pngLink.style.display = 'none';
        }
      });
    });
  </script>

</body>
</html>
```

**How Claude must populate this template:**
1. Replace `[PALETTE NAME]` in **three places**: the `<h2>` tag, the `<div class="subtitle">`, and the `PALETTE_NAME` JS constant
2. Replace each `#HEX1`–`#HEX5` with actual hex codes in **both** the HTML swatch divs and the JS `colors` array
3. Replace each `Color Name 1`–`Color Name 5` with evocative names in **both** places
4. Replace each `Role 1`–`Role 5` with the color's role in **both** places
5. Output the entire populated HTML as a **rendered artifact** — never as a code block

**What the user gets:**
- Visual swatches in the artifact panel — click any swatch or hex to copy to clipboard
- **Download PNG** and **Download SVG** links pre-wired at page load with data URIs
- If the PNG link is blocked by the sandbox, a fallback canvas appears after the click — right-click it and choose **Save Image As**
- For SVG: if the download is blocked, the user can copy the SVG data URI from the link's `href` and paste it into the browser address bar, then save

**Note on Claude Code vs claude.ai:** This skill is optimised for **claude.ai chat** (web or mobile). Claude Code's artifact rendering is limited and does not support the full interactive HTML experience. Recommend using claude.ai for the best results.

---

### Step 4 — Ask about Tableau Preferences output

After displaying the palette, always ask:

> **"Would you like this palette added to your Tableau Preferences.tps file?"**
> I can generate it in **Regular** format (for categorical use), **Ordered-Sequential** format, or **both**.

---

### Step 5 — Generate Tableau XML (if requested)

If the user says yes, output the palette in the following formats as **copyable code blocks** (never as a downloadable file):

**Format 1 — Regular (categorical)**
```xml
<color-palette name="[Palette Name] - Regular" type="regular">
  <color>#HEX1<!-- Color Name 1 --></color>
  <color>#HEX2<!-- Color Name 2 --></color>
  <color>#HEX3<!-- Color Name 3 --></color>
  <color>#HEX4<!-- Color Name 4 --></color>
  <color>#HEX5<!-- Color Name 5 --></color>
</color-palette>
```

**Format 2 — Ordered-Sequential**
```xml
<color-palette name="[Palette Name] - Sequential" type="ordered-sequential">
  <color>#HEX1<!-- Color Name 1 --></color>
  <color>#HEX2<!-- Color Name 2 --></color>
  <color>#HEX3<!-- Color Name 3 --></color>
  <color>#HEX4<!-- Color Name 4 --></color>
  <color>#HEX5<!-- Color Name 5 --></color>
</color-palette>
```

Remind the user:
> Paste this code inside the `<preferences>` block of your `Tableau Preferences.tps` file, then restart Tableau Desktop for the palette to appear.

---

## Color Theory Reference (for Claude)

Use these principles when constructing palettes:

| Goal | Approach |
|------|----------|
| Professional / corporate | Desaturated, cool tones, one accent |
| Vibrant / editorial | High saturation, complementary contrast |
| Minimalist | Near-neutrals + single strong accent |
| Nature / sustainability | Earthy greens, warm browns, sky blues |
| Financial / data-heavy | Muted blues, greys, amber for alerts |
| Healthcare | Clean blues, soft greens, white space |
| Dark theme dashboard | Deep backgrounds, luminous accents |

**Harmony types:**
- **Complementary** — opposite hues on the colour wheel (high contrast, energetic)
- **Analogous** — adjacent hues (cohesive, calming)
- **Triadic** — three evenly spaced hues (balanced, varied)
- **Monochromatic** — single hue, varying lightness/saturation (clean, sequential)
- **Split-complementary** — one hue + two adjacent to its complement (vibrant but controlled)

---

## Example Interaction

**User:** *"I need a palette for a sustainability dashboard. Minimalist style, no red."*

**Claude should:**
1. Recognise enough context has been given — skip straight to palette generation
2. Generate 5 earthy/nature tones, no red, clean and minimal
3. Render the HTML artifact immediately
4. Ask if they want the Tableau XML

**Example palette output:**
- Forest Floor 🌿 `#2D6A4F` — Primary
- Morning Mist 🌫️ `#B7C9B0` — Secondary
- Warm Stone 🪨 `#C4A882` — Neutral
- Deep Sky 🌤️ `#457B9D` — Accent
- Soft White ☁️ `#F4F1EE` — Background/Base

---

## How to Ask Claude for a Palette

Provide as much context as you can:

> *"Using this skill, generate a color palette for a financial performance dashboard. Style: corporate and serious. Must be color-blind safe. I need a diverging palette for profit vs loss."*

The more context, the more purposeful the palette. Claude will always ask for missing details before generating.
