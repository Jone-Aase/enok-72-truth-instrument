# AGENTS.md — Enok 72 Truth Instrument
# For bruk av lokale AI-agenter i VS Code (Continue, Cline, GitHub Copilot)
# Sist oppdatert: 2026-06-13 av Perplexity Agent

---

## 0. HVEM DU ER OG HVEM SOM LEDER

Du er en lokal AI-kodingsagent (Continue eller Cline) som kjører i VS Code på Jone-Aases PC i Oslo.

**Prosjektleder:** Jone-Aase  
**Overordnet arkitekt og koordinator:** Perplexity-agenten (på perplexity.ai)  
**Din rolle:** Lokal kodeeksekutor — du implementerer det Perplexity-agenten eller Jone-Aase instruerer

Når det er konflikt mellom din vurdering og Perplexity-agentens instrukser, følger du Perplexity-agenten. Når det er konflikt mellom Perplexity-agenten og Jone-Aase, følger du Jone-Aase.

---

## 1. MASTER-REGLER (ALDRI BRYT)

1. **Norsk i all kommunikasjon med Jone-Aase.** Han bor i Oslo og snakker norsk.
2. **Ingen emojis. Aldri.**
3. **Oscar-nivå kvalitet — premien er sannheten.** Ikke ta snarveier.
4. **Hierarki ved konflikt:**
   1. Ark T (Excel H212 = 23,7° — dette er solens akse-vinkel i modellen)
   2. Enoks bok kapittel 72
   3. Jone-Aase (prosjektleder)
   4. `simulator-master-referanse.md`
   5. `STATUS-NA.md`
   6. Agent-minne (svakest)
5. **Lokasjoner skal IKKE flyttes.** Geografiske data er kanoniske og låst.
6. **Ingen endring i geometri, portsystem, kalender eller projeksjon uten Jone-Aases eksplisitte godkjenning.**
7. **Fase 1: Modellen bygges KUN fra den Astronomiske boken.** Ingen sammenligning med kule/flat-modell før Fase 7.
8. **IKKE commit direkte til main midt i en pågående fase.** Bruk feature-branch og PR.

---

## 2. PROSJEKTOVERSIKT

### Hva dette er
Enok 72 Truth Instrument er et interaktivt forskningsverktøy basert på Enoks bok kapittel 72 og den 364-dagers solkalenderen. Prosjektet bygger en geometrisk modell av solens bevegelse slik den beskrives i den Astronomiske boken (1 Enok), og verifiserer denne mot:
- Aramaiske Qumran-fragmenter (4Q208-211, DSSSE 1999)
- Etiopisk Ge'ez (Neugebauer 1981)
- Charles 1917 engelsk oversettelse (154 vers, 11 .md-filer)
- Excel-datasett (Ark T, H212 = 23,7°)

### Tilknyttede repos
| Repo | Formål |
|------|--------|
| `enok-72-truth-instrument` | Hoved-simulator, Vercel-deployed |
| `enok-atlas-flat` | Flatt verdenskart (Equal Earth + Equirectangular) |
| `enok-72-norge` | Kartverket WMTS + norske byer (SSR) |
| `enok-72-grok` | Hoved kartmotor-repo (aktiv utvikling, multi-agent) |
| `Tidslinjen-versjon-12` | AM-kronologi (Jubileumsboken, kanoniske tekster) |
| `enok-orakel-simulator` | Tidlig orakel-simulator (HTML) |

---

## 3. TEKNISK ARKITEKTUR

### Teknologistack
- **Språk:** Vanilla JavaScript (ES6+), HTML5, CSS3
- **Kartbibliotek:** Leaflet.js
- **Kartprojeksjoner i bruk:**
  - Web Mercator (standard Leaflet-tiles)
  - Equal Earth (enok-atlas-flat)
  - Equirectangular / Plate Carrée (flat kartvisning)
  - Kartverket WMTS (norsk topo, EPSG:3857 og EPSG:25833)
- **Data-format:** JSON (calendar.json, sol-bane-arkT.json, timeline.json, enok72-vers.json)
- **Deployment:** Vercel (automatisk fra `main`-branch på GitHub)
- **Passord-port:** JavaScript sessionStorage, passord `enok364`, `noindex` aktivt

### Kritiske filer — IKKE rør uten eksplisitt tillatelse
- `app.js` — hoved-applikasjonslogikk (211 KB, svært stor)
- `index.html` — hoved-HTML (101 KB)
- `calendar.json` — 364-dagers kalenderdata (kanonisk)
- `sol-bane-arkT.json` — solbane-data fra Ark T
- `un-map.png` / `un-map.webp` — UN-kartet brukt som base (IKKE overskriv)
- `vercel.json` — deployment-konfigurasjon

### Backup-filer (ikke slett)
Filene `un-map-v16.65` til `un-map-v16.76` er versjonerte backups. Ikke slett noen av disse.

---

## 4. KODESTIL OG PREFERANSER

- **Kommentarer:** Norsk i kommentarer der det er naturlig, engelsk i tekniske funksjoner
- **Variabelnavn:** camelCase for JavaScript
- **Innrykk:** 2 mellomrom (ikke tabs)
- **Ingen rammeverk:** Prosjektet bruker bevisst vanilla JS — ikke foreslå React/Vue/etc.
- **Ingen npm-pakker** uten Jone-Aases godkjenning
- **Feilhåndtering:** Alltid `try/catch` rundt kart-operasjoner og JSON-parsing

---

## 5. FASEPLAN

| Fase | Status | Beskrivelse |
|------|--------|-------------|
| Fase 1 | FERDIG | Kildemateriale + vers-uttrekk |
| Fase 2 | Neste | Strukturert vers-uttrekk, indre konsistens-sjekk |
| Fase 3 | Planlagt | Modellbygging (3D-simulator + statiske diagrammer + numerisk datasett) |
| Fase 4 | Planlagt | Excel-integrasjon (7+30 ark) + GitHub-deployment av Excel |
| Fase 5 | Planlagt | Verifisering vers for vers |
| Fase 6 | Planlagt | Team-konsultasjon |
| Fase 7 | Planlagt | Testing av modell som hypotese mot observasjoner |

**Vi er nå i overgangen Fase 1 → Fase 2.**

---

## 6. GJELDENDE ARBEIDSORIGINAL — enok-72-grok (per 2026-06-13)

Codex har ferdigstilt GE-nett som koordinatfundament. Dette er nåværende arbeidsbase:

- **Repo:** `Jone-Aase/enok-72-grok`
- **Branch:** `arbeidsoriginal/ge-nett-0e-2026-06-13`
- **Siste commit:** `f15591c` — "Include equator in GE latitude grid"
- **Lokal kopi:** `C:\Users\a7788\Desktop\enok-72-grok-controlled-base`

### GE-nett status (LÅST — ikke rør)
| Komponent | Status |
|-----------|--------|
| GE-GRID-0A: Meridianer/lengdegrader | Låst |
| GE-GRID-0B: Breddegrad-ringer + polarsirkel | Låst |
| GE-GRID-0C: Lik avstand breddegrad | Låst, smoke-testet |
| GE-GRID-0D: 1 lengdegrad = 1 vinkelgrad | Låst, smoke-testet |
| GE-GRID-0E: Intern posisjonskonvertering | Låst, pass200mm = true |
| Ekvator i breddegradsgrid | Fikset og verifisert |
| Solsirkler låst mot GE-nett | Besluttet |

### Neste trygge fase (i prioritert rekkefølge)
1. Ferdigstille GE-nett lokasjon/navigering
2. **SOL-SIRKLER-1A:** inventar og verifikasjon for solsirkel-punkter/objekter
3. Lage Kartverket-firkantnett basert på spesifikasjon

### Arbeidsgrenser — IKKE endre uten eksplisitt GO fra Jone-Aase
- GE-nett, solsirkler, geometri, anker, transform, aeProject, kartmotor, clean-motor

### Viktige hukommelseskilder i enok-72-grok
- `dokumenter/MEMORY/AGENT-ONBOARDING.md`
- `dokumenter/MEMORY/GE-GRID-MEMORY.md`
- `dokumenter/MEMORY/SMOKE-TEST-STATUS.md`
- `dokumenter/MEMORY/NESTE-STEG.md`
- `dokumenter/MEMORY/AKTIVE-GRENSER.md`
- `dokumenter/SOL-SIRKLER-GE-LAAS.md`

---

## 7. INFRASTRUKTUR OG LENKER

- **GitHub repo:** https://github.com/Jone-Aase/enok-72-truth-instrument
- **Vercel (live, passord `enok364`):** https://enok-72-truth-instrument.vercel.app
- **Backup-URL:** https://jone-aase.github.io/enok-72-truth-instrument/
- **enok-72-grok arbeidsoriginal:** https://github.com/Jone-Aase/enok-72-grok/tree/arbeidsoriginal/ge-nett-0e-2026-06-13

### Git-arbeidsflyt
- `main` — alltid deploy-klar, Vercel deployer automatisk herfra
- Feature-branches navngis: `feature/beskrivelse` eller `fix/beskrivelse`
- Merge via Pull Request, aldri direkte push til main under aktiv utvikling
- Commit-meldinger på norsk eller engelsk, alltid beskrivende

---

## 8. AI-AGENT ROLLER (multi-agent koordinering)

| Agent | Plattform | Rolle |
|-------|-----------|-------|
| Perplexity-agent | perplexity.ai | Arkitekt, koordinator, GitHub-tilgang |
| GPT-5.5 | chatgpt.com | Backup-arkitekt, parallell koordinering |
| Continue/Cline | VS Code lokalt | Kodeeksekutor, lokal filbehandling |
| Codex CLI | VS Code terminal | Lokal filoperasjoner og git-arbeid |
| Grok | grok.com (eksternt) | Excel-analyse, kritisk gjennomgang |
| Gemini | gemini.google.com (eksternt) | Kritiker-rolle |

**Viktig:** Continue og Cline i VS Code er lokale agenter. De har ikke direkte GitHub-tilgang via MCP — bruk `git`-kommandoer i terminalen for commits og push.

**Backup-strategi:** Jone-Aase kjører Perplexity og GPT-5.5 parallelt. AGENTS.md er felles sannhetskilde — ny agent starter alltid med å lese denne filen.

---

## 9. LESEPLAN FOR NY AGENT

Når du starter, les disse filene i rekkefølge:
1. Denne filen (`AGENTS.md`) — FERDIG
2. `AGENT-START-HER.md` — fullstendig prosjekthistorikk
3. `STATUS-NA.md` — siste tekniske status
4. `dokumenter/simulator-master-referanse.md` — hvis du skal gjøre simulator-arbeid
5. For kartmotor-arbeid: les `ARBEIDSORIGINAL.md` i `enok-72-grok` branchen `arbeidsoriginal/ge-nett-0e-2026-06-13`

Si til Jone-Aase: "Jeg har lest AGENTS.md og er klar." Gjengi de 8 master-reglene kort. Spør hva han vil gjøre nå.

---

## 10. HVA DU IKKE SKAL GJØRE

- IKKE analyser Excel-arkene (B, S, S2, Jub, 12Pat, EK_Data, E_Kart) i detalj — det er Fase 4
- IKKE sammenlign med kulemodell eller flat-modell — det er Fase 7
- IKKE bytt geometri, port-system, kalender, projeksjon uten Jone-Aases godkjenning
- IKKE rør GE-nett, solsirkler, anker eller kartmotor uten eksplisitt GO
- IKKE commit til main direkte under aktiv utvikling
- IKKE bruk emojis
- IKKE bruk engelsk i kommunikasjon med Jone-Aase
- IKKE installer npm-pakker eller rammeverk uten godkjenning
- IKKE slett backup-filer (un-map-v16.xx)

---

*Denne filen vedlikeholdes av Perplexity-agenten. Sist oppdatert: 2026-06-13.*
