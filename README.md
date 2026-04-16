# Shire Audio — Hugo Site

A Hugo static site for Shire Audio, deployed on Netlify.

## Project Structure

```
shire-audio/
├── archetypes/          # Templates for hugo new commands
│   ├── projects.md
│   └── services.md
├── content/             # All site content (edit these!)
│   ├── _index.md        # Home page
│   ├── about/
│   │   └── index.md     # About page + bio + audiobook credits
│   ├── contact/
│   │   └── index.md     # Contact page text
│   ├── projects/
│   │   ├── _index.md    # Projects section landing
│   │   └── refracted-reality/
│   │       └── index.md # Project + all episodes in front matter
│   └── services/
│       ├── _index.md    # Services landing page
│       ├── project-production/index.md
│       ├── audiobook-production/index.md
│       └── audio-drama/index.md
├── layouts/             # HTML templates (structure, not content)
│   ├── _default/
│   │   ├── baseof.html  # Master layout (header/footer)
│   │   ├── single.html  # Generic single page
│   │   └── list.html    # Generic list page
│   ├── partials/
│   │   ├── header.html
│   │   └── footer.html
│   ├── index.html       # Home page template
│   ├── about/
│   ├── contact/
│   ├── projects/
│   └── services/
├── static/              # Static files served as-is
│   ├── css/styles.css
│   ├── fonts/           # Add your font files here
│   └── images/          # Logo, photos, project covers
├── hugo.toml            # Site configuration
└── netlify.toml         # Netlify build settings
```

## Local Development

### Prerequisites
- [Hugo](https://gohugo.io/installation/) v0.140+ (`brew install hugo` on Mac)

### Run locally
```bash
hugo server -D
```
Then visit http://localhost:1313

## Adding Content

### Add a new project
```bash
hugo new projects/my-new-project/index.md
```
Edit the generated file — add episodes directly in the front matter as YAML.

### Add a new service
```bash
hugo new services/my-new-service/index.md
```

### Add episodes to an existing project
Open `content/projects/<project-name>/index.md` and add to the `episodes:` list:
```yaml
episodes:
  - title: "Episode Title"
    date: "2025-01-15"
    audio_file: "/media/my-episode.mp3"
    description: |
      Episode description in markdown.
    guests:
      - "Guest Name"
```

### Update the about page
Edit `content/about/index.md`:
- `story:` — the "Our Story" paragraph
- `experience:` — list of roles (YAML)
- `audiobook_credits:` — books by year (YAML)
- The markdown body is Josh's bio paragraph(s)

## Fonts

Place your font files in `static/fonts/`. The CSS expects:
- `Vollkorn-Regular.woff2` / `.woff`
- `Vollkorn-Bold.woff2` / `.woff`
- `Vollkorn-Italic.woff2` / `.woff`
- `EagleLake-Regular.ttf`
- `YsabeauOffice-VariableFont_wght.ttf`
- `YsabeauOffice-Italic-VariableFont_wght.ttf`

## Media Files

Audio files referenced in project front matter (e.g. `/media/episode.mp3`) should be served from Netlify's Large Media or an external host (e.g. S3, Transistor, Buzzsprout). Place them in `static/media/` if hosting directly — but note Hugo will copy them into the build, which can make the repo large.

## Deployment on Netlify

1. Push this repo to GitHub/GitLab
2. In Netlify: **Add new site → Import an existing project**
3. Set build command: `hugo`
4. Set publish directory: `public`
5. Netlify will auto-detect `netlify.toml` and use Hugo 0.140

### Contact Form
The contact form uses Netlify Forms (`data-netlify="true"`). No configuration needed — Netlify detects it automatically on deploy.

## Navigation

Edit the `[menu]` section in `hugo.toml` to add, remove, or reorder navigation links.

## Colors & Branding

CSS custom properties in `static/css/styles.css`:
```css
:root {
    --green:  #426C4C;
    --cream:  #EBE6D7;
}
```
Change these two values to re-theme the entire site.
