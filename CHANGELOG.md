# Changelog

## 1.2.0 (26 November 2026)

From a real campaign page on a staging site (T34) and a four-page build on Divi 5.19.1 (T35). Tested on Divi 5.16.0 and 5.19.1, Novamira 1.12.12 and 1.12.16, WordPress 7.1.3 and 7.1.5, ACF 6.8.12.

### Skills

- `divi5-styling`: sticky settings per breakpoint and values that apply only while stuck; Group grid layouts with column counts per breakpoint; hiding a module per breakpoint (`disabledOn`); heading letter spacing; line height on large numbers; button padding on the module's own spacing.
- `divi5-modules`: Number Counter titles (always headings) and width; Group Carousel for carousels of cards (the module labelled Post Carousel is the old Portfolio); breadcrumbs; hiding the testimonial quote mark; contact form receiver, message pattern, labels, styling paths and the keyboard-access gap; a new section on semantic tags (`nav`, `ul`, `li`, `section`), accessibility attributes and builder layer names.
- `divi5-dynamic`: checking a loop without publishing; how two taxonomy filters combine (OR, or AND once an exclude is added); the empty-loop message; File fields in links.
- From T34: date display conditions and date windows, page caches and date switches, a page without the title bar, column order on phones, icon list alignment, countdown limits, contrast and all-width checks, no facts from general knowledge, safe link building, number counter percent sign, icon list check marks, image aspect ratio with cover fit.
- Fixed: the contact form recipient is `email.advanced.receiver`; `email.innerContent` is the message pattern.
- `divi5-styling` no longer refers to one site's mu-plugin; `divi5-presets` drops a note about the upstream skill; `manifest.json` descriptions cover the new content.

### Setup and docs

- README and `novamira-setup` list the tested versions and mention the Novamira CLI connection. The setup skill is still written for the MCP connection.
- docs/00 status, docs/03 (how the CLI was used), docs/09 (T34 and T35), docs/10 (update note).
- Finished or superseded documents moved to `docs/archive/`: the first session log, the audit of `divilovewp/divi5-skill`, the original authoring notes, the original plan and the design brief. docs/08 is marked as no longer maintained (site writes are logged in the git-ignored `site-logs/`). The superseded User Context texts are removed from `docs/user-context-proposed.md`.
- Public docs no longer name the organisations or campaigns the skills were used for.
- The repository is renamed `novamira-divi` (from `novamira-divi5`), so the name suits later Divi versions. GitHub redirects the old addresses. The skills keep their `divi5-` names because they are written for Divi 5.

## 1.1.1 (22 October 2026)

From the first setup on a staging site and the tests run there (T31 to T33). Tested on Divi 5.16.0, Novamira 1.12.12, WordPress 7.1.3, MySQL and LiteSpeed Cache 7.9.2.

- The repository is renamed `novamira-divi5`. The README and NOTICE say it is an independent project, not made or endorsed by Novamira or Elegant Themes.
- Public docs name the staging site only as "a charity's staging site on Krystal".

- User Context opens with "This is a Divi 5 development or staging copy of the site", so it fits staging sites.
- Fresh-agent regression run on the staging site passed (T32). `divi5-styling`: `orientation` aligns Heading as well as Text. `divi5-core`: component instances keep no version stamp; use `PHP_EOL` for line breaks.
- Caches checked on MySQL hosting (T33): saving a published page refreshes Divi's CSS and module list and purges it from LiteSpeed Cache, without a manual purge; after a Theme Builder layout or component edit, agents purge all on staging. `divi5-core` notes that staging sites usually hide pages from logged-out visitors.
- `novamira-setup`: installs on a remote site by fetching the release's skill files from GitHub and checking each md5; calls `agent-context` as a tool; tested on Novamira up to 1.12.12.

## 1.1.0 (22 October 2026)

From the fresh-site install test (T30, T30b). Tested on Divi 5.16.0, Novamira 1.12.11 and WordPress 7.1.3. The new setup offers (activating Divi, footer widgets, the permission rule) and `site-logs/` have not yet run on a site.

### Setup

- `CLAUDE.md` works on any site without editing. Personal rules go in a git-ignored `CLAUDE.local.md`.
- Changes to a user's site are logged in a git-ignored `site-logs/` folder, so `git pull` never conflicts.
- `novamira-setup` offers to activate Divi when it is installed but inactive, reports the Novamira version, and offers to move WordPress's default footer widgets and to allow Novamira calls without a prompt (risk stated first).
- `.gitattributes` keeps every file LF, so hashes match on Windows clones.

### Skills

- `divi5-styling`: Image border and radius on `image.decoration.border`; background image with a gradient overlay.
- `divi5-theme-builder`: works on a site where the Theme Builder was never used; layouts created with `et_theme_builder_insert_layout()`.
- `divi5-dynamic`: styling the post content module's text; ACF Link fields do not resolve; even card images with `et-pb-post-main-image`; check featured-image alt text before a loop.
- `divi5-modules`: accordion and toggle title heading levels.
- `divi5-core`: removing a child block safely; computed-style checks in the browser; ask the user to sign in to the browser, never create an admin link; a harmless WP Studio cache warning.

## 1.0.0 (21 October 2026)

First public release. Tested on Divi 5.16.0 (and 5.15.1), Novamira 1.12.11 (free, from 1.12.9), WordPress 7.1.3 and ACF 6.8.10, on a local WP Studio site. Evidence for every rule is in [docs/09](docs/09-test-results.md) (tests T0 to T29).

### Skills

- `divi5-core`: how Divi 5 stores a page, the `serialize_blocks()` build recipe, rows and columns, choosing modules, editing and copying pages, components, silent failures, and how to check the result.
- `divi5-styling`: backgrounds, gradients, video backgrounds, spacing, borders, shadows, sizing, fonts, hover, sticky, position, breakpoints, global colours and every variable type. Text alignment uses `orientation` from Divi 5.16.
- `divi5-modules`: attribute shapes for every registered module, contact forms, fullwidth sections, and the Menu module's collapsible mobile menu (Divi 5.16).
- `divi5-theme-builder`: Theme Builder storage, editing header, body and footer layouts, single and archive templates for a post type.
- `divi5-dynamic`: dynamic content, ACF fields, Loop Builder, pagination, filters by custom field and term, dates, custom post types, and moving date windows through the Date Conditions for Divi plugin.
- `divi5-presets`: reading and applying presets; proposing new ones and writing them after the user agrees.
- `divi5-design-system`: new-site and redesign workflow built around a design showcase draft the user approves first.
- `divi5-page-production`: draft pages from supplied content, with gaps and sources reported and no invented facts.

### Setup

- `novamira-setup` Claude Code skill: checks versions, uploads the skills from `skills/manifest.json`, writes the User Context after the user agrees, adds the WP Studio (SQLite) variables lock fix, verifies each copy and builds a smoke-test draft.
- User Context ([docs/user-context-proposed.md](docs/user-context-proposed.md)): drafts only, no deletion, presets and variables only after agreement, native modules only, and routing away from Novamira's built-in `novamira-design` skill.

### Documentation

- README for a public audience, including the Claude Code settings a clone does not bring (connection, permissions, auto mode, CLAUDE.md).
- MIT licence for this project's own content; NOTICE.md with the upstream divi5-skill licence.

### Known limits

- Not yet run on a fresh second site or on a real staging site.
- Instagram Feed, the post-content modules and Divi's Shortcode wrapper were not covered by the all-modules browser check.
