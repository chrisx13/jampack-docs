# Fonctions indispensables (backlog priorisé)

Avis d'architecte sur les fonctions **indispensables** d'un ERP pour TPE/PME françaises. Priorités : **P0** = incontournable pour commercialiser, **P1** = attendu rapidement, **P2** = important ensuite. Statut : **Prévu** (déjà au plan) / **À ajouter** (manque à combler).

> **Principe transverse — simplicité d'abord.** Au-delà du P0, ces fonctions sont des **plus** activables **progressivement** : elles ne doivent jamais complexifier l'expérience par défaut. JAMPACK doit rester **simple d'approche**, la richesse se révélant au besoin.

## Socle transverse

| Fonction | Priorité | Statut |
|---|---|---|
| Authentification, RBAC par société, multi-société | P0 | Prévu |
| Audit / historisation, soft-delete généralisé | P0 | Prévu |
| **Paramétrage société** (logo, coordonnées, RIB/IBAN, mentions légales, CGV) | P0 | **À ajouter** |
| **Modèles de documents PDF personnalisables** (devis, factures) | P0 | **À ajouter** |
| **Numérotation des pièces** par société | P0 | Prévu |
| **Notifications** in-app + e-mail (relances, échéances, validations) | P0 | **À ajouter** |
| **Import / export** CSV-Excel (clients, articles, écritures…) — reprise de données | P0 | **À ajouter** |
| **Pièces jointes / GED légère** (documents rattachés aux fiches) | P1 | **À ajouter** |
| Recherche globale | P1 | Prévu (IA incluse) |
| **Tableaux de bord / KPI par rôle** | P1 | **À ajouter** |
| **API publique + webhooks** (intégrations) | P1 | Prévu (note archi) |
| **Sauvegarde / restauration** automatisées | P0 | **À ajouter** |
| Multi-devise | P2 | À ajouter |

## CRM

| Fonction | Priorité | Statut |
|---|---|---|
| Clients/tiers, contacts, établissements, pipeline | P0 | Prévu ✓ |
| Activités, tâches, **agenda & rappels** | P1 | Partiel (à étoffer) |
| Suivi des e-mails / interactions | P2 | À ajouter |

## Ventes & facturation

| Fonction | Priorité | Statut |
|---|---|---|
| Devis → facture → avoir, lignes, TVA, totaux | P0 | Prévu (en cours) |
| **Numéro auto à la validation, PDF** | P0 | Prévu |
| **Facturation électronique** (Factur-X / PDP) | P0 | Prévu (échéance 2026-27) |
| **Conditions & échéances de paiement**, pénalités de retard | P0 | À ajouter |
| **Suivi des règlements / encaissements** + rapprochement | P0 | À ajouter |
| **Relances automatiques** (impayés) | P1 | À ajouter |
| **Factures d'acompte** | P1 | À ajouter |
| **Factures récurrentes / abonnements** | P1 | À ajouter |
| Remises, **tarifs par client**, catalogue | P1 | Partiel (catalogue ✓) |
| Bon de commande / bon de livraison | P2 | À ajouter |

## Achats & stock

| Fonction | Priorité | Statut |
|---|---|---|
| Fournisseurs (tiers) | P1 | Prévu (modèle ✓) |
| Commandes fournisseurs, réceptions, factures fournisseurs, 3-way match | P1 | À ajouter |
| Articles/catalogue | P0 | Prévu ✓ |
| Entrepôts, mouvements, **inventaire**, valorisation (PMP/FIFO) | P1 | À ajouter |
| Seuils & réapprovisionnement | P2 | À ajouter |
| Traçabilité lots / n° série | P2 | À ajouter |

## Comptabilité & trésorerie

| Fonction | Priorité | Statut |
|---|---|---|
| Plan comptable (PCG), journaux, **écritures auto** depuis la gestion | P0 | À ajouter |
| **TVA (CA3)**, **FEC** | P0 | À ajouter (réglementaire) |
| Lettrage, **rapprochement bancaire** | P1 | À ajouter |
| **Import relevés bancaires** (OFX/CSV) / agrégation | P1 | À ajouter |
| Export vers l'expert-comptable | P1 | À ajouter |
| Immobilisations, comptabilité analytique | P2 | À ajouter |
| **Prévisionnel de trésorerie** | P1 | À ajouter |

## Conformité France (non négociable)

| Fonction | Priorité | Statut |
|---|---|---|
| Facturation électronique Factur-X / PDP | P0 | Prévu |
| FEC | P0 | À ajouter |
| Mentions légales obligatoires sur les pièces | P0 | À ajouter |
| RGPD : registre, **droit à l'effacement / export** des données personnelles | P0 | À ajouter |
| NF525 / attestation éditeur (si encaissement B2C) | P1 | À évaluer selon usage |

## IA (transverse)

| Fonction | Priorité | Statut |
|---|---|---|
| IA incluse (contrôles, anomalies, scoring, dédoublonnage…) | P1 | Prévu (cartographie IA) |
| IA générative (rédaction, assistant, synthèses) + crédits | P1 | Prévu |

## Plateforme & adaptabilité (différenciateur transverse)

Permettre au client d'adapter l'ERP à son métier **sans développement** — c'est ce qui fidélise.

| Fonction | Priorité | Statut |
|---|---|---|
| **Personnalisation de l'affichage** par utilisateur (colonnes, tri, filtres, vues enregistrées, mise en page) | P1 | À ajouter |
| **Vues génériques** créées par l'administration (partagées / par rôle) | P1 | À ajouter |
| **Champs personnalisés** de tout type sur un domaine (ex. Contact) + **statuts configurables** | P1 | À ajouter |
| **Moteur d'automatisations no-code** (déclencheurs → actions : « facture échue → relance ») | P1 | À ajouter |
| **Workflows d'approbation** configurables (devis, remises, achats, notes de frais) | P1 | À ajouter |
| **Générateur d'états / rapports** self-service (au-delà des tableaux de bord) | P2 | À ajouter |
| **Multi-langue (i18n)** interface + documents | P2 | À ajouter |

## Projets & services (nouveau domaine — élargit fortement le marché)

Couvre les TPE/PME de services (agences, conseil, IT, BE, artisans), aujourd'hui non adressées.

| Fonction | Priorité | Statut |
|---|---|---|
| **Projets / affaires** (structure, budget, suivi) | P1 | À ajouter |
| **Feuilles de temps** | P1 | À ajouter |
| **Facturation au temps passé / au forfait / à l'avancement** | P1 | À ajouter |
| **Suivi de rentabilité** par affaire | P2 | À ajouter |
| **SAV / tickets / interventions** (field service, planning) | P2 | À ajouter |
| **Notes de frais** | P1 | À ajouter |
| **Contrats & renouvellements** (complète les factures récurrentes) | P2 | À ajouter |

## Self-service externe (portails)

| Fonction | Priorité | Statut |
|---|---|---|
| **Portail client** : consulter et **payer les factures en ligne**, signer un devis, suivre ses commandes | P1 | À ajouter |
| **Portail fournisseur** : commandes, factures | P2 | À ajouter |

## Logistique avancée (si cible négoce / distribution)

À ne prioriser que si cette cible est visée — sinon poids inutile.

| Fonction | Priorité | Statut |
|---|---|---|
| **Bons de livraison**, préparation / **picking**, expéditions | P2 | À ajouter |
| **Étiquettes transporteurs** + suivi | P2 | À ajouter |
| **Transferts inter-entrepôts** | P2 | À ajouter |
| **Codes-barres / QR + scan mobile** | P2 | À ajouter |
| **Retours (RMA)** | P2 | À ajouter |
| **Nomenclatures / kits**, **variantes**, **unités & conditionnements** | P2 | À ajouter |

## Mobilité, sécurité & adoption

| Fonction | Priorité | Statut |
|---|---|---|
| **Application mobile native** (+ **mode hors-ligne**) | P1 | À ajouter (vision d'origine web/RCP/mobile) |
| **MFA / 2FA**, politique de mot de passe | P1 | À ajouter (via Keycloak) |
| **Chiffrement au repos**, **archivage à valeur probante (NF203)** | P1 | À ajouter |
| **Assistant de configuration** (wizard) + **données de démo** | P1 | À ajouter |
| **Aide contextuelle & « how-to » intégrés** : à tout moment, explication de **chaque action possible** (adaptée aux droits) | P1 | À ajouter |
| **Accessibilité RGAA / WCAG** (secteur public, inclusivité) | P2 | À ajouter |

## Finance complémentaire

| Fonction | Priorité | Statut |
|---|---|---|
| **Budgets & suivi budgétaire** | P2 | À ajouter |
| **Recouvrement avancé** (scénarios de relance / escalade) | P2 | À ajouter |

## Mon top des manques à traiter en priorité (P0)

1. **Paramétrage société + modèles de documents PDF** (sans ça, pas de facture présentable).
2. **Suivi des règlements + échéances de paiement** (le cœur de la facturation).
3. **Notifications** (relances, échéances, validations).
4. **Import/export de données** (reprise de l'existant à l'onboarding — bloquant commercial).
5. **Sauvegarde/restauration** (confiance & sécurité des données).
6. **Comptabilité : écritures auto + TVA + FEC** et **RGPD (effacement/export)** — obligations légales.

## Mes paris stratégiques (après le socle vendable & la conformité)

Ce qui élargit le marché et différencie JAMPACK de Sellsy / Axonaut / Pennylane, dans l'ordre :

1. **Plateforme adaptable** : champs personnalisés + moteur d'automatisations no-code. Fidélise, car chaque client « tord » l'outil à son métier sans dev.
2. **Projets & services + feuilles de temps + notes de frais**. Ouvre tout le segment des sociétés de services, aujourd'hui non couvert.
3. **Portail client avec paiement en ligne** (et signature de devis). Fort effet commercial et gros gain de temps ADV.

La **profondeur logistique** (picking, transporteurs, RMA…) et l'**app mobile native** viennent ensuite, selon la cible. Ces paris pèsent plus, pour un dev solo, que d'approfondir un domaine déjà couvert.
