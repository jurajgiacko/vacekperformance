# Vacek Performance — trhový a feasibility research (júl 2026)

> Hĺbkový research k nápadu: white-label / brandovateľná platforma na tréningové plány + tracking atlétov
> pre malých cyklistických trénerov a kluby. Pilot: **Vacek Performance** (Karel Vacek).
> Metóda: 5 search uhlov → 22 zdrojov → 108 extrahovaných tvrdení → 25 top tvrdení adversariálne overených
> (3 nezávislé hlasy na tvrdenie): 19 potvrdených, 6 vyvrátených. Ceny platné k júlu 2026.

## TL;DR verdikt

Príležitosť je **reálna, ale úzka**. Trh sa konsoliduje (Today's Plan — vlastnený Specialized — zatvoril
12. 3. 2024), líder TrainingPeaks zdražuje, a medzera „brandovaná platforma pre malého kouča" je obsadená
len čiastočne (GoodCoach robí logo + farby, ale nie plný white-label). Jediná realistická integračná
chrbtica je **Garmin Connect Developer Program** (zadarmo, ale len pre firmy — treba s.r.o./živnosť).
**Strava sa ako základ použiť nedá** (platené API od 30. 6. 2026, limit ~10 atlétov na standard tieri,
zákaz AI použitia dát). Odporúčanie: web-first MVP s Garmin integráciou, pilotovať s Karlom, cena
~€5–8/atlét/mes.

---

## 1. Konkurenčná mapa a ceny (overené)

| Platforma | Cena pre kouča | Branding / white-label | Poznámka |
|---|---|---|---|
| **TrainingPeaks** | $21.99/mes. (1 Premium + 4 Basic atléti, $99 aktivácia — často odpustená kupónom TPCOACH); Unlimited $54.99/mes.; + **$9/atlét/mes.** Premium (zľavy: $8.55 pri 10–19, $8.10 pri 20–49) | žiadny white-label | dominantný líder; Premium pre atlétov zdraželo o 8 % na $134.99/rok (od 4/2025) |
| **intervals.icu** | zadarmo (voliteľný supporter tier ~½ ceny TP) | žiadny | silný low-cost hráč, obľúbený medzi data-geeks; coach features existujú |
| **Final Surge** | od ~$19/mes. | **len logo + header obrázok**, nie plný white-label | lacnejšia TP alternatíva |
| **GoodCoach** | zadarmo do 2 atlétov, potom **~€3/atlét/mes.** (klesá k €1) | vlastné farby + logo naprieč Web/Android/iOS | najbližší konkurent tejto idey; integrácie Garmin/Wahoo/Coros/Suunto/Polar |
| **Today's Plan** | — | — | **zatvorený 12. 3. 2024** napriek vlastníctvu Specialized — dôkaz, že ekonomika segmentu je tvrdá |

Vyvrátené počas verifikácie (pozor na tieto mýty): TP Coach Edition nezačína na $19/mes.;
Audiorista nie je reálny white-label builder pre cycling coaching; TrainingPeaks predaj plánov
priamo atlétom ako „konkurencia koučom" sa nepotvrdil.

## 2. Existuje medzera?

**Čiastočne áno.** Nikto z veľkých nerobí plný white-label (appka/web pod menom a doménou kouča).
GoodCoach je najbližšie, ale končí pri farbách a logu. Otvorené diferenciácie:

1. **Plný white-label** — platforma beží pod brandom kouča (vlastná doména, appka „Vacek Performance", nie „GoodCoach").
2. **CZ/SK lokalizácia a servisná blízkosť** — nikto z hráčov nemá lokálny jazyk ani podporu.
3. **Workflow malého kouča** (1–50 atlétov) — TP je stavaný na profíkov a veľké rostery; malí kouči sa na fórach (Slowtwitch, TrainerRoad forum) sťažujú hlavne na per-athlete ceny.
4. Príležitostný segment: **manažéri/hobby jazdci** — Karlov klient nechce CTL/TSS grafy, chce „čo mám dnes jazdiť a ako mi to išlo" — jednoduchosť ako feature.

⚠️ Slabina researchu: primárne dôkazy o sťažnostiach koučov (rozhovory, recenzie) sú tenké — bolesti sú
odvodené z cien a feature medzier. Pred stavbou treba 3–5 rozhovorov s reálnymi koučmi (Karel + jeho okolie).

## 3. Integrácie — čo je reálne v 2026

### Garmin Connect Developer Program — ✅ primárna cesta
- **Zadarmo** (bez licenčných/udržiavacích poplatkov za základný prístup); niektoré prémiové metriky môžu byť platené.
- **Training API**: push štruktúrovaných tréningov priamo do Garmin Connect kalendára atléta → sync do Edge/hodiniek na krok-za-krokom vykonanie. Presne to, čo koučovacia platforma potrebuje (dôkaz: Tredict, intervals.icu to takto robia).
- Activity/Health API: automatický import dokončených aktivít (koniec screenshotov).
- **Podmienky**: len pre firmy — žiadosť musí podať s.r.o./živnosť, fyzické osoby zamietajú. Potvrdenie žiadosti ~2 pracovné dni, evaluation tier ~15 test userov, potom produkčné review; produkcia spočiatku throttlovaná.

### Strava — ❌ nie ako základ
- Od **30. 6. 2026** standard tier vyžaduje platené Strava predplatné developera (~$12/mes.).
- Standard tier limitovaný na dáta **~10 atlétov** (FAQ spomína až 9 999 po schválení — rozpor v zdrojoch, treba overiť priamo).
- Extended Access Tier: nezverejnené ceny, individuálne schvaľovanie.
- **Zákaz použitia Strava dát v AI modeloch** (od 11/2024) — blokuje AI-coaching na Strava dátach.
- intervals.icu verejne: zmeny z 11/2024 „break all coaching features" viazané na Strava dáta. Právny stav zobrazovania dát atléta koučovi = šedá zóna.
- Strava max. ako *voliteľný doplnok* (social sharing), nikdy ako dátová chrbtica.

### Apple Watch / HealthKit
- Vyžaduje natívnu iOS appku (HealthKit nemá server-side API) → **nie v MVP**. Karlovi klienti na bicykloch majú prevažne Garmin. Doplniť vo fáze 2, ak dopyt.

## 4. Cenový benchmark a model

- Strop: TrainingPeaks efektívne ~$9/atlét/mes. + base fee. Dno: GoodCoach €3/atlét/mes., intervals.icu zadarmo.
- **Pilot pricing: ~€5–8/atlét/mes.** alebo flat fee pre kouča (napr. €99–149/mes. do 30 atlétov) — flat fee je pre malého kouča predvídateľnejší a odlišuje od TP per-athlete modelu.
- Veľkosť trhu CZ/SK/EU amatérskeho koučingu: **research nepriniesol tvrdé čísla** — otvorená otázka; validovať zdola (koľko koučov pozná Karel, koľko atlétov majú, čo dnes platia).
- Memento mori: Today's Plan neprežil ani so Specialized za chrbtom. Stavať lean, s pilotným zákazníkom, ktorý platí od začiatku (hoci symbolicky).

## 5. Odporúčané MVP pre pilot s Vacek Performance

*(syntéza — odvodené z overených faktov, nie samostatne overený fakt)*

**In:**
1. **Garmin obojsmerná integrácia** — import dokončených aktivít (Activity API) + push štruktúrovaných tréningov do zariadení (Training API).
2. **Tréningový kalendár** — kouč plánuje týždne/bloky (drag-and-drop), atlét vidí „čo dnes".
3. **Coach dashboard s compliance** — naplánované vs. odjazdené, HR/zóny, red flags (vynechané tréningy, prekročená intenzita). Presne to, čo dnes robí road-classics-2026 repo ručne cez commity.
4. **Branding kouča** — logo, farby, vlastná doména (vacekperformance.cz) od prvého dňa.
5. **Web-first** (responzívny), žiadna natívna appka v MVP.

**Out (zámerne):** Strava integrácia, AI features na cudzích dátach, platobný modul, natívne appky, iné športy než bike (+ prípadne beh/sila ako jednoduché manuálne typy — model už existuje v road-classics PLAN schéme).

**Prerekvizity:**
- Právna forma (s.r.o./živnosť) → žiadosť do Garmin Connect Developer Program (počítať s evaluation tierom ~15 userov = na pilot presne stačí).
- Rozhovor s Karlom: jeho dnešný workflow (ako píše plány, kanál komunikácie s klientmi, počet atlétov, cena jeho koučingu) → z toho finálny scope MVP.

## 6. Otvorené otázky

1. Skutočný limit atlétov na Strava standard tieri (10 vs. 9 999) a cena Extended tieru — priamy dopyt na Stravu (nízka priorita, ak Strava nebude v MVP).
2. Veľkosť a ochota platiť trhu CZ/SK koučov — validovať rozhovormi, nie desk researchom.
3. Reálna dĺžka Garmin schválenia pre malú SK s.r.o. + ktoré metriky sú platené.
4. Je branding pre koučov reálny kúpny motív, alebo nice-to-have? (kľúčová hypotéza celej idey — testovať na Karlovi a 3–5 ďalších koučoch pred písaním kódu)

## 7. Kľúčové zdroje

- TrainingPeaks pricing: trainingpeaks.com/pricing/for-coaches, help.trainingpeaks.com (204072544)
- TP zdraženie: dcrainmaker.com/2025/02/trainingpeaks-announces-subscribers.html
- Today's Plan shutdown: cyclingweekly.com, velo.outsideonline.com, trainingpeaks.com/todays-plan-alternative
- Garmin: developer.garmin.com/gc-developer-program/ (program-faq, training-api), tredict.com blog
- Strava API zmeny: press.strava.com/articles/updates-to-stravas-api-agreement, heise.de, communityhub.strava.com, dcrainmaker.com/2024/11
- GoodCoach: goodcoach.app, the5krunner.com (2026/05)
- Final Surge branding: finalsurge.com/coaches, trainingtilt.com (blog konkurenta — brať s rezervou)
