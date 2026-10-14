# LE SHIELD — V1.2

**Version validée : SHIELD V1.2.** L’animation des étoiles filantes a été retirée ; les effets lumineux du logo principal et des circuits sont conservés.

**Savoir et Habileté Informatique en Libre Diffusion.** Cette web app responsive organise les vidéos YouTube dans une interface accessible sur iPhone, iPad, Android et navigateur. Elle ne demande pas de compte élève et ne nécessite pas d’abonnement à un service applicatif.

## Structure de l’application

- Accueil avec recherche globale et cinq grands thèmes : Office 365, Retouche d’images, Programmation Python, Apple iPad et Systèmes d’information géographique. Un motif discret de circuit imprimé, inspiré du logo, accompagne le fond de toutes les pages.
- Office 365 mène à Word, Excel et PowerPoint.
- Retouche d’images mène à GIMP.
- Programmation Python et SIG montrent les vidéos directement.
- Les rubriques recensées dans Glide sont déjà structurées : Word, Excel, PowerPoint, GIMP, Python et QGIS.
- Apple iPad est présent dans l’accueil. La version publique Glide consultée ne montrait pas de rubriques sur cette page.

## Modifier les contenus

Tout le catalogue est dans [`data/videos.json`](data/videos.json). L’interface lit ce fichier au chargement : il n’y a pas de base de données ni de code à modifier pour ajouter une vidéo.

Chaque objet dans `videos` utilise ces champs :

```json
{
  "categoryId": "office-365",
  "subcategoryId": "word",
  "title": "Titre de la vidéo",
  "description": "Courte description destinée aux élèves.",
  "youtube": "https://www.youtube.com/watch?v=ID_DE_LA_VIDEO",
  "isNew": true
}
```

`subcategoryId` est nécessaire pour Office 365 et Retouche d’images, et absent pour les catégories à liste directe. Tant qu’un lien YouTube exact n’a pas été associé, l’application affiche « Lien YouTube à associer » et ne propose pas de faux lien. Quand `youtube` est renseigné, la miniature est récupérée automatiquement. Le bouton triangulaire au centre de chaque miniature et les résultats de recherche ouvrent un lecteur de prévisualisation intégré à l’application. Le bouton de fermeture arrête la vidéo et ramène au catalogue. `isNew: true` affiche le badge « Nouveau ».

Les 65 fiches vidéo conservées ont été relevées dans Glide et leurs liens YouTube exacts ont été ajoutés. La rubrique Canva et sa fiche vide ont été retirées à la demande de Manu. La catégorie Apple iPad ne montrait aucune fiche dans la version publique consultée.

## Voir l’application sur son ordinateur

Le fichier JSON doit être chargé depuis un serveur web local, et non en ouvrant `index.html` directement.

Depuis le dossier du projet, démarre un serveur local avec Python :

```sh
python3 -m http.server 8000
```

Puis ouvre <http://localhost:8000>.

## Mise en ligne gratuite

Le projet est un site statique : aucun serveur applicatif n’est nécessaire. Pour le publier gratuitement avec GitHub Pages :

1. Crée un dépôt GitHub public et ajoute les fichiers du projet.
2. Dans les paramètres du dépôt, ouvre **Pages**.
3. Choisis **Deploy from a branch**, puis la branche principale et le dossier `/ (root)`.
4. Enregistre, puis partage l’adresse `https://…github.io/…` fournie par GitHub.

Toute personne disposant du lien pourra consulter l’application. Pour modifier le catalogue, modifie `data/videos.json` et republie le changement.

## Installation sur l’écran d’accueil

Sur iPhone ou iPad, ouvre le lien HTTPS dans Safari puis choisis **Partager → Sur l’écran d’accueil**. Sur Android, utilise le menu du navigateur **Installer l’application** ou **Ajouter à l’écran d’accueil**. Le contenu YouTube et ses miniatures nécessitent une connexion internet.

## Fichiers principaux

- `data/videos.json` : thèmes, logiciels, titres, descriptions et liens YouTube.
- `app.js` : navigation, affichage et recherche.
- `styles.css` : présentation et adaptations aux écrans mobiles.
- `assets/` : logos et images officielles fournis pour LE SHIELD.
- `manifest.webmanifest` et `service-worker.js` : installation PWA et cache de l’application.

## Fichiers d’exercice à télécharger

Pour joindre un document à une vidéo, dépose le fichier dans le dossier [`downloads/`](downloads/) (tu peux créer des sous-dossiers), puis ajoute à cette fiche un champ `resources` dans `data/videos.json` :

```json
"resources": [
  {
    "label": "Fichier de départ Excel",
    "file": "downloads/excel/fichier-de-depart.xlsx"
  }
]
```

Le bouton de téléchargement apparaît sur la fiche de la vidéo. Une fiche peut proposer plusieurs ressources ; le champ `label` donne le nom affiché aux élèves et `file` indique le chemin du fichier. Pense à publier les fichiers avec le site pour qu’ils soient accessibles aux élèves.
