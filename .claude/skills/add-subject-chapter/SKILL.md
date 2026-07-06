---
name: add-subject-chapter
description: Add a new subject chapter to the Oracle Knowledgebase (index.html) — either a summary card in the "Suggested Knowledge Areas" grid, or a full deep-dive section like RMAN with its own nav link, concepts, and command reference. Use when the user asks to add a topic, subject, chapter, or knowledge area to the knowledgebase.
---

# Add Subject Chapter

Adds a new topic to `index.html`, the single-file Oracle knowledgebase page. The
site has two ways a "chapter" can show up, and this skill covers both.

## 1. Gather the chapter details

Ask (or infer from the user's request) for:

- **Subject tag**: one of `Database`, `SQL`, `Admin`, `Performance`. This picks
  the color-coded `.tag` class (`database`, `sql`, `admin`, `performance` — see
  the `.tag.*` rules in the `<style>` block). If the topic doesn't fit an
  existing tag, ask before inventing a new color/class.
- **Chapter title** (e.g. "Partitioning", "Data Guard").
- **Short description** (one sentence, matches the tone of existing `<p>` copy
  in the cards — plain, factual, no marketing language).
- **Depth**: a short card only, or a full dedicated section (like `#rman`) with
  concepts and command references.

## 2. Add the summary card (always)

Open `index.html` and find the `.grid` inside `<section id="map">`. Add a new
`<article class="card">` following the existing pattern exactly:

```html
<article class="card">
  <span class="tag TAGCLASS">SUBJECT</span>
  <h4>Chapter Title</h4>
  <p>One-sentence description.</p>
  <ul>
    <li>Subtopic one</li>
    <li>Subtopic two</li>
    <li>Subtopic three</li>
  </ul>
</article>
```

- `TAGCLASS` is lowercase (`database`, `sql`, `admin`, `performance`).
- Keep bullets to 3-4 short subtopics, matching the style of sibling cards.
- If this chapter also gets a full section (step 3), add a
  `<a class="topic-link" href="#chapter-id">Open ... </a>` line after the
  `<ul>`, mirroring how the Admin card links to `#rman`.
- Place the card at the end of the grid unless the user specifies where it
  belongs.

## 3. Add a full section (only if the chapter needs depth)

For a deep-dive chapter (concepts + commands, not just a summary card), model
it on `<section id="rman">`:

- Add a new `<section id="chapter-id">` after the existing sections in
  `<div class="content">`, with a `.section-header` (`<h3>` title + `<p>`
  intro).
- Use a two-column layout: a `.concept-list` of `.concept-item` blocks (each
  `<h4>` + one-paragraph `<p>`) alongside a stack of `<details class="command-group">`
  elements, each with a `<summary>` and a `.command-body` containing a `<p>`
  and a `<pre><code>` block of real, runnable-looking SQL/RMAN/shell commands.
  Reuse the `.rman-layout` grid class if the two-column concept/commands split
  fits; otherwise use `.two-column`.
- Add a matching entry to the `<nav>` list in `<aside>`
  (`<a href="#chapter-id">Chapter Title</a>`), placed in reading order with the
  other nav links.
- Do not introduce new CSS classes unless nothing existing fits — reuse
  `.card`, `.concept-item`, `.command-group`, `.tag`, etc.

## 4. Constraints (from AGENTS.md)

- Keep the site static — no build step, no new dependencies, no framework.
- Do not commit passwords, wallets, connection strings, hostnames, usernames,
  customer details, or server-specific information in example commands (use
  placeholders like `ORCL`, `HR.EMPLOYEES`, `/backup/rman/` as the existing
  content does).
- Keep prose short and direct, consistent with the existing card and section
  copy.
- `index.html` must stay at the repository root for GitHub Pages.

## 5. Verify

After editing, confirm the file still opens correctly:

```bash
python3 -c "import html.parser; html.parser.HTMLParser().feed(open('index.html').read())"
```

Open `index.html` in a browser (or at least visually re-check the diff) to
confirm the new card/section renders inside the grid/layout and the nav link
(if added) jumps to the right anchor.
