# Les modes de Claude Code : Plan, Ask et Edit Automatically

Guide pratique pour exploiter les différents modes de Claude Code afin de planifier, développer et automatiser un projet logiciel de manière structurée.

---

## Table des matières

- [Concepts clés](#concepts-clés)
- [Plan Mode](#plan-mode)
  - [Cas d'usage](#cas-dusage)
  - [Planifier un projet](#planifier-un-projet)
  - [Ajuster le plan](#ajuster-le-plan)
- [Ask Mode](#ask-mode)
  - [Initialiser le projet et Git](#initialiser-le-projet-et-git)
  - [Implémenter une tâche](#implémenter-une-tâche)
- [Edit Automatically Mode](#edit-automatically-mode)
  - [Implémenter les tâches automatiquement](#implémenter-les-tâches-automatiquement)
  - [Suivre l'avancement](#suivre-lavancement)
  - [Vérifier le code avec des tests](#vérifier-le-code-avec-des-tests)
- [Workflow combiné](#workflow-combiné)
- [Points à retenir](#points-à-retenir)

---

## Concepts clés

| Mode | Description |
|---|---|
| **Plan Mode** | Analyse et planification sans modifier les fichiers |
| **Ask Mode** | Propose des modifications et demande une validation avant d'éditer |
| **Edit Automatically Mode** | Effectue les modifications directement, sans validation intermédiaire |

**Changer de mode :** raccourci `Shift + Tab`

**Référencer un fichier** dans une requête : `@nom_du_fichier`

---

## Plan Mode

Le Plan Mode sert à réfléchir à la structure d'un projet **avant toute modification du code**.

### Cas d'usage

- Planifier un nouveau projet
- Définir l'architecture technique
- Analyser un code existant
- Préparer des implémentations complexes impliquant plusieurs fichiers
- Explorer un codebase avant d'y apporter des modifications

Exemples de questions à poser en Plan Mode :

- Obtenir une vue d'ensemble du code
- Comprendre les patterns d'architecture
- Identifier les modèles de données
- Localiser les fichiers liés à une fonctionnalité
- Suivre un flux technique (ex. processus de connexion)

### Planifier un projet

Claude Code peut générer une liste de tâches structurée à partir des exigences du projet.

**Prompt :**

```text
Could you create a list of tasks to implement the technical requirements outlined in
@Documents/Requirements.md, at a level of detail that an experienced developer would
find appropriate? Put those tasks in a Tasks.md file.
```

Le plan généré est sauvegardé dans un fichier Markdown contenant :

- Les différentes phases du projet
- Des sous-tâches avec cases à cocher
- Une estimation du calendrier

**Objectifs de cette planification :**

- Découper le projet en petites tâches compréhensibles
- Adapter le niveau à un développeur intermédiaire
- Permettre un travail parallèle entre plusieurs développeurs ou agents
- Transformer les tâches en tickets de développement

### Ajuster le plan

Le fichier de tâches peut être :

- Modifié directement par le développeur
- Ajusté via Claude en restant en Plan Mode

---

## Ask Mode

Une fois la planification terminée, passer en **Ask Mode** pour implémenter les tâches avec validation à chaque étape.

### Initialiser le projet et Git

**Prompt :**

```text
First, create a .gitignore file appropriate for the technologies used in this project
and initialize a Git repository in this directory. Then set the remote origin to
https://github.com/<username>/<project-name>.git
```

Claude peut automatiser :

- La création de l'arborescence du projet
- La génération du `.gitignore`
- L'initialisation du dépôt Git
- La configuration du dépôt distant GitHub
- Les commandes `git add`, `commit` et `push` (avec validation)

### Implémenter une tâche

**Prompt :**

```text
Go ahead and complete the first task from @Documents/Tasks.md
```

Claude propose les modifications sous forme de **diff**, que l'utilisateur valide ou refuse avant chaque édition.

---

## Edit Automatically Mode

Le mode **Edit Automatically** permet à Claude de modifier directement les fichiers du projet sans validation intermédiaire, pour accélérer le développement.

> **Note :** les commandes système (création de dossiers, commandes Git, etc.) nécessitent toujours une approbation manuelle.

### Implémenter les tâches automatiquement

**Prompt :**

```text
Could you please implement the next item — Task 2 from @Documents/Tasks.md?
Also, from now on, please create a new branch and a pull request for each task.
```

Pour chaque tâche, Claude peut :

- Modifier les fichiers nécessaires
- Créer une branche dédiée
- Générer une Pull Request sur GitHub

Cela maintient un **workflow Git propre et isolé** pour chaque fonctionnalité.

### Suivre l'avancement

Le fichier `Tasks.md` permet de suivre les progrès :

- Claude coche automatiquement les sous-tâches réalisées
- Si certaines ne sont pas complétées, le prompt manquait probablement de précision

### Vérifier le code avec des tests

**Étape 1 — En Plan Mode**, demander une stratégie de tests :

```text
Could you complete the remaining 1.1 Project Initialization tasks? After that,
please create both unit tests and integration tests for the code we've written so far.
```

**Étape 2 —** Vérifier le plan proposé par Claude.

**Étape 3 — En Ask Mode**, exécuter le plan :

```text
Can you execute this plan?
```

Claude peut alors :

- Ajouter les tests unitaires et d'intégration
- Créer une branche dédiée
- Générer une Pull Request associée

---

## Workflow combiné

```
Plan Mode        → Analyser les requirements, générer Tasks.md
Ask Mode         → Initialiser Git, valider les premières implémentations
Edit Auto Mode   → Implémenter les tâches restantes (branche + PR par tâche)
Plan Mode        → Définir la stratégie de tests
Ask Mode         → Exécuter les tests et ouvrir la PR finale
```

---

## Points à retenir

- **Plan Mode** sert à analyser et organiser un projet sans modifier le code
- **Ask Mode** permet d'appliquer des modifications avec validation utilisateur
- **Edit Automatically Mode** accélère le développement en modifiant les fichiers directement
- Les **commandes système et Git** nécessitent toujours une validation manuelle
- Une **branche et une Pull Request par tâche** facilitent l'organisation du travail
- Les **tests unitaires et d'intégration** permettent de vérifier le code généré
- L'utilisation combinée des trois modes permet de planifier, implémenter, versionner et tester un projet de bout en bout
