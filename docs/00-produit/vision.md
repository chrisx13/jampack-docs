# Vision & périmètre

## 1. Résumé

**JAMPACK** est un **ERP cloud tout-en-un pour les TPE et PME françaises**, réunissant dans un socle unique la relation client (CRM), la facturation, la comptabilité et le stock. Il est accessible en **web**, en **client lourd desktop** et en **application mobile**, sur une base de code partagée, et il est conçu dès l'origine comme une plateforme **multi-société** et **conforme aux exigences françaises** (facturation électronique, FEC, RGPD).

## 2. Problème adressé

Les TPE/PME françaises jonglent aujourd'hui avec des outils disparates — un CRM, un logiciel de facturation, un tableur, un expert-comptable — mal reliés entre eux, source de ressaisies, d'erreurs et de perte de temps. L'arrivée de la **facturation électronique obligatoire** (réception pour toutes les entreprises au 1er septembre 2026, émission pour les TPE/PME au 1er septembre 2027) impose par ailleurs une mise en conformité que beaucoup d'outils anciens ne couvrent pas.

## 3. Proposition de valeur

JAMPACK propose une **chaîne de gestion intégrée de bout en bout** : une opportunité commerciale devient un devis, puis une facture, puis une écriture comptable, sans ressaisie. Trois axes différenciants :

- **Intégration native** entre CRM, ventes, stock et comptabilité.
- **Conformité française de premier plan** : facturation électronique (Factur-X via PDP), FEC, TVA, RGPD.
- **Multi-société** : un même compte pilote plusieurs entités juridiques, avec données cloisonnées et vue consolidée.

## 4. Utilisateurs cibles

- **Dirigeant de TPE/PME** : pilotage global, tableau de bord, trésorerie.
- **Commercial** : CRM, pipeline, devis.
- **Assistant(e) de gestion / ADV** : facturation, clients, relances.
- **Comptable (interne ou cabinet)** : écritures, TVA, FEC, export.
- **Gestionnaire multi-sociétés** (holding, cabinet) : bascule entre sociétés, consolidation.

## 5. Périmètre fonctionnel

### Dans le périmètre

Relation client (sociétés, contacts, établissements, opportunités, activités) ; ventes (devis, commandes, factures, avoirs, e-invoicing) ; achats (fournisseurs, commandes, réceptions) ; stock (articles, entrepôts, mouvements, valorisation) ; comptabilité (plan comptable, écritures, TVA, FEC) ; référentiels (articles, TVA, numérotation) ; administration (comptes, sociétés, utilisateurs, rôles).

### Hors périmètre (à ce stade)

Paie complète (envisagée en interface avec un outil dédié), production/MRP industriel (optionnel selon secteur), et gestion de la relation fournisseur avancée (SRM).

## 6. Objectifs et indicateurs

L'objectif est un produit **commercialisable tôt** : le socle CRM + facturation conforme suffit à adresser le marché. Les indicateurs de succès porteront sur le temps de création d'une facture conforme, le taux de ressaisie évité entre modules, et la capacité à gérer plusieurs sociétés sous un seul compte.

## 7. Contraintes structurantes

- **Réglementaire** : facturation électronique (échéances 2026-2027), FEC, NF525 le cas échéant, RGPD (hébergement UE).
- **Technique** : produit porté par une petite équipe → architecture modulaire, réutilisation maximale, séquencement strict des modules.
- **Sécurité** : isolation stricte des données entre comptes, contrôle d'accès par rôle et par société.

## 8. État d'avancement (au 1er août 2026)

Socle livré : multi-société (compte ▸ société ▸ données), authentification OIDC (Keycloak) et RBAC par société, CRM (clients, contacts, établissements, pipeline), référentiels (articles, TVA, numérotation des pièces). Module de facturation en cours (modèle de données posé).

Voir la *feuille de route* pour la suite (facturation & e-invoicing, achats, stock, comptabilité).
