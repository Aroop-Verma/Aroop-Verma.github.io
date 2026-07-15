# CLAUDE.md

Guidance for working in this repo.

## What this is

Personal website for **Aroop Verma** (molecular biologist & bioinformatician).
Astro static site — no client framework — deployed to **GitHub Pages** at
<https://aroop-verma.github.io/>.

Sections: home (minimal hero), about (bio + skills + contact), projects, blog.

## Toolchain

- Node is managed with **nvm**. Run `nvm use default` (Node 24 LTS) in every new
  shell before any `npm`/`astro` command.
- Astro dev server runs in background mode (`astro dev --background`); manage with
  `astro dev stop` / `status` / `logs`.

Commands (from repo root, after `nvm use default`):

| Command           | Action                                        |
| :---------------- | :-------------------------------------------- |
| `npm run dev`     | Local preview at `localhost:4321`, hot-reload |
| `npm run build`   | Build static site to `./dist/`                |
| `npm run preview` | Preview the built `./dist/` locally           |

## Structure

```text
src/
├── content/
│   ├── blog/          # blog posts (.md); has hello-world placeholder
│   └── projects/      # projects (.md); currently empty
├── content.config.ts  # collection schemas (blog, projects)
├── layouts/Base.astro # shared shell: nav, footer, theme toggle, meta
├── pages/             # index, about, projects, blog/index, blog/[slug]
└── styles/global.css  # design tokens + base styles
public/
├── fonts/Monocraft.ttf
└── favicon.svg        # hand-drawn vector notepad (NOT emoji — see note)
```

## Design system

- **Theme**: light by default (white bg, black text); a `dark mode` text toggle in
  the nav flips to an inverted dark palette. Both palettes live in
  `src/styles/global.css` — `:root` (light) and `:root[data-theme="dark"]` (dark).
  Accent/heading colours are the SAME in both themes; only surfaces/text invert.
  Theme choice persists in `localStorage`; an inline `<head>` script sets it before
  paint to avoid flash.
- **Font**: self-hosted **Monocraft** (pixel monospace) everywhere. Keep body
  line-height generous (~1.75) for readability.
- **Accents**: magenta `--magenta: #d6006e` (headings), cyan `--cyan: #0e7d94`
  (links, subheads). Darkened for contrast on white — don't use raw neon.
- **Cards & tags**: squared corners (`border-radius: 0`), fill = page background,
  thin border. Reusable `.card` / `.tag` classes in `global.css`.
- **Background**: faint grid via `--grid` (flips with theme).
- Reuse the CSS custom properties in `global.css`; don't hardcode colours.
- Respect `prefers-reduced-motion` (handled globally).

## Content workflow

Markdown is picked up automatically — no command needed to register a file.

- **Blog post**: add `src/content/blog/<slug>.md` with frontmatter
  `title`, `date`, optional `description`, `tags`, `draft`. Newest first.
- **Project**: add `src/content/projects/<slug>.md` with `title`, `description`,
  `tags`, optional `url`/`repo`, `featured`, `order`.
- Allowed fields are defined in `src/content.config.ts`.

## Deploying

Pushing to `main` triggers `.github/workflows/deploy.yml`
(build via `withastro/action` → deploy to Pages). **Publish = `git push`**;
site rebuilds in ~30s. Astro `site` is set in `astro.config.mjs`.

## Notes / gotchas

- **Favicon must be vector shapes, not an emoji.** Emoji-in-SVG favicons render
  blank on Linux/Firefox (no color-emoji font in the favicon path).
- Do not commit PII (passport, DOB, phone, etc.) — the public email was
  intentionally removed from the site; contact is via LinkedIn/GitHub only.
- Browsers cache favicons aggressively; a hard refresh is needed to see changes.
