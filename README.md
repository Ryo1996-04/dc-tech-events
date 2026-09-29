# DC Tech Radar

A two-page static website listing highly technical tech events in the Washington, DC area (conferences, security cons, meetups, workshops and hackathons) from October 2026 to March 2027, each with a link to its registration page.

Built with plain HTML and CSS only: no JavaScript and no outside libraries.

**Live site:** <https://ryo1996-04.github.io/dc-tech-events/>

## Run it

The pages must be viewed through a web server:

```bash
npx serve
```

Then open the address it prints (usually <http://localhost:3000>).

## Files

```
index.html          Events Board (homepage): two sections of event cards
guide.html          Planning Guide: month-by-month calendar plus planning tips
styles/site.css     Shared by both pages: design tokens, base, header, footer, shared building blocks
styles/events.css   Only for index.html: 12-column card grid and event cards
styles/guide.css    Only for guide.html: calendar list and sidebar
images/logo.svg     Site logo, drawn for this project
```

## How the requirements are met

| Requirement | Where |
| --- | --- |
| Common look and feel | Both pages share the color and spacing tokens, typography and building blocks (`.page-intro`, `.section-title`, `.cta-link`, `.register-link`) in `styles/site.css`. |
| Identical header and footer, one shared CSS file | The `<header class="site-header">` and `<footer class="site-footer">` markup is byte-for-byte identical in both pages, and only `styles/site.css` styles it. |
| Page-specific CSS | `index.html` loads `styles/events.css`; `guide.html` loads `styles/guide.css`. Neither file styles anything that appears on the other page. |
| 3-across and 4-across card sections on one 12-column grid | `index.html`: `.card-grid` is `repeat(12, minmax(0, 1fr))`. Conference cards span 4 columns (3 per row) and meetup cards span 3 columns (4 per row). |
| Responsive rem breakpoints | See the table below. Mobile first: cards span all 12 columns until a `min-width` breakpoint makes room for more. |
| Pages link to each other usefully | Header and footer nav on both pages; the "See the month-by-month calendar" button and the teaser on the Events Board; on the Planning Guide, the "Browse the event cards" button and every event name, which jumps to that event's card (`index.html#card-id`, highlighted with `:target`). |

| Viewport width | Conference cards per row | Meetup cards per row |
| --- | --- | --- |
| under 30rem | 1 | 1 |
| 30rem to 48rem | 1 | 2 |
| 48rem to 64rem | 2 | 3 |
| 64rem and up | 3 | 4 |

### Design principles

- **Visual hierarchy.** On every page, size, weight and color step down in a fixed order: red kicker, large navy `h1`, section `h2`, card `h3`, then small muted detail text. Conference titles are larger than meetup titles, because conferences are the bigger commitment.
- **Balance.** The header balances the logo on the left against the nav on the right. The card grids are symmetrical: every card in a row has the same width, and `.card-action { margin-top: auto; }` lines the Register buttons up even when the text above them differs in length. The Planning Guide uses asymmetrical balance: a wide, light calendar column (2fr) is weighed against a narrow sidebar (1fr) of tinted, dense panels.
- **Proximity.** Inside a card, the date badge sits right next to the event type and title, and When, Where and Cost are grouped in one tight `<dl>` (0.25rem gaps). Separate cards are 1.5rem apart. On the guide, events are grouped under their month heading with a rule, and each row keeps date, name, details and button together.
- **Emphasis.** The red accent is saved for what matters most: Register buttons, the headline numbers and the kickers. "Free" gets a green pill so budget-friendly events stand out. The navy date badges make dates scannable. A card reached from the guide gets a red outline.

### Code conventions

- Semantic HTML: `header`, `nav`, `main`, `section`, `article` for each event card, `aside`, `footer`, `dl`/`dt`/`dd` for event details, `time datetime`, ordered lists for chronological content, and headings from `h1` to `h4` in order.
- Class names are lowercase kebab-case and describe the content, not its appearance (`event-card`, `register-link`, `agenda-month`).
- Every selector is class based except `body`. There are no id selectors and no `!important`, and each property goes on its own line.
- Accessibility touches: repeated "Register" links get an `aria-label` that names the event, the decorative date badge is `aria-hidden`, and the logo image has empty `alt` because the brand name sits right next to it.

## Images

`images/logo.svg` is an original drawing made for this project: three stars and two bars, a nod to the DC flag. The site uses no other images, and no third-party image files.

## Keeping the listings current

This is a static site with no scripts, so it cannot update itself. Each event was checked by hand against the organizer's own page on **September 29, 2026**, and that date appears in the footer. To update the site, edit the card in `index.html` and the matching row in `guide.html`, then change the date in both footers.
