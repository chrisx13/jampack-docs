# Module IA — assistance & crédits

## 1. Principe

JAMPACK intègre une **assistance IA transverse**, disponible sur **l'ensemble du périmètre** (CRM, ventes, achats, stock, comptabilité) et sur **toute action ou opportunité**. Elle est :

- **Optionnelle** — l'ERP fonctionne intégralement sans elle ; toute opération reste faisable manuellement. L'IA ne fait que **proposer**.
- **À la demande + suggestions discrètes** — l'utilisateur déclenche explicitement une aide (bouton « Assistance IA ») ; des suggestions non intrusives (icône/badge) peuvent apparaître mais **ne consomment un crédit que si l'utilisateur les ouvre**.
- **À deux niveaux** — une **IA incluse (sans crédit)** et une **IA générative (facturée aux crédits)** (voir §2 bis).
- **Soumise aux droits** — l'usage de l'IA dépend d'un droit utilisateur (voir §5).
- **Traçée** — chaque appel IA est historisé au journal d'audit avec son coût (voir §6).

## 2. Capacités

| Famille | Exemples sur le périmètre JAMPACK |
|---|---|
| **Assistant contextuel (chat)** | Questions en langage naturel sur la société active : « factures impayées > 30 j », « résume ce client », « pipeline du trimestre ». |
| **Rédaction assistée** | Générer un devis/une facture depuis une description, rédiger e-mails et relances, descriptions d'articles, conditions. |
| **Intelligence CRM** | Scoring d'opportunités, prochaine meilleure action, résumé d'historique client, détection de risques/churn. |
| **Comptabilité & anomalies** | Catégorisation d'écritures, contrôles TVA, détection d'anomalies/doublons, aide au rapprochement. |

Chaque capacité est rendue dans le **contexte de l'écran** (une opportunité, une facture, un relevé…) et propose un résultat que l'utilisateur **accepte, modifie ou ignore**.

## 2 bis. Deux niveaux d'assistance

JAMPACK distingue deux niveaux, pour offrir de la valeur IA **sans coût** dès que possible et réserver les crédits au génératif.

### IA incluse — coût nul, sans crédit

**Critère de classement :** une fonction est « incluse » **uniquement si son coût marginal pour JAMPACK (l'éditeur) est nul**. Ce sont donc des fonctions **gratuites pour le client** qui ne génèrent **aucun coût par appel** pour l'éditeur : **règles métier**, **calculs statistiques**, **modèles locaux / open-source** tournant sur l'infrastructure **déjà provisionnée** (hébergeables en UE). Dès qu'une fonction engendre un coût réel par appel (API/inférence facturée), elle bascule en IA générative (crédits). Exemples d'IA incluse :

- **Contrôles & anomalies** : doublons clients/factures, écarts TVA, IBAN/SIREN invalides, incohérences de montants.
- **Scoring & suggestions par calcul** : score d'opportunité, réappro suggéré, relances à prévoir, meilleures ventes.
- **Catégorisation** par modèle local léger (écritures, articles) et **recherche sémantique** (embeddings locaux).
- **Rapprochement** bancaire assisté par règles.

Ces fonctions sont **activées automatiquement et par défaut, partout où c'est techniquement possible**, **sans consommer de crédit** — elles font partie du socle du produit (valeur immédiate pour le client, coût marginal quasi nul pour l'éditeur). Un compte peut les désactiver, mais elles sont présentes d'origine.

### IA générative — avec crédits

Fonctions s'appuyant sur des **LLM** (rédaction libre, chat contextuel, résumés, génération de documents). Puissantes mais à **coût réel par appel** → **facturées aux crédits** (voir §4) et **fournisseur UE privilégié quand c'est possible**.

Le même bouton « Assistance IA » expose les deux niveaux ; l'interface indique clairement quand une action est **incluse** ou **consomme des crédits** (avec estimation avant lancement).

## 3. Déclenchement & expérience

- **Bouton « Assistance IA »** sur les écrans/records concernés → l'utilisateur voit une **estimation du coût en crédits** avant de lancer, puis le résultat.
- **Suggestions discrètes** : un indicateur signale qu'une aide est disponible ; l'ouvrir déclenche l'appel (et le coût). Rien n'est envoyé à l'IA sans action de l'utilisateur.
- Le résultat n'est jamais appliqué automatiquement : l'utilisateur garde la main (proposer, pas décider).

## 4. Modèle de crédits

Les crédits ne concernent que l'**IA générative** ; l'**IA incluse** est gratuite.

- **Pool de crédits au niveau du compte** + **plafonds paramétrables par utilisateur et/ou par rôle** (évite qu'un seul consomme tout).
- **Coût variable** selon la capacité et la taille du traitement (proportionnel aux jetons consommés), converti en crédits via un **barème** interne. Le coût estimé est affiché **avant** exécution.
- **Décompte** à chaque appel réussi ; un appel refusé (droit, solde, plafond) ne consomme rien.
- **Recharge / allocation** des crédits au niveau du compte (réservée à un droit d'administration).
- **Journal de consommation** immuable (qui, quoi, quand, société, capacité, crédits) — sert au suivi et à la facturation.

## 5. Droits (arbre des droits)

Nouveau module **`ia`** :

| Domaine | Code | Actions |
|---|---|---|
| Assistant IA | `ia.assistant` | **utiliser** |
| Crédits IA | `ia.credits` | **voir** (consommation/solde) · **gérer** (plafonds, recharge) |

L'**IA incluse** requiert uniquement `ia.assistant.utiliser` (aucun crédit). L'**IA générative** requiert `ia.assistant.utiliser` **et** un solde/plafond suffisant. La gestion des crédits et plafonds requiert `ia.credits.gerer` (typiquement l'Administrateur).

## 6. Gouvernance & conformité

- **Traçabilité** : chaque appel IA est enregistré au **journal d'audit** (RG-20) avec le coût en crédits, l'utilisateur, la société, la capacité et un résumé du contexte.
- **RGPD** : fournisseurs **UE privilégiés quand c'est possible** ; à défaut, recours hors-UE encadré (DPA, minimisation/anonymisation des données envoyées, consentement). Aucune donnée envoyée sans action utilisateur.
- **Non-obligatoire & transparent** : coût affiché avant exécution ; l'IA reste un confort, jamais un point de passage obligé.
- **Architecture agnostique** : le fournisseur est **configurable** (Mistral/UE, Azure OpenAI UE, Anthropic/OpenAI sous DPA…) derrière une interface interne unique.

## 7. Modèle de données (esquisse)

- **`AiCreditBalance`** — solde de crédits par compte (et historique de recharges).
- **`AiQuota`** — plafond par utilisateur et/ou par rôle (crédits par période).
- **`AiUsage`** — journal immuable des appels : utilisateur, société, capacité, contexte (référence de l'entité), crédits consommés, horodatage, fournisseur/modèle.

## 8. À définir ensemble (prochaines décisions)

- **Barème crédits ↔ jetons** et prix d'un crédit (modèle économique).
- **Périodicité des plafonds** (mensuel, glissant…) et politique de dépassement (blocage vs alerte).
- **Fournisseur(s)** retenus par capacité et par défaut, et modalités de configuration par compte.
- **Rétention** des prompts/résultats et niveau d'anonymisation.
