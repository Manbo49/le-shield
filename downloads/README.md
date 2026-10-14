# Fichiers d’exercice

Dépose ici les documents que les élèves doivent télécharger, dans des sous-dossiers si besoin (par exemple `downloads/excel/exercice-1.xlsx`).

Pour associer un document à une vidéo, ajoute un tableau `resources` à la fiche correspondante dans `data/videos.json` :

```json
"resources": [
  {
    "label": "Fichier de départ Excel",
    "file": "downloads/excel/fichier-de-depart.xlsx"
  }
]
```

Le champ `label` est le texte du bouton. Une vidéo peut proposer plusieurs fichiers. Les chemins sont relatifs à la racine du projet.
