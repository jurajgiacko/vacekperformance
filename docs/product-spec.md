# Produktová špecifikácia — MVP (draft v1, 2026-07-03)

Pracovný názov platformy: **CoachDeck** (interné; navonok vždy brand kouča — pilot = Vacek Performance).

## 1. Problém

Malí cyklistickí kouči (1–50 atlétov) píšu plány ručne (WhatsApp, Excel, PDF) a výsledky dostávajú
späť ako screenshoty z Garminu. Žiadny prehľad plán vs. realita, žiadna história, žiadny brand.
Existujúce nástroje (TrainingPeaks) sú drahé per-athlete, zložité pre hobby klientov a nesú cudzí brand.

## 2. Persony

- **Kouč (Karel).** Chce: napísať týždenný plán za minúty, vidieť kto trénuje a kto nie, pôsobiť
  profesionálne pod vlastnou značkou. Nechce: učiť sa TrainingPeaks, platiť $9/atlét.
- **Atlét (manažér-hobbista).** Chce: otvoriť appku a vidieť „čo mám dnes jazdiť", mať tréning
  v Garmine pripravený, vidieť že sa zlepšuje. Nechce: CTL/TSS grafy, ďalší účet s cudzím logom.

## 3. MVP scope

### In
1. **Účty a roles:** kouč + atléti (pozvánka e-mailom). Multi-tenant od začiatku (tenant = kouč/klub).
2. **Garmin integrácia (obojsmerná):**
   - Atlét pripojí Garmin účet (OAuth) raz.
   - Push: kouč naplánuje štruktúrovaný tréning → Training API → Garmin Connect kalendár → Edge/hodinky.
   - Pull: dokončená aktivita → webhook/Activity API → automaticky spárovaná s plánovaným tréningom.
3. **Tréningový kalendár (kouč):** týždenný pohľad per atlét, knižnica šablón tréningov
   (Z2 endurance, intervaly, sila, rest), kopírovanie týždňov.
4. **Coach dashboard:** roster s compliance (splnené/naplánované), red flags (vynechané 2+ tréningy,
   HR nad zónou, žiadny sync 5+ dní), posledná aktivita.
5. **Atlét view:** dnešný tréning + týždeň dopredu, výsledky (km, čas, HR, zóny), jednoduchý trend.
6. **White-label branding:** logo, farby, subdoména/vlastná doména per tenant. Konfigurácia, nie fork.
7. **Manuálne typy tréningov** (beh, sila, mobilita) — bez device syncu, len check-off + poznámka.
8. **Feedback slučka** (vzory overené z konkurencie, viď demo):
   - poznámky/chat priamo na tréningu (flat log, vzor TP post-activity comments / Final Surge Quick Comment),
   - post-workout survey atléta: feel 1–5 smajlíky + RPE 1–10 + voliteľná poznámka (vzor TP/TrainerRoad),
   - compliance farby podľa TP pravidiel (±20 % zelená, 50–79/121–150 % žltá, mimo ±50 % oranžová, vynechaný červená),
   - coach dashboard: compliance dots per deň, feed nepřečtených reakcií (unread inbox),
   - denný wellness check-in (readiness, spánok, HRV, RHR — sync z Garmin/Oura; vzor intervals.icu, JOIN „pre-fill & correct"),
   - súkromné poznámky trénera (atlét nevidí) vs. zdieľané poznámky (vzor TP Private Notes).

### Out (zámerne, fáza 2+)
- Strava (právne/cenovo riziková), Apple HealthKit (vyžaduje natívnu iOS appku), Wahoo/Polar.
- AI generovanie plánov, chat/messaging (zatiaľ WhatsApp), platby atlétov, natívne appky, výživa.

## 4. Dátový model (jadro)

Overený vzor: road-classics-2026 `PLAN` schéma, rozšírená o plán/realita split.

```
Tenant   { id, name, brand: {logo, colors, domain}, plan, locale }
User     { id, tenantId, role: coach|athlete, name, email, garminUserId?, zones: {hrMax, ftp?} }
Workout  { id, athleteId, date, type: bike|run|strength|mobility|rest,
           title, planned: { durationMin, zones[], steps[] { type, duration, target } },
           status: planned|synced|done|skipped,
           actual?: { km, movingTime, avgHr, maxHr, elevation, te, garminActivityId },
           complianceScore?, coachNote?, athleteNote? }
Template { id, tenantId, title, type, steps[] }
```

Párovanie actual↔planned: Garmin aktivita v deň D typu T → workout(D, T); nespárované aktivity
sa zobrazia ako „extra" (vzor: road-classics logy „viac ako plán!").

## 5. Architektúra (návrh)

- **Web-first monolit:** Next.js (app router) + Postgres (Neon/Supabase) + jeden worker na webhooky.
  Hosting Vercel/Fly. Žiadne mikroslužby — sme solo dev.
- **Garmin:** OAuth 1.0a/2.0 podľa programu; webhook endpoint na Activity push notifikácie;
  queue (pg-boss) na retry. Evaluation tier ~15 userov = presne pilot.
- **White-label:** tenant resolution podľa domény, brand config v DB, CSS variables.
- **Lokalizácia:** CZ default, SK/EN neskôr (i18n od začiatku, stringy mimo kódu).

## 6. Pricing hypotéza (validovať s Karlom)

- Pilot: flat **€99/mes.** do 30 atlétov (Karel možno zadarmo prvé 3 mesiace výmenou za feedback + referenciu).
- Verejne neskôr: €5–8/atlét/mes. alebo tiery (Starter 10 atlétov / Studio 30 / Club 100).
- Kotva: TrainingPeaks stojí kouča s 20 atlétmi ~$54.99 + 20×$8.10 ≈ **$217/mes.** — my polovica.

## 7. Riziká

| Riziko | Mitigácia |
|---|---|
| Garmin schválenie sa vlečie / odmietne | podať žiadosť hneď po založení s.r.o.; plán B: FIT file upload + e-mail import |
| Branding nie je kúpny motív | validovať pred buildom (Karel + 3–5 koučov); fallback pitch = „lacnejší a jednoduchší TP" |
| Ekonomika segmentu (Today's Plan zomrel) | lean, platiaci pilot od začiatku, žiadne fundraising ambície v MVP |
| Solo dev kapacita | MVP ≤ 8 týždňov práce; všetko out-of-scope tvrdo držať vonku |

## 8. Míľniky

1. **M0 (teraz):** demo prototyp → rozhovor s Karlom → go/no-go.
2. **M1:** s.r.o./živnosť + Garmin developer žiadosť podaná.
3. **M2 (+4 týždne od M1):** auth, tenant, kalendár, manuálne logy — použiteľné bez Garminu.
4. **M3 (+8 týždňov):** Garmin push/pull live s Karlovými atlétmi (evaluation tier).
5. **M4:** 3 mesiace pilotu → metriky (compliance, retention atlétov, Karlov čas ušetrený) → rozhodnutie o škálovaní.
