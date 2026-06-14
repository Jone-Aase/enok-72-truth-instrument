# AGENTS.md — Enok 72 Truth Instrument
# For bruk av lokale AI-agenter i VS Code (Continue, Cline, GitHub Copilot)
# Sist oppdatert: 2026-06-14 av Perplexity + ChatGPT

---

## VIKTIG: Denne filen overstyrer
Ved konflikt etter 2026-06-13 overstyrer denne `AGENTS.md` eldre `STATUS-NA.md` og `AGENT-START-HER.md`, med mindre Jone-Aase eksplisitt sier noe annet.

---

## 0. HVEM DU ER OG HVEM SOM LEDER

Du er en lokal AI-kodingsagent (Continue, Grok Build eller Codex) som kjører i VS Code på Jone-Aases PC i Oslo.

**Prosjektleder:** Jone-Aase  
**Koordinatorer:** Perplexity-agenten og GPT-5.5 (parallelle backup-koordinatorer)  
**Din rolle:** Lokal kodeeksekutor — du implementerer eksakte instrukser fra koordinatorene eller Jone-Aase

Jone-Aase er alltid øverste beslutningstaker. Ingen agent velger selv retning.

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

## 2. VIKTIG REPO-SKILLE

| Repo | Rolle |
|------|-------|
| `enok-72-truth-instrument` | Hovedsimulator og deploy-repo (Vercel). IKKE aktiv kartmotor-utvikling. |
| `enok-72-grok` | Aktiv kartmotor og GE-nett arbeidsoriginal. All kartmotor-utvikling skjer her. |

Forveksl ikke disse to. Kodeendringer i kartmotoren gjøres i `enok-72-grok`, ikke her.

---

## 3. KATASTROFE-GJENOPPRETTING

Hvis alt chatminne forsvinner, er dette minimumsprosedyren.

Aktiv arbeidsoriginal for kartmotor/GE-nett er **ikke** `main` i dette repoet. Aktiv arbeidsoriginal ligger i:

- **Repo:** `Jone-Aase/enok-72-grok`
- **Branch:** `arbeidsoriginal/ge-nett-0e-2026-06-13`
- **Full HEAD:** `f15591cf07bbdf2194d7d09c8e75c2668dc0d8fd`
- **Kort commit:** `f15591c`
- **Commit-melding:** `Include equator in GE latitude grid`

### Commit-kjede
- `3e87f51` — `Record solar circle GE lock`
- `f18197e` — `Marker gjeldende arbeidsoriginal`
- `f15591c` — `Include equator in GE latitude grid`

### Gjenopprettingskommandoer
```bash
cd C:\Users\a7788\Desktop
git clone https://github.com/Jone-Aase/enok-72-grok.git enok-72-grok-controlled-base
cd enok-72-grok-controlled-base
git checkout arbeidsoriginal/ge-nett-0e-2026-06-13
git status
git rev-parse HEAD
```
Forventet HEAD: `f15591cf07bbdf2194d7d09c8e75c2668dc0d8fd`

### Første 5 minutter for ny agent
1. Les `AGENTS.md`
2. Bekreft repo og branch
3. Kjør `git status`
4. Kjør `git rev-parse HEAD`
5. Ikke endre filer
6. Rapporter til Jone-Aase før arbeid starter

---

## 4. KOMPLETT WORKFLOW

```
STEG 1 — PLAN
  Jone-Aase + GPT-5.5 + Perplexity
  Lager eksakt kode-instruks til Grok Build
  Godkjennes av Jone-Aase før Grok starter

STEG 2 — UTFØR
  Grok Build (penn)
  Utfører eksakt instruks — maks 1-3 filer
  Stopper etter: git status --short / git diff --stat / git diff
  Rapporterer til Jone-Aase

STEG 3 — VURDER
  GPT-5.5 og/eller Perplexity
  Vurderer Grok sin rapport mot AGENTS.md
  Gir GO eller stopp

STEG 4 — RELEASE-GATE
  Codex (kontrollør)
  Verifiserer at kun avtalte filer er endret
  Kjører node --check app.js
  Bekrefter at lokal kopi = GitHub
  Pusher kun etter eksplisitt GO fra Jone-Aase
  Oppretter IKKE PR eller merger uten GO

STEG 5 — MERGE
  Perplexity eller GPT-5.5
  Oppretter PR og merger ved Jone-Aases GO
  Oppdaterer AGENTS.md med ny SHA
```

**Grok har pennen. Claude er reservepenn. Codex er kontrollør. Ingen velger selv retning.**

---

## 5. AGENT-ROLLER OG KAPABILITETER

### Fullstendig rolleoversikt

| Agent | Plattform | GitHub-tilgang | Lokal VS Code | Rolle |
|-------|-----------|---------------|---------------|-------|
| **Jone-Aase** | PC + alle | Full | Full | Beslutningstaker — endelig GO |
| **Perplexity** | perplexity.ai | Ja — MCP | Nei | Koordinator, GitHub-operatør, Vercel |
| **GPT-5.5** | chatgpt.com | Ja — connector | Nei | Parallell koordinator, kontrolltårn |
| **Grok Build** | VS Code lokalt | Nei | Ja | **Primær kodeagent (penn)** |
| **Claude Sonnet 4.5** | VS Code lokalt | Nei | Ja | **Reservepenn — hvile til GO** |
| **Codex CLI** | VS Code terminal | Nei | Ja | **Release-gate og kontrollør** |

### Tre-modus-regel (alle lokale agenter)

**LES-MODUS** — lese og forklare. Ingen filendring.

**PLAN-MODUS** — lage plan eller markdown. Maks 1 fil. Ingen kodeendring.

**SKRIVE-MODUS** — kun én agent om gangen. Maks 1–3 filer. Stopp etter `git diff`. Ingen push uten GO.

### Standard git-kontroll før og etter hvert oppdrag
```bash
# FØR
git status --short
git branch --show-current
git rev-parse --short HEAD

# ETTER
git status --short
git diff --stat
git diff
```
Hvis `git diff --stat` viser en fil som ikke var avtalt — stopp og rapporter til Jone-Aase.

---

## 6. GROK BUILD — PRIMÆR KODEAGENT

Grok Build er primær lokal kodeagent. Den får eksakte instrukser og utfører dem.

**Grok skal aldri:**
- Velge neste steg selv
- Refaktorere fritt
- Endre filer utenfor oppdraget
- Committe eller pushe
- Merge

**Standard åpningsprompt til Grok Build:**
```
Les AGENTS.md først.

Du er primær kodeagent i Enok 72-prosjektet.

Regler:
- Norsk
- Ingen emojis
- Kun SKRIVE-MODUS ved eksplisitt ordre
- Maks 1-3 filer per oppdrag
- Stopp etter git diff og rapporter
- Ikke commit, ikke push, ikke merge
- Ikke rør geometri, anker, transform, aeProject, kartmotor eller clean-motor uten GO

Første svar: bekreft repo, branch og HEAD.
```

---

## 7. CLAUDE SONNET 4.5 — RESERVEPENN (HVILEMODUS)

Claude Sonnet 4.5 er **ikke** primær kodeagent. Den ligger i hvile og overtar Grok sin rolle kun ved eksplisitt ordre fra Jone-Aase: **"Claude overtar Grok-rollen."**

**I hvilemodus skal Claude:**
- Ikke gjøre kodeendringer
- Ikke lese hele repoet fritt
- Ikke bruke mange tokens
- Vente på eksakt oppdrag

**Hvis Claude overtar Grok-rollen:**
- Endre kun filene oppdraget nevner
- Maks 1–3 filer
- Ingen ekstra forbedringer
- Stopp etter: `git status --short` / `git diff --stat` / `git diff`

**Rapportformat for Claude:**
1. Branch
2. HEAD
3. Endrede filer
4. Hva du endret
5. Hva du ikke rørte
6. Eventuelle uklarheter
7. Om oppdraget er ferdig eller trenger review

**Standard åpningsprompt til Claude Sonnet 4.5:**
```
Les AGENTS.md først.

Du er IKKE primær kodeagent akkurat nå.
Primær lokal kodeagent er Grok Build.

Din rolle er backup-reservepenn.
Ligg i hvile. Ikke endre filer.
Ikke endre filer uten eksplisitt SKRIVE-MODUS og ordre:
"Claude overtar Grok-rollen."

Bekreft at du har lest AGENTS.md og er i hvilemodus.
```

**Statusoppdateringsmal til Claude ved ny arbeidsoriginal:**
```
STATUSOPPDATERING TIL CLAUDE

Gjeldende arbeidsoriginal:
Repo: Jone-Aase/enok-72-grok
Branch: arbeidsoriginal/ge-nett-0e-2026-06-13
HEAD: <ny full SHA>
Kort HEAD: <kort SHA>
Commit: <commit-melding>

Din rolle er fortsatt:
Backup for Grok Build.
Ikke skriv filer før eksplisitt ordre.
Ikke commit. Ikke push.
Stopp etter git diff hvis du får skriveoppdrag.
```

---

## 8. CODEX — RELEASE-GATE OG KONTROLLØR

Codex kontrollerer arbeid gjort av Grok Build og pusher kun etter eksplisitt GO.

**Codex sin faste rolle:**
```
Du er kvalitetskontrollør og git-operatør i Enok 72-prosjektet.

Din rolle:
- Les og kontroller arbeid gjort av Grok Build
- Verifiser at kun avtalte filer er endret (git diff --stat)
- Kjør node --check app.js
- Bekreft at lokal arbeidskopi og GitHub er identiske
- Push og rapporter commit-SHA ved eksplisitt GO
- Opprett IKKE PR eller merge uten GO fra Jone-Aase

Du skriver ikke ny kode. Du kontrollerer og overferer.

Norsk. Ingen emojis. Stopp og rapporter ved avvik.
```

---

## 9. PROSJEKTOVERSIKT

### Hva dette er
Enok 72 Truth Instrument er et interaktivt forskningsverktøy basert på Enoks bok kapittel 72 og den 364-dagers solkalenderen.

### Tilknyttede repos
| Repo | Formål |
|------|--------|
| `enok-72-truth-instrument` | Hoved-simulator, Vercel-deployed |
| `enok-atlas-flat` | Flatt verdenskart (Equal Earth + Equirectangular) |
| `enok-72-norge` | Kartverket WMTS + norske byer (SSR) |
| `enok-72-grok` | Aktiv kartmotor/GE-nett (arbeidsoriginal) |
| `Tidslinjen-versjon-12` | AM-kronologi (Jubileumsboken, kanoniske tekster) |
| `enok-orakel-simulator` | Tidlig orakel-simulator (HTML) |

---

## 10. TEKNISK ARKITEKTUR

### Teknologistack
- **Språk:** Vanilla JavaScript (ES6+), HTML5, CSS3
- **Kartbibliotek:** Leaflet.js
- **Data-format:** JSON (calendar.json, sol-bane-arkT.json, timeline.json, enok72-vers.json)
- **Deployment:** Vercel (automatisk fra `main`-branch på GitHub)
- **Passord-port:** JavaScript sessionStorage, passord `enok364`, `noindex` aktivt

### Kritiske filer — IKKE rør uten eksplisitt tillatelse
- `app.js` — hoved-applikasjonslogikk (211 KB)
- `index.html` — hoved-HTML (101 KB)
- `calendar.json` — 364-dagers kalenderdata (kanonisk)
- `sol-bane-arkT.json` — solbane-data fra Ark T
- `un-map.png` / `un-map.webp` — UN-kartet (IKKE overskriv)
- `vercel.json` — deployment-konfigurasjon
- Backup-filer `un-map-v16.65` til `un-map-v16.76` — ikke slett

---

## 11. KODESTIL OG PREFERANSER

- **Kommentarer:** Norsk der naturlig, engelsk i tekniske funksjoner
- **Variabelnavn:** camelCase
- **Innrykk:** 2 mellomrom
- **Ingen rammeverk:** Vanilla JS — ikke foreslå React/Vue/etc.
- **Ingen npm-pakker** uten Jone-Aases godkjenning
- **Feilhåndtering:** Alltid `try/catch` rundt kart-operasjoner og JSON-parsing

---

## 12. FASEPLAN

| Fase | Status | Beskrivelse |
|------|--------|-------------|
| Fase 1 | FERDIG | Kildemateriale + vers-uttrekk |
| Fase 2 | Neste | Strukturert vers-uttrekk, indre konsistens-sjekk |
| Fase 3 | Planlagt | Modellbygging |
| Fase 4 | Planlagt | Excel-integrasjon |
| Fase 5 | Planlagt | Verifisering vers for vers |
| Fase 6 | Planlagt | Team-konsultasjon |
| Fase 7 | Planlagt | Testing mot observasjoner |

**Vi er nå i overgangen Fase 1 → Fase 2.**

---

## 13. GJELDENDE GE-NETT STATUS (LÅST)

| Komponent | Status |
|-----------|--------|
| GE-GRID-0A til 0E | Låst og smoke-testet |
| Ekvator i breddegradsgrid | Fikset og verifisert |
| Solsirkler låst mot GE-nett | Besluttet |

**Neste trygge fase:**
1. Ferdigstille GE-nett lokasjon/navigering
2. SOL-SIRKLER-1A: inventar og verifikasjon
3. Kartverket-firkantnett

**Første handling etter ny agentstart: plan/inventar, ikke motorendring.**

### Arbeidsgrenser — IKKE endre uten GO
- GE-nett, solsirkler, geometri, anker, transform, aeProject, kartmotor, clean-motor

### Hukommelseskilder i enok-72-grok
- `dokumenter/MEMORY/AGENT-ONBOARDING.md`
- `dokumenter/MEMORY/GE-GRID-MEMORY.md`
- `dokumenter/MEMORY/SMOKE-TEST-STATUS.md`
- `dokumenter/MEMORY/NESTE-STEG.md`
- `dokumenter/MEMORY/AKTIVE-GRENSER.md`
- `dokumenter/SOL-SIRKLER-GE-LAAS.md`

---

## 14. AI-KOST OG AGENTBRUK

- **Grok Build** — billig arbeidshest, primær kodeagent
- **Claude Sonnet 4.5** — sterk reviewer, reservepenn i hvile
- **Codex** — spesialoperatør, release-gate

Arbeidsmåte:
- Små oppdrag, maks 1–3 filer
- Ingen brede refaktoreringer
- Ingen commit/push uten GO
- Stopp etter `git diff` og rapporter

---

## 15. SANNHETSLAGER (prioritert rekkefølge)

1. GitHub commits og markdown-filer i repo
2. `AGENTS.md` (denne filen)
3. `ARBEIDSORIGINAL.md` i aktiv branch
4. `dokumenter/MEMORY/*`
5. Chatdialoger — kun støtte, ikke sannhetslager

---

## 16. INFRASTRUKTUR OG LENKER

- **GitHub:** https://github.com/Jone-Aase/enok-72-truth-instrument
- **Vercel (passord `enok364`):** https://enok-72-truth-instrument.vercel.app
- **enok-72-grok arbeidsoriginal:** https://github.com/Jone-Aase/enok-72-grok/tree/arbeidsoriginal/ge-nett-0e-2026-06-13

### Git-arbeidsflyt
- `main` — alltid deploy-klar
- Feature-branches: `feature/beskrivelse` eller `fix/beskrivelse`
- Merge via PR, aldri direkte push til main

---

## 17. LESEPLAN FOR NY AGENT

1. Denne filen (`AGENTS.md`) — FERDIG
2. `AGENT-START-HER.md` — historikk (AGENTS.md overstyrer ved konflikt etter 2026-06-13)
3. `STATUS-NA.md` — teknisk status (AGENTS.md overstyrer ved konflikt etter 2026-06-13)
4. For kartmotor: `ARBEIDSORIGINAL.md` i `enok-72-grok` branch `arbeidsoriginal/ge-nett-0e-2026-06-13`
5. `dokumenter/MEMORY/*`

Si til Jone-Aase: "Jeg har lest AGENTS.md og er klar." Gjengi de 8 master-reglene. Spør hva han vil gjøre nå.

---

## 18. HVA DU IKKE SKAL GJØRE

- IKKE analyser Excel-arkene i detalj — Fase 4
- IKKE sammenlign med kulemodell/flat-modell — Fase 7
- IKKE rør GE-nett, solsirkler, anker, geometri, kartmotor uten GO
- IKKE commit til main direkte
- IKKE bruk emojis
- IKKE bruk engelsk til Jone-Aase
- IKKE installer npm-pakker uten godkjenning
- IKKE slett backup-filer
- IKKE start motorendring før plan er godkjent
- IKKE les hele repoet fritt
- IKKE både skriv, push og merge uten at Jone-Aase godkjenner hvert steg

---

## 19. SKY-WORKFLOW — BEKREFTET 2026-06-14

Bekreftet via Vercel preview smoke-test (enok-72-grok PR #4, 2026-06-14).

### Ny hovedworkflow
GitHub feature-branch → Vercel preview → diff-review → Jone GO → merge.

### Steg

1. Plan: Jone + ChatGPT + Perplexity
2. Koding: Perplexity/Grok på GitHub feature-branch. Kun én agent skriver.
3. Preview: Vercel preview-URL genereres automatisk fra feature-branch.
4. Review: ChatGPT + Perplexity. Gemini/Codex som ekstra kontroll ved behov.
5. GO: Jone-Aase
6. Merge: Etter eksplisitt GO
7. Lokal VS Code / Live Server: Kun reserve, nødkontroll og debug.

### Codex
- Codex sky = foretrukket release-gate når tilgjengelig.
- Codex CLI lokalt = reserve/nødkontroll.

### Lovable
- Lovable = backup-demo / UI-prototype.
- Lovable får aldri definere fasit.
- Lovable er ikke release-gate.
- Lovable er ikke standard kodeagent på arbeidsoriginal før separat test
  viser trygg GitHub-branch-flyt.

### Skriverregel
- Kun én agent skriver.
- Flere kan reviewe.
- Jone-Aase gir endelig GO.

### PR #4
- Er kun Vercel smoke-test på enok-72-grok.
- Skal ikke merges inn i arbeidsoriginal.

*Oppdatert: 2026-06-14 av Perplexity + ChatGPT.*

---

*Denne filen vedlikeholdes av Perplexity-agenten i samarbeid med GPT-5.5. Sist oppdatert: 2026-06-14.*
