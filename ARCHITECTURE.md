# ARCHITECTURE.md — BLACK PARIS Studio

## Organisation générale
Le Studio est un **fichier unique** `index.html` (HTML + CSS + JavaScript inline), sans backend.
Il fonctionne dans le navigateur, hors ligne une fois chargé, et se déploie tel quel sur GitHub Pages.

Structure interne du fichier :
1. `<style>` — thème (variables CSS), layout 2 colonnes, styles des cartes et modules.
2. `<body>` — onglets, panneaux de saisie (colonne gauche), cartes de rendu (colonne droite), overlay Reel.
3. `<script>` — logique des modules + initialisation.

## Dépendances externes (CDN)
- `html2canvas` — export des cartes en image.
- `qrcodejs` — génération des QR (avec secours via api.qrserver.com).
- `tesseract.js` — OCR, chargé **à la demande** seulement (pas au démarrage).

## Modules existants
| Module | Onglet | Fonctions clés |
|---|---|---|
| AI Director | 🧠 | `aiSend`, `aiDetect`, `aiAddMsg`, `aiSetTasks` — pilote les autres modules |
| Prédiction | 🎯 | `renderPred`, OCR (`runOCR`, `applyOCR`) |
| Bilan | 📊 | `renderBilan`, `buildRowInputs`, `addRow`, `upRow` |
| Publicité | 📣 | `renderPub`, `applyTpl`, `setFmt`, `genCopy`, `genPrompt`, `clearBg` |
| Thèmes | — | `setTheme` (Luxe / Minimaliste / Futuriste / Sport) |
| Bibliothèque | — | `savePreset`, `loadPreset`, `delPreset`, `listPresets` |
| Sauvegarde auto | — | `saveState`, `restoreState` |
| Export | — | `doCapture` (+ `fallbackDataURL`) |
| QR | — | `makeQR` |
| Mode Reel | — | `openReel`, `playReel`, `recCountdown`, `toggleLoop`, `closeReel`, `fitReel` |

## Stockage (localStorage)
- `bp_state` — état courant (mode, thème, format, champs, lignes bilan) pour la sauvegarde auto.
- `bp_presets` — bibliothèque de préréglages.
- `bp_ai_hist` — historique de conversation de l'AI Director.

## Flux de données
Saisie utilisateur → `render<Module>()` met à jour la carte → `saveState()` persiste.
Bibliothèque : `collectFields()` / `applyFields()` sérialisent tous les champs `.panel input[id]`.

## Points d'extension prévus (non développés)
Architecture pensée pour accueillir plus tard, sans refonte :
- **OCR avancé** — `applyOCR()` centralise l'extraction ; y brancher de meilleures heuristiques ou un modèle.
- **Génération d'images IA** — `genPrompt()` produit déjà les prompts ; prévoir un connecteur qui envoie le prompt à une API et réinjecte l'image via le mécanisme d'image de fond (`pub-bgfile`).
- **Génération de vidéos IA** — le Mode Reel prépare l'animation ; point d'extension pour un export vidéo automatique (ex. ffmpeg.wasm) si un jour nécessaire.
- **Automatisation de campagne** — `aiSend()` route déjà les intentions ; y enchaîner la génération multi-formats + textes.

Chaque futur module IA doit rester **indépendant** et **interchangeable** (changer de fournisseur sans toucher au reste).
