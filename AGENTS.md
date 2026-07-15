## This site

Personal website for Aroop Verma: home, about/skills, projects, papers, blog.
Static Astro output, no client JS. Design: restrained synthwave (dark indigo
base, neon accents used sparingly, glow on hover only) with the self-hosted
**Monocraft** pixel font used everywhere.

- **Design tokens** (palette, font, glow, spacing) live in `src/styles/global.css`
  as CSS custom properties. Reuse them — do not hardcode colors.
- **Layout**: every page wraps content in `src/layouts/Base.astro` (nav, footer,
  meta). Pass `title` / `description` props.
- **Content** is Markdown in `src/content/{blog,projects,papers}/`, typed by
  `src/content.config.ts`. Add a post/project/paper by dropping a new `.md` file
  with the required frontmatter — it appears automatically.
- **Font**: `public/fonts/Monocraft.ttf`, preloaded in Base. Keep body
  line-height generous (~1.75+) so the pixel font stays readable.
- Respect `prefers-reduced-motion` (already handled globally).

Node is managed via `nvm`; run `nvm use default` (Node 24 LTS) before npm commands.

## Development

When starting the dev server, use background mode:

```
astro dev --background
```

Manage the background server with `astro dev stop`, `astro dev status`, and `astro dev logs`.

## Documentation

Full documentation: https://docs.astro.build

Consult these guides before working on related tasks:

- [Adding pages, dynamic routes, or middleware](https://docs.astro.build/en/guides/routing/)
- [Working with Astro components](https://docs.astro.build/en/basics/astro-components/)
- [Using React, Vue, Svelte, or other framework components](https://docs.astro.build/en/guides/framework-components/)
- [Adding or managing content](https://docs.astro.build/en/guides/content-collections/)
- [Adding styles or using Tailwind](https://docs.astro.build/en/guides/styling/)
- [Supporting multiple languages](https://docs.astro.build/en/guides/internationalization/)
