# Grok-svar v16.78 - Hypsometrisk høyde + togglable høydekurver

Mottatt fra Grok 2026-05-31, lagret av Perplexity Agent (Grok rapporterte commit men fila landet ikke i repoet - fjerde gang. Master Rule 7: kun Perplexity committer).

## Plan-godkjenning
v16.78 godkjent. Hypsometrisk høyde + togglable høydekurver vil gjøre Enok 72 til et ekte atlas-verktøy. Bruker ETOPO1 direkte (ingen ny nedlasting), alt toggles i Three.js som separate lag.

## Python-kode for å generere lagene (build_combo_v1k.py)

```python
import numpy as np
from PIL import Image
from skimage.measure import find_contours
import matplotlib.pyplot as plt

# 1. Hypsometrisk høyde-overlay (atlas-stil: grønn-gul-brun-hvit)
def create_hypsometric_overlay(etopo1_np):
    HYPSO_STOPS = [
        (0.0,   (80, 140,  60)),  # lavland / vegetasjon
        (0.25,  (160, 190,  80)), # midt-høyland
        (0.50,  (200, 180, 110)), # høyland / steppe
        (0.75,  (210, 170, 130)), # fjell / ørken
        (1.0,   (245, 248, 255))  # snø / høyfjell
    ]
    lut = create_land_color_lut(HYPSO_STOPS, gamma=0.9)  # gjenbruk fra landfarge

    norm = np.clip(etopo1_np / etopo1_np.max(), 0, 1)
    idx = (norm * (len(lut)-1)).astype(int)
    return lut[idx]

# 2. Høydekurver (100m / 500m / 1000m som separate PNG-overlays)
def generate_contour_overlays(etopo1_np, levels=[100, 500, 1000], thicknesses=[1, 2, 3]):
    overlays = {}
    for level, thick in zip(levels, thicknesses):
        contours = find_contours(etopo1_np, level)
        fig, ax = plt.subplots(figsize=(etopo1_np.shape[1]/100, etopo1_np.shape[0]/100), dpi=100)
        ax.set_axis_off()
        for contour in contours:
            ax.plot(contour[:, 1], contour[:, 0], color='black', linewidth=thick, alpha=0.85)
        fig.tight_layout(pad=0)
        plt.savefig(f'contours_{level}m.png', bbox_inches='tight', pad_inches=0, transparent=True, dpi=100)
        plt.close()
        overlays[level] = f'contours_{level}m.png'
    return overlays

# Eksempelbruk
etopo1 = np.load('ETOPO1_AE.npy')  # din reprojiserte ETOPO1
hypsometric = create_hypsometric_overlay(etopo1)
Image.fromarray(hypsometric).save('hypsometric_overlay.png')

contours = generate_contour_overlays(etopo1)
print("Generert:", list(contours.keys()))
```

## Three.js toggle-lag

```javascript
// Tre nye lag
const layers = {
  standard: scene.getObjectByName('atlasLayer'),        // v16.77
  hypsometric: new THREE.Mesh(geometry, new THREE.MeshBasicMaterial({
    map: new THREE.TextureLoader().load('hypsometric_overlay.png'),
    transparent: true, opacity: 0.75, depthTest: false
  })),
  contours100: new THREE.Mesh(geometry, new THREE.MeshBasicMaterial({
    map: new THREE.TextureLoader().load('contours_100m.png'),
    transparent: true, opacity: 1.0, depthTest: false
  })),
  contours500: new THREE.Mesh(geometry, new THREE.MeshBasicMaterial({
    map: new THREE.TextureLoader().load('contours_500m.png'),
    transparent: true, opacity: 1.0, depthTest: false
  })),
  contours1000: new THREE.Mesh(geometry, new THREE.MeshBasicMaterial({
    map: new THREE.TextureLoader().load('contours_1000m.png'),
    transparent: true, opacity: 1.0, depthTest: false
  }))
};

// Toggle-knapper (HTML eller dat.GUI)
function toggleLayer(name) {
  layers[name].visible = !layers[name].visible;
}

// Stack alle lagene - brukeren kan velge kombinasjon
```

## Groks anbefalinger
- Hypsometrisk: bruk ATLAS_STOPS fra tidligere for ekstra metning.
- Konturer: 100m (tynn), 500m (medium), 1000m (tykk) - perfekt for zoom.
- Performance: generer kontur-PNG-er én gang på desktop, last inn som textures i Three.js (lett på mobil).
- Deploy-melding: samle v16.75-v16.77 som milepæl og push til Vercel + pplx.app nå - v16.78 kan komme som neste oppdatering.
