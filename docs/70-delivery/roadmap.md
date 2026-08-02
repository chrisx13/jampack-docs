# Feuille de route

Séquencement des jalons, intégrant les **fonctions indispensables** (voir *Fonctions indispensables*). Principe : livrer tôt un produit **vendable et conforme**, puis étendre. Un dev principal → un jalon à la fois, l'**IA incluse** (coût nul) ajoutée en continu là où c'est pertinent.

## Fait

Socle multi-société (Compte ▸ Société ▸ données) · authentification OIDC + **RBAC par société** (modèle de droits Rôle▸Module▸Domaine▸Action, testé) · **CRM** (clients, contacts, établissements, pipeline) · **référentiels** (articles, TVA, numérotation) · **modèle de données Facturation** · thème Jampack · Docker · specifications (SRS, habilitation, module IA, cartographie IA).

## Jalon A — Facturation vendable (P0)

Le cœur commercial. **Objectif : émettre une vraie facture conforme et suivre son paiement.**

- Finaliser **factures** : lignes (articles/TVA), totaux HT/TVA/TTC, statut brouillon→validée, **numéro auto**, **PDF**.
- **Paramétrage société** : logo, coordonnées, RIB/IBAN, mentions légales, CGV.
- **Modèles de documents PDF** personnalisables (devis, factures, avoirs).
- **Conditions & échéances de paiement**, pénalités de retard.
- **Suivi des règlements / encaissements**.
- **Notifications** in-app + e-mail (échéances, validations) + **relances** impayés.
- Devis → facture, avoirs, **factures d'acompte**.

## Jalon B — Onboarding & robustesse (P0)

Ce qui rend le produit adoptable et fiable.

- **Import / export** CSV-Excel (clients, articles, contacts…) — reprise de données.
- **Sauvegarde / restauration** automatisées et chiffrées.
- **Pièces jointes / GED légère** sur les fiches.
- **Tableaux de bord / KPI par rôle**.

## Jalon C — Conformité France (P0)

Non négociable, avec l'échéance e-invoicing.

- **Facturation électronique** Factur-X via **PDP** (réception oblig. 09/2026).
- **FEC**, **mentions légales** obligatoires sur les pièces.
- **RGPD** : registre, **droit à l'effacement / export** des données personnelles.
- NF525 / attestation éditeur si encaissement B2C (à évaluer).

## Jalon D — Administration & pilotage des droits

Rendre la gouvernance pilotable par le client.

- Module **Administration** : utilisateurs (actif/inactif), rôles, **éditeur de l'arbre des droits** (tri-état), rôles prédéfinis, garde **dernier admin actif**.
- **Paramètres utilisateur** (avatar, téléphone…).
- **Crédits IA** : soldes, **plafonds par utilisateur/rôle**, journal de consommation.
- Premières briques **IA incluse** (coût nul) : dédoublonnage, contrôles TVA, anomalies.

## Jalon E — Achats & stock

Compléter le cycle marchandises.

- Fournisseurs, **commandes fournisseurs**, réceptions, factures fournisseurs, **3-way match**.
- **Stock** : entrepôts, mouvements, **inventaire**, valorisation, seuils/réappro.

## Jalon F — Comptabilité & trésorerie (P0 réglementaire)

- **Écritures automatiques** depuis ventes/achats, plan comptable (PCG), journaux.
- **TVA (CA3)**, lettrage, **rapprochement bancaire** + **import relevés** (OFX/CSV).
- **Export expert-comptable**, immobilisations, analytique.
- **Prévisionnel de trésorerie**.

## Jalon G — IA générative & extensions

- **IA générative** (assistant contextuel, rédaction, synthèses) + décompte crédits.
- **API publique + webhooks**, multi-devise, montée en puissance des usages IA (cartographie).

## Transverse & continu

Audit/historisation, soft-delete, recherche globale, sécurité, et **IA incluse** ajoutée au fil de l'eau partout où c'est possible et pertinent (voir *Cartographie des usages IA*).
