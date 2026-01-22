# .ai/ Template

> Structure de travail IA prête à l'emploi pour n'importe quel projet.

---

## C'est quoi ?

Un dossier `.ai/` à ajouter à ton projet pour structurer le travail avec une IA (Cursor, Windsurf, Claude, oh-my-opencode, etc.).

**Contenu :**
- `ENTRY.md` — Point d'entrée pour l'IA
- `PROJECT-STATE.md` — État du projet (source de vérité)
- `RULES.md` — Règles de code non-négociables
- `ARCHITECTURE.md` — Architecture technique
- `ROADMAP.md` — Vision et phases

---

## Installation

**Copie ce prompt dans ton IA :**

```
SETUP .ai/ depuis GitHub

## SOURCE
Repo: https://github.com/gregouz66/ia-folder-generic
Variante: [standard / ohmyopencode]

## CONTEXTE
- Nom: [MonApp]
- Type: [SaaS / API / Mobile / CLI]
- Stack: [Ex: TypeScript + React + Node]
- Commandes: dev=[pnpm dev], build=[pnpm build], test=[pnpm test]

## INSTRUCTIONS
1. Télécharge le dossier de la variante choisie depuis GitHub (pas git clone)
2. Copie dans .ai/ à la racine du projet
3. Adapte les fichiers avec le contexte fourni
4. NE CRÉE PAS de contenu inventé — uniquement adapter les placeholders
```

> **Variantes :** `standard` (avec agents/) ou `ohmyopencode` (sans agents/)

---

## Mise à jour

```
MISE À JOUR .ai/ depuis https://github.com/gregouz66/ia-folder-generic
Variante: [standard / ohmyopencode]

Compare avec mon .ai/, affiche les différences, demande confirmation avant de modifier.
Préserve mes personnalisations (contexte, stack, etc.).
```

---

## Structure

```
.ai/
├── ENTRY.md           # L'IA commence ici
├── PROJECT-STATE.md   # Ce qui est fait / à faire
├── RULES.md           # Comment coder
├── ARCHITECTURE.md    # Comment c'est organisé
├── ROADMAP.md         # Où on va
└── agents/            # (standard uniquement)
```

---

## Détails

Voir [SETUP.md](./SETUP.md) pour les instructions complètes.

---

## Contribuer

PRs bienvenues.
