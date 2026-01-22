# Setup .ai/

> **1 prompt. L'IA fait tout.**

---

## Installation

Copie ce prompt dans ton IA et remplace les `[...]` :

```
SETUP .ai/ depuis GitHub

## SOURCE
Repo: https://github.com/gregouz66/ia-folder-generic
Variante: [standard / ohmyopencode]
  - standard = .ai.generic (tout IDE/CLI IA avec agents/)
  - ohmyopencode = .ai.generic.ohmyopencode (oh-my-opencode, sans agents/)

## CONTEXTE PROJET
- Nom: [Ex: MonApp]
- Type: [SaaS / API / Mobile / Desktop / CLI / Lib]
- État: [Nouveau / MVP / Production / Maintenance]

## STACK
- Langage: [Ex: TypeScript]
- Backend: [Ex: NestJS + Prisma + PostgreSQL] (ou "N/A")
- Frontend: [Ex: React + Vite + TailwindCSS] (ou "N/A")
- Tests: [Ex: Vitest + Playwright] (ou "N/A")

## COMMANDES
- Dev: [Ex: pnpm dev]
- Build: [Ex: pnpm build]
- Test: [Ex: pnpm test]
- Lint: [Ex: pnpm lint]
- Typecheck: [Ex: pnpm typecheck] (ou "N/A")

## STRUCTURE (optionnel)
[Colle `tree -L 2` ou laisse vide pour auto-détection]

---

## INSTRUCTIONS

1. Télécharge le contenu du dossier choisi depuis le repo GitHub (PAS de git clone)
   - Si "standard" → récupère .ai.generic/*
   - Si "ohmyopencode" → récupère .ai.generic.ohmyopencode/*

2. Crée le dossier .ai/ à la racine du projet actuel et copie les fichiers dedans

3. Adapte TOUS les fichiers avec le contexte fourni :
   - Remplace les placeholders [...]
   - ARCHITECTURE.md : utilise la structure fournie OU auto-détecte
   - PROJECT-STATE.md : date du jour, phases adaptées
   - ROADMAP.md : phases réalistes selon l'état

## CONTRAINTES STRICTES

- NE MODIFIE QUE les fichiers copiés dans .ai/
- NE RAJOUTE PAS de sections, features ou architecture inventées
- Si info manquante → "À définir"
- CONSERVE la structure exacte de chaque fichier template

## OUTPUT

Liste chaque fichier créé avec résumé des adaptations (1 ligne).
```

---

## Mise à jour

Pour mettre à jour `.ai/` avec la dernière version du repo :

```
MISE À JOUR .ai/

Source: https://github.com/gregouz66/ia-folder-generic
Variante: [standard / ohmyopencode]

## INSTRUCTIONS

1. Télécharge la dernière version du dossier depuis GitHub
2. Compare avec mon .ai/ actuel
3. Affiche les DIFFÉRENCES (nouveaux fichiers, sections modifiées)
4. Demande confirmation AVANT de modifier

## CONTRAINTES

- NE TOUCHE PAS aux sections que j'ai personnalisées (contexte projet, stack, etc.)
- MERGE uniquement les nouvelles sections/règles du template
- Si conflit → affiche les deux versions et demande mon choix
```

---

## Variantes

| Variante | Dossier source | Pour qui |
|----------|----------------|----------|
| `standard` | `.ai.generic` | Cursor, Windsurf, Claude CLI, etc. |
| `ohmyopencode` | `.ai.generic.ohmyopencode` | oh-my-opencode uniquement |

**Différence** : La version standard inclut `/agents/` avec les définitions d'agents et recommandations de modèles. oh-my-opencode gère ça nativement.

---

## Vérification

```
Vérifie .ai/*.md : liste les placeholders [...] restants et incohérences.
```

---

## FAQ

**Q: Pourquoi pas git clone ?**
- Pour éviter de lier ton projet au repo source. Tu gardes le contrôle total.

**Q: Comment contribuer au template ?**
- Fork le repo, propose ta PR sur https://github.com/gregouz66/ia-folder-generic

**Q: L'IA peut-elle inventer du contenu ?**
- Non. Elle adapte UNIQUEMENT avec les infos fournies ou "À définir".
