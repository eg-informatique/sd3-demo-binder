# SD3 — Notebooks Deno sur Binder

[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/eg-informatique/sd3-demo-binder/HEAD?urlpath=lab/tree/notebooks/00_demarrage.ipynb)

Environnement Jupyter prêt à l'emploi, avec **Deno** comme moteur (JavaScript / TypeScript), utilisable **dans le navigateur, sans rien installer**.

## Pour les élèves

1. Clique sur le bouton **launch binder** ci-dessus.
2. Patiente (quelques secondes, ou quelques minutes si l'environnement doit être reconstruit).
3. Ouvre `notebooks/00_demarrage.ipynb` et exécute les cellules avec **Shift + Entrée**.

> ⚠️ Une session Binder est **temporaire** : elle s'arrête après ~10 minutes d'inactivité et les fichiers modifiés sont perdus.
> Télécharge régulièrement ton notebook (clic droit sur le fichier → *Download*).

## Contenu

| Fichier | Rôle |
|---|---|
| `environment.yml` | Installe JupyterLab et Deno (depuis conda-forge). |
| `postBuild` | Enregistre le noyau Deno, pré-télécharge les paquets npm, fait de Deno le noyau par défaut. |
| `deno.json` | Paquets npm disponibles dans les notebooks. |
| `notebooks/` | Notebooks (noyau **Deno**). |
| `data/` | Jeux de données CSV. |

Bibliothèques pré-installées : `nodejs-polars`, `simple-statistics`, `ml-regression`, `@observablehq/plot`, `topojson-client`, `linkedom` (document virtuel pour Observable Plot). Plotly.js est chargé depuis son CDN par le navigateur.

## Pour les enseignants

### Publier

Binder lit la configuration **à la racine d'un dépôt GitHub public**. Ce dossier doit donc devenir son propre dépôt, par exemple `eg-informatique/sd3-demo-binder` :

```bash
cd binder-deno
git init -b main
git add .
git commit -m "Environnement Binder Deno"
git remote add origin git@github.com:eg-informatique/sd3-demo-binder.git
git push -u origin main
```

Si le dépôt porte un autre nom, adapter l'URL du badge ci-dessus. Un lien de lancement se construit ainsi :

```
https://mybinder.org/v2/gh/<organisation>/<dépôt>/HEAD?urlpath=lab/tree/notebooks/<notebook>.ipynb
```

### Avant le cours

La **première** construction de l'image prend plusieurs minutes. Lancer le lien soi-même une fois après chaque `git push`, pour que les élèves trouvent une image déjà prête.

### Ajouter des notebooks ou des paquets

- Ajouter des `.ipynb` dans `notebooks/` avec le noyau **Deno** ; les données sont accessibles via `../data/...`.
- Ajouter un paquet npm dans `deno.json` : il sera pré-téléchargé à la prochaine construction.
- Pour changer de version de Deno, modifier `environment.yml` (versions disponibles : <https://anaconda.org/conda-forge/deno>).

### Tester localement

```bash
pip install jupyter-repo2docker   # nécessite Docker
repo2docker .
```
