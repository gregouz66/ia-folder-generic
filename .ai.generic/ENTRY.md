# Point d'Entrée Agent IA

> **Tu es un agent IA travaillant sur ce projet.**  
> **Ce fichier est ta PREMIÈRE lecture obligatoire.**

---

## Lecture Obligatoire (dans cet ordre)

| # | Fichier | Contenu | Quand le lire |
|---|---------|---------|---------------|
| 1 | `PROJECT-STATE.md` | État actuel, tâches, progression | **TOUJOURS en premier** |
| 2 | `RULES.md` | Règles de code, conventions, interdictions | **TOUJOURS avant de coder** |
| 3 | `ARCHITECTURE.md` | Structure technique, packages, features | Si tu modifies l'architecture |
| 4 | `ROADMAP.md` | Phases futures, vision produit | Si tu planifies une feature |

---

## Système d'Agents Spécialisés

Ce projet utilise un **système d'agents spécialisés** pour déléguer le travail au bon modèle IA.

### Agents Disponibles

| Agent | Spécialité | Invocation |
|-------|------------|------------|
| @orchestrator | Coordination, état | Agent principal |
| @ultravwork | **Mode haute performance** (parallèle + vérification) | `@ultravwork` |
| @planner | Planification scopes | `@planner` |
| @techlead | Architecture, design | `@techlead` |
| @analyst | Analyse business | `@analyst` |
| @builder | Implémentation backend | `@builder` |
| @frontend-engineer | **UI/UX, composants, animations** | `@frontend-engineer` |
| @qa-security | QA, sécurité, audit | `@qa-security` |
| @product-manager | User stories | `@product-manager` |
| @consolidator | Nettoyage état | `@consolidator` |
| @spec-agent | Specs interactives | `@spec-agent` |

> **Modèles IA**: Recommandations dans `agents/MODELS.md`

### Comment Utiliser les Agents

**Option 1: Mention directe**
```
@builder Implémente le endpoint GET /api/resources selon la spec
```

**Option 2: Via l'orchestrator**
```
@orchestrator Je veux créer une nouvelle feature "notifications"
```
→ L'orchestrator délègue automatiquement aux bons agents

**Option 3: Mode ULTRAVWORK (haute performance)**
```
@ultravwork Implémente la feature "notifications" avec tous les tests
```
→ ULTRAVWORK parallélise les agents, vérifie avec preuves, garantit 100% complet

---

## Contexte Projet

<!-- PERSONNALISER: Adapter ces informations à votre projet -->

| Élément | Valeur |
|---------|--------|
| **Nom** | [NOM_PROJET] |
| **Type** | [TYPE_APPLICATION] |
| **Stack Backend** | [TECHNOLOGIES_BACKEND] |
| **Stack Frontend** | [TECHNOLOGIES_FRONTEND] |
| **État** | [ÉTAT_ACTUEL] |
| **Phase actuelle** | [PHASE_ACTUELLE] |

---

## Règles Critiques (mémorise-les)

### Ce que tu DOIS faire

1. **Lire PROJECT-STATE.md** avant toute action
2. **Mettre à jour PROJECT-STATE.md** après chaque tâche terminée
3. **Suivre les conventions de code** définies dans RULES.md
4. **Valider avec les commandes de test/lint** avant de considérer une tâche terminée

### Ce que tu ne dois JAMAIS faire

1. Utiliser `any` en TypeScript (si applicable)
2. Ignorer les erreurs de type (`@ts-ignore`, `@ts-expect-error`)
3. Committer sans que les tests passent
4. Modifier du code sans comprendre le contexte

---

## Workflow avec Agents

### Pour une Nouvelle Feature

```
1. @orchestrator → Analyse la demande, crée le plan
2. @planner → Coordonne les spécialistes
3. @product-manager → User stories
4. @analyst → Analyse business
5. @techlead → Architecture, interfaces
6. @builder → Implémentation backend
7. @frontend-engineer → Implémentation UI/UX
8. @qa-security → Revue code
9. @consolidator → Nettoyage état
```

### Pour une Correction de Bug

```
1. @analyst → Analyse du problème
2. @builder → Fix
3. @qa-security → Validation
```

### Pour une Question/Exploration

```
@analyst Explique-moi comment fonctionne [FEATURE]
```

---

## Après Chaque Tâche Terminée

1. **Mettre à jour `PROJECT-STATE.md`**:
   - Ajouter la tâche dans "Tâches Complétées"
   - Mettre à jour la progression de la phase concernée
   - Ajouter les learnings si tu as découvert quelque chose d'utile

2. **Vérifier**:
   - Commandes de vérification (lint, test, typecheck) → 0 erreurs
   - Pas de `console.log` oublié

---

## Structure du Projet

<!-- PERSONNALISER: Adapter cette structure à votre projet -->

```
[PROJET]/
├── .ai/                    # Documentation IA (tu es ici)
│   ├── ENTRY.md            # Ce fichier (point d'entrée)
│   ├── PROJECT-STATE.md    # État du projet (source de vérité)
│   ├── RULES.md            # Règles de code (interdictions)
│   ├── ARCHITECTURE.md     # Architecture technique
│   ├── ROADMAP.md          # Phases futures
│   └── agents/             # Agents IA spécialisés
│       ├── MODELS.md       # Recommandations modèles IA
│       ├── orchestrator.md
│       ├── ultravwork.md
│       ├── builder.md
│       ├── frontend-engineer.md
│       ├── planner.md
│       ├── techlead.md
│       ├── analyst.md
│       ├── qa-security.md
│       ├── product-manager.md
│       ├── consolidator.md
│       └── spec-agent.md
│
├── [STRUCTURE_PROJET]/     # Code source
└── README.md               # Vue d'ensemble projet
```

---

## Commandes Utiles

<!-- PERSONNALISER: Adapter les commandes à votre projet -->

```bash
# Commandes de développement
[COMMANDE_DEV]        # Lancer en mode développement
[COMMANDE_BUILD]      # Build production
[COMMANDE_TEST]       # Lancer tests
[COMMANDE_LINT]       # Vérifier le code
[COMMANDE_TYPECHECK]  # Vérifier les types (si TypeScript)
```

---

## En Cas de Doute

1. **Consulte `RULES.md`** pour les conventions de code
2. **Regarde le code existant** dans la même feature comme exemple
3. **Demande clarification** si la tâche est ambiguë
4. **Utilise le bon agent** pour la tâche

**Ne devine jamais. Demande.**
