# Feuille de route

Séquencement des jalons, intégrant les **fonctions indispensables** (voir *Fonctions indispensables*). Principe : livrer tôt un produit **vendable et conforme**, puis étendre. Un dev principal → un jalon à la fois, l'**IA incluse** (coût nul) ajoutée en continu là où c'est pertinent.

## Fait

Socle multi-société (Compte ▸ Société ▸ données) · authentification OIDC + **RBAC par société** (modèle de droits Rôle▸Module▸Domaine▸Action, testé) · **CRM** (clients, contacts, établissements, pipeline) · **référentiels** (articles, TVA, numérotation) · **modèle de données Facturation** · thème Jampack · Docker · specifications (SRS, habilitation, module IA, cartographie IA).

## Jalon A — Facturation vendable (P0)

Le cœur commercial. **Objectif : émettre une vraie facture conforme et suivre son paiement.**

- Finaliser **factures** : lignes (articles/TVA), totaux HT/TVA/TTC, statut brouillon→validée, **numéro auto**, **PDF**.
- **Paramétrage société** : logo, coordonnées, RIB/IBAN, mentions légales, CGV, **coordonnées d'affacturage & clause de subrogation** (zone activable sur les documents).
- **Tous les documents personnalisables** (modèles PDF + champs de fusion, par société) : devis, factures, avoirs — extensible à relances, BL, courriers, e-mails, états.
- **Conditions & échéances de paiement**, pénalités de retard.
- **Suivi des règlements / encaissements**.
- **Notifications** in-app + e-mail (échéances, validations) + **relances** impayés.
- Devis → facture, avoirs, **factures d'acompte**.

## Jalon B — Onboarding & robustesse (P0)

Ce qui rend le produit adoptable et fiable.

- **Import / export multi-canal** (fichiers CSV/Excel/ODS/JSON, **API/webhooks**, connecteurs, e-mail, iPaaS) : mapping réutilisable, prévisualisation, dry-run, dédoublonnage/upsert — reprise de données (voir *Connecteurs & intégrations* §6).
- **Sauvegarde / restauration** automatisées et chiffrées.
- **Pièces jointes / GED légère** sur les fiches.
- **Tâches personnelles & mutualisées** (assignation, échéances, priorités, rappels/notifications), liées aux fiches.
- **Tableaux de bord / KPI par rôle**.

## Jalon C — Conformité France (P0)

Non négociable, avec l'échéance e-invoicing.

- **Facturation électronique** Factur-X via **PDP** (réception oblig. 09/2026).
- **FEC**, **mentions légales** obligatoires sur les pièces.
- **RGPD** : registre, **droit à l'effacement / export** des données personnelles.
- NF525 / attestation éditeur si encaissement B2C (à évaluer).

## Jalon D — Administration & pilotage des droits

Rendre la gouvernance pilotable par le client.

- Module **Administration** : utilisateurs (actif/inactif), rôles, **éditeur de l'arbre des droits** (tri-état), rôles prédéfinis, garde **dernier admin actif**, **gestion des modèles de documents** (tous personnalisables, par société) et des **vues génériques**, **champs personnalisés**.
- **Paramètres utilisateur** (avatar, téléphone…).
- **Crédits IA** : soldes, **plafonds par utilisateur/rôle**, journal de consommation.
- Premières briques **IA incluse** (coût nul) : dédoublonnage, contrôles TVA, anomalies.

## Jalon E — Achats & stock

Compléter le cycle marchandises.

- Fournisseurs, **commandes fournisseurs**, réceptions, factures fournisseurs, **3-way match**.
- **Stock** : entrepôts, mouvements, **inventaire**, valorisation, seuils/réappro.

## Jalon F — Comptabilité & trésorerie (P0 réglementaire)

- **Écritures automatiques** depuis ventes/achats, plan comptable (PCG), journaux.
- **TVA (CA3)**, lettrage, **rapprochement bancaire** + **connexion multi-banque** (agrégation DSP2 + relevés CAMT.053/OFX/CFONB/CSV).
- **Import/export comptable conforme FR** : **FEC export + import**, formats expert-comptable (Sage/Cegid/Quadratus/EBP/Pennylane) ; immobilisations, analytique.
- **Prévisionnel de trésorerie**.

## Jalon G — IA générative & extensions

- **IA générative** (assistant contextuel, rédaction, synthèses) + décompte crédits.
- **API publique + webhooks**, multi-devise, montée en puissance des usages IA (cartographie).

## Jalon H — Plateforme & adaptabilité

Le différenciateur transverse : adapter l'ERP au métier **sans développement**.

- **Personnalisation de l'affichage** par utilisateur (colonnes, tri, filtres, **vues enregistrées**, mise en page) + **vues génériques** créées par l'administration (partagées/par rôle).
- **Champs personnalisés** de tout type sur un domaine (ex. Contact) + **statuts configurables** par objet.
- **Moteur d'automatisations no-code** (déclencheurs → actions), au-dessus des notifications.
- **Workflows d'approbation** configurables (devis, remises, achats, notes de frais).
- **Générateur d'états / rapports** self-service ; **multi-langue (i18n)** interface + documents.

## Jalon I — Projets & services

Ouvre le segment des sociétés de services (aujourd'hui non adressé).

- **Projets / affaires**, **feuilles de temps**, **facturation au temps passé / forfait / avancement**, **rentabilité par affaire**.
- **Notes de frais** ; **contrats & renouvellements** (complète les factures récurrentes).
- **SAV / tickets / interventions** (field service, planning).

## Jalon J — Portails self-service

- **Portail client** : consulter et **payer les factures en ligne**, **signer un devis**, suivre ses commandes.
- **Portail fournisseur** : commandes, factures.

## Jalon K — Logistique avancée *(si cible négoce / distribution)*

- **Bons de livraison**, **picking**/préparation, expéditions, **étiquettes transporteurs**, **transferts inter-entrepôts**.
- **Codes-barres / QR + scan mobile**, **retours (RMA)**.
- **Nomenclatures / kits**, **variantes**, **unités & conditionnements**.

## Jalon L — Mobilité, sécurité & adoption

- **Application mobile native** (+ **mode hors-ligne**) — la vision d'origine web/RCP/mobile.
- **MFA / 2FA**, politique de mot de passe (Keycloak), **chiffrement au repos**, **archivage à valeur probante (NF203)**.
- **Assistant de configuration** (wizard) + **données de démo** + **aide contextuelle & « how-to »** (explication de chaque action, à tout moment) + **parcours d'utilisation guidés** (visite pas-à-pas, couche IA) ; **accessibilité RGAA / WCAG**.
- **Budgets & suivi budgétaire** ; **recouvrement avancé** (scénarios de relance / escalade).

## Transverse & continu

Audit/historisation, soft-delete, recherche globale, sécurité, et **IA incluse** ajoutée au fil de l'eau partout où c'est possible et pertinent (voir *Cartographie des usages IA*).
