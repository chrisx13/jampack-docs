# Cartographie des usages IA par module

Recensement des usages d'IA sur **tout le périmètre JAMPACK**, retenus quand c'est **techniquement possible** *et* **opérationnellement pertinent**. Chaque usage est classé :

- **Incluse** — coût marginal **nul** pour l'éditeur (règles, calculs, modèles locaux/open-source). Gratuite, activée par défaut.
- **Générative** — coût réel par appel (LLM/API), **facturée aux crédits**, à la demande.

Règle transverse : l'IA **propose**, l'utilisateur **valide**. Les résultats génératifs ne sont jamais appliqués sans confirmation.

## CRM

| Usage | Niveau | Valeur |
|---|---|---|
| Dédoublonnage clients/contacts | Incluse | Qualité de la base |
| Complétion fiche via annuaire SIRENE (API publique gratuite) | Incluse | Saisie accélérée, fiabilité |
| Scoring & priorisation d'opportunités | Incluse | Focalise l'effort commercial |
| Prévision de closing (modèle local) | Incluse | Pilotage du pipeline |
| Prochaine meilleure action | Incluse | Guidage commercial |
| Résumé d'un client / d'un historique d'activités | Générative | Gain de temps, préparation RDV |
| Rédaction d'e-mails / relances contextualisés | Générative | Productivité |

## Ventes & facturation

| Usage | Niveau | Valeur |
|---|---|---|
| Contrôles de cohérence (TVA, totaux, mentions légales) | Incluse | Conformité, moins d'erreurs |
| Suggestion d'articles / de prix sur un devis | Incluse | Vitesse de devis |
| Contrôle marge / remise | Incluse | Protection de la marge |
| Priorisation des relances (risque de retard) | Incluse | Trésorerie |
| Prévision de paiement / retard client | Incluse | Anticipation |
| Génération d'un devis/facture depuis une description | Générative | Productivité |
| Rédaction du message de relance | Générative | Productivité |

## Achats & fournisseurs

| Usage | Niveau | Valeur |
|---|---|---|
| Dédoublonnage & scoring fournisseurs | Incluse | Qualité, sélection |
| Suggestion de réapprovisionnement | Incluse | Évite ruptures |
| Rapprochement commande ⇄ réception ⇄ facture (3-way match) | Incluse | Contrôle, fraude |
| Extraction de facture fournisseur (OCR local) | Incluse* | Saisie automatique |
| Extraction avancée / mise en forme (service OCR/LLM externe) | Générative | Cas complexes |

\* *Incluse si l'OCR tourne en local (coût nul) ; sinon Générative.*

## Stock

| Usage | Niveau | Valeur |
|---|---|---|
| Prévision de demande (modèle local) | Incluse | Réappro juste |
| Détection ruptures / surstock | Incluse | Optimisation |
| Réapprovisionnement optimal (calcul) | Incluse | Coûts de stock |
| Anomalies de valorisation / mouvements | Incluse | Fiabilité comptable |

## Comptabilité & trésorerie

| Usage | Niveau | Valeur |
|---|---|---|
| Catégorisation d'écritures (modèle local) | Incluse | Productivité compta |
| Détection d'anomalies / doublons / écarts TVA | Incluse | Fiabilité, contrôle |
| Rapprochement bancaire & lettrage — **propositions automatiques à valider** (relevé ↔ écriture/facture) sur les vues concernées | Incluse | Gain de temps, contrôle |
| Rapprochement des cas complexes (libellés ambigus, multi-échéances) | Générative | Couverture accrue |
| Prévisionnel de trésorerie & alertes | Incluse | Pilotage |
| Aide à la clôture (checklist intelligente) | Incluse | Sérénité |
| Synthèse/explication d'un compte, note d'analyse | Générative | Restitution |

## Frais / notes de frais

| Usage | Niveau | Valeur |
|---|---|---|
| Extraction du justificatif (OCR local) : montant, TVA, date, marchand | Incluse* | Saisie automatique |
| Extraction avancée (OCR/LLM externe, tickets complexes) | Générative | Cas difficiles |
| Catégorisation automatique de la dépense | Incluse | Productivité |
| Contrôle de la politique de frais & détection doublons/anomalies | Incluse | Conformité, fraude |

\* *Incluse si l'OCR tourne en local (coût nul) ; sinon Générative.*

## Transverse

| Usage | Niveau | Valeur |
|---|---|---|
| Recherche sémantique globale (embeddings locaux) | Incluse | Retrouver l'information |
| Aide contextuelle & **how-to** de base (guides pas-à-pas, FAQ produit) | Incluse | Adoption, simplicité |
| Assistant **« comment faire… »** en langage naturel (how-to guidé, contextualisé à l'écran/action) | Générative | Autonomie, prise en main |
| **Parcours d'utilisation guidés** (visite interactive pas-à-pas dans l'écran) | Incluse / Générative | Prise en main, autonomie |
| Assistant contextuel en langage naturel (chat sur les données) | Générative | Puissance, exploration |
| Narration de tableaux de bord / synthèses | Générative | Restitution dirigeant |
| Génération de documents (courriers, comptes-rendus) | Générative | Productivité |

## Mise en œuvre

Ces usages sont livrés **progressivement**, module par module, en commençant par l'**IA incluse** (valeur immédiate, coût nul) puis en ajoutant le **génératif** là où il apporte le plus. Chaque nouvel usage est ajouté à cette cartographie avec son niveau, et respecte : droit `ia.assistant.utiliser`, traçabilité au journal d'audit, et (pour le génératif) affichage du coût avant exécution.
