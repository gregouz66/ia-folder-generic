# Guide d'Initialisation .ai/

> **Ce fichier te guide pour configurer le dossier `.ai/` sur un nouveau projet.**
> **Utilise les prompts ci-dessous avec ton IA préférée.**

---

## Étape 1 : Informations Projet

Copie ce prompt et remplis les `[...]` :

```
Voici les informations de mon projet :

- Nom du projet : [Ex: MonApp]
- Type : [SaaS / API / Mobile / Desktop / CLI / Autre]
- État actuel : [MVP / Production / Maintenance / Nouveau]

Stack :
- Langage : [Ex: TypeScript]
- Backend : [Ex: NestJS + Prisma + PostgreSQL]
- Frontend : [Ex: React + Vite + TailwindCSS]
- Monorepo : [NX / Turborepo / Aucun]
- Tests : [Ex: Vitest + Playwright]
- Auth : [Ex: Better Auth / Auth0 / Custom]

Commandes :
- Dev : [Ex: pnpm dev]
- Build : [Ex: pnpm build]
- Test : [Ex: pnpm test]
- Typecheck : [Ex: pnpm typecheck]
- Lint : [Ex: pnpm lint]

Structure des dossiers :
[Colle ici le résultat de `tree -L 2` ou décris ta structure]
```

---

## Étape 2 : Initialiser chaque fichier

### ENTRY.md

```
Lis .ai/ENTRY.md et remplace tous les placeholders [NOM_PROJET], [TYPE], [STACK_*], [COMMANDE_*], etc. avec les informations projet que je t'ai données.

Garde la structure du fichier intacte.
```

### PROJECT-STATE.md

```
Lis .ai/PROJECT-STATE.md et initialise-le :

1. Mets la date du jour
2. Remplis la section "Stack Technique" avec ma stack
3. Crée les phases initiales basées sur l'état actuel du projet :
   - Si nouveau projet : Phase 1 = Setup, Phase 2 = Core Features
   - Si projet existant : Décris les phases actuelles

4. Section "Ce Qui Fonctionne" : liste ce qui marche déjà (ou mets "À définir")
5. Section "Prochaines Actions" : mets les premières tâches à faire
```

### ARCHITECTURE.md

```
Lis .ai/ARCHITECTURE.md et personnalise-le :

1. Remplis le tableau "Stack Technique" avec ma stack exacte
2. Adapte la section "Vue d'Ensemble" à MA structure de dossiers
3. Si j'utilise un pattern différent de Vertical Slice, adapte la section "Organisation du Code"
4. Remplis les URLs d'environnement (local, staging, prod)
5. Décris le système d'auth utilisé
```

### RULES.md

```
Lis .ai/RULES.md et adapte les règles à mon projet :

1. Adapte les conventions de nommage si différentes
2. Vérifie que les exemples de code correspondent à ma stack
3. Ajoute des règles spécifiques à mon projet si nécessaire
4. Vérifie la langue des commentaires (français/anglais)
```

### ROADMAP.md

```
Lis .ai/ROADMAP.md et crée une roadmap pour mon projet :

1. Décris la vision produit
2. Crée 3-4 phases réalistes basées sur l'état actuel
3. Pour chaque phase, liste les features principales
4. Indique les dépendances entre phases
```

### DECISIONS.md

```
Lis .ai/DECISIONS.md et initialise-le :

1. Documente les choix technologiques déjà faits :
   - Pourquoi cette stack ?
   - Pourquoi ce pattern d'architecture ?
   - Quelles alternatives ont été considérées ?

2. Utilise le format ADR (Architecture Decision Record) existant
```

---

## Étape 3 : Vérification

Après initialisation, demande :

```
Lis tous les fichiers .ai/*.md et vérifie :
1. Plus aucun placeholder [XXX] ne reste
2. Les informations sont cohérentes entre les fichiers
3. Les commandes sont correctes

Liste les incohérences trouvées.
```

---

## Prompt Express (Tout-en-un)

Si tu veux tout faire d'un coup :

```
Voici les informations de mon projet :

- Nom : [NOM]
- Type : [TYPE]
- Stack : [STACK]
- Commandes : dev=[CMD], build=[CMD], test=[CMD]
- Structure : [STRUCTURE ou "standard"]

Lis tous les fichiers dans .ai/ et initialise-les avec ces informations.
Pour chaque fichier modifié, montre-moi un résumé des changements.
```

---

## Notes

- **Langue** : Ce template est en français. Adapte si ton projet est en anglais.
- **Agents** : Les fichiers dans `agents/` sont génériques et n'ont pas besoin d'être modifiés.
- **MODELS.md** : Contient un prompt de veille pour mettre à jour les recommandations IA.
