# Repository Guidelines

## Project Structure & Module Organization
The site is intentionally flat: `index.html` renders the full page, `style.css` stores all presentation rules, and `avatar.jpg` is the only binary asset. Keep new sections in `index.html` grouped by `<section>` tags with descriptive `id`s (e.g., `id="skills"`), and collect shared rules near the top of `style.css` under comment banners. If you introduce large assets or scripts, mirror the root layout by creating `assets/` or `scripts/` directories and reference them with relative paths.

## Build, Test, and Development Commands
Use simple local tooling rather than a formal build. Typical workflow:
- `python -m http.server 4173` - quick preview server; visit `http://localhost:4173`.
- `npx prettier --check index.html style.css` - confirm formatting before committing.
- `npx lightningcss style.css --minify -o style.min.css` when you need an optimized drop-in for production (commit both files).

## Coding Style & Naming Conventions
Stick to two-space indentation in both HTML and CSS, keep attribute order logical (`id`, `class`, `data-*`, `aria-*`), and favor BEM-like class names (`profile__avatar`, `skills__item`). Define colors and spacing tokens once inside the existing `:root` custom properties block, and reuse those variables instead of hard-coded values. Keep selectors shallow (max three levels) to avoid specificity fights.

## Testing Guidelines
There is no automated suite yet, so regression confidence comes from manual passes. After each change, load the page in Chromium and Firefox, resize down to 320px width, and run Lighthouse to ensure performance stays above 90. For structural sanity, run `npx html-validate index.html`; for CSS mistakes, `npx stylelint style.css --config .stylelintrc.json` (add the config if you extend the system). When you add JS, place corresponding tests under a new `tests/` directory and name files `<feature>.spec.js`.

## Commit & Pull Request Guidelines
Prefer short, imperative commit subjects (`feat: add portfolio grid`, `fix: correct avatar alt text`) followed by a single blank line and a concise body when needed. Each pull request should explain the motivation, list observable changes, and link tracking issues. Include before/after screenshots for visual tweaks and paste Lighthouse scores for layout refactors. Draft PRs are encouraged until screenshots, formatting checks, and manual browser tests are complete.

## Assets & Accessibility
Compress any new imagery with `cwebp` or `avifenc` before committing and keep raster assets under 500 KB. Always supply descriptive `alt` text and ensure interactive elements remain keyboard-focusable. If you add embeds or external scripts, document required API keys in a new `CONFIG.md` without committing secrets.
