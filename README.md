# Créer et développer un projet à partir d'un `requirements.md` avec Claude Code

Méthode structurée pour partir d'un fichier `requirements.md`, générer des tâches indépendantes, configurer Claude Code, et développer un projet avec un workflow Git et des tests automatisés.

---

## Table des matières

- [Concepts clés](#concepts-clés)
- [Workflow du projet](#workflow-du-projet)
- [Étapes détaillées](#étapes-détaillées)
    - [1. Initialiser le projet](#1-initialiser-le-projet)
    - [2. Générer les tâches avec Plan Mode](#2-générer-les-tâches-avec-plan-mode)
    - [3. Structurer les tâches](#3-structurer-les-tâches)
    - [4. Initialiser Git](#4-initialiser-git)
    - [5. Générer le contexte projet](#5-générer-le-contexte-projet)
    - [6. Configurer les règles du projet](#6-configurer-les-règles-du-projet)
    - [7. Implémenter les tâches](#7-implémenter-les-tâches)
    - [8. Utiliser Edit Automatically Mode](#8-utiliser-edit-automatically-mode)
    - [9. Vérifier le code avec Test-Driven Iteration](#9-vérifier-le-code-avec-test-driven-iteration)
    - [10. Gérer la fenêtre de contexte](#10-gérer-la-fenêtre-de-contexte)
- [Structure finale du projet](#structure-finale-du-projet)
- [Points à retenir](#points-à-retenir)

---

## Concepts clés

| Concept | Description |
|---|---|
| **Requirements.md** | Document décrivant les besoins fonctionnels et techniques du projet |
| **Tasks.md** | Liste de tâches générée à partir des requirements |
| **Plan Mode** | Planification et analyse sans modifier le code |
| **Ask Mode** | Exécution des tâches avec validation des modifications |
| **Edit Automatically Mode** | Implémentation automatique avec supervision |
| **CLAUDE.md** | Fichier de contexte du projet chargé au début de chaque conversation |
| **Test-Driven Iteration** | Boucle automatique code → tests → correction |
| **Branches Git par tâche** | Chaque tâche est développée et testée isolément |

---

## Workflow du projet

```
Requirements.md
    → Plan Mode
    → Tasks.md
    → Git initialization
    → /init
    → CLAUDE.md configuration
    → Task execution
    → Branch + Pull Request
    → Tests
    → Merge
```

---

## Étapes détaillées

### 1. Initialiser le projet

Créer un dossier projet et ajouter le document des exigences.

**Structure minimale :**

```
project/
├── Documents/
│   └── Requirements.md
└── README.md
```

Le fichier `Requirements.md` doit contenir :

- Description du projet
- Stack technique
- Fonctionnalités principales
- Modèles de données
- Endpoints API
- Wireframes éventuels

---

### 2. Générer les tâches avec Plan Mode

Utiliser Claude Code en **Plan Mode** pour transformer les requirements en tâches.

**Prompt :**

```text
Could you create a list of tasks to implement the technical requirements outlined in
@Documents/Requirements.md, at a level of detail that an experienced developer would
find appropriate? Put those tasks in a Tasks.md file in Documents/Tasks.md.
```

---

### 3. Structurer les tâches

Les tâches doivent être organisées en **phases indépendantes** pour éviter les dépendances.

**Exemple de phases :**

```
1 - Project initialization
2 - Core infrastructure
3 - Data models
4 - Backend API
5 - Frontend features
6 - Integration
7 - Testing
8 - Deployment
```

**Exemple de tâches granulaires :**

```
1.1 Setup project structure
1.2 Configure database connection
1.3 Create User model
1.4 Create authentication endpoints
1.5 Add login frontend form
```

**Principe :**

> 1 tâche = 1 fonctionnalité complète et testable

Chaque tâche doit :

- Modifier un module précis
- Être testable indépendamment
- Être développée dans une branche Git dédiée

---

### 4. Initialiser Git

Passer en **Ask Mode**, puis utiliser le prompt suivant :

```text
First create a .gitignore file appropriate for the technologies used in this project.
Then initialize a Git repository in this directory and set the remote origin to:
https://github.com/<username>/<project-name>.git
```

Claude va :

- Générer le `.gitignore`
- Initialiser le dépôt Git
- Connecter le dépôt GitHub

---

### 5. Générer le contexte projet

Exécuter la commande suivante dans Claude Code :

```
/init
```

Claude analyse le projet et crée automatiquement un fichier `CLAUDE.md` contenant :

- Stack technique
- Architecture
- Endpoints
- Modèles de données
- Commandes importantes

---

### 6. Configurer les règles du projet

Compléter `CLAUDE.md` pour automatiser les workflows.

#### Git Workflow

```markdown
## Git Workflow

When working on tasks listed in Tasks.md:

1. Before starting, create a new branch named `<type>/<task-number>-<brief-description>`,
   where the branch type reflects the nature of the change:
   - feat      → new features
   - fix       → bug fixes
   - docs      → documentation updates
   - test      → tests
   - refactor  → refactoring

2. Use atomic commits with conventional commit messages.

3. Once the task is finished, open a pull request that includes:
   - A title matching the task description
   - A brief summary of the changes made
   - Any relevant testing notes or considerations
   - An updated checkbox in TASKS.md to mark the task as complete
```

#### Testing Requirements

```markdown
## Testing Requirements

Before marking any task as complete:

1. Write unit tests for new functionality
2. Run the full test suite
3. If tests fail:
   - Analyse the failure output
   - Fix the code (not the tests, unless the tests are incorrect)
   - Re-run tests until all pass
```

---

### 7. Implémenter les tâches

**Prompt :**

```text
Complete task 1.1 from @Documents/Tasks.md
```

Claude va :

- Créer une branche
- Écrire le code
- Générer les tests
- Créer un commit
- Ouvrir une Pull Request

---

### 8. Utiliser Edit Automatically Mode

Passer en **Edit Automatically Mode**, puis utiliser le prompt suivant :

```text
Please implement task 1.2 from @Documents/Tasks.md.
Create a new branch and a pull request for the task.
```

Claude va :

- Modifier plusieurs fichiers
- Implémenter la fonctionnalité
- Mettre à jour `Tasks.md`
- Créer la Pull Request

---

### 9. Vérifier le code avec Test-Driven Iteration

**Prompt :**

```text
Implement task 1.3 from @Documents/Tasks.md.
Make sure all tests pass before marking the task as complete.
```

**Boucle automatisée :**

```
1. Écrire le code
2. Générer les tests
3. Exécuter les tests
4. Corriger les erreurs
5. Créer commit et Pull Request
```

---

### 10. Gérer la fenêtre de contexte

Pour maintenir la qualité des réponses, suivre ces bonnes pratiques :

#### Travailler par petites tâches

```text
# ❌ Mauvais
Refactor the entire backend

# ✅ Bon
Refactor the authentication module to use the new error handling pattern
```

#### Charger uniquement les fichiers nécessaires

```text
Looking only at:
@backend/src/routes/auth.ts
@backend/src/controllers/authController.ts

Refactor the login endpoint.
```

#### Démarrer de nouvelles conversations

Les conversations longues peuvent :

- Consommer plus de tokens
- Provoquer une perte de contexte
- Réduire la qualité des réponses

---

## Structure finale du projet

```
project/
│
├── Documents/
│   ├── Requirements.md
│   └── Tasks.md
│
├── backend/
├── frontend/
│
├── CLAUDE.md
├── package.json
├── .gitignore
└── README.md
```

---

## Points à retenir

- **Plan Mode** permet de transformer les requirements en tâches structurées
- **CLAUDE.md** fournit un contexte permanent du projet
- Chaque tâche doit être **indépendante et testable**
- Une **branche Git et une Pull Request par tâche** facilitent l'organisation
- La **Test-Driven Iteration** garantit la fiabilité du code
- Les tâches verticales permettent le **travail parallèle** et un projet maintenable
