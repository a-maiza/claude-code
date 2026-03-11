# Analyse de fichiers et implémentation full-stack avec Claude Code

Guide pratique pour analyser un codebase existant et implémenter des fonctionnalités complètes couvrant backend et frontend avec Claude Code.

---

## Table des matières

- [Analyse de fichiers](#analyse-de-fichiers)
  - [Concepts clés](#concepts-clés)
  - [Cas d'usage](#cas-dusage)
  - [Analyser un flux fonctionnel](#analyser-un-flux-fonctionnel)
  - [Analyser les dépendances](#analyser-les-dépendances)
- [Implémentation d'une fonctionnalité full-stack](#implémentation-dune-fonctionnalité-full-stack)
  - [Concepts clés](#concepts-clés-1)
  - [Implémentation côté backend](#implémentation-côté-backend)
  - [Intégration côté frontend](#intégration-côté-frontend)
  - [Ajustement et amélioration](#ajustement-et-amélioration)
- [Points à retenir](#points-à-retenir)

---

## Analyse de fichiers

### Concepts clés

| Concept | Description |
|---|---|
| **File Analysis** | Analyse des relations entre fichiers d'un projet |
| **Flow Analysis** | Suivi du chemin d'une requête ou d'une donnée à travers le système |
| **Dependency Analysis** | Identification des fichiers ou modules qui dépendent d'un composant donné |
| **Plan Mode** | Mode recommandé pour analyser le code sans modifier les fichiers |

### Cas d'usage

L'analyse de fichiers est particulièrement utile pour :

- Comprendre un codebase existant
- Former un nouveau développeur
- Effectuer une revue de code
- Préparer un refactoring
- Diagnostiquer des problèmes dans le flux de données

Au lieu de lire chaque fichier manuellement, Claude peut analyser plusieurs fichiers simultanément et **reconstituer la logique complète d'une fonctionnalité**.

### Analyser un flux fonctionnel

Claude peut suivre le chemin complet d'une requête à travers le système :

```
1. Requête du client
2. Route backend
3. Logique métier
4. Accès à la base de données
5. Réponse renvoyée au client
```

**Méthode :**

1. Demander à Claude d'identifier les fichiers concernés
2. Tracer le flux de données entre ces fichiers
3. Décrire chaque étape du processus
4. Générer une documentation ou un diagramme du flux

**Exemple de prompt :**

```text
We have a new developer joining the team, and I'd like to walk them through the
authentication process. Could you analyze the authentication flow across all related
files and trace how a login request moves from the route handler to the database
and back to the response? Please include all the files involved.
```

Claude peut produire un document (ex. `AUTH_FLOW`) contenant les fichiers impliqués, les étapes du processus et un diagramme de flux.

### Analyser les dépendances

Lors d'un refactoring, il est essentiel de savoir **quels composants dépendent d'un module spécifique** pour anticiper l'impact d'une modification.

Claude peut :

- Identifier tous les fichiers qui importent un module
- Analyser les dépendances indirectes
- Produire un arbre complet de dépendances

**Exemple de prompt :**

```text
I'd also like to show the new developer what components depend on the User model.
Show me the full dependency chain — everything that imports or uses User directly
or indirectly.
```

Cela permet de visualiser **quelles parties du système seraient impactées** par une modification avant de la réaliser.

---

## Implémentation d'une fonctionnalité full-stack

### Concepts clés

| Concept | Description |
|---|---|
| **Full-stack feature** | Fonctionnalité impliquant plusieurs couches (API, logique métier, base de données, UI) |
| **Modifications multi-fichiers** | Claude crée et modifie tous les composants nécessaires de façon coordonnée |
| **Coordination backend / frontend** | L'API et l'interface utilisateur sont développées ensemble |
| **Réutilisation de patterns** | Claude suit les structures et conventions déjà présentes dans le codebase |

Les fonctionnalités réelles d'une application ne se limitent jamais à un seul fichier. Par exemple, ajouter un endpoint API peut nécessiter une route, un controller, une fonction de service, des types, des tests et une interface utilisateur. Claude Code peut orchestrer toutes ces modifications pour produire une **solution cohérente sur toute la stack**.

### Implémentation côté backend

**Exemple de prompt :**

```text
Add a new endpoint, GET /api/stats, that returns aggregated statistics for the
authenticated user, including:
  - The average mood score over the last 30 days
  - The most frequently logged symptoms
  - The current logging streak (consecutive days with at least one log)
  - The total number of logs by type

This will require:
  - Adding a new route in the user router
  - Creating a new controller method
  - Implementing a service function containing the aggregation logic
  - Defining TypeScript response types
  - Providing seed/initial data for moods and symptoms over the last 30 days

Please follow the same structure and conventions used in the existing auth endpoint.
```

Claude planifie et génère :

- Les types TypeScript
- Les requêtes de base de données
- La route API
- Les tests unitaires

### Intégration côté frontend

Une fois l'endpoint créé, Claude connecte l'interface utilisateur à la nouvelle API.

**Exemple de prompt :**

```text
Now let's continue with this feature by adding a "Your Stats" card to the Dashboard
page that fetches and displays the user stats from our new endpoint.

Include:
  - A loading state while fetching
  - Error handling if the request fails
  - Nice formatting for the statistics

Use our existing patterns from other dashboard components.
```

Claude génère :

- Le hook d'appel API
- Le composant React
- L'intégration dans le dashboard avec gestion des états (chargement, erreur, succès)

### Ajustement et amélioration

Les résultats peuvent être affinés via de nouveaux prompts ciblés.

**Exemple :** un affichage utilisant les abréviations `S, M, R, H` (symptoms, moods, medications, habits) n'était pas suffisamment clair. Un prompt supplémentaire permet de demander à Claude de remplacer cet affichage par une liste plus explicite et lisible.

---

## Points à retenir

- **Plan Mode** est idéal pour analyser le code sans le modifier
- Claude peut suivre le **flux complet d'une fonctionnalité** à travers plusieurs fichiers
- L'analyse de dépendances aide à **préparer des refactorings** sans casser le système
- Des **prompts ciblés** produisent des analyses plus utiles que des demandes trop générales
- Pour les fonctionnalités full-stack, préciser dans le prompt **tous les composants attendus** (route, controller, service, types, tests, UI)
- Claude suit les **conventions existantes** du codebase si cela lui est explicitement demandé
- Les résultats peuvent toujours être **affinés par des prompts successifs**

