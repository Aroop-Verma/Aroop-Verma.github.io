# Personal website — Aroop Verma

A small, fast personal site built with [Astro](https://astro.build): static
output, no client-side framework, self-hosted Monocraft font. Sections: home,
about, projects, and a blog. Light/dark theme toggle in the nav.

## Prerequisites

Node is managed with [`nvm`](https://github.com/nvm-sh/nvm). **Every new terminal
needs Node activated first:**

```bash
nvm use default    # Node 24 LTS
```

If dependencies aren't installed yet: `npm install`.

## Commands

Run from the project root (after `nvm use default`):

| Command           | What it does                                             |
| :---------------- | :------------------------------------------------------ |
| `npm run dev`     | Local preview at `localhost:4321`, auto-reloads on save |
| `npm run build`   | Build the static site to `./dist/`                      |
| `npm run preview` | Preview the built `./dist/` locally                     |

## Updating the site with new content

Content is plain Markdown — no commands needed to "register" a new file, it's
picked up automatically.

**Day-to-day workflow:**

1. Start the preview once: `nvm use default && npm run dev`, then open
   <http://localhost:4321>.
2. Add or edit a file (see below). **Save** — the browser refreshes on its own.
3. When it looks right, `npm run build` to produce the deployable site in
   `./dist/`.

### Add a blog post

Drop a new `.md` file in `src/content/blog/` (copy `hello-world.md` as a
template). Frontmatter:

```markdown
---
title: "My post title"
description: "Optional one-line summary."
date: 2026-07-20
tags: ["genomics", "notes"]
draft: false            # set true to hide it from the site
---

Write in plain Markdown — headings, lists, `code`, links, images all work.
```

Posts show newest first automatically.

### Add a project

Drop a `.md` file in `src/content/projects/`:

```markdown
---
title: "Project title"
description: "One-line summary shown on the card."
tags: ["WGS", "GATK"]
url: "https://…"        # optional link
repo: "https://…"       # optional repo link
featured: true
order: 1                 # lower numbers sort first
---

Longer write-up (optional).
```

The exact fields allowed for each are defined in `src/content.config.ts`.

## Editing text and design

| To change…                                    | Edit…                             |
| :-------------------------------------------- | :-------------------------------- |
| Homepage name / tagline                       | `src/pages/index.astro`           |
| About bio, skills, contact links              | `src/pages/about.astro`           |
| Nav, footer, theme toggle, `<title>`/meta     | `src/layouts/Base.astro`          |
| Colors, font, grid, spacing (design tokens)   | `src/styles/global.css` (`:root`) |
| Font file / favicon                           | `public/fonts/`, `public/favicon.svg` |

The site is light by default with a dark theme; both palettes live in
`src/styles/global.css` (`:root` and `:root[data-theme="dark"]`).

## Project structure

```text
/
├── public/
│   ├── fonts/Monocraft.ttf
│   └── favicon.svg
├── src/
│   ├── content/
│   │   ├── blog/          # blog posts (.md)
│   │   └── projects/      # projects (.md)
│   ├── content.config.ts  # content schemas
│   ├── layouts/Base.astro # shared shell: nav, footer, theme toggle
│   ├── pages/             # routes (index, about, projects, blog)
│   └── styles/global.css  # design tokens + base styles
├── drafts/                # stashed content not currently published
└── package.json
```

## Publishing (not set up yet)

`npm run build` produces the static site in `./dist/`, but there's no public URL
yet. To go live, deploy `./dist/` to a static host (GitHub Pages, Netlify, or
Cloudflare Pages). Once a repo-connected host is set up, updating the live site
becomes a single `git push`.
