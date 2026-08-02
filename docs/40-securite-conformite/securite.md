# Sécurité, habilitation & gouvernance des données

## 1. Authentification

Authentification déléguée à **Keycloak** (OpenID Connect, auto-hébergé UE). L'application ne stocke aucun mot de passe : l'API valide chaque jeton (signature via JWKS, `issuer` + `audience`), le web utilise le flux **Authorization Code + PKCE**. Un utilisateur est **identifié par son adresse e-mail** (unique). Un utilisateur **inactif** ne peut pas se connecter.

## 2. Modèle d'habilitation

La hiérarchie des droits est **Rôle ▸ Module ▸ Domaine ▸ Action** (le rôle au sommet), avec pour actions standard **voir / créer / modifier**. Un droit s'écrit `module.domaine.action`. Chaque action sensible est **contrôlée côté serveur** ; l'interface masque en plus ce qui n'est pas autorisé. Voir le *Modèle d'habilitation* pour la matrice complète.

Les rôles sont **prédéfinis** (Administrateur, Stock, Facturation, Comptable, Commercial, Lecture seule…), **duplicables** et **personnalisables**. Ils sont attribués **par société** et **cumulables** ; les droits effectifs sont l'**union** des rôles de l'utilisateur dans la société active. Un administrateur gère les rôles (voir/créer/modifier + actif/inactif). **Invariant** : au moins un administrateur actif est toujours présent.

## 3. Isolation multi-tenant (RLS) — deux niveaux

L'isolation repose sur le **Row-Level Security PostgreSQL** et s'applique à **deux niveaux**. L'API s'exécute avec un rôle SQL **non-propriétaire** (`jampack_app`) pour que le RLS s'applique réellement (le propriétaire des tables le contournerait).

Au niveau **compte**, une policy **permissive** `org_isolation` filtre chaque table sur `app.current_org` : aucune donnée d'un compte n'est atteignable depuis un autre — isolation **totale, garantie en base**.

Au niveau **société** (indépendance renforcée entre sociétés d'un même compte), une policy **restrictive** `societe_isolation` filtre sur `app.current_societe` les tables métier portant une société (clients, contacts, opportunités, activités, établissements, produits, numérotation, factures). Étant *restrictive*, elle est **ANDée** avec l'isolation compte : deux sociétés d'un même compte sont donc **étanches en base**, pas seulement par filtrage applicatif. Le helper `withTenant(org, societeId, …)` positionne les deux variables ; `app.current_societe` **absent** = **vue consolidée** (toutes les sociétés du compte accessibles à l'utilisateur), réservée à la restitution transverse.

Restent **mutualisés au niveau compte** (choix « indépendance renforcée », pas « comptes séparés ») : l'annuaire des utilisateurs, les définitions de rôles, et les référentiels partagés (TVA, étapes de pipeline). L'isolation est **vérifiée automatiquement** (`scripts/verify-rls.sh`, en rôle non-propriétaire).

## 4. Gouvernance des données

- **Aucune suppression physique** (`RG-19`, `SRS-NF-DATA-1`) : tout enregistrement est **actif/inactif (archivé)**, conservé avec son historique.
- **Traçabilité totale** (`RG-20`, `SRS-NF-AUD-1`) : toute action est **historisée** dans un **journal d'audit inaltérable** (qui, quoi, avant/après, quand, quelle société).

## 5. Paramétrage

Deux espaces : **paramètres globaux** (soumis à permission) et **paramètres utilisateur** (avatar, téléphone, nom… modifiables librement par chacun, sans toucher à ses rôles ni à son statut).

## 6. Conformité française

- **RGPD** : hébergement UE, consentement, droit à l'effacement des données personnelles.
- **Facturation électronique** : émission/réception via **PDP agréée**, format **Factur-X** (échéances 2026-2027).
- **Comptabilité** : production du **FEC** ; numérotation des pièces séquentielle et insécable, par société.
