<wizard-report>
# PostHog post-wizard report

The wizard has completed a deep integration of PostHog analytics into the FashionHero Premium Analytics validation page (`index.html`). The posthog-js SDK is initialized via the standard browser snippet in `<head>`, pointing to the EU PostHog host. Six custom events are instrumented across the full user journey — from initial section scroll through CTA click, modal interaction, and final waitlist signup — with rich properties (UTM segment, category, has_card) on every event. Users are identified by email on successful signup using `posthog.identify()`. Airtable capture errors are forwarded to PostHog via `posthog.captureException()`.

| Event | Description | File |
|---|---|---|
| `section_viewed` | Fired once per section (benchmarks, prices, demand) when it first scrolls into view — top of funnel. Properties: `section_id`, `utm_segment`, `category`. | `index.html` |
| `waitlist_cta_clicked` | Fired when the primary CTA button ("Dołącz do waitlist") is clicked (desktop sidebar or mobile CTA). Properties: `cta_location`, `utm_segment`, `category`. | `index.html` |
| `unlock_premium_clicked` | Fired when the "Odblokuj Premium" button in the locked price table is clicked. Properties: `utm_segment`, `category`. | `index.html` |
| `waitlist_modal_closed` | Fired when the modal is dismissed without submitting. Skipped if the form was already submitted. Properties: `utm_segment`, `category`. | `index.html` |
| `waitlist_form_submitted` | Fired when the waitlist form passes validation and is submitted. Properties: `has_card`, `utm_segment`, `category`, `segment_label`. | `index.html` |
| `waitlist_signup_completed` | Primary conversion event — fired after Airtable capture, success screen shown. User is identified by email at this point. Properties: `has_card`, `utm_segment`, `category`, `segment_label`. | `index.html` |

## Next steps

We've built some insights and a dashboard for you to keep an eye on user behavior, based on the events we just instrumented:

- [Analytics basics dashboard](/dashboard/684882)
- [Waitlist Conversion Funnel](/insights/a39OdDsA) — end-to-end funnel from section view → CTA click → form submit → signup completed
- [Daily Signups](/insights/AdT6D0DV) — primary conversion metric time series
- [Signups by UTM Segment](/insights/pSoJPkQ5) — per-persona breakdown (cichy / negocjator / nowy)
- [Signups With vs Without Card](/insights/B6BRoGUG) — payment commitment signal
- [Modal Abandonment vs Signup](/insights/PVTf5VQB) — form drop-off rate

### Agent skill

We've left an agent skill folder in your project. You can use this context for further agent development when using Claude Code. This will help ensure the model provides the most up-to-date approaches for integrating PostHog.

</wizard-report>
