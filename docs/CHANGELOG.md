# CHANGELOG.md

## v16.30 — 26. mai 2026

- Buestreng-uretting implementert (`latToR(lat) = R_OUTER * (90 - lat) / 180`)
- UN_MAP_RADIUS justert til `R_OUTER * 150/180`
- Posisjoner langs buestrengen omberegnet (polar 4089, krepsen 11608, ekvator 15710, steinbukken 19812, antarktis 31421)
- Sol-bane lest fra `sol-bane-arkT.json` (ark T rad 26-227)
- 4 ekstrarunder integrert (dag 91, 182, 273, 364)
- 23,7° vendekrets-mestermal låst fra Ark T H212

## v17 — under planlegging

Grok-pipeline etablert 27. mai 2026. Kandidat-endringer kommer som zip-filer fra Grok, deployes til separat live-URL, mergres bare ved godkjenning.

Foreslåtte kandidater (ikke startet):

1. Bedre glød + puls på de 4 ekstrarundene (dag 91, 182, 273, 364)
2. Eksporter dagens solbane som CSV
3. Sammenligningsknapp mot ekte soldeklinasjon
4. Touch-støtte + bedre mobilvisning
5. Ytelsesforbedring på de 192 banene (InstancedMesh)
