# PROJECT_RULES.md — BLACK PARIS Studio

Règles de développement à suivre pour **tous les futurs sprints**.

## 1. Règle d'or
La **stabilité** prime sur les nouvelles fonctionnalités. Ne jamais casser ce qui marche.
Si une modification n'est pas sûre à 100 %, ne pas la faire.

## 2. Composants critiques — NE JAMAIS CASSER
Ces fonctions sont le cœur du Studio. Toute modification doit être testée avant livraison :

- `doCapture(kind)` — export PNG/JPG (méthode Blob + secours nouvel onglet). **Point le plus sensible.**
- `switchMode(m)` — navigation entre AI Director / Prédiction / Bilan / Pub.
- `renderPred()`, `renderBilan()`, `renderPub()` — rendu des 3 cartes.
- `saveState()` / `restoreState()` — sauvegarde auto (localStorage `bp_state`).
- `savePreset()` / `loadPreset()` / `listPresets()` — bibliothèque (localStorage `bp_presets`).
- `makeQR()` — QR code (librairie + secours image API).

## 3. Variables globales
Déclarées **en haut du script**, jamais ailleurs (éviter la zone morte temporelle du `let`) :
`MODE`, `THEME`, `FMT`, `rows`, `aiHistory`, `reelLoop`, `reelTimer`.

## 4. Conventions de nommage
- IDs des champs de saisie : `p-*` (prédiction), `b-*` (bilan), `pub-*` (publicité).
- IDs des éléments affichés dans les cartes : `o-*` (prédiction), `ob-*` (bilan), `op-*` (publicité).
- Fonctions de rendu : `render<Module>()`.
- Fonctions de l'AI Director : préfixe `ai*`.
- Fonctions du Mode Reel : suffixe/préfixe `reel` / `*Reel`.

## 5. Bonnes pratiques
- Toujours passer par le helper `v(id)` pour lire un champ (sécurisé contre l'absence d'élément).
- Tout accès à `localStorage` doit être entouré d'un `try/catch`.
- Modifier `.value` en JS ne déclenche pas les `oninput` → toujours rappeler le `render` concerné ensuite.
- Ne pas utiliser `innerHTML +=` dans une boucle (perf) → construire puis assigner en une passe.
- Emojis drapeaux et fond image = points fragiles pour l'export ; toujours garder le secours.

## 6. Limites connues (à ne pas « corriger » à tort)
- L'export, l'OCR, le QR et le Mode Reel **ne fonctionnent que dans le vrai fichier** ouvert dans un navigateur, jamais dans un aperçu en bac à sable.
- L'OCR (Tesseract) est imparfait sur des visuels très stylisés : résultat « à corriger », pas magique.
- Le Studio ne peut pas enregistrer l'écran lui-même (restriction navigateur, surtout iOS) : le Mode Reel prépare l'animation, l'enregistrement se fait via l'outil natif du téléphone.

## 7. Procédure de test avant chaque livraison
Voir CHANGELOG.md pour l'historique ; vérifier systématiquement : structure des balises, aucune fonction dupliquée, aucun handler sans fonction, aucun ID référencé manquant, et test manuel de l'export dans un vrai navigateur.
