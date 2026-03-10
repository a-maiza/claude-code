# Plan Mode et Ask Mode de Claude Code

## Sujet
Utilisation des **modes de Claude Code** pour planifier et développer efficacement une application. Le cours explique comment exploiter **Plan Mode** et **Ask Mode** afin d’organiser un projet logiciel, analyser un code existant et automatiser certaines tâches de développement.

---

## Concepts clés
- **Claude Code** : assistant de développement utilisable dans le terminal ou dans VS Code.
- **Modes principaux** :
    - **Plan Mode** : analyse et planification sans modifier les fichiers.
    - **Ask Mode (Ask before edits)** : propose des modifications et demande une validation avant d’éditer le code.
    - **Edit automatique** : effectue les modifications sans validation intermédiaire.
- **Changement de mode** : raccourci **Shift + Tab**.
- **Référencer des fichiers** dans les requêtes avec `@nom_du_fichier`.

---

## Explications essentielles
Le **Plan Mode** sert à réfléchir à la structure d’un projet avant toute modification du code. Il permet notamment de :

- planifier un nouveau projet
- définir l’architecture technique
- analyser un code existant
- préparer des implémentations complexes impliquant plusieurs fichiers
- explorer un codebase avant d’y apporter des modifications

Exemples de requêtes possibles :

- obtenir une vue d’ensemble du code
- comprendre les modèles d’architecture
- identifier les modèles de données
- localiser les fichiers d’une fonctionnalité spécifique
- suivre un flux technique (ex. processus de connexion)

Un exemple est présenté avec la création d’une application appelée **WellTrack**, destinée aux personnes atteintes de maladies chroniques. L’application permet :

- d’enregistrer symptômes, humeurs, médicaments et habitudes
- d’analyser les données pour identifier des tendances et patterns de santé

Stack technique utilisée :

- React
- Node.js
- Express
- PostgreSQL

Les ressources fournies incluent :

- un document de spécifications (`requirements.md`)
- les modèles de données
- les fonctionnalités principales
- les écrans
- les endpoints API
- des wireframes d’interface.

---

## Méthodes / Raisonnements

### Planification du projet
Claude Code peut générer une **liste de tâches à partir des exigences** du projet.

```text
Could you create a list of tasks to implement the technical requirements outlined in `@Documents/Requirements.md`, at a level of detail that an experienced developer would find appropriate ?
Put those task in a Tasks.md file
```

Objectifs de cette planification :
- découper le projet en **petites tâches compréhensibles**
- adapter le niveau à un **développeur intermédiaire**
- permettre un **travail parallèle entre plusieurs développeurs ou agents**
- transformer les tâches en **tickets de développement**

Le plan généré est sauvegardé dans un **fichier Markdown** contenant :
- différentes phases du projet
- des sous-tâches avec cases à cocher
- une estimation du calendrier (ex. environ **12 semaines jusqu’au lancement bêta**).

### Ajustement du plan
Le fichier de tâches peut être :
- modifié directement par le développeur
- ajusté via Claude en utilisant le **Plan Mode**.

### Implémentation avec Ask Mode
Une fois la planification terminée :

- Crer le projet et initialiser un repository git
```text
First, create a `.gitignore` file appropriate for the technologies used in this project and initialize a Git repository in this directory. Then set the remote origin to `https://github.com/a-maiza/my-project.git`, 
replacing `my-project` with the name of the repository you created on GitHub.

```
- Claude exécute une tâche (ex. « compléter la tâche 1 »)
```text
Go ahead and complete the first task from `@Documents/Tasks.md`
```
- il propose les modifications sous forme de **diff**
- l’utilisateur valide ou refuse chaque modification.

### Automatisation des tâches de développement
Claude Code peut également automatiser :

- la création de l’arborescence du projet
- la génération d’un fichier `.gitignore`
- l’initialisation d’un dépôt **Git**
- la configuration du dépôt distant **GitHub**
- les commandes `git add`, `commit` et `push` avec validation de l’utilisateur.

---

## Exemples importants
Application **WellTrack** :

- tableau de bord affichant un résumé de la journée
- ajout rapide de symptômes ou d’humeurs
- écran dédié pour la saisie des données
- visualisation de tendances afin d’identifier des patterns de santé.

---

## Points à retenir
- **Plan Mode** sert à analyser et organiser un projet sans modifier le code.
- **Ask Mode** permet d’appliquer des modifications avec validation utilisateur.
- Claude Code peut générer **des plans de développement structurés et détaillés**.
- Les tâches sont stockées dans **des fichiers Markdown facilement modifiables**.
- L’outil peut automatiser **la configuration du projet et la gestion Git**.
- Une utilisation stratégique des modes améliore **la productivité et la structuration du développement logiciel**.


# Edit Automatically Mode de Claude Code

## Sujet
Utilisation du **mode Edit Automatically** de Claude Code pour automatiser l’implémentation de tâches de développement, tout en conservant un contrôle sur certaines opérations comme les commandes système et Git.

---

## Concepts clés
- **Edit Automatically Mode** : mode dans lequel Claude modifie automatiquement les fichiers du projet.
- **Limitations du mode** :
    - ne peut pas exécuter directement certaines **commandes bash**
    - nécessite toujours une **validation pour les actions système** (création de fichiers, commandes Git, etc.).
- **Stratégie Git recommandée** :
    - créer une **branche par tâche**
    - générer une **Pull Request (PR)** pour chaque implémentation.

```text
Could you please implement the next item—Task 2 from @Documents/Tasks.md? Also, from now on, please create a new branch and a pull request for each task.
```
---

## Explications essentielles
Le **mode Edit Automatically** permet d’accélérer le développement en laissant Claude modifier automatiquement le code nécessaire pour accomplir une tâche.

Cependant :
- les **commandes système** (création de dossiers, commandes Git, etc.) doivent toujours être approuvées
- certaines actions restent donc sous contrôle humain.

Lorsqu’une tâche est lancée (par exemple : *implémenter la prochaine tâche du fichier tasks*), Claude peut :
- modifier les fichiers nécessaires
- créer une branche associée à la tâche
- générer une **Pull Request sur GitHub**.

Cela permet de maintenir un **workflow Git propre et isolé** pour chaque fonctionnalité.

---

## Méthodes / Raisonnements

### Implémentation automatique des tâches
Processus typique :

1. Passer en **Edit Automatically Mode**.
2. Demander à Claude d’implémenter la prochaine tâche du fichier `tasks`.
3. Demander la création :
    - d’une **branche dédiée**
    - d’une **Pull Request** pour chaque tâche.

Une fois terminé :
- la Pull Request apparaît sur GitHub
- elle peut être examinée puis fermée ou fusionnée.

### Vérification de l’avancement
Le fichier **Tasks** permet de suivre les progrès :
- Claude coche automatiquement les sous-tâches réalisées.
- Si certaines ne sont pas complétées, cela peut indiquer que le **prompt n’était pas assez précis**.

### Vérification du fonctionnement du code
Pour tester le code généré, il est possible de demander à Claude de :

- écrire des **tests unitaires**
- écrire des **tests d’intégration**
- vérifier que ces tests passent.

Pour cela :
1. Utiliser **Plan Mode** afin que Claude propose une stratégie de tests.
```text
Could you complete the remaining 1.1 Project Initialization tasks? After that, please create both unit tests and integration tests for the code we’ve written so far.
```
---
2. Vérifier le plan.
3. Passer en **Ask Mode** pour exécuter ce plan.
```text
Can you execute this plan ?
```

Claude peut alors :
- ajouter les tests
- créer une branche
- générer une Pull Request associée.

---

## Exemples importants
Actions réalisées automatiquement par Claude :

- implémentation d’une tâche depuis `tasks.md`
- création d’une **branche Git**
- création d’une **Pull Request**
- ajout de **tests unitaires et d’intégration**
- mise à jour du suivi des tâches.

---

## Points à retenir
- **Edit Automatically Mode** permet à Claude de modifier directement les fichiers du projet.
- Les **commandes système et Git doivent toujours être validées** par l’utilisateur.
- Une **branche et une Pull Request par tâche** facilitent l’organisation du travail.
- Les **tests unitaires et d’intégration** permettent de vérifier le code généré.
- L’utilisation combinée de **Plan Mode, Ask Mode et Auto Edit Mode** permet de :
    - planifier un projet
    - implémenter les fonctionnalités
    - automatiser le workflow Git
    - tester le code produit.