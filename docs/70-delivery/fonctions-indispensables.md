# Fonctions indispensables (backlog priorisé)

Avis d'architecte sur les fonctions **indispensables** d'un ERP pour TPE/PME françaises. Priorités : **P0** = incontournable pour commercialiser, **P1** = attendu rapidement, **P2** = important ensuite. Statut : **Prévu** (déjà au plan) / **À ajouter** (manque à combler).

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

## Mon top des manques à traiter en priorité (P0)

1. **Paramétrage société + modèles de documents PDF** (sans ça, pas de facture présentable).
2. **Suivi des règlements + échéances de paiement** (le cœur de la facturation).
3. **Notifications** (relances, échéances, validations).
4. **Import/export de données** (reprise de l'existant à l'onboarding — bloquant commercial).
5. **Sauvegarde/restauration** (confiance & sécurité des données).
6. **Comptabilité : écritures auto + TVA + FEC** et **RGPD (effacement/export)** — obligations légales.
