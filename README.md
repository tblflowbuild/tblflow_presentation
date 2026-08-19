# Présentation TblFlow — site statique

`index.html` est **autonome** : tout le CSS et tout le JavaScript sont inline, aucune
dépendance à installer, aucune étape de build. Les seules requêtes externes sont les
polices Google (Inter + JetBrains Mono) ; sans réseau, le site retombe sur les polices
système et reste parfaitement lisible.

## Héberger sur GitHub Pages

`docs/` étant déjà occupé par la documentation technique, trois options :

**1. Branche `gh-pages` dédiée** (la plus simple, rien à configurer d'autre)
```bash
git subtree push --prefix site origin gh-pages
```
Puis Settings → Pages → Source: *Deploy from a branch* → `gh-pages` / `(root)`.

**2. Dépôt séparé** — copiez `index.html` à la racine d'un dépôt vide, activez Pages.

**3. GitHub Actions** — Settings → Pages → Source: *GitHub Actions*, puis un workflow
qui publie `site/` (`actions/upload-pages-artifact` avec `path: site`).
Non fourni ici volontairement : c'est une publication publique, à activer sciemment.

## Régénérer

Le site et le `.pptx` sortent des **mêmes** modules de contenu, dans `.planning/deck/` :

```bash
cd .planning/deck
python3 build.py    # → .planning/TblFlow-Presentation.pptx
python3 site.py     # → site/index.html
node test-site.mjs  # 13 contrôles d'interaction (nécessite jsdom)
```

Pour modifier un discours ou une slide, éditez le fichier `c*.py` concerné et relancez
les deux commandes : le support et le site restent alignés.

## Raccourcis clavier

| Touche | Effet |
|---|---|
| `P` | mode présentation |
| `←` `→` `Espace` | slide précédente / suivante |
| `N` | afficher le discours dans le mode présentation |
| `/` | focus sur la recherche |
| `Esc` | quitter la présentation ou la modale |
