# Guide d'Initialisation .ai/

> **Ce fichier te guide pour configurer le dossier `.ai/` sur un nouveau projet.**
> **Utilise les prompts ci-dessous avec ton IA préférée.**

---

## Structure du Dossier

```
[PROJET]/
├── SETUP.md              # Ce fichier (guide d'initialisation) - À LA RACINE
└── .ai/
    ├── ENTRY.md              # Point d'entrée agent IA (PREMIÈRE lecture)
    ├── PROJECT-STATE.md      # État du projet (source de vérité)
    ├── RULES.md              # Règles de code NON-NÉGOCIABLES
    ├── ARCHITECTURE.md       # Architecture technique
    ├── ROADMAP.md            # Phases et vision produit
    └── agents/               # Agents IA spécialisés
        ├── MODELS.md         # Recommandations modèles IA + prompt veille
        ├── orchestrator.md   # Agent coordinateur principal
        ├── ultravwork.md     # Mode haute performance
        ├── planner.md        # Planification de scopes
        ├── techlead.md       # Architecture et design
        ├── analyst.md        # Analyse business
        ├── builder.md        # Implémentation backend
        ├── frontend-engineer.md  # UI/UX et composants
        ├── qa-security.md    # QA et sécurité
        ├── product-manager.md    # User stories
        ├── consolidator.md   # Nettoyage et état
        └── spec-agent.md     # Spécifications interactives
```

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
2. Remplis la section "Progression Globale" avec des phases réalistes
3. Crée les phases initiales basées sur l'état actuel du projet :
   - Si nouveau projet : Phase 1 = Setup, Phase 2 = Core Features
   - Si projet existant : Décris les phases actuelles

4. Section "Ce Qui Fonctionne" : liste ce qui marche déjà (ou mets "À définir")
5. Section "Actions En Attente" : mets les premières tâches à faire
```

### ARCHITECTURE.md

```
Lis .ai/ARCHITECTURE.md et personnalise-le :

1. Remplis le tableau "Stack Technique" avec ma stack exacte
2. Adapte la section "Vue d'Ensemble" à MA structure de dossiers
3. Si j'utilise un pattern différent, adapte la section "Organisation du Code"
4. Décris le système d'auth utilisé
5. Remplis les conventions de fichiers selon mon projet
```

### RULES.md

```
Lis .ai/RULES.md et adapte les règles à mon projet :

1. Choisis la langue des commentaires (français/anglais)
2. Adapte les conventions de nommage si différentes de la base
3. Vérifie que les exemples de code correspondent à ma stack
4. Si pas TypeScript, adapte ou supprime la section TypeScript
5. Ajoute des règles spécifiques à mon projet si nécessaire
```

### ROADMAP.md

```
Lis .ai/ROADMAP.md et crée une roadmap pour mon projet :

1. Décris la vision produit
2. Crée 3-4 phases réalistes basées sur l'état actuel
3. Pour chaque phase, liste les features principales
4. Indique les dépendances entre phases
5. Ajoute une timeline estimée réaliste
```

### agents/MODELS.md

```
Lis .ai/agents/MODELS.md et personnalise-le :

1. Liste tes abonnements IA actuels (Anthropic, OpenAI, Google, etc.)
2. Mets à jour le tableau des recommandations avec tes modèles disponibles
3. Garde le prompt de veille pour les mises à jour futures
```

---

## Étape 3 : Vérification

Après initialisation, demande :

```
Lis tous les fichiers .ai/*.md et .ai/agents/*.md et vérifie :
1. Plus aucun placeholder [XXX] ne reste
2. Les informations sont cohérentes entre les fichiers
3. Les commandes sont correctes
4. La structure décrite correspond à la réalité

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
Pour chaque fichier modifié, affiche uniquement les changements effectués.
```

---

## Notes

- **Langue** : Ce template est en français. Adapte si ton projet est en anglais.
- **Agents** : Les fichiers dans `agents/` sont déjà génériques et ne nécessitent que peu de modifications.
- **MODELS.md** : Contient un prompt de veille pour mettre à jour les recommandations IA.
- **Personnalisation** : Les sections marquées `<!-- PERSONNALISER -->` nécessitent ton attention.

---

## Workflow Recommandé

1. **Copie le dossier `.ai/` et `SETUP.md`** dans ton projet
2. **Exécute l'Étape 1** pour donner le contexte à l'IA
3. **Exécute l'Étape 2** fichier par fichier
4. **Vérifie avec l'Étape 3**
5. **Utilise** en commençant par `@orchestrator` ou en lisant `ENTRY.md`

---

## Commandes Agent

Une fois initialisé, utilise :

```
# Pour démarrer avec l'orchestrator
@orchestrator [ta demande]

# Pour mode haute performance
@ultravwork [tâche complexe]

# Pour créer une spécification
@spec-agent [idée de feature]

# Pour planifier un scope
@planner [description du scope]
```
