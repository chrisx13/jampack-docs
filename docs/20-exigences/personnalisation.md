# Personnalisation & champs personnalisés

JAMPACK doit pouvoir s'**adapter à chaque métier sans développement**. La personnalisation se décline en **deux niveaux distincts**, à ne pas confondre, et **toujours soumis aux droits** :

| Niveau | Qui | Quoi | Portée | Droit |
|---|---|---|---|---|
| **Personnalisation de l'affichage** | Chaque **utilisateur** | Adapter la présentation des écrans/fiches à son goût | **Personnelle** (n'affecte que lui) | Self-service (paramètres utilisateur, RG-11) |
| **Vues génériques (modèles)** | **Administrateur** / paramétrage | Créer des **vues partagées** (colonnes, tri, filtres, mise en page) | **Partagée** (compte ou **par rôle**) | Soumis à un **droit de paramétrage** |
| **Champs personnalisés** | **Administrateur** / paramétrage | Créer de **nouveaux champs** sur un domaine (structure de données) | **Partagée** (tout le compte) | Soumis à un **droit de paramétrage** |

Le premier touche **comment on voit** les données ; le second touche **quelles données existent**.

> **Simplicité d'abord.** Toutes ces possibilités sont **optionnelles** et n'existent que si on les active. Par défaut, JAMPACK reste **simple et prêt à l'emploi** : les écrans standard suffisent, les champs et vues supplémentaires n'apparaissent que lorsqu'on les crée. La personnalisation est un **plus**, jamais un prérequis.

## 1. Personnalisation de l'affichage (par utilisateur)

Chaque utilisateur peut mettre l'ERP **à son goût**, sans impacter les autres ni les données. Par exemple, régler la liste des tiers du CRM, l'ordre des blocs d'une fiche contact, etc.

Réglages personnels possibles :

- **Colonnes des listes** : lesquelles afficher/masquer, leur **ordre** et leur **largeur**.
- **Tri, regroupement et filtres** par défaut ; **vues enregistrées** (« Mes vues » : ex. « Mes clients actifs », « Prospects à relancer »).
- **Mise en page des fiches** : ordre et **repli des sections**, densité d'affichage.
- **Tableau de bord / page d'accueil** : **onglet épinglé toujours présent** (non fermable), avec des **marqueurs / indicateurs paramétrables** (widgets, KPI, raccourcis, tâches, échéances) — choix et disposition par l'utilisateur. Voir le *modèle de navigation type VS Code* (charte front).
- **Favoris / épingles** et raccourcis.

Principes :

- **Strictement personnel** : ne modifie **aucune donnée** et n'a **aucun effet** sur les autres utilisateurs.
- **Ne contourne jamais les droits** : un utilisateur ne peut afficher que des **champs et des données qu'il est autorisé à voir**. La personnalisation réorganise l'autorisé, elle n'élargit rien.
- **Réversible** : bouton « **Revenir à la vue par défaut** » à tout moment.
- Part d'une **vue par défaut** ou d'une **vue générique** définie par l'administration (voir ci-dessous).

### Vues génériques créées par l'administration

Au-delà des vues personnelles, l'**administration peut créer des vues de manière générique** — de véritables **modèles de vues** (colonnes affichées et ordre, tri, filtres, regroupements, mise en page de fiche) — et les **mettre à disposition de tous** ou **par rôle**.

- Elles servent de **vue par défaut** et de **point de départ** : chaque utilisateur peut ensuite les **personnaliser pour lui-même** (sans altérer la vue partagée) ou **y revenir** d'un clic.
- Créer / modifier une **vue générique** est **soumis à un droit de paramétrage** ; une **vue personnelle** reste self-service.
- Comme partout, une vue générique **ne montre à chacun que les données et les champs qu'il a le droit de voir** — elle organise l'affichage, elle n'élargit aucun droit.
- Les vues génériques ne sont **jamais supprimées** (actif/inactif, RG-19) et leur gestion est **tracée** (RG-20).

## 2. Champs personnalisés (par l'administrateur, sur un domaine)

L'administrateur (ou tout utilisateur disposant du droit de paramétrage) peut **créer de nouveaux champs** dans un **domaine précis** — par exemple ajouter un champ sur la **table Contact**, sur les tiers, les articles, les factures, les projets, etc. Ces champs deviennent des **champs de premier rang**, exploités comme les champs natifs.

### 2.1 Types de champs

Un champ personnalisé peut être de **toute nature** :

| Type | Exemples d'usage |
|---|---|
| **Texte court** (une ligne) | Référence interne, code |
| **Texte long / riche** (multi-lignes) | Notes, description |
| **Nombre entier** | Quantité, effectif |
| **Nombre décimal** | Mesure, coefficient |
| **Montant / monétaire** (avec devise) | Budget, plafond |
| **Pourcentage** | Taux, marge |
| **Booléen** (oui/non, case à cocher) | VIP, sous contrat |
| **Date** / **Date & heure** | Échéance, dernier contact |
| **Téléphone** | Ligne directe, mobile |
| **E-mail** | Contact secondaire |
| **URL / lien web** | Site, profil |
| **Liste de choix** (valeur unique) | Segment, catégorie |
| **Liste à choix multiples** (étiquettes) | Centres d'intérêt |
| **Relation / référentiel** (lien vers un autre objet) | Commercial référent, article lié |
| **Fichier / pièce jointe** | Contrat scanné |
| **Adresse structurée** | Adresse complémentaire |
| **Champ calculé / formule** (avancé) | Valeur dérivée |

*(Liste extensible : de nouveaux types peuvent être ajoutés ultérieurement.)*

### 2.2 Propriétés d'un champ

À la création, l'administrateur définit : **libellé**, **code technique** (`module.domaine.champ`), **type** et ses paramètres (longueur, min/max, décimales, devise, options de liste, objet cible d'une relation), **obligatoire ou non**, **valeur par défaut**, **unicité**, **texte d'aide**, **section et position** dans la fiche, et **visibilité conditionnelle** (ultérieur). La **validation** est automatique selon le type (ex. format e-mail/téléphone, bornes numériques).

### 2.3 Où les champs personnalisés apparaissent

Une fois créés, ils sont exploitables **partout** comme les champs natifs :

- **Fiches** (saisie/consultation) et **sections** dédiées.
- **Listes / colonnes**, **filtres** et **recherche**.
- **Import / export** (CSV-Excel).
- **Modèles à champs de fusion** (documents et messages) — ex. `{{contact.champ_perso.n_importe_quoi}}`.
- **Automatisations**, **rapports** et **tableaux de bord**.
- **API publique & webhooks**.

### 2.4 Portée & cloisonnement

Les **définitions** de champs sont posées au **niveau du compte** et s'appliquent à l'objet dans **toutes les sociétés** (option de restreindre à certaines sociétés — ultérieur). Les **valeurs** saisies restent **cloisonnées par société** (isolation RLS), exactement comme les données natives.

## 3. Gouvernance — toujours soumis aux droits (et tracé)

- **Créer / modifier une définition** de champ personnalisé (ou une vue par défaut) est **soumis à un droit de paramétrage** (`parametres.personnalisation.creer` / `.modifier` / `.voir`).
- La **visibilité et l'édition d'un champ** (perso comme natif) suivent les **droits du domaine** (`voir` / `créer` / `modifier`) — un champ peut donc être restreint à certains rôles.
- **Aucune suppression physique** : un champ personnalisé se **désactive / archive** (RG-19) ; ses **valeurs historiques sont conservées**. Les définitions sont **versionnées**.
- **Traçabilité** : la création/modification d'une définition **et** la saisie/modification d'une valeur sont **journalisées** au journal d'audit inaltérable (RG-20).
- **IA incluse** (coût nul) peut proposer un type ou des options de liste ; elle ne crée jamais un champ seule.

## 4. Note d'implémentation (indicative)

Stockage recommandé des valeurs personnalisées en colonne **`JSONB` indexable** par entité (souple, performant, requêtable) plutôt qu'un modèle EAV ; les **définitions** dans une table dédiée (objet, code, type, paramètres, droits, statut, version). Le rendu des fiches/listes est **piloté par métadonnées** (definition-driven UI), ce qui permet d'exposer les champs partout sans code spécifique. Détails dans l'*Architecture technique*.
