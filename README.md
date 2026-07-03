---
owner: JG
category: P
status: active
created: 2026-07-03
---

# Vacek Performance — white-label coaching platforma (pilot)

B2B SaaS nápad: **brandovateľná platforma na tréningové plány + tracking atlétov** pre malých
cyklistických koučov a kluby. Pilotný zákazník: **Vacek Performance** (Karel Vacek — český ex-profík,
trénuje manažérov a amatérov na bicykli, dnes píše plány ručne bez trackingu).

## Stav projektu

| Fáza | Stav |
|---|---|
| 1. Trhový research | ✅ hotový — [research/market-research-2026-07.md](research/market-research-2026-07.md) |
| 2. Produktová špecifikácia MVP | ✅ draft — [docs/product-spec.md](docs/product-spec.md) |
| 3. Klikateľné demo (mock dáta) | ✅ [index.html](index.html) — na ukážku Karlovi |
| 4. Validácia s Karlom (workflow, cena, branding ako motív) | ⬜ |
| 5. Právna forma + Garmin Connect Developer Program žiadosť | ⬜ |
| 6. MVP build (backend + Garmin integrácia) | ⬜ |

## Kľúčové rozhodnutia (z researchu)

- **Garmin Connect API = dátová chrbtica.** Training API push tréningov do zariadení + Activity API import jázd. Zadarmo, ale žiadosť musí podať firma (s.r.o./živnosť).
- **Strava nie.** Od 30. 6. 2026 platené API, ~10 atlétov limit, AI zákaz. Max. voliteľný doplnok neskôr.
- **Diferenciácia:** plný white-label (platforma pod menom kouča), CZ/SK lokalizácia, jednoduchosť pre hobby klientov. GoodCoach (€3/atlét) robí len logo+farby.
- **Pricing hypotéza:** ~€5–8/atlét/mes. alebo flat fee €99–149/mes. do 30 atlétov.

## Demo

- Single-file prototyp `index.html` — bez buildu, otvor v prehliadači alebo GitHub Pages.
- Dva pohľady: **Trenér** (roster, compliance, detail atléta, push tréningu do Garminu — mock) a **Atlet** ("co mám dnes", týždeň, výsledky).
- White-label je demonštrovaný `BRAND` objektom na začiatku skriptu — zmena mena/farby/loga = iný kouč.
- UI v češtine (cieľový trh pilotu).

## Repo štruktúra

- `index.html` — klikateľné demo (mock dáta, žiadny backend)
- `docs/product-spec.md` — špecifikácia MVP
- `research/market-research-2026-07.md` — overený trhový research (júl 2026)
