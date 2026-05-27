# STATUS-NA.md — Nåværende tilstand

Sist oppdatert: 2026-05-27 22:55 CEST

## Prosjekt

- **Navn:** enok-72-truth-instrument
- **Formål:** Enok 72 / AE-projeksjon simulator og sannhetsinstrument
- **Gjeldende versjon:** v16.30 (deployet 26. mai 2026)
- **Status:** Stabil baseline. Buestreng-uretting er implementert. Forbereder Grok-pipeline mot v17.

## Masterregel

Ved alt arbeid med simulatoren skal `simulator-master-referanse.md` leses først.

Hvis denne statusfilen, agentminne eller tidligere dialog er i konflikt med `simulator-master-referanse.md`, gjelder masterfilen.

Hierarki ved konflikt:
1. Ark T (Excel H212 = 23,7°)
2. Enoks bok kapittel 72
3. Jone-Aase (prosjektleder)
4. simulator-master-referanse.md
5. STATUS-NA.md
6. Agent-minne (svakest)

Ingen endring i geometri, portsystem, kalender eller projeksjon skal gjøres uten eksplisitt godkjenning fra prosjektleder.

## Roller (låst arbeidsmodell)

| Rolle | Ansvar | Bærer |
|---|---|---|
| Beslutningstaker | Endelig godkjenning av alle endringer | Jone-Aase |
| Minne-/utviklerlag | Husker dialog, foreslår kodeendringer, dokumenterer valg | Grok |
| Utfører-/deploylag | GitHub-push, deploy, arkivering, kjøring | Perplexity-agent |
| Kvalitetskontroll | Validering, kritisk review, URL/koordinat-sjekk | ChatGPT |
| Avgrensede oppgaver | Datainnsamling, verifikasjon | Mistral, Copilot, Gemini, Google AI, Justdone, Grok 12-agenter, Grok Heavy |

## Nåværende teknisk tilstand

### Live-versjoner

- **GitHub Pages:** https://jone-aase.github.io/enok-72-truth-instrument/
- **Computer asset:** https://www.perplexity.ai/computer/a/enoch-72-the-truth-instrument-OEcJXJkpSumshIfR5grJWg
- **GitHub repo:** https://github.com/Jone-Aase/enok-72-truth-instrument

### Hovedfiler

- `index.html` (1432 linjer)
- `app.js` (3016 linjer, v16.30)
- `calendar.json` (139 KB)
- `sol-bane-arkT.json` (37 KB)
- `enok-himmel-vers.json` (30 KB)
- `enok72-vers.json` (7 KB)
- `timeline.json` (5 KB)
- `un-map.png` (112 KB)
- `Ark-T-V6-uttrekk.xlsx` (401 KB)

### Implementert geometri (v16.30)

Buestreng-uretting er IMPLEMENTERT (app.js linje 18-22):

```javascript
// BUESTRENG-URETTING (v16): hele 180° breddegrad strekkes til R_OUTER.
// r(90) = 0, r(0) = R_OUTER/2 = 15710 km, r(-90) = R_OUTER = 31420 km.
function latToR(lat) {
  return R_OUTER * (90 - lat) / 180;
}
```

Dette betyr at den gamle v15-formelen `R_EQUATOR * (90 - lat) / 90` er forlatt.

### Kjernekonstanter v16.30

- `R_EQUATOR_KM = 10001.47`
- `R_OUTER_KM = 31420.55`
- `SCALE = 1/1000`
- Full omkrets = 197 421,10 km

### Posisjoner langs buestrengen

| Punkt | Breddegrad | r (km fra polen) |
|---|---|---|
| Nordpol | +90° | 0 |
| Polarsirkel | +66,5° | 4 089 |
| Krepsens vendekrets | +23,7° | 11 608 |
| Ekvator | 0° | 15 710 |
| Steinbukkens vendekrets | −23,7° | 19 812 |
| Antarktis (ytterring) | −90° | 31 421 |

### Portsystem

Portsekvens (12 måneder):

```
4 → 5 → 6 → 6 → 5 → 4 → 3 → 2 → 1 → 1 → 2 → 3
```

Hovedankere (kjente sol-bane-punkter):

| Dag | Hendelse | Port | Breddegrad |
|---|---|---|---|
| 1 | Vårjevndøgn (1 Abib) | 4 | 0° |
| 91 | Sommersolverv | 6 | +23,7° |
| 182 | Høstjevndøgn | 4 | 0° |
| 273 | Vintersolverv | 1 | −23,7° |
| 364 | Tilbake til vårjevndøgn | 4 | 0° |

Pluss 4 ekstrarunder (dag 91, 182, 273, 364) → 368 reelle sol-runder.

### Kalender

- Master: Ark T (Time-364-354-versjon)
- Simulatorfil: `calendar.json`
- Enok år 5676 AM
- Starter 2026-03-21 (1 Abib), slutter 2027-03-19
- 364 dager, 12 måneder, 4 kvartaler × 91 dager
- 30+30+31-mønster per kvartal
- 31-dagers måneder: Sivan, Elul, Kislev, Adar

### Måne

Status: **Holdes utenfor solinstrumentet.** Skal få eget instrument senere.

Begrunnelse: Månesystemet er komplekst og skal ikke blandes inn før solmodellen er stabil.

## Empiriske funn til nå

| Funn | Konklusjon |
|---|---|
| Polarsirkelen (Fort Yukon, Bodø, Grímsey) 24 t sol ved sommersolverv | Matcher Enok port 6 = 18/0 **100 %** |
| Aswan +24,088° hadde 13 t 40 min dag | Avviker fra Enok 9/9 (12 t 00) med +1 t 40 min |
| Cancer-test 19 punkter, omkrets 36 548 km | Kule −0,60 %, AE-Enok −21,35 % — Cancer alene støtter kule |
| Cook RESOLUTION 1774 ved 53°S | AE-Enok krever 19,91 knop — fysisk umulig |
| CLIWOC 249 649 observasjoner | Bekrefter 15°/time, kan ikke avsløre hav-forskyvning |
| Pontianak-Antofagasta-akse | 179,72° (avvik 0,28° fra perfekt 180°) |
| Earth-circumference | GE-radius 10 001,47 km gir 62 841 km, WGS84 40 075 km gir radius 6 378 km — intern motsigelse |

## Aktiv hypotese

Verbatim Jone-Aase: *"Jeg tror at lengdegradene er rett men kontinentene er forskjøvet, i havområdene."*

Testes med fire Krepsen-observatorier (Aswan, Modhera, Chiayi, Ujjain — 88° lengde-spredning, forventet 5 t 52 min mellom østligste og vestligste).

## Fire åpne gåter

1. **Port-paradokset:** kontinuerlig 0,2604°/dag bevegelse vs. 6 fysiske porter i Enok 72
2. **Krepsen-avviket:** 9/9 vs. 13 t 40 min faktisk i Aswan
3. **Systematisk 3-min restavvik** solar noon på 5 kontinenter
4. **Kontinent-forskyvningen** (aktiv hypotese over)

## Pågående arbeid

- **Grok-pipeline mot v17** etableres
- Mappestruktur for grok-dialog/, grok-versjoner/, validation/, docs/ opprettet
- Første endring i pipeline: ikke valgt ennå (Grok foreslo glød/puls på 4 ekstrarunder som nr. 1)

## Godkjent / ikke godkjent

### Godkjent
- Masterreferanse etablert
- v16.30-baseline (buestreng-uretting LIVE)
- R_OUTER_KM = 31 420,55 implementert
- Enok 72 portsekvens definert
- Kalender 5676 AM definert
- Månen holdes utenfor solinstrumentet
- Arbeidsmodell med fire roller (beslutning, minne, utfører, QA)
- Grok-pipeline med kandidat-branch

### Ikke godkjent ennå
- Konkrete v17-endringer (venter på Grok sine forslag)
- Re-projisering av FN-karttekstur
- Endring av vendekretser (23,7° er låst inntil videre)
- Måneinstrument
- Offentlig geometri-konklusjon

## Arbeidsregel før hver større endring

Dette dokumentet skal oppdateres med:

1. Hva skal endres?
2. Hvorfor?
3. Hvilke filer berøres?
4. Hvilken risiko finnes?
5. Er prosjektleder-godkjenning gitt?
6. Er backup/branch opprettet?

## Neste steg

1. Sette opp `grok-v17-kandidater` branch
2. Vente på første Grok-endring (zip eller filer)
3. Deploye til separat live-URL for testing
4. Logge dialog i `grok-dialog/`
5. Versjonere kandidater i `grok-versjoner/`
6. Bare godkjente endringer merges mot main
