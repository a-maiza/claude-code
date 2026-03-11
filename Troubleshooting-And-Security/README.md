# Dépannage (Troubleshooting) avec Claude Code

Guide de référence pour identifier et résoudre les problèmes courants lors de l'utilisation de Claude Code, afin de maintenir un workflow de développement fluide.

---

## Table des matières

- [Commandes de diagnostic](#commandes-de-diagnostic)
- [Problèmes courants et solutions](#problèmes-courants-et-solutions)
  - [1. Erreurs d'authentification](#1-erreurs-dauthentification)
  - [2. Limites d'utilisation](#2-limites-dutilisation)
  - [3. Réponses tronquées](#3-réponses-tronquées)
  - [4. Perte de contexte](#4-perte-de-contexte)
  - [5. Boucle de corrections répétitives](#5-boucle-de-corrections-répétitives)
- [Points à retenir](#points-à-retenir)

---

## Commandes de diagnostic

| Commande | Description |
|---|---|
| **`/config`** | Vérifier la configuration et les clés API |
| **`/login`** | Se reconnecter ou renouveler l'authentification |
| **`/usage`** | Consulter l'utilisation actuelle et les quotas |

---

## Problèmes courants et solutions

### 1. Erreurs d'authentification

**Symptômes :** clé API invalide, erreur de connexion.

**Solutions :**

- Vérifier la configuration avec `/config`
- Relancer l'authentification avec `/login`
- Corriger ou renouveler la clé API

---

### 2. Limites d'utilisation

**Symptômes :** ralentissements, erreurs de quota ou de rate limit.

La commande `/usage` permet de vérifier l'utilisation de la session actuelle et le quota hebdomadaire.

**Types de limites :**

| Type | Description |
|---|---|
| **Session** | Fenêtre glissante d'environ 5 heures avec un plafond |
| **Quota hebdomadaire** | Limite globale sur 7 jours |
| **Rate limit** | Limitation temporaire du nombre de tokens par minute |

**Stratégies pour réduire la consommation :**

- Utiliser **Plan Mode** pour l'exploration (moins coûteux)
- Démarrer de **nouvelles conversations** plutôt que d'allonger les existantes
- Diviser les tâches en **lots de fichiers plus petits**

---

### 3. Réponses tronquées

**Symptôme :** la réponse s'arrête au milieu du code.

**Cause :** la réponse dépasse la taille maximale d'un message.

**Solution :** demander à Claude de continuer là où il s'est arrêté.

```text
Please continue from where you left off.
```

**Prévention :** demander le code en plusieurs parties plutôt qu'en une seule réponse.

```text
# ❌ Trop large
Implement all the endpoints

# ✅ Ciblé
Implement the GET and POST endpoints for symptoms
```

---

### 4. Perte de contexte

**Symptôme :** Claude semble oublier des informations ou des fichiers utilisés plus tôt dans la conversation.

**Cause :** les anciens éléments ont été retirés du contexte pour faire place à de nouveaux messages.

**Solution :** référencer à nouveau le fichier avec `@fichier`.

```text
Looking at @backend/src/controllers/authController.ts, let's continue working
on the password reset function.
```

Claude recharge le fichier dans le contexte et reprend là où la conversation s'était arrêtée.

---

### 5. Boucle de corrections répétitives

**Symptôme :** Claude tente plusieurs fois la même approche incorrecte sans progresser.

**Exemple :** tentative répétée de corriger une validation regex qui échoue toujours.

**Solution :** fournir une nouvelle direction claire en proposant une approche alternative.

**Exemple :** demander de remplacer la regex par un validateur intégré comme Zod.

---

## Points à retenir

| Problème | Solution rapide |
|---|---|
| Erreur d'authentification | `/config` ou `/login` |
| Limite d'usage atteinte | `/usage`, réduire la taille des tâches |
| Réponse tronquée | `Please continue from where you left off` |
| Perte de contexte | Recharger les fichiers avec `@fichier` |
| Boucle d'erreurs | Proposer une approche alternative |

La plupart des problèmes rencontrés avec Claude Code ont des solutions rapides. Une bonne gestion des prompts, du contexte et des limites d'usage permet de résoudre la grande majorité des difficultés.

