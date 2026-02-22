# 📊 Tableau Chart Type Decisions Skill
**A Claude AI skill by [DataMonster](https://Data.Monster) — Pablo Gomez**
*Tableau Visionary · Ambassador · London, UK*

> Choose the right chart every time. This skill applies DataMonster's visualisation philosophy to recommend, critique, and design chart types for Tableau dashboards — with decision frameworks, rules for what to avoid, color guidelines, and layout principles.

---

## What this skill does

Load this skill and Claude applies DataMonster's design thinking to every chart recommendation:

- **Decision framework** — analytical task → data shape → audience, before any chart is suggested
- **Chart type reference** — comparison, time series, distribution, composition, relationship, geography, small multiples
- **The never-use list** — pie charts, 3D charts, gauges, radar charts, word clouds, and why
- **Colour usage rules** — sequential, diverging, categorical, highlight palettes and when to use each
- **Dashboard layout principles** — hierarchy, whitespace, grid alignment, KPI placement

**DataMonster's core philosophy:** clarity over complexity, one chart one insight, colour is meaning — never decoration.

---

## How to use it

### In claude.ai chat ✅ Recommended for most users

> **Requires:** Free claude.ai account at [claude.ai](https://claude.ai)

1. Click the **download icon** on this file's GitHub page to save the `.md` file to your computer
2. Open [claude.ai](https://claude.ai) and start a new conversation
3. Click the **paperclip / attachment icon** in the chat input and attach the `.md` file
4. Write your request in the same message — Claude reads the skill and gets straight to work

### In Claude Code

> **Requires:** Claude Pro or Max subscription

1. Save this file to `.claude/skills/tableau-chart-type-decisions-skill.md` in your project
2. Reference it at the start of a session:
   > *"Read `tableau-chart-type-decisions-skill.md` then recommend a chart for..."*

---

## Example prompts

```
Which regions are underperforming vs target this quarter?
Data: [Region], [Sales], [Target]. One row per region. Executive audience.
```

```
I want to show how 12 product categories have trended over the last 3 years.
Analyst audience. What chart type should I use?
```

```
I have customer satisfaction scores from 0–10 across 5 departments.
I want to show distribution, not just averages. What do you recommend?
```

```
My dashboard has 6 charts and feels cluttered. Review my layout approach:
[describe your current layout]. What should I change?
```

```
Should I use a pie chart to show market share across 5 competitors?
```

---

## The "Never Use" List

| Chart | Why DataMonster avoids it |
|-------|--------------------------|
| Pie chart | Humans cannot accurately compare angles |
| Donut chart | Same problems as pie, with a hole |
| 3D charts (any) | Distorts perception, adds zero information |
| Gauge / speedometer | Wastes space, terrible data-ink ratio |
| Radar / spider chart | Perceptually misleading, hard to compare |
| Word cloud | Font size ≠ frequency is not reliable encoding |

---

## About DataMonster

These skills were created by **Pablo Gomez**, known in the DataFam as **DataMonster** — a Tableau Visionary and Tableau Ambassador, Data Storyteller, and public speaker based in London, UK. Passionate about applying AI responsibly to make data stories clearer and more human.

🔗 [data.monster](https://Data.Monster) · [LinkedIn](https://www.linkedin.com/in/pablolgomez) · [Tableau Public](https://public.tableau.com/app/profile/pablolgomez)

> Shared freely with the DataFam community. Use it, adapt it, build on it — a shoutout is always appreciated but never required. That's the DataFam way. 💙

---
---

<!--
  ============================================================
  CLAUDE INSTRUCTIONS — Everything below is for Claude only.
  Human readers can stop here.
  ============================================================
-->

## Purpose

This skill guides Claude when recommending, critiquing, or designing chart types for Tableau dashboards. Always read this file before suggesting a visualisation approach. Recommendations should reflect DataMonster's design philosophy: clarity over complexity, earned sophistication, and data storytelling over data displaying.

---

## DataMonster's Visualisation Philosophy

1. **Chart type serves the question** — never choose a chart because it looks impressive
2. **One chart, one insight** — if a chart needs a paragraph to explain, it needs to be redesigned
3. **Interaction is not a substitute for clarity** — the static state of a dashboard should already communicate the main message
4. **Reduce to essentials** — remove every element that doesn't carry information
5. **Colour is meaning** — never use colour decoratively

---

## The Decision Framework

Before recommending a chart, always establish:

1. **What is the analytical task?**
   - Compare values
   - Show distribution
   - Show composition / part-to-whole
   - Show relationship / correlation
   - Show change over time
   - Show geography
   - Show ranking

2. **What is the data shape?**
   - How many dimensions? (1, 2, many)
   - How many measures?
   - Is time involved?
   - What is the cardinality of key dimensions? (few = <8, many = 8+)

3. **Who is the audience?**
   - Executive (needs immediate answer, minimal detail)
   - Analyst (needs drill-down, tolerates complexity)
   - Operational (needs current status, thresholds, alerts)

---

## Chart Type Reference

### Comparison

| Situation | Preferred Chart | Avoid |
|-----------|----------------|-------|
| Comparing few categories (≤8), single measure | Horizontal bar | Vertical bar if labels are long |
| Comparing many categories (8+) | Horizontal bar with scrolling or TOP N + Other | Cluttered legend |
| Comparing two measures across categories | Dot plot / connected dot plot | Dual-axis bar (misleading scales) |
| Comparing before/after for many items | Slope chart | Side-by-side bars |
| Comparing actual vs target | Bullet chart | Gauge / speedometer |
| Ranking with magnitude | Bar chart sorted descending | Arbitrary sort order |

**DataMonster's rules:**
- Sort bars by value by default — alphabetical sort is almost never the right choice
- Horizontal bars beat vertical when category labels are words (avoids diagonal text)
- Bullet charts are DataMonster's go-to for KPI + target in one
- Never use a 3D bar chart

---

### Change Over Time

| Situation | Preferred Chart | Avoid |
|-----------|----------------|-------|
| Single measure over time, continuous | Line chart | Bar chart for dense time series |
| Multiple measures over time (≤4 lines) | Multi-line chart with direct labels | Legend-only labelling |
| Multiple measures over time (5+ lines) | Small multiples (trellis) | Spaghetti chart |
| Part-to-whole over time | Stacked area (normalised if % is key) | Stacked bar for time series |
| Highlighting anomalies over time | Line + reference band/line | Raw table |
| YoY or period comparison | Dual-line with current/prior | Side-by-side bars |

**DataMonster's rules:**
- Direct labelling on line ends is always preferred over legends
- If lines cross more than 3 times, consider small multiples instead
- Time should always run left to right on the x-axis — never reversed
- Use `DATETRUNC()` not raw dates to control time granularity
- Avoid starting the y-axis above zero on area charts — it implies a baseline that doesn't exist

---

### Distribution

| Situation | Preferred Chart | Avoid |
|-----------|----------------|-------|
| Distribution of one continuous measure | Histogram | Bar chart with raw values |
| Distribution across categories | Box plot | Multiple histograms overlaid |
| Showing individual data points | Strip plot / dot plot | Hiding outliers in aggregates |
| Large dataset distribution | Binned histogram or violin | Showing every dot |

**DataMonster's rules:**
- Box plots are underused in business — advocate for them when showing spread matters
- Always show the number of records (n=) when showing a distribution
- Outliers should be visible, not hidden in aggregation

---

### Composition / Part-to-Whole

| Situation | Preferred Chart | Avoid |
|-----------|----------------|-------|
| 2–4 parts, static snapshot | Waffle chart or stacked bar (single) | Pie chart |
| 5+ parts, static snapshot | Treemap or horizontal stacked bar | Donut chart |
| Composition change over time | Normalised stacked area | Multiple pies |
| Hierarchical composition | Treemap | Nested pie / sunburst |

**DataMonster's rules:**
- **Pie charts are almost always wrong** — humans cannot accurately compare angles
- The only exception: a single prominent metric shown as % complete (e.g., 73% of target), and even then a bullet chart or arc is cleaner
- Donut charts inherit all of pie's problems and add a hole
- Treemaps work well for 2-level hierarchy; beyond that they become unreadable
- For stacked bars, put the most important segment at the baseline (bottom/left)

---

### Relationship / Correlation

| Situation | Preferred Chart | Avoid |
|-----------|----------------|-------|
| Relationship between 2 measures | Scatter plot | Line chart |
| Relationship between 2 measures, many points | Scatter with density/hex bins | Overplotted scatter |
| 3 measures | Scatter with size encoding | 3D chart |
| Correlation matrix | Heatmap | Table of numbers |
| Network / flow | Sankey (use sparingly) | Chord diagram |

**DataMonster's rules:**
- Scatter plots are underused in business dashboards — push for them when showing correlation
- Size encoding (bubble charts) works for a 3rd measure but becomes unreliable beyond that
- Trend lines should be added intentionally, with R² shown or explained
- Sankey charts are visually impressive but hard to read — use only when flow between stages is the core question

---

### Geography

| Situation | Preferred Chart | Avoid |
|-----------|----------------|-------|
| Country/region level data | Filled map (choropleth) | Symbol map for large polygons |
| Point data (stores, events) | Symbol map | Filled map for points |
| Density of events | Density map | Cluttered symbol map |
| Comparing regions to a metric | Bar chart + map side by side | Map alone |

**DataMonster's rules:**
- Always use a diverging palette for choropleths where a meaningful midpoint exists (e.g., profit positive/negative)
- Sequential palette for one-directional metrics (e.g., revenue)
- Never use a rainbow/spectrum palette — it implies order that doesn't exist
- Maps are context, not always the primary chart — pair with a bar for the actual comparison

---

### Small Multiples (Trellis)

Use small multiples when:
- You have 5+ categories that each need their own time series
- The pattern across panels is as important as the values within them
- You want to avoid a spaghetti chart

DataMonster's small multiple rules:
- **Shared axis scale across all panels** unless the explicit point is scale difference
- Keep panels compact — label only, no full axis on every panel
- Order panels by a meaningful metric (e.g., highest total sales first), not alphabetically
- Maximum ~12 panels before it becomes a wall of charts

---

## Charts DataMonster Never Uses

| Chart | Reason |
|-------|--------|
| Pie chart | Angle perception is inaccurate |
| Donut chart | Same as pie, worse |
| 3D charts (any type) | Distorts perception, adds no information |
| Gauge / speedometer | Wastes space, poor data-ink ratio |
| Radar / spider chart | Perceptually misleading, hard to compare |
| Waterfall (default Tableau) | Use only for financial P&L, never for general comparison |
| Word cloud | Frequency ≠ font size is not a reliable encoding |

---

## Colour Usage Rules

### Palette Types
- **Sequential** (light→dark, one hue): for one-directional continuous measures (revenue, volume)
- **Diverging** (two hues meeting at midpoint): for measures with a meaningful zero or target (profit, variance to plan)
- **Categorical** (distinct hues): for nominal dimensions; max 8 colours before it breaks down
- **Highlight** (one accent + grey): for drawing attention to a single category

### Rules
- Max 8 categorical colours in any single view
- Grey is a colour — use it for "everything else" or "context"
- Red = bad, Green = good is a near-universal convention — don't subvert it without a reason
- Never use red/green as the only differentiator (colour blindness)
- Colour blind safe alternatives: Blue/Orange, Blue/Red with sufficient contrast

### DataMonster's Accent Palette
```xml
<!-- Add to Tableau Preferences.tps -->
<color-palette name="DataMonster Custom" type="regular">
  <color>#1A6FAF</color>  <!-- Primary blue -->
  <color>#F28C00</color>  <!-- Accent orange -->
  <color>#CC2936</color>  <!-- Alert red -->
  <color>#3DAA6E</color>  <!-- Positive green -->
  <color>#7F7F7F</color>  <!-- Neutral grey -->
  <color>#4E4E8A</color>  <!-- Secondary purple -->
</color-palette>
```

---

## Dashboard Layout Principles

### The Hierarchy
1. **Top left = most important** — eye tracks F-pattern or Z-pattern
2. **KPIs first** — headline numbers at the top before supporting charts
3. **Context before detail** — overview → filter → detail flow
4. **Consistent visual weight** — don't let one chart dominate unless it's intentionally the hero

### DataMonster's Layout Rules
- Max 3–4 charts on a single dashboard view — more needs tabs or drill-through
- Whitespace is not wasted space — padding creates breathing room and hierarchy
- Align everything to a grid — misaligned elements read as mistakes
- Fixed size dashboards for controlled presentation; range/auto for embedded

---

## How to Ask Claude for Chart Recommendations

Provide:
1. **The question the chart answers** (e.g., "Which regions are underperforming vs target?")
2. **The data shape** (dimensions, measures, row grain)
3. **The audience** (executive, analyst, operational)
4. **Any constraints** (must work in Tableau Public, must be printable, etc.)

Example prompt:
> "Using this skill, recommend a chart for: showing how 12 product categories perform vs last year's sales, for an executive audience. Data has [Category], [Sales this year], [Sales last year], [Target]. One row per category."

Claude should respond with: recommended chart type, reasoning against the alternatives, colour approach, and any Tableau-specific implementation notes.
