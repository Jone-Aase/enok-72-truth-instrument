# DECISIONS.md — Beslutningslogg

Hver beslutning logges med dato, hva, hvorfor og konsekvens. Eldste først.

---

## 2026-05-26 — Buestreng-uretting implementert (v16)

**Beslutning:** Erstatt v15-formel `R_EQUATOR * (90 - lat) / 90` med `R_OUTER * (90 - lat) / 180`.

**Begrunnelse:** Hele 180° breddegrad skal strekkes til R_OUTER, slik at sør-halvkulen får riktig posisjon i AE-projeksjonen. r(90) = 0, r(0) = 15 710 km, r(−90) = 31 421 km.

**Konsekvens:** UN_MAP_RADIUS justert til `R_OUTER * 150/180 = 26.184`. Alle posisjoner langs buestrengen omberegnet. v16.30 deployet 26. mai 2026.

---

## 2026-05-27 — Masterfil styrer simulatorarbeid

**Beslutning:** `simulator-master-referanse.md` er øverste sannhetskilde for simulatoren. Ved konflikt med agent-minne, gjelder masterfilen.

**Begrunnelse:** Agenter resettes. Dialoghukommelse er ikke pålitelig over tid. Repo-filer må styre kontinuitet.

**Konsekvens:** Ingen AI-agent skal endre geometri, portsystem eller kalender uten først å sjekke masterfilen og få eksplisitt godkjenning fra Jone-Aase.

---

## 2026-05-27 — Komplett arkiv pushet til GitHub

**Beslutning:** Speile hele workspace-rota til `arkiv/`-mappe i repoet (358 filer, ~81 MB).

**Begrunnelse:** Workspace-sandkassen kan resirkuleres. Materialet må eksistere utenfor sandkassen for å overleve.

**Konsekvens:** Tre lag av redundans: workspace-sandkasse, GitHub `arkiv/`, og zip-fil delt med Jone-Aase. Commit b21fd41.

---

## 2026-05-27 — Låst arbeidsmodell etablert

**Beslutning:** Fire roller med klar ansvarsdeling:

- Beslutningstaker: Jone-Aase
- Minne-/utviklerlag: Grok
- Utfører-/deploylag: Perplexity-agent
- Kvalitetskontroll: ChatGPT

**Begrunnelse:** Perplexity-agenten mister hukommelse mellom sesjoner. Grok beholder kontinuitet over dager. Ved å gjøre Grok til minne-bæreren av utviklingsdialogen, blir Perplexity-agentens resett ikke lenger katastrofalt — utfører-laget kan rekonstruere kontekst fra repo-filer.

**Konsekvens:** STATUS-NA.md og DECISIONS.md må alltid være fersk. Grok-dialog arkiveres i `grok-dialog/`. Versjoner i `grok-versjoner/`.

---

## 2026-05-27 — Grok-pipeline mot v17 etablert

**Beslutning:** Hver Grok-endring lages som lokal zip, mottas av Perplexity-agenten, deployes til separat live-URL, og pushes til egen branch. Først når flere endringer er testet og godkjent, samles de til en final v17.

**Begrunnelse:** Inkrementell utvikling med isolert testing. Hver endring kan rulles tilbake uten å påvirke hovedinstrumentet.

**Konsekvens:** Branch `grok-v17-kandidater` etableres. Hovedinstrumentet (main) endres ikke før Jone-Aase godkjenner samlet v17.

---

## 2026-05-27 — Månen holdes utenfor solinstrumentet

**Beslutning:** Ingen måne-implementasjon i Enok 72 Truth Instrument inntil solmodellen er stabil og verifisert.

**Begrunnelse:** Månesystemet i Enok er komplekst (vers 73-82) og må få eget instrument. Sammenblanding ville forurense sol-verifikasjonen.

**Konsekvens:** Månen er senere arbeid. Solmodellen prioriteres.
