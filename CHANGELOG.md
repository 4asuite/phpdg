# Changelog

## v1.0

**UI redesign**
- New dark design system: Sofia Sans, indigo accent, shell layout (top bar / sidebar / main / status bar)
- Sidebar with full project tree, collapsible directories, inline search (filters by class/function/file as you type)
- Top bar: PHPDG logo (SVG), version pill, language picker
- Dark / light mode toggle (pill switch, persisted in localStorage)
- Visibility dots + badge for every method (`public` / `protected` / `private`) with fixed-width badges for left-edge alignment
- Stats cards on the homepage (files / classes / functions count)
- Homepage symbol index (Classes + Functions sections) — collapsed by default, click to expand, shows count badge
- Relative file paths in file headers (instead of absolute OS paths)

**Real-time progress**
- Generation endpoint streams Server-Sent Events instead of returning JSON on completion
- Per-file progress for the heavy steps (parsing, directory structure creation, HTML generation)
- Progress throttled to ~100 events per step (every 1% tick)

**Source viewer**
- Click any method or function to view its source code in an AJAX modal
- "Copy" button added next to "View Source" in every expanded method/function
- Copy icon button in the source viewer modal header (3-second feedback on both)

**Bug fixes**
- Source viewer "Unexpected token '<'" — AJAX call now checks `response.ok`, reads body as text, parses JSON with try/catch
- `generatorPath` in output HTML files pointed to the wrong location — corrected for nested pages
- AJAX source endpoint used a hardcoded `output/` path — now resolves `$settings['output_dir']` to an absolute path
- Translation headings for Classes/Functions used genitive forms — fixed to nominative plural for all 10 languages

## v0.5

- Source code viewer (AJAX modal)
- Expanded from 6 to 10 UI languages
- RTL support (Persian)
- Rebranding from phpDoc to phpdg
