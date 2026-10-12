
# Forge Engine v1

Moteur de génération d'images modulaire à architecture de packs.
Une seule page HTML autonome — aucun framework, aucune dépendance, aucun build.

## Le principe

Le moteur ne sait rien faire par lui-même. Toutes les capacités — styles
artistiques, recettes de génération, actions par image, bibliothèques de
couches — sont déclarées dans des **packs JSON installables**. Le moteur lit
ces packs et construit dynamiquement son interface autour d'eux.

Un pack peut être n'importe quoi : les grands photographes, des storyboards
pour scénaristes, des visuels de monétisation, une identité de galerie, un
usage sectoriel. Cent packs ou mille : le code du moteur ne change jamais.

## Fonctionnalités

- 📦 Installation, désinstallation, export et import de packs JSON
- ✨ Génération de packs par IA : décris le pack voulu en langage naturel,
  le modèle texte construit le JSON, le validateur le contrôle, le pack s'installe
- ✅ Validation stricte à l'installation avec messages d'erreur précis
- 🔧 Réparation tolérante du JSON renvoyé par l'IA : ré-échappement,
  troncature intelligente, jusqu'à 3 tentatives avec renvoi de l'erreur au modèle
- 🎬 Moteur de recettes déclaratives : chaque recette définit ses entrées
  requises (image et/ou texte), sa source et son pipeline de prompt en étapes
- 📝 Recettes texte pur : le brief écrit remplace la photo de référence
- 🌿 Actions par image générée, déclarées par le pack, avec dérivation en branche
- 🔑 Pool de clés API : rotation automatique, cooldown 65 s sur les 429,
  mise en quarantaine des clés mortes
- 💾 Persistance localStorage : clés, configuration API, packs
- 🖥️ Interface sobre et autonome, fonctionne depuis un fichier local

## Schéma d'un pack

```json
{
  "id": "mon-pack",
  "name": "Nom du pack",
  "icon": "📸",
  "desc": "Ce que couvre ce pack.",
  "profiles": ["photographe", "realisateur"],
  "styles": [
    { "id": "s1", "cat": "categorie", "name": "Artiste", "prompt": "..." }
  ],
  "layers": {
    "locations": ["in a quiet gallery", "..."],
    "moods": ["contemplative", "..."]
  },
  "recipes": [
    {
      "id": "serie",
      "name": "Série stylée",
      "hint": "Ce que ça produit",
      "inputs": ["image"],
      "source": "image",
      "count": true,
      "steps": [
        { "use": "face" },
        { "style": true },
        { "layer": "locations" },
        { "use": "quality" }
      ]
    }
  ],
  "actions": [
    { "id": "var", "name": "Variantes", "icon": "🎨", "n": 3 }
  ],
  "blocks": {
    "face": "instruction critique de préservation du visage",
    "ref": "Take THIS image as the new reference.",
    "quality": "Masterpiece quality, no watermark."
  }
}
```

## Démarrage

1. Ouvre le fichier HTML dans un navigateur.
2. Ajoute tes clés API et l'endpoint dans « Clés & API ».
3. Installe un pack — un pack de démonstration s'installe au premier
   lancement — ou génère-en un avec l'IA (« ✨ Créer un pack avec l'IA »).
4. Choisis un pack, une recette, exécute.

## Compatibilité API

Conçu pour les endpoints au format OpenAI :

- `POST /v1/images/generations`
- `POST /v1/chat/completions`

Endpoint, modèle texte et modèle image configurables depuis l'interface.

## Structure du projet

```text
forge-engine/
└── index.html   ← moteur + interface, fichier unique autonome
```

## Licence

MIT
