# Développer JAMPACK avec VS Code

Ce guide décrit, pas à pas, comment récupérer le dépôt, ouvrir le projet dans
Visual Studio Code et lancer JAMPACK en local — en mode **tout Docker**
(le plus simple) ou en mode **dev hot-reload**. Il couvre aussi les extensions
recommandées, le workflow Prisma / base de données et le débogage.

!!! info "À qui s'adresse ce guide"
    Développeur qui reprend le dépôt `jampack` sur une machine neuve.
    Aucune connaissance préalable du monorepo n'est supposée.

## 1. Prérequis

À installer une fois sur la machine :

| Outil | Version | Pourquoi |
| --- | --- | --- |
| **Node.js** | ≥ 20 (LTS) | exécution TypeScript / outillage |
| **pnpm** | 9.x | gestionnaire de paquets du monorepo |
| **Docker Desktop** | récent | PostgreSQL (et la stack complète) |
| **Git** | récent | clonage / commits |
| **VS Code** | récent | l'éditeur |

Installer **pnpm** sous Windows (sans droits admin) :

```powershell
npm install -g pnpm@9
pnpm -v   # doit afficher 9.x
```

!!! warning "OneDrive"
    Ne pas cloner le dépôt dans un dossier synchronisé OneDrive : la synchro
    peut corrompre `.git` et fait tourner en boucle `node_modules`.
    Cloner plutôt hors OneDrive, par exemple `D:\Dev\jampack`.

## 2. Cloner et ouvrir dans VS Code

```bash
git clone https://github.com/chrisx13/jampack.git
cd jampack
code .
```

À la première ouverture, VS Code détecte le fichier `.vscode/extensions.json`
et propose d'installer les **extensions recommandées** — accepter. Les
principales :

- **ESLint** et **Prettier** — lint + formatage automatique à la sauvegarde ;
- **Prisma** — coloration et autocomplétion du schéma `schema.prisma` ;
- **Docker** — piloter les conteneurs depuis la barre latérale ;
- **Error Lens** et **Pretty TS Errors** — erreurs lisibles, affichées en ligne ;
- **Code Spell Checker (FR)** — correcteur orthographique français.

Le dépôt fournit aussi un `.vscode/settings.json` (format à la sauvegarde,
correction ESLint automatique, exclusion de `node_modules` / `dist` / `.turbo`
de la recherche) : rien à configurer côté éditeur.

## 3. Lancer JAMPACK — option A : tout en Docker (recommandé)

Une seule commande démarre PostgreSQL, l'API (migrations + RLS + rôle applicatif
+ seed automatiques), Keycloak et le web :

```bash
docker compose up --build
```

| Service | URL |
| --- | --- |
| Web | <http://localhost:5173> |
| API (tRPC) | <http://localhost:3000/trpc> |
| Keycloak | <http://localhost:8080> (admin / admin) |

Connexion de démonstration : **admin@demo.fr / admin** (Admin + Comptable sur la
Boulangerie, Commercial sur le Studio) ou **compta@demo.fr / compta**.

Pour tout arrêter : `docker compose down` (ajouter `-v` pour effacer aussi la
base de données).

Depuis VS Code, la même commande est disponible via **Terminal ▸ Exécuter la
tâche… ▸ JAMPACK ▸ Stack complète (Docker)**.

## 4. Lancer JAMPACK — option B : mode dev (hot-reload)

Idéal pour développer : le front et l'API se rechargent à chaque modification.
On ne lance en Docker que PostgreSQL ; l'authentification passe en repli dev
(pas de login Keycloak requis).

```bash
pnpm install
docker compose -f docker/docker-compose.yml up -d          # Postgres seul
cp .env.example .env
pnpm --filter @jampack/db exec prisma migrate dev --name init
pnpm db:rls        # active le Row-Level Security
pnpm db:seed       # compte démo + 2 sociétés + CRM
pnpm dev           # API :3000 + Web :5173 (hot-reload)
```

Ces étapes correspondent aux tâches VS Code préconfigurées (**Terminal ▸
Exécuter la tâche…**) :

- *JAMPACK ▸ Installer les dépendances*
- *JAMPACK ▸ Base de données (Docker, Postgres seul)*
- *JAMPACK ▸ Seed + RLS*
- *JAMPACK ▸ Dev (API :3000 + Web :5173)*

Le serveur de dev web (Vite, port **5173**) proxie automatiquement `/trpc` vers
l'API sur le port **3000** — pas de configuration CORS à gérer.

## 5. Workflow base de données (Prisma)

Le schéma vit dans `packages/db/prisma/schema.prisma`. Après l'avoir modifié :

```bash
# Crée une migration et régénère le client Prisma
pnpm --filter @jampack/db exec prisma migrate dev --name ma_modif

# Réappliquer les policies RLS et les droits après un reset de la base
pnpm db:rls

# Repeupler les données de démonstration
pnpm db:seed
```

!!! note "Reset complet"
    Après un `prisma migrate reset`, la base est vidée **et** les policies RLS
    et le rôle applicatif `jampack_app` sont perdus : relancer `pnpm db:rls`
    puis `pnpm db:seed`. Le setup Docker (option A) refait tout cela
    automatiquement à chaque démarrage.

L'extension **Prisma** de VS Code formate le schéma (clic droit ▸ *Format
Document*) et signale les erreurs de modèle en direct.

## 6. Déboguer

**Front React** — lancer d'abord `pnpm dev`, puis la configuration de débogage
**« Web (Chrome) — front React »** (menu *Exécuter et déboguer*, `F5`). Chrome
s'ouvre sur `http://localhost:5173` et les points d'arrêt dans `apps/web/src`
sont actifs.

**API NestJS / tRPC** — l'API tourne sous `tsx`. Le plus simple est le
**JavaScript Debug Terminal** (palette `Ctrl+Shift+P` ▸ *Debug: JavaScript Debug
Terminal*) : y lancer `pnpm --filter @jampack/api dev` ; VS Code attache
automatiquement le débogueur et respecte les points d'arrêt côté serveur.

Pour inspecter la base, l'option dev expose **Adminer** sur
<http://localhost:8080> (serveur `db`, utilisateur `jampack` / `jampack`).

## 7. Vérifier avant de committer

```bash
pnpm typecheck   # vérifie les types sur tout le monorepo
pnpm lint        # ESLint
```

Ces deux commandes sont aussi disponibles en tâches VS Code (*JAMPACK ▸
Typecheck*, *JAMPACK ▸ Lint*). Le formatage Prettier s'applique déjà à chaque
sauvegarde.

## 8. Aide-mémoire des commandes

| Besoin | Commande |
| --- | --- |
| Tout lancer (Docker) | `docker compose up --build` |
| Postgres seul | `docker compose -f docker/docker-compose.yml up -d` |
| Installer les paquets | `pnpm install` |
| Dev hot-reload | `pnpm dev` |
| Migration Prisma | `pnpm --filter @jampack/db exec prisma migrate dev` |
| RLS + seed | `pnpm db:rls && pnpm db:seed` |
| Types | `pnpm typecheck` |
| Lint | `pnpm lint` |

## 9. Problèmes courants

**`pnpm` non reconnu (Windows)** — installer via `npm install -g pnpm@9`
(écrit dans `%AppData%\npm`, sans droits admin). Éviter `corepack enable` si
Node est dans `C:\Program Files\nodejs` : il échoue en `EPERM`.

**Port déjà utilisé** — un `docker compose` précédent tourne encore : faire
`docker compose down`, ou vérifier ce qui occupe les ports 5173 / 3000 / 5432.

**Erreurs de types Prisma après modification du schéma** — le client généré est
périmé : relancer `prisma migrate dev` (ou `prisma generate`), puis recharger la
fenêtre VS Code (`Ctrl+Shift+P` ▸ *Developer: Reload Window*).

**Le RLS ne filtre plus après un reset** — relancer `pnpm db:rls` puis
`pnpm db:seed`.
