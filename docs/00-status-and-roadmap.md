# 00. Status and roadmap

Planning, progress tracking and next steps for the project. The README describes the project; this file says where it stands. Test evidence is in docs/09, every site write in docs/08.

## Status (22 October 2026)

The Studio site runs Divi 5.16.0 and Novamira 1.12.11. On 21 October:

- Upgrade check (T23): one change, Text module alignment, now in `divi5-styling`.
- Novamira 1.12.11 tells agents to load its `novamira-design` skill for visual work; a User Context sentence overrides that (T24).
- Global variable references verified for every type (T25); the Visual Builder saves variables on Studio (T27); all test variables deleted.
- Menu module collapsible mobile option added to `divi5-modules` (T26, render only).
- Outstanding desktop and phone checks done and the Button preset colour doubt resolved (T28).
- Moving date windows: `divi5-dynamic` explains Date Conditions for Divi, verified on a Movies loop: `after` and `before`, undated posts and the empty state (T29).
- README rewritten for a public audience.

The original plan (docs/06, "Recommended order") is complete, and the scope was then widened to Theme Builder, dynamic content and custom post types. Both gates the user owned are decided: no Novamira Pro (gate e), and Divi globals stay the source of truth for design tokens (gate d, option 1). See docs/10.

### On the Studio site now

| Item | Where | Notes |
|---|---|---|
| User Context | option `novamira_instructions_content` | Text in docs/user-context-proposed.md (revised 21 October: excludes `novamira-design`) |
| Skill `divi5-core` | post 30 | Structure, `serialize_blocks()` recipe, meta, rows and columns, module choice, clone, components, silent failures, verification including browser checks |
| Skill `divi5-styling` | post 53 | Decoration paths, fonts, hover, sticky, position, video background, responsive, global colours and variables of every type |
| Skill `divi5-modules` | post 54 | Shapes for every registered module, contact form fields, fullwidth sections, Menu collapsible mobile option |
| Skill `divi5-theme-builder` | post 90 | Theme Builder storage, editing layouts, creating templates for a post type and its archive |
| Skill `divi5-dynamic` | post 103 | Dynamic content, ACF fields, Loop Builder, pagination, filters by custom field and term, dates, custom post types, moving date windows through Date Conditions for Divi |
| Skill `divi5-presets` | post 131 | Read and apply module and option-group presets; propose new or changed ones, write after the user agrees |
| Skill `divi5-design-system` | post 136 | New-site and redesign workflow: design showcase draft and approval gate (T20) |
| Skill `divi5-page-production` | post 153 | Build a draft page from supplied content, with gaps and sources reported (T22) |
| Theme Builder template "All Movies" | template 99, body layout 98 | Single movie pages (`singular:post_type:movie:all`), with a "More movies" loop |
| Theme Builder template "Movies archive" | template 112, body layout 111 | `/movies/` (`archive:post_type:movie`), paginated grid |
| Theme Builder template for S5 | template 87, layouts 81 and 83 | Built by the user, header and footer edited by Claude |
| Test movies | posts 92, 93 | Published, with ACF values; post 91 is the user's |

The skill sources in `skills/` match the stored skills byte for byte (md5 checked after every upload, last on 21 October 2026).

### What was tested (on Divi 5.15.1; T1, T6, T10 and T12 rerun on 5.16.0 in T23 and T12b)

| Area | Result |
|---|---|
| Storage method | `serialize_blocks()` from PHP arrays is byte-identical to the Visual Builder; parse, modify, serialise round-trips exactly (T0, T1) |
| Builder compatibility | Every PHP-written draft opened, edited and saved in the Visual Builder |
| Silent-failure rules from divi5-skill | Confirmed or corrected (T5, T6) |
| All registered modules | 62 of 63 visible in a browser; the rest need outside setup (T12) |
| Styling | Backgrounds, gradients, video backgrounds, spacing, borders, shadows, fonts, hover, sticky, position, breakpoints (T10, T12) |
| Clone a published page | Byte-identical draft copy, original untouched (T12) |
| Theme Builder | Edit layouts; create single and archive templates for a post type (T13, T14, T16) |
| Loops and ACF | Group, blurb and column loops; ACF text, WYSIWYG, image, URL, date; `excludeCurrentPost`; pagination; filters by custom field and by taxonomy term (T14 to T18) |
| Presets | Builder and PHP-made module and group presets, applied and checked in a browser; local settings override presets (T19, T28) |
| Variables | Number, font (custom and built-in), text, image, link and gradient references render and resolve in the browser; the builder saves variables on Studio (T21, T25, T27) |
| Upgrades | Divi 5.16.0 and Novamira 1.12.11 checked against their changelogs (T23, T24) |
| Fresh agents | Eight fresh agents with only the skills completed every task after one fix round (six on Opus, two on Haiku) |

## History

1. Chat session (Claude Desktop): Novamira installed and connected, research written up (docs/01 to docs/07).
2. Claude Code session: tests T0 to T7, User Context, `divi5-core`, sample tasks in two rounds, `divi5-styling` and `divi5-modules`, decision memo and gates.
3. Same session, widened scope: all-modules page, cloning, browser checks, Theme Builder, loops, ACF, Movies single and archive templates, `divi5-theme-builder` and `divi5-dynamic`.
4. 15 October: presets, design system and page production skills, global variables (T19 to T22), setup skill.
5. 21 October: upgrade check for Divi 5.16.0 and Novamira 1.12.11, design skill routing, variable types, Menu option, outstanding visual checks, date windows guidance, public README (T23 to T29); then footer widgets moved to inactive, Date Conditions and Menu browser checks, all-modules browser check on 5.16.0 (T29b, T26b, T26c, T12b), MIT licence and release 1.0.0.

## Open items

- 8881 needs every skill changed after 22 October 15:00 resynced (`divi5-core`, `divi5-dynamic`, `divi5-modules`, `divi5-styling`, `divi5-theme-builder`, `divi5-page-production`, `divi5-design-system`); it was not running.
- Local folder still named `novamira-d5`; the repo is now `novamira-divi`.
- A charity's staging site on Krystal is set up (T31) and passed a fresh-agent regression run (T32); Divi's caches and LiteSpeed's page cache both refresh on save there (T33, T33b); a layout edit's reach into the LiteSpeed cache is untested; writes there are logged in the git-ignored `site-logs/`, not docs/08. Its PHP 8.3.35 needs checking with Krystal (CVE-2026-109618/109619).
- Rerun `novamira-setup` on a fresh site to exercise its new steps: inactive Divi, the footer-widget and permission offers, and `site-logs/`.

## Roadmap

| Next step | Why | Needs |
|---|---|---|
| Real sites | Use the skills on Foodbank and Bristol Charities staging builds | Staging sites with Novamira, never live |
| Upgrade checks | Divi ships weekly | After each Divi or Novamira update, read the changelogs and rerun only the tests the changes touch (T23 is the pattern) |
| Divi MCP alongside Novamira | Elegant Themes is releasing an official Divi MCP that would replace most of the Divi write route | Its release; the plan is the next section |

## Divi MCP alongside Novamira (planned, 4 November 2026)

Nothing here has been run. It plans for a product that is not yet released, so every claim about it is [Web] (a sneak-peek video by Elegant Themes' founder, 4 November 2026, listed in docs/07) or [Inferred]. No skill rule changes until a test on a site produces evidence (CLAUDE.md).

### What the video says [Web]

- Elegant Themes will release a Divi MCP. It exposes Divi's existing agent tools through WordPress's Abilities API, and a client connects with an application password. The setup generates a connect prompt, as Novamira does.
- The demo agent listed 69 tools, and the speaker said "over 150". Both numbers cannot describe one build, so the final tool list is unknown.
- It builds pages from native modules, edits attributes, creates variables and presets, edits Theme Builder templates and assigns them, and publishes. The speaker says output is validated.
- Tools are scoped by severity, and some need approval, with deleting a preset, variable or component given as the example.
- A skill for building a variable system ships with it. Image generation and stock image tools were not in the demo build.
- It is free for all Divi users and needs no Divi AI.
- Not stated: release date, minimum Divi, WordPress and PHP versions, the endpoint path, whether it covers Loop Builder, ACF dynamic content or custom post types, and how approvals are collected.

### What stays with Novamira

The Divi MCP covers Divi. Novamira's free tier covers everything else, and nothing in the video overlaps it: custom post types, ACF field groups and values, options, plugin and theme files, the database, users, menus, media imports, caches, `execute-php` for anything without a dedicated tool, and reading the site for diagnosis. The WP Studio lock fix (`tools/studio-divi-variables-lock.php`) is a Divi filter that is independent of both, and the MCP's variable tools very probably hit the same lock on SQLite [Inferred].

### Three ways the two could connect

Which one applies is a fact to find, not a choice to make. Phase 1 settles it.

| | Topology | How Claude sees it | Consequences |
|---|---|---|---|
| A | Two servers: `/wp-json/mcp/novamira` and a separate Divi endpoint | Two MCP servers in `/mcp`, two application passwords | Simplest to reason about. Claude routes by tool name. Two credentials to manage and revoke per site. |
| B | Divi's abilities appear in Novamira's Abilities Hub and run through Novamira's `execute-ability` gateway | One server, Divi tools reached by discover and execute | One credential. Novamira's per-ability toggles can switch Divi tools off. Possible only if Divi registers its abilities as public to the adapter. docs/03 records that the Hub auto-discovers abilities registered through the Abilities API, which makes this plausible [Docs, Inferred]. |
| C | Divi MCP only, Novamira dropped | Divi tools only | Loses PHP, files and everything outside Divi. Not planned, because those are needed for CPTs, ACF and options. |

If A, the Divi MCP is a second thing to install and trust on every site. If B, it may arrive with a Divi update and need no setup beyond enabling it.

### Routing rule to write (after Phase 1)

- Writing Divi objects (pages, sections and modules, Theme Builder templates and assignments, global colours, variables, presets, library items) uses a Divi MCP tool when one exists.
- Novamira PHP may read Divi data to inspect it, and writes Divi data only where no Divi tool exists, saying so first.
- Everything outside Divi uses Novamira.
- When a task needs both (a CPT with ACF fields, a Theme Builder template for it, a loop page), Novamira creates the data model and the Divi MCP builds on it. Claude reads the result back after each handoff.

### Risks, and what each needs

1. **PHP bypasses the Divi MCP's gates.** Novamira runs as the administrator with unrestricted PHP. It can delete a preset or variable, or call a Divi ability directly with `wp_get_ability()`, without any approval prompt the MCP would show [Inferred]. Approvals protect only the calls made through the MCP, so the real guard stays the written rule: never delete a Divi object without the user's explicit approval, whichever route. Test whether an approval is a server-side check or only a client prompt.
2. **Two sets of guidance competing.** Skills trigger on their descriptions, and several can fire together (docs/03). `divi5-core`, `-styling`, `-modules`, `-theme-builder` and `-presets` all say to write through PHP, and the Divi MCP ships its own skill. An agent given both may follow the older PHP route. These five skills are cut to policy and edge-case notes, or removed, once the MCP covers their area.
3. **Two write routes to one object.** A page saved by the MCP and then edited through `serialize_blocks()`, or a layout edited by both, could leave Divi's CSS and module caches stale (T33). Use one route per object type and purge after a layout or component edit, as now.
4. **Behaviour the repo has tested and the MCP may not match.** Draft by default, publish only on request, no overwrite of existing pages, and the design showcase gate. In the demo the agent published a page it was asked to publish. It built a whole site in one go, which `divi5-design-system` forbids until approval. These stay as policy rules in `CLAUDE.md` and the User Context.
5. **Unreleased software on a real site.** The same rule as for Novamira: a Studio site first, then a staging copy, never live.
6. **The Novamira Pro question reopens in part.** Gate (e) said no Pro because the free route works. The Divi MCP is free and vendor-maintained, so it removes the main reason Pro's Divi expertise might be wanted, and no purchase decision is needed.
7. **Two charities, two sites.** One connection per site, never both sites in one session, as the existing "ask which site" rule says. Applies to the Divi endpoint as much as Novamira's.

### Plan

| Phase | Work | Exit condition |
|---|---|---|
| 0. Watch | Read the release notes when the MCP ships. Record the minimum Divi, WordPress and PHP versions, the endpoint and the tool list in docs/03 or a new reference file. | Release is public. |
| 1. Probe (Studio site) | Install it. Run discover through Novamira's adapter and look for Divi abilities. Check the Abilities Hub. Connect through the generated prompt. Decide topology A, B or C. Count the tools and read their names, descriptions and approval flags. Check the variable save on SQLite with and without the lock fix. | Topology and tool list recorded as [Run]. |
| 2. Compare | Rerun a subset of docs/09 through the MCP and compare with the PHP route: T1 round trip (an MCP-built page opens and saves in the builder), T10 styling, T13 to T16 Theme Builder, T14 to T18 loops with ACF, T19 presets, T21 and T25 variables, T12 clone. Add a new test for each gap or failure. Also test the handoff: Novamira creates a CPT and ACF fields, the MCP builds the template and loop. Also test whether approvals can be bypassed from `execute-php`. | A pass, fail or not-covered mark per area, in docs/09 with the Divi and Novamira versions. |
| 3. Rules | Write the routing rule in the User Context and `CLAUDE.md`. Cut or remove the five superseded skills in the order the Compare phase supports. Keep `divi5-design-system`, `divi5-page-production`, a `site-design` skill and the safety rules. Remove the `novamira-design` sentence if the MCP's own skill makes it unnecessary. | A fresh agent, given only the new rules, completes a CPT plus loop plus template task using both servers. |
| 4. Setup | Change `novamira-setup`: check the Divi MCP is present and enabled, record its topology, upload only the surviving skills, update the manifest, version rules and smoke test. Keep the SQLite lock fix step. | A fresh-site install passes. |
| 5. Release | README, CHANGELOG, docs/10 addendum (what changed since gate e), and a note on the Divi version range tested. | Tagged release. |

### Decisions the user will need to make

- After Phase 1: whether to adopt the MCP at all, once its tool list is known. Skipping it keeps the repo as it is.
- After Phase 2: for each area where both routes work, which one is the default. The proposal is the MCP, because it is validated and vendor-maintained, with the PHP skills kept only where the MCP fails.
- Whether to keep the approval gates as written rules only, or to restrict Novamira's `execute-php` on a site that matters (Abilities Hub toggles, Read Mode needs Pro).

## Setup skill: version rules (decided 15 October 2026)

The `novamira-setup` Claude Code skill installs the Novamira skills and User Context on a new WordPress + Novamira site. Each check changes what it does:

- Divi missing or below 5: stop; the skills are Divi 5 only.
- Divi 5 below 5.7.0: warn, then run the T1 round-trip test before page work. 5.7.0 is the earliest version with every feature the skills use (gradient variables were added in 5.7.0; loop pagination targeting appears by 5.3.0; Loop Builder, ACF dynamic content, group presets, variables, flex rows, Theme Builder, sticky, position and video backgrounds were all in the 5.0.0 public betas). Source: Divi changelog, read 15 October 2026. Most lines there are fixes, so these are latest-possible dates. Components were excluded. No warning from 5.7.0 up.
- Novamira lacking `execute-php`, `skill-write`, `skill-edit` or User Context: stop and name what is missing.
- SQLite database (WP Studio): add the variables lock mu-plugin.
- Divi installed but not active (T30): offer to activate it. Novamira outside 1.12.9 to 1.12.11: continue with a note.
- WordPress version: not checked; nothing depends on it.

## Learnings worth keeping

- Novamira's skill storage strips every backslash from skill text, even doubled ones. Skills avoid backslashes and build class names with `implode(chr(92), [...])`.
- The Write tool turned `&` into `&` in a local file, so the local and stored skills differed by two bytes. Hash-check after every upload.
- Save to Library is under a section's three-dot hover menu in 5.15.1, not the right-click menu the local docs describe. The local docs also describe the breakpoint direction wrongly.
- Divi skips a save in the builder when nothing changed.
- Binning a page renames its slug (`__trashed-N`), and restoring it does not rename it back.
- Logged-in previews skip Divi's dynamic-assets cache, so cache bugs only show on published pages.
- The browser pane only shows drafts once the user signs in. `.et-l--body` wraps ordinary pages too, so check for content, not that class.

## Resuming in a new session

1. Read `CLAUDE.md` (and `CLAUDE.local.md` if present), this file and the README.
2. Check the connection: `novamira/execute-php` returning `ET_BUILDER_VERSION`. If the Novamira tools are missing from a Claude Code session, switch the "Novamira, Divi 5" extension off and on in the session's + menu, Connectors, after Studio is running; the tools arrive on the next turn.
3. Compare the stored skills with `skills/` by md5 before editing either.
4. Pick from the Roadmap. Follow the standing approvals and gates in CLAUDE.local.md (maintainer only), and log every test-site write in docs/08.
