# Connecteurs & intégrations

## 1. Principe : ouverture maximale

JAMPACK vise, **de manière absolue, le maximum de connecteurs vers tous les outils pertinents de l'écosystème d'un ERP**. L'ouverture est un objectif produit central : un ERP n'a de valeur que connecté au reste des outils de l'entreprise. La stratégie combine des **connecteurs natifs** (fournisseurs majeurs), un **socle d'ouverture** (API + webhooks) et la **compatibilité iPaaS** pour couvrir la longue traîne. Priorité aux **standards ouverts** et aux **fournisseurs UE** (RGPD).

## 2. Socle d'ouverture (ce qui rend « le maximum » possible)

- **API publique REST** documentée (OpenAPI) — toute donnée/action accessible selon les droits.
- **Webhooks** (événements sortants) pour réagir en temps réel dans les outils tiers.
- **Architecture par adaptateurs** : une interface interne unique par famille (messagerie, drive, banque…) ; ajouter un fournisseur = ajouter un adaptateur, sans toucher au métier.
- **Compatibilité iPaaS** (Zapier / Make / n8n) : atteindre des milliers d'applications à faible coût.
- **Import / export** de fichiers (CSV, Excel/ODS) universels.
- **Marketplace de connecteurs** (cible) : activation/configuration par compte.

## 3. Catalogue des connecteurs (domaine ERP)

| Catégorie | Exemples de cibles | Priorité |
|---|---|---|
| **Bureautique** | Microsoft Office (Word/Excel), LibreOffice (Writer/Calc), OpenXML + ODF, PDF | P0/P1 |
| **Messagerie** | Microsoft 365/Outlook (Graph), Google Workspace/Gmail, SMTP/IMAP générique | P0/P1 |
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
| **Collaboration** | Slack, Microsoft Teams | P2 |
| **BI / données** | Power BI, Google Sheets, entrepôt de données | P2 |
| **Transporteurs** | Colissimo, Chronopost, UPS | P2 |
| **Administrations FR** | SIRENE/INSEE, VIES (TVA intracom), Chorus Pro | P1 |
| **Automatisation (iPaaS)** | Zapier, Make, n8n | P1 |

*(Liste non exhaustive : la cartographie s'étend au fil des besoins ; l'API + iPaaS couvrent les outils non listés.)*

## 4. Familles prioritaires — détail

### Bureautique (Office & LibreOffice)
Génération devis/factures/états en `.docx`/`.odt`/`.xlsx`/`.ods`/PDF via **LibreOffice headless** (coût nul) ; **modèles éditables** + publipostage ; **import** Excel/Calc/CSV ; add-ins (ultérieur).

### Messagerie
Envoi de pièces et **relances** (Microsoft 365/Graph, Gmail API, **SMTP/IMAP** générique) ; **modèles d'e-mails** ; **journalisation** des échanges dans le CRM (IMAP/API ou BCC dropbox) ; notifications transactionnelles.

### Stockage / Drive
Archivage automatique des pièces et **GED** (rattachement de fichiers) sur OneDrive/SharePoint, Google Drive, Dropbox, **Nextcloud** (UE), WebDAV/S3 — via un **adaptateur de stockage** unique, en OAuth.

## 5. Gouvernance

Connexions **OAuth/OIDC**, secrets chiffrés ; chaque opération de connecteur respecte les **droits** du module concerné et est **tracée** au journal d'audit ; **résidence UE privilégiée** ; le client garde ses données chez ses fournisseurs.

## 6. Positionnement roadmap

Socle **API + webhooks + import/export** dès que possible (débloque tout le reste), puis connecteurs **P0/P1** (bureautique, messagerie, e-invoicing/PDP, banque, paiement, signature, administrations FR), puis élargissement continu (e-commerce, RH, BI, transporteurs…) et **iPaaS** pour la longue traîne.
