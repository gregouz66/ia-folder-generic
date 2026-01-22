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
