# Setup .ai/

> **1 prompt. L'IA fait tout.**

---

## Installation

Copie ce prompt, remplis les variables en haut, envoie :

```
SETUP .ai/ depuis GitHub

# === VARIABLES (à remplir) ===

VARIANTE=standard
# standard = tout IDE/CLI IA (avec agents/)
# ohmyopencode = oh-my-opencode (sans agents/)

NOM=MonApp
TYPE=SaaS
# SaaS / API / Mobile / Desktop / CLI / Lib

ETAT=Nouveau
# Nouveau / MVP / Production / Maintenance

LANGAGE=TypeScript
BACKEND=NestJS + Prisma + PostgreSQL
FRONTEND=React + Vite + TailwindCSS
TESTS=Vitest + Playwright
AUTRE=BetterAuth + Shadcn/ui
# Mets "N/A" si non applicable

CMD_DEV=pnpm dev
CMD_BUILD=pnpm build
CMD_TEST=pnpm test
CMD_LINT=pnpm lint
CMD_TYPECHECK=pnpm typecheck
# Mets "N/A" si non applicable

STRUCTURE=
# Colle `tree -L 2` ici ou laisse vide pour auto-détection

# === FIN DES VARIABLES ===

## SOURCE
Repo: https://github.com/gregouz66/ia-folder-generic

## INSTRUCTIONS

1. Télécharge le contenu du dossier selon VARIANTE depuis le repo GitHub (PAS de git clone)
   - standard → .ai.generic/*
   - ohmyopencode → .ai.generic.ohmyopencode/*

2. Crée .ai/ à la racine du projet et copie les fichiers dedans

3. Adapte TOUS les fichiers avec les variables ci-dessus :
   - Remplace les placeholders [...]
   - ARCHITECTURE.md : utilise STRUCTURE ou auto-détecte
   - PROJECT-STATE.md : date du jour, phases adaptées à ETAT
   - ROADMAP.md : phases réalistes selon ETAT et TYPE

## CONTRAINTES STRICTES

- NE MODIFIE QUE les fichiers copiés dans .ai/
- NE RAJOUTE PAS de sections, features ou architecture inventées
- Si variable vide ou N/A → mets "À définir"
- CONSERVE la structure exacte de chaque fichier template

## OUTPUT

Liste chaque fichier créé avec résumé des adaptations (1 ligne).
```

---

## Mise à jour

```
MISE À JOUR .ai/

# === VARIABLES ===
VARIANTE=standard
# === FIN ===

Source: https://github.com/gregouz66/ia-folder-generic

## INSTRUCTIONS

1. Télécharge la dernière version du dossier selon VARIANTE
2. Compare avec mon .ai/ actuel
3. Affiche les DIFFÉRENCES (nouveaux fichiers, sections modifiées)
4. Demande confirmation AVANT de modifier

## CONTRAINTES

- NE TOUCHE PAS aux sections personnalisées (contexte, stack, etc.)
- MERGE uniquement les nouvelles sections/règles du template
- Si conflit → affiche les deux versions, demande mon choix
```

---

## Variantes

| Valeur | Dossier source | Pour qui |
|--------|----------------|----------|
| `standard` | `.ai.generic` | Cursor, Windsurf, Claude CLI, etc. |
| `ohmyopencode` | `.ai.generic.ohmyopencode` | oh-my-opencode |

---

## Vérification

```
Vérifie .ai/*.md : liste les placeholders [...] restants.
```
