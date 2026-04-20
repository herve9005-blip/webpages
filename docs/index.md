---
title: Documentation
description: Notes et documents en Markdown
---

[← Accueil]({{ '/' | relative_url }})

# Documentation

Documents rédigés en Markdown, convertis automatiquement en HTML par Jekyll.

## Documents publiés

<ul>
{% assign docs_pages = site.pages | where_exp: "p", "p.path contains 'docs/'" | where_exp: "p", "p.name != 'index.md'" %}
{% for doc in docs_pages %}
  <li><a href="{{ doc.url | relative_url }}">{{ doc.title | default: doc.name }}</a></li>
{% endfor %}
</ul>

## Comment ajouter un document

1. Créez un fichier `.md` dans ce dossier `docs/`
2. Ajoutez un front matter en tête :

```yaml
---
title: Mon titre
description: Description courte pour le SEO
---
```

3. Rédigez en Markdown standard (GFM supporté)
4. Commit + push → publication automatique
