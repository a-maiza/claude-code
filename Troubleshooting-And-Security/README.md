# Dépannage (Troubleshooting) avec Claude Code

## Sujet
Identification des **problèmes courants lors de l’utilisation de Claude Code** et des méthodes simples pour les résoudre afin de maintenir un workflow de développement fluide.

---

## Concepts clés
- **Commandes utiles de diagnostic** :
    - `/config` : vérifier la configuration et les clés API.
    - `/login` : se reconnecter ou renouveler l’authentification.
    - `/usage` : consulter l’utilisation actuelle et les quotas.
- **Limites d’usage** :
    - limites de session
    - quotas hebdomadaires
    - rate limits (tokens par minute).
- **Gestion du contexte et des réponses longues**.

---

## Explications essentielles
Même avec une configuration correcte, certains problèmes peuvent apparaître lors de l’utilisation de Claude Code. Les plus fréquents concernent :

- l’authentification
- les limites d’utilisation
- les réponses tronquées
- la perte de contexte
- les boucles de correction répétitives.

Ces problèmes ont généralement **des solutions simples** et ne nécessitent pas de modifications complexes.

---

## Méthodes / Raisonnements

### 1. Erreurs d’authentification
Symptômes possibles :
- clé API invalide
- erreur de connexion.

Solutions :
- vérifier la configuration avec **`/config`**
- relancer l’authentification avec **`/login`**
- corriger ou renouveler la clé API.

---

### 2. Limites d’utilisation
Si trop de requêtes sont effectuées :

- Claude peut ralentir
- des erreurs de **quota ou rate limit** peuvent apparaître.

Avec la commande **`/usage`**, il est possible de vérifier :

- l’utilisation de la session actuelle
- l’utilisation hebdomadaire.

Caractéristiques des limites :

- **session** : fenêtre glissante d’environ **5 heures** avec un plafond
- **quota hebdomadaire**
- **rate limit** : limitation temporaire du nombre de tokens par minute.

Stratégies pour réduire la consommation :

- utiliser **Plan Mode** pour l’exploration
- commencer **de nouvelles conversations**
- diviser les tâches en **plus petits lots de fichiers**.

---

### 3. Réponses tronquées
Parfois une réponse s’arrête au milieu du code.

Cause :
- la réponse dépasse la taille maximale d’un message.

Solution :
- demander simplement **« continue à partir d’où tu t’es arrêté »**.
```text 
please continue from where you left off
```

Prévention :
- demander le code **en plusieurs parties** plutôt qu’en une seule réponse.
```text 
instead of 'Implement all the endpoints' use 'Implement the GET and POST endpoint for symptoms'
```
---

### 4. Perte de contexte
Claude peut sembler oublier des informations ou des fichiers utilisés plus tôt dans la conversation.

Cause :
- les anciens éléments ont été retirés du contexte pour faire place à de nouveaux messages.

Solution :
- **référencer à nouveau le fichier** avec `@fichier`.

Exemple :
```text 
Looking at @backend/src/controllers/authController.ts, let’s continue working on the password reset function 
```


Claude recharge alors le fichier dans le contexte.

---

### 5. Boucle de corrections répétitives
Claude peut parfois essayer plusieurs fois la **même approche incorrecte**.

Exemple :
- tentative répétée de corriger une validation regex qui échoue toujours.

Solution :
- fournir **une nouvelle direction claire**.

Exemple :
- remplacer la regex par un **validateur intégré (ex. Zod email validator)**.

---

## Points à retenir
- La plupart des problèmes rencontrés avec Claude Code ont **des solutions rapides**.
- **Authentification** : vérifier `/config` ou relancer `/login`.
- **Limites d’usage** : consulter `/usage` et réduire la taille des tâches.
- **Réponses tronquées** : demander à Claude de continuer.
- **Perte de contexte** : recharger les fichiers avec `@`.
- **Boucles d’erreurs** : proposer une approche alternative.

Une bonne gestion des prompts, du contexte et des limites d’usage permet de résoudre la majorité des difficultés rencontrées.
