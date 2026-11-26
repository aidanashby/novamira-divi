Tested on Divi 5.15.1 (14 October 2026) and rechecked on 5.16.0 (21 October 2026); items marked 5.19.1 were added on Divi 5.19.1 (25 and 26 November 2026, T35). Each shape below was written with `serialize_blocks()` and rendered, and those marked "builder" were also opened in the Visual Builder. Load `divi5-core` first. All values sit under `<bp>.value` as `{"desktop":{"value":...}}`; shown here as the desktop value only.

## Parent and child modules

A parent holds only its children; give the parent just `builderVersion` unless styling it.

| Parent | Child | Child attributes |
|---|---|---|
| `divi/accordion` | `divi/accordion-item` | `title.innerContent` text, `content.innerContent` HTML, `module.advanced.open` `"on"` for the open item (builder); title heading level `title.decoration.font.font.<bp>.value.headingLevel` (default `h5`) |
| `divi/tabs` | `divi/tab` | `title.innerContent` text, `content.innerContent` HTML. The first tab is active. |
| `divi/slider` | `divi/slide` | `title.innerContent` text, `content.innerContent` HTML, `button.innerContent` `{text, linkUrl}` |
| `divi/icon-list` | `divi/icon-list-item` | `content.innerContent` text |
| `divi/contact-form` | `divi/contact-field` | see Contact form |

## Single modules

- Blurb (builder): `title.innerContent` `{text}`, `content.innerContent` HTML, `imageIcon.innerContent` `{src}`.
- Call to action (builder): `title.innerContent` text, `content.innerContent` HTML, `button.innerContent` `{text, linkUrl}`. Default background is the theme primary colour.
- Image (builder): `image.innerContent` `{src, id, alt, titleText, width, height}` (strings), from `wp_get_attachment_image_src($id, 'full')`.
- Toggle: `title.innerContent` text, `content.innerContent` HTML. Renders closed.
- Number counter: `number.innerContent` (digits only, no prefix or suffix, no thousands separator), `title.innerContent`; the percent sign is `number.advanced.enablePercentSign` (`"off"` to hide it; `percentSign` is the circle counter's key and is ignored here). Verified on 5.16.0. The module has no currency or unit setting: put the unit in the title ("pounds gained or saved"), or ask the user how their site shows one. 5.19.1: the title is always a heading (`title.decoration.font.font` `headingLevel` `h1` to `h6`, default `h3`), so a row of counters adds one heading each: pick the level below the section heading. The module renders centred and only as wide as its content inside a flex Group; `module.decoration.sizing` `{"width":"100%"}` with `module.advanced.text.text` `orientation` `"left"` aligned it. `module.decoration.layout` `rowGap` sets the gap between number and title. Number font: `number.decoration.font.font`.
- Icon list item icon: `icon.innerContent.<bp>.value` `{"unicode":"&#x4e;","type":"divi","weight":"400"}` gives a check mark (verified on 5.16.0). Items are flex rows centred vertically, so on items that wrap to two lines the icon drops below the first line: set each item's `module.decoration.layout.<bp>.value.alignItems` to `"flex-start"` (verified at 768px).
- Accordion and toggle titles default to `h5`, which skips heading levels after an `h2`. Set each title's `headingLevel` to the next level down from the section heading (verified on 5.16.0 for accordion items and toggles: `h3` rendered `h3`).
- Testimonial: `content.innerContent` HTML, `author.innerContent` text, `jobTitle.innerContent` text, `company.innerContent` `{text, linkUrl}`, `portrait.innerContent` `{src}`. Hide the quote mark with `quoteIcon.decoration.icon` `{"show":"off"}` (5.19.1).
- Carousels (5.19.1): the module labelled Post Carousel is `divi/fullwidth-portfolio`, an image grid or slider with title and date only. For a carousel of cards, use `divi/group-carousel` with one looped `divi/group` child (`divi5-dynamic`): it gave one slide per post. Slides per view: `module.advanced.slidesToShow` per breakpoint (`"4"`, `"2"`, `"1"`); arrows `arrows.advanced.showArrows`, `position` (`inside`, `outside`, `center`), `size`, `color`; dots `dotNav.advanced.showDots`. Arrows are spans with `role="button"`, `tabindex` and labels. `inside` arrows overlap the slides unless the carousel has side padding (`module.decoration.spacing`).
- Breadcrumbs (5.19.1): `home.innerContent` `{text, url}` and `separator.innerContent` `{text}`; fonts on `home`, `breadcrumb` (current page) and `breadcrumbLink` `decoration.font`. Renders a `nav`.
- Team member: `name.innerContent`, `position.innerContent` text, `content.innerContent` HTML, `image.innerContent` `{url}`. `src` does not render here; use `url`.

## Contact form

```php
$form = $b('divi/contact-form', [
    'module' => ['advanced' => ['uniqueId' => $d(wp_generate_uuid4())]],
    'title'  => ['innerContent' => $d('Get in touch')],
    'button' => ['innerContent' => $d(['text' => 'Send'])],
], [
    $b('divi/contact-field', ['fieldItem' => ['innerContent' => $d('Name'),
        'advanced' => ['id' => $d('name'), 'type' => $d('input'), 'required' => $d('on')]]]),
    $b('divi/contact-field', ['fieldItem' => ['innerContent' => $d('Email'),
        'advanced' => ['id' => $d('email'), 'type' => $d('email')]]]),
    $b('divi/contact-field', ['fieldItem' => ['innerContent' => $d('Message'),
        'advanced' => ['id' => $d('message'), 'type' => $d('text')]]]),
]);
```

- Field types (all rendered): `input`, `email`, `text` (message box), `select` with `fieldItem.advanced.selectOptions` `[{"value":"One","id":"o1"}]`, `checkbox` with `checkboxOptions` `[{"value":"Tick","checked":"0","dragID":0}]`, `radio` with `radioOptions` (same shape). Give every field a unique `id`.
- Divi adds a maths CAPTCHA and the submit button itself.
- The recipient address is `email.advanced.receiver`; when it is empty Divi sends to the site admin address. Ask the user before setting it. `email.innerContent` is the message pattern, with fields as `%%field_id%%`, for example a body that lists every answer so the inbox can sort messages (5.19.1, from source).
- Other form settings (5.19.1): `module.advanced.showLabels` `"on"` shows labels above fields; `module.advanced.successMessage` text; a checkbox option can carry a link, `{"value":"I agree ... See our","checked":"0","dragID":0,"link":{"url":"<URL>","text":"privacy notice"}}`. Styling: fields `field.decoration` (`background`, `border`, `font`, `spacing`), labels `field.decoration.labelFont.font`, option text `checkbox.decoration.font.font` and `radio.decoration.font.font`, submit `button.decoration`.
- Divi hides radio and checkbox inputs with `display: none`, so keyboard users cannot reach them, and a required tick box cannot be ticked without a mouse (5.19.1). Fixing it needs module CSS (`css.desktop.value.freeForm` that shows the inputs at opacity 0 with a focus ring). These skills avoid custom CSS, so tell the user and add it only if they agree.

## Semantics and accessibility attributes (5.19.1, checked in a browser)

- `module.advanced.html` `{"elementType":"<tag>"}` changes a Group's tag: `nav`, `ul`, `ol`, `li` and `aside` rendered. On a section, `section` rendered. A Group made `ul` keeps the browser's list indent; set its `module.decoration.spacing` padding-left and margin to `0px`. Children made `li` show no bullets while the parent is a flex or grid layout.
- Custom attributes go in `module.decoration.attributes.desktop.value.attributes`, a list of `{"id":"<uuid>","name":"<attribute>","value":"<value>","adminLabel":"<label>"}` (`targetElement` aims at an inner element, for example `"image"`). `aria-label`, `aria-labelledby`, `role` and `aria-roledescription` all reached the wrapper.
- Label a section by its heading: give the Heading module an `id` attribute and the section `aria-labelledby` with that id, plus `elementType` `section`. Name a `nav` Group with `aria-label`. A Group Carousel can take `role` `region`, `aria-roledescription` `carousel` and an `aria-label`.
- Image alt text set in the builder can live in two places: `image.innerContent` `alt` and an `alt` entry in the attributes list. Change both.
- Builder layer names: `module.meta.adminLabel` `{"desktop":{"value":"Hero"}}`. Give every section a name that says what it is.

## More modules (rendered and seen in a browser, T12)

- Audio: `audio.innerContent` is a plain URL string (media library, `wp_get_attachment_url($id)`; WAV works), plus `title.innerContent`, `artistName.innerContent` text.
- Video: `video.innerContent` `{src}` (a YouTube URL works). Video slider: `divi/video-slider` holding `divi/video-slider-item` with the same `video` shape.
- Before and after: `beforeImage.innerContent` and `afterImage.innerContent` `{src}`, `beforeLabel`, `afterLabel` text.
- Circle counter: `title.innerContent` text, `number.innerContent` `"70"`. Number counter: same, plus `number.advanced.enablePercentSign` `"off"` to drop the default percent sign.
- Bar counters: `divi/counters` holding `divi/counter` with `title.innerContent` and `barProgress.innerContent` `"80"`.
- Countdown: `title.innerContent`, `content.advanced.dateTime` `"2027-01-01 00:00"` (site timezone). It has no setting to hide seconds or leading zeros: Divi's script always pads the days to three digits ("039"). Hiding the seconds needs CSS on the module, which these skills avoid; offer it to the user rather than adding it. Hide the countdown after its date with a date condition (`divi5-dynamic`).
- Pricing: `divi/pricing-tables` holding `divi/pricing-table` with `title`, `price`, `content` (HTML list), `button` `{text, linkUrl}`.
- Timeline: `divi/timeline` holding `divi/timeline-item` with `date`, `title`, `content`.
- Divider: `divider.advanced.line` `{show, color, weight}`. Icon: `icon.innerContent` `{unicode, type: "divi", weight}`. Link: `content.innerContent` `{text, linkUrl}`.
- Social follow: `divi/social-media-follow` holding `divi/social-media-follow-network` with `socialNetwork.innerContent` `{title: "facebook", link}`.
- Tooltip: a `divi/tooltip` child inside the module it annotates, with `content.innerContent` and `module.advanced.tooltip` `{trigger: "always"}` (or `hover`, `click`).
- Group: `divi/group` holding any modules. Group carousel: `divi/group-carousel` holding `divi/group` children.
- SVG: `svg.innerContent` `{sourceType: "code", code: "<svg>...</svg>"}`. Charts: `chart.innerContent` `{title}` (data needs the builder's table editor).
- Gallery: `gallery.innerContent` `{galleryIds: "37,38"}` (comma-separated attachment IDs).
- With defaults only (site data fills them): blog, portfolio, filterable portfolio, post slider, post navigation, post title, comments, breadcrumbs, search, sidebar, menu, table of contents.
- Menu, collapsible mobile submenus (Divi 5.16 and later): `menuMobile.advanced.collapsible` `"on"` (default `"off"`), and `menuMobile.advanced.parentLinksActive` `"off"` to make a parent item open its submenu instead of navigating (default `"on"`). Rendering adds the class `et_pb_menu--collapsible-mobile`. Verified in a browser at 375px (T26): submenus start closed, each parent gets a plus toggle, and with `parentLinksActive` `"off"` tapping the parent's name opens its submenu without leaving the page; with the default `"on"`, the plus opens the submenu and the name follows its link. Submenus open independently: opening one leaves the others as they are. Select the menu with `menu.advanced.menuId` set to the nav menu's term ID as a string.
- Fullwidth section: `divi/section` with `module.advanced.type` `"fullwidth"`; fullwidth modules sit directly in it, with no row (header, image, slider, code, menu, portfolio, post slider, post title, map).

Need outside setup, so they render empty or hidden until configured: signup (email provider), payment button (payment provider), map and fullwidth map (Google Maps API key), lottie (animation URL), post filter (a Loop Builder module), dropdown (a trigger). Login shows "Log out" to a logged-in viewer. Contact Form 7, Gravity Forms and Imagely need their plugins. Theme Builder only: post content modules. Components only: `divi/global-slot`.

Adapted in part from divilovewp/divi5-skill (MIT, copyright 2026 Shashank Gupta, divilove.com), verified and rewritten for Divi 5.15.1.
