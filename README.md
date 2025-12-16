# 🔐 Cadenas - Collection de Mini-Jeux de Déverrouillage

Une collection de 4 mini-jeux interactifs de type "escape game" où chaque puzzle déverrouillé révèle un indice pour le suivant.

## 🎮 Les Jeux

### 1. 🔓 Cryptex (Snapchat)
**Type:** Puzzle à cadran rotatif
**Solution:** `CYBER`
**Mécanisme:** Tournez les roues avec les flèches ou en glissant pour aligner les lettres

### 2. 🎨 Couleurs (Identifiant Snapchat)
**Type:** Séquence de couleurs
**Solution:** Bleu → Jaune → Vert → Rouge
**Mécanisme:** Cliquez sur les couleurs dans le bon ordre

### 3. 🔢 Clavnum (Code de déverrouillage)
**Type:** Clavier numérique
**Solution:** `0809`
**Mécanisme:** Entrez le code avec les touches numériques (clavier physique supporté)

### 4. 🎹 Piano (Identifiant WhatsApp)
**Type:** Mélodie musicale
**Solution:** Do - Do - Do - Ré - Mi - Ré - Do - Mi - Ré - Ré - Do
**Mécanisme:** Jouez "Au clair de la lune" sur le piano

## 🔄 Chaîne des Indices

Chaque jeu révèle un indice pour le suivant:

```
Cryptex (CYBER)
    ↓ [indice audio]
Couleurs (Bleu-Jaune-Vert-Rouge)
    ↓ "Mon identifiant snapchat est ma date de naissance + 3 jours"
Clavnum (0809)
    ↓ "Jouez 'Au clair de la lune' sur le piano..."
Piano (Do-Do-Do-Ré-Mi-Ré-Do-Mi-Ré-Ré-Do)
    ↓ "Mon code WhatsApp est 3080"
FIN 🎉
```

## 🚀 Utilisation

### Jouer aux jeux

Ouvrez simplement les fichiers HTML dans votre navigateur:

```bash
# Ouvrir dans le navigateur par défaut (Linux)
xdg-open cryptex/index.html
xdg-open couleurs/index.html
xdg-open clavnum/index.html
xdg-open piano/index.html

# Ou double-cliquez sur les fichiers index.html
```

**Aucune installation requise!** Les jeux fonctionnent entièrement côté client.

## ⚙️ Personnalisation Rapide

Tous les jeux utilisent une configuration centralisée pour faciliter la personnalisation.

### Changer le Titre d'un Jeu

Dans chaque `index.html`, modifiez le `CONFIG` en haut du fichier:

```javascript
const CONFIG = {
    gameTitle: 'Votre Titre',  // ← Changez ici
    // ... autres paramètres
};
```

### Changer la Solution

```javascript
// Cryptex
password: 'CYBER',

// Couleurs
correctSequence: ['Bleu', 'Jaune', 'Vert', 'Rouge'],

// Clavnum
correctCode: '0809',

// Piano
correctMelody: ['Do', 'Do', 'Do', 'Ré', 'Mi', 'Ré', 'Do', 'Mi', 'Ré', 'Ré', 'Do'],
```

### Changer les Indices/Récompenses

Chaque jeu a un fichier `modal.html` qui affiche le contenu de réussite. Éditez-le pour changer les indices:

**Texte simple:**
```html
<p>Votre indice ici...</p>
```

**Image:**
```html
<img src="indice.jpg" alt="Indice" style="max-width: 100%; border-radius: 10px;">
```

**Audio:**
```html
<audio controls style="width: 100%;">
    <source src="indice.mp3" type="audio/mpeg">
</audio>
```

**Vidéo:**
```html
<video controls style="max-width: 100%; border-radius: 10px;">
    <source src="indice.mp4" type="video/mp4">
</video>
```

**YouTube:**
```html
<iframe width="100%" height="315"
    src="https://www.youtube.com/embed/VIDEO_ID"
    frameborder="0" allowfullscreen>
</iframe>
```

## 📁 Structure du Projet

```
cadenas/
├── README.md           # Ce fichier
├── CLAUDE.md          # Documentation pour développement avec Claude Code
│
├── cryptex/           # Jeu 1: Cryptex
│   ├── index.html     # Jeu complet (HTML+CSS+JS)
│   └── modal.html     # Contenu de réussite/indices
│
├── couleurs/          # Jeu 2: Séquence de couleurs
│   ├── index.html
│   └── modal.html
│
├── clavnum/           # Jeu 3: Clavier numérique
│   ├── index.html
│   └── modal.html
│
└── piano/             # Jeu 4: Piano musical
    ├── index.html
    ├── modal.html
    └── sounds/        # Sons du piano
```

## 🎨 Caractéristiques

### Design
- ✨ Interface sombre moderne avec effets de glow cyan
- 🎭 Animations fluides et feedback visuel
- 📱 Responsive (fonctionne sur mobile et desktop)
- 🎯 Style cohérent entre tous les jeux

### Techniques
- 🚫 Aucune dépendance externe
- 💯 Vanilla JavaScript pur
- 📦 Fichiers auto-contenus
- ⚡ Pas de build process nécessaire
- 🔒 Fonctionne entièrement offline

### Fonctionnalités
- ⌨️ Support clavier physique (clavnum, piano)
- 🎵 Audio intégré (piano avec sons réels)
- 📊 Configuration centralisée
- 🎁 Système de modales pour récompenses/indices
- 🔄 Support pour médias externes (audio, vidéo, images)

## 🛠️ Configuration Avancée

### Paramètres Disponibles par Jeu

#### Cryptex
```javascript
const CONFIG = {
    gameTitle: 'Snapchat',
    password: 'CYBER',
    modalTitle: '🎉 DÉVERROUILLÉ ! 🎉',
    modalContentFile: 'modal.html',
    dragSensitivity: 1.5  // Sensibilité du glisser
};
```

#### Couleurs
```javascript
const CONFIG = {
    gameTitle: 'Identifiant Snapchat',
    correctSequence: ['Bleu', 'Jaune', 'Vert', 'Rouge'],
    modalTitle: '🎉 DÉVERROUILLÉ ! 🎉',
    modalContentFile: 'modal.html'
};
```

#### Clavnum
```javascript
const CONFIG = {
    gameTitle: 'Code de déverrouillage :',
    correctCode: '0809',
    maxLength: 6,          // Longueur max du code
    hideCode: false,       // true = afficher des •
    modalTitle: '🎉 DÉVERROUILLÉ ! 🎉',
    modalContentFile: 'modal.html'
};
```

#### Piano
```javascript
const CONFIG = {
    gameTitle: 'Identifiant WhatsApp',
    correctMelody: ['Do', 'Do', 'Do', 'Ré', 'Mi', 'Ré', 'Do', 'Mi', 'Ré', 'Ré', 'Do'],
    modalTitle: '🎉 BRAVO ! 🎉',
    modalContentFile: 'modal.html',
    showHint: false,       // true = afficher la solution
    soundEnabled: true     // false = désactiver les sons
};
```

## 📝 Référence Rapide

| Jeu | Fichier Config | Fichier Modal | Ligne Config | Titre par Défaut |
|-----|---------------|---------------|--------------|------------------|
| **Cryptex** | `cryptex/index.html` | `cryptex/modal.html` | ~293 | Snapchat |
| **Couleurs** | `couleurs/index.html` | `couleurs/modal.html` | ~354 | Identifiant Snapchat |
| **Clavnum** | `clavnum/index.html` | `clavnum/modal.html` | ~351 | Code de déverrouillage : |
| **Piano** | `piano/index.html` | `piano/modal.html` | ~411 | Identifiant WhatsApp |

## 🎯 Cas d'Usage

- **Escape Game physique:** Imprimez les indices et intégrez les mini-jeux
- **Animation d'événement:** Personnalisez les titres et indices pour votre thème
- **Chasse au trésor:** Créez une chaîne d'énigmes personnalisée
- **Éducation:** Adaptez les solutions pour enseigner des concepts
- **Team Building:** Travail d'équipe pour résoudre les puzzles

## 🔧 Développement

Pour modifier le code des jeux ou ajouter de nouvelles fonctionnalités, consultez `CLAUDE.md` qui contient:
- Principes de design établis
- Structure de code standardisée
- Guidelines pour maintenir la cohérence
- Templates pour créer de nouveaux jeux

## 📄 Licence

Projet éducatif - Libre d'utilisation et de modification.

## 🤝 Contribution

Pour maintenir la cohérence:
1. Suivez les conventions du `CLAUDE.md`
2. Gardez les jeux auto-contenus (un seul fichier HTML)
3. Utilisez le système de CONFIG centralisé
4. Maintenez le style visuel cohérent (dark + cyan glow)
5. Testez sur mobile et desktop

---

**Amusez-vous bien! 🎮🔓**
