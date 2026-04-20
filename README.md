# webpages

Collection de pages publiées via **GitHub Pages** à l'adresse :

**👉 https://herve9005-blip.github.io/webpages/**

## Structure

```
webpages/
├── index.html          # Accueil
├── _config.yml         # Config Jekyll + plugins SEO/sitemap
├── robots.txt          # Autorisation indexation
├── assets/
│   └── css/style.css   # Feuille de style (responsive + dark mode)
├── pages/              # Pages HTML statiques
│   └── index.html      # Index auto des .html du dossier
├── landings/           # Mini-sites / landing pages
│   └── index.html      # Index auto des sous-dossiers
└── docs/               # Documentation Markdown (rendue par Jekyll)
    └── index.md        # Index auto des .md du dossier
```

## Ajouter une page

### Page HTML statique

Déposer un fichier `.html` dans `pages/`. Pour qu'il bénéficie du SEO et de la feuille de style :

```html
---
title: Titre de la page
description: Description courte pour les moteurs de recherche
---
<!doctype html>
<html lang="fr">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  {% raw %}{% seo %}{% endraw %}
  <link rel="stylesheet" href="{% raw %}{{ '/assets/css/style.css' | relative_url }}{% endraw %}">
</head>
<body>
  <main class="container">
    <h1>Mon titre</h1>
    <p>Contenu…</p>
  </main>
</body>
</html>
```

Ou simplement du HTML pur sans front matter : Jekyll le copiera tel quel.

### Landing page

Créer un sous-dossier dans `landings/` avec son propre `index.html` (et ses assets) :

```
landings/
└── ma-campagne/
    ├── index.html
    └── assets/
```

Elle sera accessible à `/webpages/landings/ma-campagne/` et listée automatiquement.

### Document Markdown

Créer un `.md` dans `docs/` avec front matter :

```markdown
---
title: Mon document
description: Description SEO
---

# Mon titre

Contenu en **Markdown** standard (GitHub Flavored Markdown).
```

Il sera rendu en HTML automatiquement et listé sur la page d'index.

## Référencement

- **Sitemap** généré automatiquement : `/webpages/sitemap.xml`
- **Métadonnées SEO** injectées par `jekyll-seo-tag` (OpenGraph, Twitter cards, JSON-LD)
- **robots.txt** autorise tous les crawlers
- Pour soumettre le site à Google : [Search Console](https://search.google.com/search-console) → ajouter la propriété `https://herve9005-blip.github.io/webpages/` et soumettre le sitemap.

## Activer GitHub Pages

Si ce n'est pas déjà fait :

1. **Settings** → **Pages**
2. **Source** : `Deploy from a branch`
3. **Branch** : `main` / `/ (root)` → **Save**
4. Attendre ~1 minute, le site est publié à https://herve9005-blip.github.io/webpages/

## Développement local (optionnel)

```bash
# Installer Jekyll (une fois)
gem install bundler jekyll

# Créer un Gemfile minimal si besoin
echo 'source "https://rubygems.org"
gem "github-pages", group: :jekyll_plugins' > Gemfile

bundle install
bundle exec jekyll serve
# → http://localhost:4000/webpages/
```

## Domaine personnalisé (plus tard)

Si tu veux utiliser un domaine à toi (ex. `pages.fluxpublics.fr`) :

1. Ajouter un fichier `CNAME` à la racine contenant le domaine
2. Configurer un enregistrement CNAME chez ton registrar pointant vers `herve9005-blip.github.io`
3. Activer **Enforce HTTPS** dans Settings → Pages
