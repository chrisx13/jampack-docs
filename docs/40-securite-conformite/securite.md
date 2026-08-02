# Sécurité, habilitation & gouvernance des données

## 1. Authentification

Authentification déléguée à **Keycloak** (OpenID Connect, auto-hébergé UE). L'application ne stocke aucun mot de passe : l'API valide chaque jeton (signature via JWKS, `issuer` + `audience`), le web utilise le flux **Authorization Code + PKCE**. Un utilisateur est **identifié par son adresse e-mail** (unique). Un utilisateur **inactif** ne peut pas se connecter.

## 2. Modèle d'habilitation

La hiérarchie des droits est **Rôle ▸ Module ▸ Domaine ▸ Action** (le rôle au sommet), avec pour actions standard **voir / créer / modifier**. Un droit s'écrit `module.domaine.action`. Chaque action sensible est **contrôlée côté serveur** ; l'interface masque en plus ce qui n'est pas autorisé. Voir le *Modèle d'habilitation* pour la matrice complète.

Les rôles sont **prédéfinis** (Administrateur, Stock, Facturation, Comptable, Commercial, Lecture seule…), **duplicables** et **personnalisables**. Ils sont attribués **par société** et **cumulables** ; les droits effectifs sont l'**union** des rôles de l'utilisateur dans la société active. Un administrateur gère les rôles (voir/créer/modifier + actif/inactif). **Invariant** : au moins un administrateur actif est toujours présent.

## 3. Isolation multi-tenant (RLS)

Isolation par compte via **Row-Level Security PostgreSQL** : chaque requête positionne `app.current_org` (helper `withTenant`) et les policies filtrent chaque table. L'API s'exécute avec un rôle SQL **non-propriétaire** pour que le RLS s'applique réellement. La société active est un filtre applicatif au-dessus de cette isolation.

## 4. Gouvernance des données

- **Aucune suppression physique** (`RG-19`, `SRS-NF-DATA-1`) : tout enregistrement est **actif/inactif (archivé)**, conservé avec son historique.
- **Traçabilité totale** (`RG-20`, `SRS-NF-AUD-1`) : toute action est **historisée** dans un **journal d'audit inaltérable** (qui, quoi, avant/après, quand, quelle société).

## 5. Paramétrage

Deux espaces : **paramètres globaux** (soumis à permission) et **paramètres utilisateur** (avatar, téléphone, nom… modifiables librement par chacun, sans toucher à ses rôles ni à son statut).

## 6. Conformité française

- **RGPD** : hébergement UE, consentement, droit à l'effacement des données personnelles.
- **Facturation électronique** : émission/réception via **PDP agréée**, format **Factur-X** (échéances 2026-2027).
- **Comptabilité** : production du **FEC** ; numérotation des pièces séquentielle et insécable, par société.
