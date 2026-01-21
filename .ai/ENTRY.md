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
| 5 | `DECISIONS.md` | Décisions techniques justifiées (ADR) | Si tu questionnes un choix techno |

---

## Système d'Agents Spécialisés

Ce projet utilise un **système d'agents spécialisés** pour déléguer le travail.

### Agents Disponibles

| Agent | Spécialité | Fichier |
|-------|------------|---------|
| @orchestrator | Coordination, état | `agents/orchestrator.md` |
| @ultrawork | **Mode haute performance** (parallèle + vérification) | `agents/ultrawork.md` |
| @planner | Planification scopes | `agents/planner.md` |
| @techlead | Architecture, design | `agents/techlead.md` |
| @analyst | Analyse business | `agents/analyst.md` |
| @builder | Implémentation backend | `agents/builder.md` |
| @frontend-engineer | UI/UX, composants | `agents/frontend-engineer.md` |
| @qa-security | QA, sécurité, audit | `agents/qa-security.md` |
| @product-manager | User stories | `agents/product-manager.md` |
| @consolidator | Nettoyage état | `agents/consolidator.md` |
| @spec-agent | Specs interactives | `agents/spec-agent.md` |

> **Modèles IA**: Recommandations dans `agents/MODELS.md` (guide de veille inclus)

### Comment Utiliser les Agents

Pour utiliser un agent, demande à l'IA de lire son fichier et d'agir selon ce rôle :

```
Lis .ai/agents/builder.md et agis comme cet agent.
[Ta tâche ici]
```

---

## Contexte Projet

> **À PERSONNALISER** pour chaque projet

| Élément | Valeur |
|---------|--------|
| **Nom** | [NOM_PROJET] |
| **Type** | [TYPE: SaaS, API, Mobile, etc.] |
| **Stack Backend** | [STACK_BACKEND: ex. NestJS + Prisma + PostgreSQL] |
| **Stack Frontend** | [STACK_FRONTEND: ex. React + TailwindCSS] |
| **Monorepo** | [OUTIL: NX, Turborepo, ou N/A] |
| **État** | [ÉTAT: MVP, Production, Maintenance, etc.] |
| **Phase actuelle** | [PHASE_ACTUELLE] |

---

## Règles Critiques (mémorise-les)

### Ce que tu DOIS faire

1. **Lire PROJECT-STATE.md** avant toute action
2. **Écrire les commentaires** dans la langue du projet (voir RULES.md)
3. **Mettre à jour PROJECT-STATE.md** après chaque tâche terminée
4. **Suivre l'architecture définie** dans ARCHITECTURE.md
5. **Valider avec les commandes de test** avant de considérer une tâche terminée
6. **Penser sécurité** à chaque ligne de code

### Ce que tu ne dois JAMAIS faire

1. ❌ Ignorer les erreurs de typage
2. ❌ Supprimer des tests pour faire passer le build
3. ❌ Committer sans que les tests passent
4. ❌ Inventer des patterns non documentés
5. ❌ Modifier l'architecture sans validation

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
Lis .ai/agents/analyst.md et agis comme cet agent.
Explique-moi comment fonctionne [X]
```

---

## Après Chaque Tâche Terminée

1. **Mettre à jour `PROJECT-STATE.md`**:
   - Ajouter la tâche dans "Tâches Complétées"
   - Mettre à jour la progression de la phase concernée
   - Ajouter les learnings si tu as découvert quelque chose d'utile

2. **Vérifier**:
   - Tests passent
   - Pas d'erreurs de typage
   - Pas de code debug oublié

---

## Structure Type du Projet

```
projet/
├── .ai/                    # Documentation IA (tu es ici)
│   ├── ENTRY.md            # ⭐ Ce fichier (point d'entrée)
│   ├── PROJECT-STATE.md    # État du projet (source de vérité)
│   ├── RULES.md            # Règles de code
│   ├── ARCHITECTURE.md     # Architecture technique
│   ├── ROADMAP.md          # Phases futures
│   ├── DECISIONS.md        # Décisions techniques (ADR)
│   └── agents/             # Agents IA spécialisés
│       ├── MODELS.md       # Recommandations modèles IA
│       ├── orchestrator.md
│       ├── ultrawork.md
│       ├── builder.md
│       └── ...
│
├── docs/                   # Documentation pour HUMAINS
│
└── src/                    # Code source (structure variable)
```

---

## Commandes Utiles

> **À PERSONNALISER** selon le projet

```bash
# Commandes de développement
[COMMANDE_DEV]        # Ex: pnpm dev

# Commandes de build
[COMMANDE_BUILD]      # Ex: pnpm build

# Commandes de test
[COMMANDE_TEST]       # Ex: pnpm test
[COMMANDE_TYPECHECK]  # Ex: pnpm typecheck
[COMMANDE_LINT]       # Ex: pnpm lint
```

---

## En Cas de Doute

1. **Consulte `RULES.md`** pour les conventions de code
2. **Regarde le code existant** comme exemple
3. **Demande clarification** si la tâche est ambiguë
4. **Utilise le bon agent** pour la tâche

**Ne devine jamais. Demande.**
