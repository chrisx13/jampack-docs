# Spécification des exigences (SRS)

*Software Requirements Specification — structure inspirée d'ISO/IEC/IEEE 29148*

## 1. Introduction

### 1.1 Objet
Ce document spécifie les exigences fonctionnelles et non-fonctionnelles de **JAMPACK**, ERP cloud pour TPE/PME françaises. Il couvre le socle livré et les modules à court terme, et sert de référence pour le développement, les tests et la recette.

### 1.2 Portée
JAMPACK gère la relation client, les ventes et la facturation, les achats, le stock et la comptabilité, en mode multi-société et conforme aux exigences françaises. Voir la *Vision & périmètre* pour le cadrage produit.

### 1.3 Définitions
Voir le *Glossaire & dictionnaire de données*.

### 1.4 Références
ISO/IEC/IEEE 29148 (exigences), ISO/IEC 25010 (qualité), RGPD, réforme française de la facturation électronique, *Analyse métier (BRD)*, *Document d'architecture*.

## 2. Description générale

JAMPACK est une application web (et desktop/mobile) multi-tenant. La hiérarchie des données est **Compte ▸ Société ▸ données de gestion**. Les utilisateurs s'authentifient via OIDC (Keycloak) et disposent de **rôles par société, cumulables**. L'isolation des comptes est garantie au niveau base (Row-Level Security). Le produit est porté par une petite équipe : l'architecture est modulaire et les modules sont livrés par jalons.

## 3. Exigences fonctionnelles

### 3.1 Authentification & accès

- **SRS-F-AUTH-1** — Le système authentifie les utilisateurs via OIDC (Keycloak) ; aucun mot de passe n'est stocké par l'application.
- **SRS-F-AUTH-2** — Un utilisateur est **identifié de façon unique par son adresse e-mail**.
- **SRS-F-AUTH-3** — À la connexion, le système résout les sociétés accessibles à l'utilisateur et ses permissions effectives (union de ses rôles pour la société active).
- **SRS-F-AUTH-4** — Un utilisateur **inactif** ne peut pas se connecter.
- **SRS-F-AUTH-5** — Toute requête est refusée (401) sans jeton valide, et interdite (403) si la permission requise n'est pas détenue.

### 3.2 Comptes & sociétés (multi-société)

- **SRS-F-ORG-1** — Un compte peut contenir plusieurs sociétés.
- **SRS-F-ORG-2** — L'utilisateur peut sélectionner la **société active** ou une **vue consolidée** (toutes ses sociétés).
- **SRS-F-ORG-3** — Les données de gestion (clients, articles, factures, écritures…) sont **cloisonnées par société** ; le sélecteur ne propose que les sociétés accessibles à l'utilisateur.
- **SRS-F-ORG-4** — L'isolation entre comptes est garantie même en cas d'erreur applicative (RLS).

### 3.3 Administration : utilisateurs, rôles & droits

- **SRS-F-ADM-1** — Un droit général **« Utilisateurs »** autorise à **voir, créer et modifier** les utilisateurs du compte.
- **SRS-F-ADM-2** — La création d'un utilisateur se fait par **adresse e-mail** (unique) ; un utilisateur déjà existant ne peut être recréé.
- **SRS-F-ADM-3** — Un utilisateur **ne peut jamais être supprimé** ; il peut uniquement être basculé **actif / inactif**. Son historique (pièces créées, activités) est conservé.
- **SRS-F-ADM-4** — Les **rôles** sont définis au niveau du compte et attribués **par société** ; un utilisateur peut cumuler plusieurs rôles dans une société et avoir des rôles différents d'une société à l'autre.
- **SRS-F-ADM-5** — Les permissions s'expriment en couples **action × sujet** (ex. `create × Invoice`) et sont évaluées côté serveur pour chaque opération sensible.

### 3.4 Paramétrage

Le paramétrage se divise en deux espaces distincts.

- **SRS-F-SET-1 (paramètres globaux)** — L'accès aux **paramètres globaux** (TVA, numérotation des pièces, sociétés, rôles, modèles de documents…) est **soumis à permission**.
- **SRS-F-SET-2 (paramètres utilisateur)** — Chaque utilisateur peut consulter et **modifier librement les informations propres à son compte** : **avatar, téléphone, nom d'affichage**, préférences d'affichage. Ces modifications ne requièrent aucun droit particulier au-delà d'être connecté.
- **SRS-F-SET-3** — Un utilisateur ne peut pas, via ses paramètres personnels, modifier ses propres rôles, permissions ou statut actif/inactif (réservés au droit « Utilisateurs »).

### 3.5 CRM — tiers, établissements, contacts, pipeline

- **SRS-F-CRM-1** — Le système gère des **tiers** (`Company`) pouvant être **client et/ou fournisseur**, avec leur SIREN.
- **SRS-F-CRM-2** — Un tiers peut avoir plusieurs **établissements** (adresses) ; chaque établissement porte son SIRET et peut être marqué **siège**, **facturation** et/ou **livraison**.
- **SRS-F-CRM-3** — Le système gère des **contacts**, rattachables à un tiers et à un établissement.
- **SRS-F-CRM-4** — Les **opportunités** sont suivies dans un **pipeline** par étapes (glisser-déposer) ; les actions sont soumises aux permissions.

### 3.6 Référentiels

- **SRS-F-REF-1** — **Catalogue** d'articles et services (référence, type bien/service, unité, prix HT, taux de TVA).
- **SRS-F-REF-2** — **Taux de TVA** paramétrables (20 %, 10 %, 5,5 %, 2,1 %, 0 %).
- **SRS-F-REF-3** — **Numérotation** des pièces par société et par type de document, attribuée de façon **atomique** (aucun doublon possible).

### 3.7 Facturation (cible)

- **SRS-F-FAC-1** — Créer devis, factures et avoirs avec lignes (article, quantité, prix HT, TVA).
- **SRS-F-FAC-2** — Calculer les totaux **HT / TVA / TTC** sans perte de précision ; le taux de TVA est **figé sur la ligne** à la facturation.
- **SRS-F-FAC-3** — Attribuer un **numéro** à la validation de la facture (séquence de la société).
- **SRS-F-FAC-4** — Éditer la facture en **PDF** et l'émettre en **facture électronique** (Factur-X via PDP).

## 4. Exigences non-fonctionnelles

- **SRS-NF-SEC-1** — Isolation stricte des comptes (RLS) ; l'application s'exécute avec un rôle base non-propriétaire.
- **SRS-NF-SEC-2** — Contrôle d'accès systématique côté serveur (permissions), pas seulement masquage UI.
- **SRS-NF-RGPD-1** — Hébergement des données dans l'**UE** ; gestion du consentement et du droit à l'effacement pour les données personnelles.
- **SRS-NF-CONF-1** — Conformité à la facturation électronique française et production du **FEC** pour la comptabilité.
- **SRS-NF-PERF-1** — Temps de réponse des écrans de gestion courants < 1 s en usage nominal.
- **SRS-NF-DISP-1** — Sauvegardes automatisées et chiffrées ; objectif de disponibilité élevé en production.
- **SRS-NF-UX-1** — Interface **unique** pour tous les clients web, au thème officiel ; modes clair et sombre ; responsive.
- **SRS-NF-AUD-1** — Journal d'audit des opérations sensibles (traçabilité).

## 5. Exigences de données

Les entités principales et leurs relations sont décrites dans le *Modèle de données (ERD)* ; le *Glossaire* en donne le dictionnaire. Contrainte transverse : les montants sont stockés en **décimal** (jamais en flottant).

## 6. Traçabilité

Chaque exigence `SRS-F-*` sera reliée à un ou plusieurs **cas de test** dans la *matrice de traçabilité* (section Qualité), et à la (aux) **décision(s) d'architecture** concernée(s).
