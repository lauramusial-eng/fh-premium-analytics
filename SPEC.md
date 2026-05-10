---
title: Feature Spec — Premium Analytics validation artifact
created: 2026-05-06
related:
  - "[[project-config]]"
  - "[[../../decisions/2026-05-06-OST-revenue-diversification]]"
template: "[[../../../../6-Templates/Feature Spec]]"
build-target: A1.4 (smoke test waitlist)
reuse: A1.3 (wywiady) używa identycznego pliku bez modyfikacji
success: ≥30 / 500 sellerów (6%) zostawia kartę, liczone per UTM segment
---

# Feature Spec — Premium Analytics validation artifact

## Co budujemy

Skinny single-page demo Premium Analytics + landing waitlist w jednym pliku HTML. **Build target: A1.4** (smoke test). A1.3 (wywiady) używa identycznego pliku bez modyfikacji — nie koduj pod niego osobno.

## User flow

1. Wejście z `?utm_segment=cichy|negocjator|nowy`
2. Scroll przez 3 widoki
3. CTA → form (email + opcjonalna karta) → capture do Airtable

## Kryteria akceptacji

- 3 widoki z mock data: (a) benchmarks kategorii (Twoja vs średnia), (b) top 10 cen konkurencji w mojej kategorii + delta, (c) demand alerts sezonowe (zapytania ±% MoM)
- CTA „Dołącz do waitlist - 99 PLN/m, start Q3 2026" pod każdym widokiem
- Form: Stripe Checkout test mode lub Tally/Airtable (nigdy real charge)
- UTM segment zapisywany w capture
- Single HTML, mobile-first, GitHub Pages, Lighthouse perf ≥80 mobile

## Czego NIE budujemy

- Real backend, real data, real charge
- Onboarding, settings, dashboard po zakupie
- A/B test ceny (99 PLN fixed)
- Inne widoki niż 3 zatwierdzone
- Osobna ścieżka dla A1.3 (ten sam plik)

## Przykłady

**Input:** `?utm_segment=cichy`, kategoria Sukienki. Konwersja 3.1% vs średnia 2.4%, ceny konkurencji 149 / 169 / 179 PLN, „Lniane sukienki +47% MoM".
**Oczekiwany rezultat:** seller zostawia email + kartę, capture: `{utm: cichy, email, card_token, ts}`.

---

**Input:** `?utm_segment=negocjator`, streetwear.
**Oczekiwany rezultat:** brak capture — success liczony per segment.
