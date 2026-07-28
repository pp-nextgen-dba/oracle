# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## About

Oracle Database knowledgebase — a single static HTML page published via GitHub Pages from `pp-nextgen-dba/oracle`. There is no build system, package manager, or test suite; the entire site is one self-contained `index.html`.

Published at: `https://pp-nextgen-dba.github.io/oracle/`

## Structure

- `index.html` — the entire site: inline `<style>` (~540 lines), markup, and inline `<script>` (~180 lines). Must stay at the repo root so GitHub Pages can serve it directly.
- `reports/repo-report.html` — local repository summary report.
- `README.md` / `AGENTS.md` — repo overview and prior agent guidance (Codex, Windows-oriented).

## Working with this repo

There is no build/lint/test tooling — edit `index.html` directly and open it in a browser to verify changes (no dev server required).

Page sections (anchored by nav links in the `<aside>`): `#map` (learning topics), `#notes` (interactive notes app), `#rman`, `#quick-reference`, `#study-plan`.

### Notes app (`#notes` section)

The only dynamic part of the page. Plain JS, no framework/dependencies:
- Notes persist to `localStorage` under key `oracleKnowledgebaseNotes` as a JSON array; falls back to the hardcoded `starterNotes` array if storage is empty/invalid.
- User-supplied text is rendered via `escapeHtml()` before being injected into `innerHTML` — preserve this when touching `renderNotes()` to avoid reintroducing XSS.
- Category values drive both filter buttons (`data-filter`) and tag styling (`tagClass()`); adding a category requires updating the `<select id="noteCategory">` options, the filter buttons, and `tagClass()` together.
- Edit/delete are handled via event delegation on `#notesList` using `data-edit`/`data-delete` attributes on generated buttons, not per-element listeners.

## Content/commit conventions (from AGENTS.md)

- Keep the site static unless a build step is clearly needed.
- Do not commit passwords, wallets, connection strings, hostnames, usernames, customer details, or server-specific information.
- For Python Oracle examples in the knowledgebase content, prefer `oracledb` thin mode.
