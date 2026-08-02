# JAMPACK — Documentation

Documentation produit de **JAMPACK**, ERP cloud pour TPE/PME françaises (CRM · Facturation · Comptabilité · Stock).

Ce dépôt est la documentation **« docs-as-code »** : Markdown versionné, revu par pull request, rendu en **site web** (MkDocs Material), en **PDF** combiné et en **livrables Word** (un par document) via la CI.

## Aperçu local

```bash
python -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
mkdocs serve        # http://127.0.0.1:8000
```

## Produire les livrables

- **Site + PDF** : la CI (`.github/workflows/docs.yml`) construit le site et, avec `ENABLE_PDF_EXPORT=1`, le PDF combiné (`site/pdf/`).
- **Word** : la CI convertit chaque document en `.docx` (via pandoc) dans `site/word/`.

## Structure

```
docs/
├─ 00-produit/            Vision & périmètre, personas, processus
├─ 10-analyse-metier/     BRD / Business Analysis, règles de gestion
├─ 20-exigences/          SRS, exigences non-fonctionnelles, use cases
├─ 30-architecture/       SAD (arc42 / C4), modèle de données, API, ADR
├─ 40-securite-conformite/ RGPD, e-invoicing, RBAC, audit
├─ 50-qualite/            Plan & cas de test, traçabilité
├─ 60-exploitation/       Déploiement, runbook
├─ 70-delivery/           Roadmap, risques, notes de version
└─ glossaire.md
```

Voir le *Plan documentaire JAMPACK* pour la feuille de route de rédaction.
