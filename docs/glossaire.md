# Glossaire & dictionnaire de données

| Terme | Définition |
|---|---|
| **Compte** (`Organization`) | L'espace client / l'abonnement JAMPACK. Contient une ou plusieurs sociétés, les utilisateurs et les rôles. Frontière d'isolation des données (multi-tenant). |
| **Société** (`Societe`) | Entité juridique gérée dans un compte. La comptabilité et la facturation sont cloisonnées par société (FEC par société). |
| **Utilisateur** (`User`) | Personne authentifiée (via Keycloak/OIDC) ayant accès à un ou plusieurs comptes. |
| **Appartenance** (`Membership`) | Lien d'accès d'un utilisateur à un compte. |
| **Rôle** (`Role`) | Ensemble nommé de permissions, défini au niveau du compte et attribué par société. |
| **Rôle par société** (`SocieteRole`) | Attribution d'un rôle à un utilisateur dans une société donnée. Cumulable : plusieurs rôles possibles par société, différents d'une société à l'autre. |
| **Permission** | Couple action × sujet (ex. `create × Company`) évalué via CASL. |
| **RLS** | Row-Level Security PostgreSQL : isolation des données par compte, garantie par la base. |
| **Client / Tiers** (`Company`) | Société cliente (et/ou fournisseur) gérée dans le CRM. |
| **Établissement** (`Establishment`) | Adresse d'un client (siège, agence, entrepôt), pouvant être adresse de facturation et/ou de livraison. |
| **Opportunité** (`Opportunity`) | Affaire commerciale suivie dans le pipeline. |
| **Article** (`Product`) | Bien ou service du catalogue, avec prix HT et taux de TVA. |
| **Taux de TVA** (`TaxRate`) | Taux de taxe paramétrable (20 %, 10 %, 5,5 %, 2,1 %, 0 %). |
| **Numérotation** (`NumberSequence`) | Séquence de numéros de pièces par société et par type de document, attribués de façon atomique. |
| **Facture** (`Invoice`) | Pièce de vente ; passe de brouillon à validée (avec numéro) puis payée. |
| **Factur-X** | Format français/européen de facture électronique (PDF/A-3 + XML). |
| **PDP** | Plateforme de Dématérialisation Partenaire, agréée pour l'échange de factures électroniques. |
| **FEC** | Fichier des Écritures Comptables, exigé par l'administration fiscale française. |
| **Actif / Inactif (archivage)** | Statut de tout enregistrement de l'ERP. Rien n'est supprimé physiquement : on **désactive/archive**. Un enregistrement inactif est masqué par défaut et non réutilisable, mais conservé pour l'historique et l'audit. |
| **Journal d'audit (historisation)** | Enregistrement inaltérable de toute action (qui / quoi / quand / société, valeurs avant-après). Ni modifiable ni effaçable ; base de la traçabilité et des obligations légales. |
