# Featured Banner Content Guidelines

Use this document to prepare content and guide edits to the **Featured promotional carousel** on UC Merced Hub. It covers events, projects, apps, resources, and opportunities.

The content lengths below are editorial recommendations, not limits enforced by the code. Check the finished slide at desktop and mobile widths.

## 1. Content to provide

| Field | Required? | Guidance |
| --- | --- | --- |
| Short label | Yes | A category or announcement, such as “Upcoming Event,” “Student Project,” or “Now Available.” Aim for 2–5 words. |
| Banner title | Yes | The main headline. Aim for 5–9 words. |
| Description | Yes | Explain what is being promoted and why it matters. Aim for 20–35 words. |
| Promotional image | Yes | A flyer, photo, or graphic. PNG, JPEG, or WebP is suitable. A 2:3 portrait image, such as 1024 × 1536 pixels, is recommended. |
| Image description | Yes | Brief, meaningful alternative text describing the image. |
| Main button | Yes | A short action label and its destination URL. Examples: “RSVP Now,” “Learn More,” or “Download App.” |
| Highlights | Optional | Up to three short benefits or important details, preferably one line each on desktop. |
| Organizer or credit | Optional | One short attribution, such as “Hosted by the Robotics Society.” |
| Event date | For events | The event's calendar date. |
| Event time | When applicable | The start time, using the campus's local time. State if the event is all-day or the time is unconfirmed. |
| Event location | For events | The venue, room, or online location. |
| Second button | Optional | Another short label and URL, such as “View Location” with a map link. |
| Copy link control | Always present | A compact icon button is added by the shared banner template after the main and optional second buttons. It copies the canonical UC Merced Hub URL; it is not a slide-specific destination. |

Also provide the **requested display dates** and a **contact name and email** for editorial follow-up. These are management details, not public banner fields. Keep private contact information out of the public page and public repository.

## 2. Content and image guidelines

- Lead with the main benefit or reason to participate. Keep button labels specific and short.
- Use less copy when including event details. Remove optional sections that add little value.
- Include essential information in the text fields even when it appears in the image.
- Desktop displays the whole image using `object-fit: contain`. At carousel container widths of 940px or less, the layout stacks and crops the image using `object-fit: cover` with `object-position: center top`.
- Keep the image's important subject near the upper portion, and check the mobile crop. The existing image viewer lets visitors expand the full image.
- Use the image's actual pixel dimensions for its HTML `width` and `height` attributes. The recommended portrait size is not mandatory.

## 3. Where Codex should edit

Search the current repository for `id="app-promotion"` to find the page containing the Featured carousel. Do not assume the page filename. Each promotion is one `<li class="slide">` inside:

```css
#app-promotion .app-promo-frame .carousel-inner > .slides
```

Scope the following selectors to the requested slide:

| Content | HTML location |
| --- | --- |
| Short label | `.app-promo-copy > .promo-eyebrow` |
| Banner title | `.promo-title-text` inside `.app-promo-title` |
| Description | `.app-promo-text` |
| Organizer or credit | `.app-promo-caption` |
| Highlights | `<li>` items inside `.app-promo-highlights` |
| Event date and time | `data-event-date="YYYY-MM-DD"` and `data-event-time="HH:MM"` on the slide; time uses 24-hour format |
| Readable event date and time | `.app-promo-date-value`; provide readable fallback text matching the attributes |
| Event location | `.app-promo-date-location` |
| Main button | First `<a>` inside `.promo-actions`: its text and `href` |
| Second button | Second `<a>` inside `.promo-actions`: its text and `href` |
| Copy link control | `.promo-copy-link` after the two banner links. Do not remove, relabel, or use it for a slide-specific URL. It uses `assets/link.svg`, copies `https://ucmercedhub.com/`, has the accessible label and tooltip “Copy link,” and shows a non-blocking “Link copied!” confirmation with a checkmark for about two seconds. |
| Promotional image | `.app-promo-art`: its `src`, `alt`, `width`, and `height` |
| Image expansion labels | `aria-label` on `.promo-image-trigger` and `.promo-fullscreen-button` |

Existing promotional images use `/img/promotional_banner/`. Follow the repository's current asset organization when adding a new image.

## 4. Editing rules for Codex

1. Identify the requested slide by its title or content. For a new promotion, duplicate an appropriate existing slide and replace its content.
2. Make the requested content edits using the existing structure and styles. Preserve other slides and shared carousel behavior unless the task also requests changes to them.
3. Remove unused optional elements entirely. For a non-event promotion, remove both `data-event-*` attributes and the entire `.app-promo-date` paragraph.
4. Keep only one initial slide marked `data-active="true"`. If changing the initial slide, move that attribute. Keep the shared controls and single `#promo-image-viewer`; navigation dots are generated by the existing script.
5. Update related accessibility text, including the highlights list label and image expansion labels. Preserve appropriate link behavior and `rel="noopener noreferrer"` for links opening in a new tab.
6. Preserve the shared copy-link button after the two banner buttons. It must not navigate, and it must retain its keyboard access, “Copy link” accessible label, and success/error announcement behavior.
7. Use provided facts, dates, images, and URLs. If essential information is missing, identify what is needed rather than inventing it. Do not leave placeholder values in published content.
8. Verify the current code before applying these mappings; update this document if the relevant structure changes.

### Existing behavior to account for

- `initPromoDates()` formats event attributes into visible text. It does not convert time zones or remove expired promotions.
- Requested display dates require manual scheduling or removal unless the repository has since added scheduling support.
- `initSlider()` and `initPromoImageViewer()` discover slides and image triggers at initialization. Reload the page after editing the HTML.
- The desktop banner has a fixed height, so long content can overflow. Narrow layouts grow with the content.
- Featured slides follow the page theme. In the supplied implementation, per-slide `data-slide-theme` settings apply only to the separate “What's New” carousel.

## 5. Review the finished edit

- Confirm text, image paths, button destinations, event attributes, and visible date text match the supplied information.
- Check desktop and phone widths for clipping, awkward wrapping, image cropping, and overlapping controls.
- Check light and dark themes, previous/next controls, dots, pause/play, image expansion, and closing the image viewer.
- Keep requested display dates and private contact details out of visible banner content.

## Example instruction for Codex

> Read `docs/FEATURED_BANNER_GUIDELINES.md`, find the Featured carousel, and update the slide titled “[existing title]” using the content below. Follow the field mappings and check the result at desktop and mobile widths. Identify any missing required information.
