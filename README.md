# CV4Ecology workshop website

A GitHub Pages-compatible Jekyll site using the HTML5 UP Editorial theme. Existing
`.html` URLs are preserved; Jekyll builds shared page chrome around each page's
content. There are no custom plugins or JavaScript build steps.

## Local preview

Install Ruby and Bundler, then run these commands from the repository root:

```sh
bundle config set --local path vendor/bundle
bundle install
bundle exec jekyll serve --host 127.0.0.1
```

Open `http://127.0.0.1:4000/`. Do not open source HTML directly or serve the
repository with a plain static server: front matter and Liquid includes must be
processed first. The pinned Jekyll 3.10 release matches the GitHub Pages Jekyll
version. On systems with versioned executable names, use `bundle3.2` instead of
`bundle`.

To check a fork published as a project site:

```sh
bundle exec jekyll serve --host 127.0.0.1 --baseurl /cv4ecology.github.io
```

Open `http://127.0.0.1:4000/cv4ecology.github.io/`. Check the homepage, an older
workshop, the archives, and the FAQ; internal links and assets should remain
under that prefix.

For a production-mode build without starting a server:

```sh
JEKYLL_ENV=production bundle exec jekyll build
```

Output is written to the ignored `_site/` directory. No automated test or lint
suite is currently configured. Before publishing, check for missing local links
and images, browser-console errors, mobile overflow, keyboard navigation, zoom,
and reduced-motion behavior.

## GitHub Pages and fork configuration

Use **Settings → Pages → Deploy from a branch**, selecting this repository's
publishing branch and its root directory. GitHub Pages must run Jekyll; uploading
the raw source as a static artifact will not render the includes. If using a
custom deployment workflow, publish the Jekyll build output instead.

Set these values in `_config.yml` for the actual deployment:

- `url`: the site's origin, such as `https://YOUR-USERNAME.github.io`, without a
  trailing slash or repository path. Canonical and social-image URLs are emitted
  only when an origin is configured.
- `baseurl`: an empty string for a user site/custom-domain root, or
  `/cv4ecology.github.io` for a project site. Do not include a trailing slash.
- `google_analytics`: empty by default, so previews and forks do not send visits
  to the upstream site's analytics property. Enable your own measurement ID only
  after reviewing applicable privacy/consent requirements; it loads only in
  production mode.

The existing `CNAME` names the upstream custom domain. **Remove it for a fork
using the default GitHub Pages URL, or replace it with a domain you control** and
configure that domain in Pages settings. Local builds cannot validate DNS or
HTTPS. Google Fonts still makes external requests; fonts use `display=swap` so
text remains available while they load or if they fail.

## Maintaining pages

- `_layouts/default.html` owns the document structure, skip link, landmarks, and
  deferred scripts. Use `sidebar: false` for standalone pages.
- `_includes/head.html`, `header.html`, and `sidebar.html` own metadata, branding,
  navigation, contact information, and attribution.
- `_data/workshop.yml` contains the current workshop year and shared contact
  links. `_data/navigation.yml` defines the menu; year-specific destinations use
  that current year.
- `_data/archives.yml` lists only existing workshop pages. Both the archive index
  and `_includes/year-navigation.html` read it, so missing speaker years are not
  presented as broken links.
- Each content page has front matter with `layout`, `title`, and `description`.
  Year-specific pages also set `archive_category` and include
  `year-navigation.html`. Keep titles/descriptions specific to the page and year.
- Use Jekyll's `relative_url` filter for every internal link and asset URL, not
  the upstream domain or a hard-coded root path. This preserves project-site
  prefixes. Use `absolute_url` only for metadata that requires an origin.
- Shared enhancements live in `assets/css/accessibility.css`; the upstream
  compiled theme and its Sass sources remain separate. Font loading is handled
  in the shared head, not a blocking font import in the theme.

For a new edition, add its content pages and archive entries before changing
the current year. Workshop dates, fees, and other editorial facts within page
content still need an explicit review; they are not automatically updated.

## Images and accessibility

Keep photographs web-sized rather than uploading camera originals. Profile
photographs are limited to 640 pixels per side, with orientation applied and
embedded metadata stripped. Preserve higher resolution for scientific figures
when necessary. Supply intrinsic `width` and `height` in the correct aspect
ratio; CSS handles displayed size.

Use `loading="lazy"` and `decoding="async"` for below-the-fold images. Keep the
first banner eager; the homepage hero has responsive variants and high fetch
priority. Regenerate its 480- and 960-pixel JPEG variants if replacing it.

Give informative images meaningful alternative text. Portraits use the person's
displayed name; decorative banners retain empty alternative text. Menu controls
are native buttons, the mobile menu supports Escape and restores focus, and
collapsed navigation is removed from keyboard and assistive-technology access.
Check both expanded and collapsed states when changing shared navigation.
