# Tubes "Œil Magique" en Javascript

Une bibliothèque de composants JavaScript permettant de simuler les tubes cathodiques de type "Œil Magique", des indicateurs visuels d'accord de fréquence et de qualité de réception largement utilisés dans les radios et téléviseurs jusque dans les années 1950.

## Caractéristiques

- Implémentation JavaScript pure sans dépendances
- Plusieurs modèles de tubes sont pris en charge : 6E5, EM34 et EM31
- Animations phosphorescentes avec inertie
- Limites de plage de signal configurables
- Apparence et rotation personnalisables
- Prise en charge optionnelle des superpositions en verre

## Démarrage rapide

### Installation

Incluez la bibliothèque `magicEye.min.js` dans votre code HTML :

```html
<script src="dist/magicEye.min.js"></script>
```

### Utilisation de base

Vous pouvez vous inspirer du fichier `simple.html` qui montre le minimum requis.

Voici le cœur :
```html
<div id="my-tube" class="tube-container"></div>

<script>
const tube = new MagicEye({
  container: '#my-tube',
  model: 'EM34',
  signal: 0.5
});
</script>
```

## Modèles disponibles

Voir la page de démonstration : `demo.html`.

## Options de configuration

| Paramètre | Type | Par défaut | Description |
|-----------|------|---------|-------------|
| `container` | chaîne\|Élément | **obligatoire** | Sélecteur CSS ou élément DOM |
| `model` | chaîne | "EM34" | Identifiant du modèle de tube |
| `size` | nombre | 350 | Taille du composant en pixels |
| `powered` | booléen | vrai | État d'alimentation initial |
| `signal` | nombre | 0.3 | Valeur initiale du signal (0-1) |
| `remanence` | nombre | 15 | Inertie de l'animation (1-50) |
| `rotation` | nombre | 0 | Angle de rotation en degrés (0-360) |
| `minValue` | nombre | 0 | Limite minimale du signal (0-1) |
| `maxValue` | nombre | 1 | Limite maximale du signal (0-1) |
| `glassOverlay` | chaîne\|null | null | Chemin d'accès au fichier SVG de superposition de verre |
| `onPowerChange` | fonction | null | Fonction de rappel lors d'un changement d'état d'alimentation |
| `onSignalChange` | fonction | null | Fonction de rappel lors d'un changement de valeur du signal |

## Méthodes API

### Contrôle du signal

```javascript
tube.setSignal(0.7);           // Paramétrage de la valeur du signal (0-1)
tube.getSignal();              // Lecture de la valeur actuelle du signal
```

### Contrôle de l'alimentation

```javascript
tube.setPower(true);           // Allumer
tube.setPower(false);          // Éteindre
tube.isPoweredOn();            // Vérifier l'état de l'alimentation
tube.toggle();                 // Activer/désactiver l'alimentation
```

### Apparence

```javascript
tube.setSize(500);             // Paramétrage de la taille en pixels
tube.setRotation(90);          // Paramétrage de l'angle de rotation
tube.setRemanence(25);         // Paramétrage de l'inertie de l'animation
tube.setMinValue(0.2);         // Paramétrage de la limite minimale
tube.setMaxValue(0.8);         // Paramétrage de la limite maximale
tube.setGlassOverlay('glass.svg'); // Paramétrage du fichier "overlay" du verre
tube.setGlassOverlay(null);    // Suppression du fichier "overlay" du verre
```

### Nettoyage

```javascript
tube.destroy();                // Supprimer le composant et nettoyer
```

## Création de modèles personnalisés

Ajoutez votre configuration à l'objet `MagicEyeModels` :

```javascript
MagicEyeModels['CUSTOM'] = {
  topAngleOffset: 2,
  bottomAngleOffset: 6,
  topCurveIntensity: 16,
  bottomCurveIntensity: 0.8,
  topCurveDirection: -1,
  bottomCurveDirection: -1,
  centerCapRadius: 18,
  phosphorOffColor: '#1a1a1a',
  phosphorOnColor: '#001505',
  glowColor: '#55ff77',
  glowBlur: 0.3,
  supportColor: '#111',
  centerCapColor: '#222',

  // Facultatif : zones fixes (comme 6E5)
  topFixed: false,
  topFixedValue: 1.0,
  bottomFixed: false,
  bottomFixedValue: 1.0,
  drawFixedAsArc: false
};
```
## Superpositions en verre

La bibliothèque prend en charge les superpositions en verre SVG ou PNG facultatives pour simuler la lentille en verre du tube. Créez des superpositions personnalisées avec une transparence, des effets de réflexion, des teintes ou des distorsions.

Exemple de structure de superposition :
```svg
<svg width="200" height="200" viewBox="0 0 200 200">
  <defs>
    <radialGradient id="glassBulge">
      <!-- Effets de réflexion -->
    </radialGradient>
  </defs>
  <circle cx="100" cy="100" r="100" fill="url(#glassBulge)"/>
</svg>
```

## Compatibilité avec les navigateurs

Fonctionne avec tous les navigateurs modernes prenant en charge :
- SVG
- Transformations et transitions CSS3
- Classes ES6

## Exemples

Consultez le fichier `demo.html` pour voir une démonstration complète des les modèles ainsi que les fonctionnalités des tubes.

## Licence

Licence APACHE 2.0 - Voir le fichier LICENSE pour plus de détails.

## Contribution

Les contributions sont les bienvenues.

## Crédits

Basé sur les conceptions historiques des tubes magiques des années 1930 à 1950, à l'époque de l'électronique à tubes à vide.
Merci à Howard pour son précieux site Web "magiceyetubes.com" et notamment pour ses patterns des différents tubes : https://www.magiceyetubes.com/patterns.htm 
