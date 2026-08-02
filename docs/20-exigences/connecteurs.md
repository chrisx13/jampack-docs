# Connecteurs & intégrations

## 1. Principe : ouverture maximale

JAMPACK vise, **de manière absolue, le maximum de connecteurs vers tous les outils pertinents de l'écosystème d'un ERP**. L'ouverture est un objectif produit central : un ERP n'a de valeur que connecté au reste des outils de l'entreprise. La stratégie combine des **connecteurs natifs** (fournisseurs majeurs), un **socle d'ouverture** (API + webhooks) et la **compatibilité iPaaS** pour couvrir la longue traîne. Priorité aux **standards ouverts** et aux **fournisseurs UE** (RGPD).

## 2. Socle d'ouverture (ce qui rend « le maximum » possible)

- **API publique REST** documentée (OpenAPI) — toute donnée/action accessible selon les droits.
- **Webhooks** (événements sortants) pour réagir en temps réel dans les outils tiers.
- **Architecture par adaptateurs** : une interface interne unique par famille (messagerie, drive, banque…) ; ajouter un fournisseur = ajouter un adaptateur, sans toucher au métier.
- **Compatibilité iPaaS** (Zapier / Make / n8n) : atteindre des milliers d'applications à faible coût.
- **Import / export** de fichiers (CSV, Excel/ODS) universels.
- **Moteur de modèles & champs de fusion** : un moteur **unique** pour les documents (bureautique) **et** les messages (e-mail, messagerie instantanée) ; les **champs de fusion** sont **auto-remplis** depuis les données de l'ERP (tiers, contact, pièce, société, utilisateur, lien de paiement…).
- **Marketplace de connecteurs** (cible) : activation/configuration par compte.

## 3. Catalogue des connecteurs (domaine ERP)

| Catégorie | Exemples de cibles | Priorité |
|---|---|---|
| **Bureautique** | Microsoft Office (Word/Excel), LibreOffice (Writer/Calc), OpenXML + ODF, PDF | P0/P1 |
| **Messagerie e-mail** | Microsoft 365/Outlook (Graph), Google Workspace/Gmail, SMTP/IMAP générique | P0/P1 |
| **Messagerie instantanée & conversationnelle** | WhatsApp Business (Cloud API), Slack, Microsoft Teams, Telegram, Signal, Facebook Messenger, SMS/RCS (Twilio, OVHcloud, Brevo…), notifications push | P1/P2 |
| **Stockage / Drive** | OneDrive/SharePoint, Google Drive, Dropbox, Nextcloud, WebDAV, S3 | P1 |
| **Banque (agrégation DSP2)** | Powens (ex-Budget Insight), Bridge, GoCardless, relevés OFX/CSV | P1 |
| **Paiement en ligne** | Stripe, GoCardless (SEPA), Mollie, PayPal | P1 |
| **Facturation électronique** | PDP agréées, Chorus Pro (secteur public) | P0 |
| **Comptabilité / expert-comptable** | Export FEC, Pennylane, Sage, Cegid, QuickBooks | P1 |
| **Paie / RH** | PayFit, Silae | P2 |
| **E-commerce** | Shopify, WooCommerce, PrestaShop, Magento | P2 |
| **CRM / marketing** | Brevo (Sendinblue), Mailchimp, HubSpot | P2 |
| **Signature électronique** | Yousign (FR), DocuSign | P1 |
| **Calendriers** | Google Calendar, Outlook, CalDAV | P2 |
| **Espaces collaboratifs & visio** | Slack, Microsoft Teams, Zoom, Google Meet (partage de pièces, liens de réunion) | P2 |
| **BI / données** | Power BI, Google Sheets, entrepôt de données | P2 |
| **Transporteurs** | Colissimo, Chronopost, UPS | P2 |
| **Administrations FR** | SIRENE/INSEE, VIES (TVA intracom), Chorus Pro | P1 |
| **Automatisation (iPaaS)** | Zapier, Make, n8n | P1 |

*(Liste non exhaustive : la cartographie s'étend au fil des besoins ; l'API + iPaaS couvrent les outils non listés.)*

## 4. Familles prioritaires — détail

### Bureautique (Office & LibreOffice)
Génération devis/factures/états en `.docx`/`.odt`/`.xlsx`/`.ods`/PDF via **LibreOffice headless** (coût nul). **Gestion des modèles** : bibliothèque de modèles éditables (Word/Writer, Excel/Calc) avec **champs de fusion automatiques** remplis depuis les données de l'ERP (tiers, pièce, lignes, société, utilisateur) ; **publipostage** en masse ; prévisualisation avant génération ; **import** Excel/Calc/CSV ; add-ins (ultérieur). Voir *Modèles & champs de fusion*.

### Messagerie e-mail
Envoi de pièces et **relances** (Microsoft 365/Graph, Gmail API, **SMTP/IMAP** générique) ; **modèles d'e-mails à champs de fusion** ; **journalisation** des échanges dans le CRM (IMAP/API ou BCC dropbox) ; notifications transactionnelles.

### Communication instantanée & conversationnelle
Émission de **notifications, relances et messages** vers les canaux conversationnels : **WhatsApp Business** (Cloud API, modèles de messages validés), **Slack** et **Microsoft Teams** (webhooks entrants + bots/DM), **Telegram**, **Signal**, **Facebook Messenger**, **SMS/RCS** (Twilio, OVHcloud, Brevo…) et **push**. Mêmes **modèles à champs de fusion** que l'e-mail — un contenu, plusieurs canaux. Chaque envoi respecte le **consentement/opt-in** du destinataire, est **soumis aux droits** et **journalisé** au journal d'audit ; les **réponses** peuvent être récupérées (webhooks entrants) et journalisées dans le CRM.

### Stockage / Drive
Archivage automatique des pièces et **GED** (rattachement de fichiers) sur OneDrive/SharePoint, Google Drive, Dropbox, **Nextcloud** (UE), WebDAV/S3 — via un **adaptateur de stockage** unique, en OAuth.

## 5. Modèles & champs de fusion

Un **moteur de modèles unique** alimente les **documents** (bureautique) **et** les **messages** (e-mail, WhatsApp, Slack, Teams, SMS…). Principes :

- **Bibliothèque de modèles** par société et par type (devis, facture, avoir, relance, accusé de réception, message de bienvenue…), **versionnés** et jamais supprimés (actif/inactif).
- **Champs de fusion** insérables (ex. `{{tiers.raison_sociale}}`, `{{facture.numero}}`, `{{facture.total_ttc}}`, `{{echeance.date}}`, `{{lien_paiement}}`, `{{utilisateur.nom}}`, `{{societe.iban}}`), **auto-remplis** depuis les données de l'ERP au moment de la génération / l'envoi.
- **Boucles & sections conditionnelles** (lignes de pièce, articles, mentions selon TVA/pays).
- **Multicanal** : un même modèle logique décliné en document PDF/Word/ODT **ou** en message court (WhatsApp/SMS) — le moteur adapte le rendu au canal.
- **Prévisualisation obligatoire** avant génération ou envoi (données réelles fusionnées).
- **Gouvernance** : création/modification des modèles **soumise à un droit** de paramétrage ; chaque génération/envoi est **tracé** (modèle, canal, destinataire) au journal d'audit.
- **IA incluse** (coût nul) suggère des formulations ; **IA générative** (crédits) peut rédiger un modèle — jamais imposé.

## 6. Gouvernance

Connexions **OAuth/OIDC**, secrets chiffrés ; chaque opération de connecteur respecte les **droits** du module concerné et est **tracée** au journal d'audit ; **résidence UE privilégiée** ; le client garde ses données chez ses fournisseurs. Les envois de **communication** respectent en outre le **consentement/opt-in** des destinataires (RGPD, règles propres à WhatsApp / e-mail / SMS).

## 7. Positionnement roadmap

Socle **API + webhooks + import/export + moteur de modèles/champs de fusion** dès que possible (débloque tout le reste), puis connecteurs **P0/P1** (bureautique, messagerie e-mail, e-invoicing/PDP, banque, paiement, signature, administrations FR), puis **messagerie conversationnelle** (WhatsApp/Slack/Teams/SMS) et élargissement continu (e-commerce, RH, BI, transporteurs…) et **iPaaS** pour la longue traîne.
