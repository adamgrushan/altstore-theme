# Newsroom

An editorial theme for [Micro.blog](https://micro.blog). Full-bleed hero images, a narrow reading measure, kicker lines above headlines, and a restrained type scale — built for long-form posts that should read like press copy rather than a timeline.

Titleless microposts still render as plain entries, so a mixed blog doesn't break.

## Install

1. Push this repo to GitHub as a public repository.
2. In Micro.blog: **Design → Edit Custom Themes → New Theme**.
3. Give it a name and paste the GitHub URL into the external repo field.
4. Save, then assign the theme to your blog under **Design**.

Micro.blog pulls from the repo on save. Push a change, then re-save the theme in Micro.blog to pick it up.

## Post parameters

All optional. Set them in a post's front matter.

| Parameter | Effect |
| --- | --- |
| `featured_image` | URL used as the full-bleed hero. Falls back to the post's first uploaded photo. |
| `featured_image_caption` | Caption under the hero. |
| `kicker` | Small uppercase line above the headline. Falls back to the post's first category. |
| `standfirst` | Large intro paragraph between headline and byline. Markdown allowed. |

Example:

```yaml
---
title: "Quarterly results and what comes next"
kicker: "Company update"
standfirst: "A longer look at the numbers, and the three things we're changing."
featured_image: "https://yourblog.com/uploads/2026/hero.jpg"
---
```

**Note:** if you don't set `featured_image`, the theme promotes the post's first photo to the hero. That photo will then appear twice if it's also in the body. Either set `featured_image` explicitly or keep the first photo out of the body text.

## Customizing

Everything visual is a CSS custom property at the top of `static/css/main.css`:

```css
--accent:   #0f7e82;   /* links, kickers */
--ink:      #1d1d1f;   /* headings, body */
--measure:  545px;     /* reading column width */
```

Dark mode is handled by a `prefers-color-scheme` block right below those, with its own values. If you change the palette, change both.

## Structure

```
config.json                       Hugo config (pagination)
plugin.json                       Theme metadata for Micro.blog
layouts/
  index.html                      Home — lead story + list
  _default/baseof.html            Page shell
  _default/single.html            Static pages
  _default/list.html              Categories and archives
  post/single.html                Articles — hero, kicker, byline
  partials/
    head.html                     Meta, fonts, microblog_head
    header.html                   Wordmark and nav
    footer.html
    story-card.html               One item in a listing
    dateformat/long.html
    dateformat/short.html
static/css/main.css
```

`microhook-*` partials are respected throughout, so Micro.blog plugins that override the byline, navigation, or post list will work.

## Fonts

Inter, loaded from Google Fonts ([SIL Open Font License](https://openfontlicense.org)). To self-host instead, drop the woff2 files in `static/fonts/`, replace the `<link>` in `layouts/partials/head.html` with an `@font-face` block, and keep `var(--font-sans)` pointing at it.

## License

Add one before you publish. MIT is the convention for Micro.blog themes.
