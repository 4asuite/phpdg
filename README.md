# PHPDG v1.0.0

**PHP Documentation Generator** — generates clear HTML documentation from PHP source code with a live source file browser, multi-language interface, and real-time progress tracking.

---

## Contents

- [Features](#features)
- [Requirements](#requirements)
- [Quick Start](#quick-start)
- [HTTP Authentication](#http-authentication)
- [Languages](#languages)
- [Color Mode](#color-mode)
- [License](#license)
- [Changelog](#changelog)

---

## Features

### Parsing & Documentation

- Recursive directory scanning with exclusion support
- Parses classes, interfaces, traits, methods, functions and DocBlocks (`@param`, `@return`, `@description`)
- Extracts line numbers for every method and function — precise source code navigation
- Generates a self-contained `output/` directory (HTML, CSS, JS — no runtime dependencies)
- Detection of anonymous classes and special constructs
- Extraction of parameter types and return types

### User Interface

- Modern dark design with light mode toggle
- Real-time client-side search (classes, functions, files)
- Expandable method details with parameter and return value documentation
- Index page for every directory and a root `index.html`
- Stats cards: file count, class count, function count

### Source Code Viewer

- Click any method or function to view its source code in an AJAX modal
- Copy source code to clipboard directly from the modal
- "Copy" button on every expanded method/function (3-second feedback)
- File identifiers (md5 of absolute path) bypass common WAF path-traversal protection rules
- Server-side lookup via stored `.file_index.json`

### Method Visibility

- Colored dots and badges for every method:
  - 🟢 green — `public`
  - 🟡 yellow — `protected`
  - 🔴 red — `private`

### Generation

- **GGUI mode** (browser) — generation starts automatically on open
- Real-time progress tracking via **Server-Sent Events** (actual % per file, not an animation)
- Progress bar steps: scan → parse → tree → structure → HTML → indexes → JSON
- **CLI mode** — run directly from the command line
- Event throttling to ~100 per step (every 1%)

### Security

- Optional HTTP Basic authentication (auto-generates `.htaccess` + `.htpasswd`)
- Passwords hashed via `crypt()`
- Multi-user support
- Output `.htaccess` blocks direct access to `.php` files in `output/`
- WAF-safe file identifier system

### Architecture

- Simple distribution — a single `generator.php` file
- No runtime dependencies (PHP 7.4+, no Composer)
- Trait-based modular architecture (10+ specialized traits)

---

## Requirements

- **PHP 7.4** or newer
- Apache or nginx for HTTP auth via `.htaccess` (optional)
- A modern browser with EventSource support (Chrome, Firefox, Safari, Edge) for live progress

---

## Quick Start

### 1. Configuration

Edit the `$settings` array at the top of `generator.php`:

```php
$settings = [
    'directories' => [
        '../your-project/app',
        '../your-project/system',
    ],
    'output_dir'         => 'output',
    'exclude_dirs'       => ['cache', 'logs', 'tmp', 'node_modules', 'vendor'],
    'http_auth'          => [
        // 'admin' => 'password123',
    ],
    'language'           => 'en',
    'available_languages'=> ['en', 'sk', 'cs', 'de', 'pl', 'pt', 'ru', 'uk', 'hi', 'fa'],
];
```

### 2. Generation

**Browser (recommended — live progress bar)**

1. Upload `generator.php` to your web server
2. Open it in a browser — it redirects automatically to the GGUI interface
3. Watch the generation progress in real time
4. Click "Open Documentation" when done

**PHP built-in server (local testing)**

```bash
php -S localhost:8000
```

Then open [http://localhost:8000/generator.php](http://localhost:8000/generator.php)

**Command line**

```bash
php generator.php
```

CLI mode skips the graphical interface and writes directly to `output_dir`.

### 3. Viewing

Open `output/index.html` directly in a browser or via an HTTP server.

---

## HTTP Authentication

```php
'http_auth' => [
    'admin' => 'secure_password',
    'johny' => 'other_password',
],
```

`.htaccess` and `.htpasswd` are auto-generated in the `output/` directory. An empty array makes the documentation publicly accessible.

---

## Languages

PHPDG supports **10 languages** with live switching directly on the page:

| Code | Language | Direction |
|------|----------|-----------|
| `en` | English | LTR |
| `sk` | Slovenčina | LTR |
| `cs` | Čeština | LTR |
| `de` | Deutsch | LTR |
| `pl` | Polski | LTR |
| `pt` | Português | LTR |
| `ru` | Русский | LTR |
| `uk` | Українська | LTR |
| `hi` | हिन्दी | LTR |
| `fa` | فارسی | **RTL** |

The language selection is saved to `localStorage`. Persian has full RTL support including layout direction.

---

## Color Mode

PHPDG includes a dark/light mode toggle in the topbar (pill switch with sun and moon icons).

- **Dark mode** — default, inspired by VS Code (`#0f1117`)
- **Light mode** — warm cream palette inspired by Claude (`#f9f7f4`)
- Topbar always stays dark
- Setting is saved to `localStorage`

---

## License

MIT

---

## Changelog

See [CHANGELOG.md](CHANGELOG.md).
