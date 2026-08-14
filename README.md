# EarthCODE Hackathon 2026

Source for the [EarthCODE Hackathon 2026](https://esa-earthcode.github.io/) website
— a [Quarto](https://quarto.org/) website with the event's schedule, logistics,
and supporting pages.

## Development

Requires [Quarto](https://quarto.org/docs/get-started/) (1.2+).

- Preview locally with live reload:

  ```sh
  quarto preview
  ```

- Render the full site (output goes to `_site/`):

  ```sh
  quarto render
  ```

### Project structure

- `.qmd` files — Quarto source files, rendered to HTML.
- `data/schedule.yml` — schedule content, rendered by the `schedule` shortcode
  (see below).
- `_extensions/ateucher/schedule/` — Quarto extension providing the
  `{{< schedule >}}` shortcode and its styling (`schedule.css`).
- `styles.css` — site-wide CSS tweaks.
- `index.css` — CSS applied only to the homepage
- `theme.scss` — Sass theme customization.
- `img/` — logos and other images.

## Editing the schedule

All schedule content lives in `data/schedule.yml` — don't edit HTML/Lua to
change schedule content, just this file. The `{{< schedule file="data/schedule.yml" >}}`
shortcode in `index.qmd` renders it as a tabbed table (one tab per day).

The file is a list of `days`, each with a `title`, `date`, and a list of
`sessions`:

```yaml
timezone: "UTC+1 (Central European Time)"
days:
  - title: "Day 1"
    date: "Monday"
    sessions:
      - time: "9:00 - 13:00"
        title: "Arrival & Check-in"
        type: "session"            # optional, see below
        leads: []                  # optional list of names, e.g. ["Dean", "Julie"]
        description: "Arrive, check in, and settle in ahead of the afternoon kickoff."
```

Notes:

- `type` controls the row's color coding (see `.sched-<type>` rules in
  `_extensions/ateucher/schedule/schedule.css`). Currently used values:
  `keynote`, `tutorial`, `work`, `break`. Omit `type` for a plain, uncolored
  session row.
- `leads` is optional; leave it as `[]` if there's no specific lead, or a
  session doesn't need one (e.g. breaks).
- `description` is optional; use `""` if there isn't one.
- Add or remove sessions/days freely — the shortcode renders however many
  days and sessions are present.

After editing, re-render (`quarto render` or `quarto preview`) to see the
updated schedule.
