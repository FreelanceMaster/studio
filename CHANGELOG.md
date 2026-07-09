# CHANGELOG — BLACK PARIS Studio

## V1 — Générateur de base
**Ajouté**
- Générateur de carte « Prédiction du jour » (équipes, %, cotes, stats).
- Générateur « Bilan du jour » (liste de matchs, ✅/❌, taux).
- Identité visuelle BLACK PARIS (noir/or, bandeaux, badge taux de réussite).
- Export image via html2canvas.
- QR code sur les cartes (avec secours image).

## V2 — Studio créatif
**Ajouté**
- Mise en page 2 colonnes sur ordinateur (grille de saisie + aperçu), empilée sur mobile.
- 4 variantes de thème : Luxe, Minimaliste, Futuriste, Sport.
- Module Screenshot → remplissage auto (OCR Tesseract, chargé à la demande).
- Bibliothèque de préréglages (sauvegarde, recherche, chargement, suppression).
- Sauvegarde automatique de l'état (localStorage).
- Module Publicité : 6 modèles marketing, 3 formats (9:16 / 1:1 / 16:9), fond image importable, générateur de textes multi-plateformes, générateur de prompts IA.
- AI Director : pilotage des modules en langage naturel, historique, suggestions, tableau des tâches.
- Mode Reel : animation plein écran de la carte pour enregistrement vidéo.

## V3 — Stabilisation & robustesse
**Corrigé (Sprint 3 / 3A)**
- Export : gestion d'erreur visible, feedback bouton, ajout du format JPG, méthode Blob compatible iPhone/Android + secours nouvel onglet.
- Bibliothèque : ligne entière cliquable pour charger un préréglage (avant, seule l'icône réagissait).
- OCR accessible depuis l'AI Director (bascule vers la zone de dépôt).
- Chargement des préréglages : restauration du mode Publicité et du format d'image.
- Bug d'initialisation : variable `FMT` hissée en tête (évite un blocage possible au démarrage).
- Mode Reel : carte mise à l'échelle pour tenir en entier à l'écran, boutons masquables pendant l'enregistrement, bouton Boucle.

**Amélioré (Sprint 3B)**
- `listPresets` : construction du HTML en une seule passe (performances).
- Helper `v(id)` sécurisé contre les champs absents (évite les crashs).
- Documentation ajoutée : PROJECT_RULES.md, ARCHITECTURE.md, CHANGELOG.md.

**Non modifié volontairement**
- Aucune nouvelle fonctionnalité visible ajoutée en V3 (sprints de stabilisation).
- Interface, design et architecture inchangés.
