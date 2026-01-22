# Architecture Technique

> **Architecture du projet**
>
> **Dernière mise à jour**: [DATE]  
> **Fichiers liés**: [`PROJECT-STATE.md`](./PROJECT-STATE.md) | [`ROADMAP.md`](./ROADMAP.md)

---

## Stack Technique

<!-- PERSONNALISER: Adapter selon votre stack -->

| Domaine | Technologie | Status |
|---------|-------------|:------:|
| **Langage** | [LANGAGE] | ✅ |
| **Frontend** | [FRAMEWORK_FRONTEND] | ✅ |
| **Backend** | [FRAMEWORK_BACKEND] | ✅ |
| **Base de données** | [DATABASE] | ✅ |
| **Testing** | [TESTING_FRAMEWORK] | ✅ |

---

## Vue d'Ensemble

<!-- PERSONNALISER: Adapter la structure -->

```
[PROJET]/
├── [DOSSIER_SOURCE]/       # Code source principal
│   ├── [MODULE_1]/         # Module/Feature 1
│   ├── [MODULE_2]/         # Module/Feature 2
│   └── [MODULE_PARTAGE]/   # Code partagé
│
├── [DOSSIER_CONFIG]/       # Configuration
├── [DOSSIER_TESTS]/        # Tests
└── [DOSSIER_DOCS]/         # Documentation
```

---

## Organisation des Modules/Features

### Structure d'un Module

<!-- PERSONNALISER: Adapter selon votre architecture -->

```
[feature]/
├── [feature].entity.ts       # Logique métier + validation
├── [feature].dto.ts          # DTOs + schemas
├── [feature].repository.ts   # Accès données
├── [feature].service.ts      # Orchestration use cases
├── [feature].controller.ts   # Endpoints HTTP/Interface
├── [feature].module.ts       # Module/Configuration
├── index.ts                  # Exports publics
└── __tests__/
    └── [feature].service.spec.ts
```

### Flux d'une Requête

```
Requête Entrante
    ↓
Controller (validation, auth)
    ↓
Service (logique métier, orchestration)
    ↓
Repository (accès données)
    ↓
Entity (validation domaine)
    ↓
Database
```

---

## Règles d'Architecture

### Règles des Modules

| Règle | Détail |
|-------|--------|
| Modules isolés | Un module ne peut pas importer un autre module directement |
| Pas d'interface single-impl | Créer l'interface quand 2ème impl existe |
| Validation | Chaque entrée a sa validation |
| Tests unitaires | Chaque service a ses tests |

### Matrice de Dépendances

<!-- PERSONNALISER: Adapter selon votre architecture -->

| Module | Peut importer |
|--------|---------------|
| Core/Shared | Rien (standalone) |
| Feature A | Core/Shared |
| Feature B | Core/Shared |

### Ce Qui est INTERDIT

```typescript
// ❌ Feature qui importe une feature
import { ServiceA } from '../feature-a/service-a';

// ❌ Dépendance circulaire
// feature-a → feature-b → feature-a
```

---

## Base de Données

### Schéma Principal

<!-- PERSONNALISER: Adapter selon votre modèle de données -->

```
[ENTITE_1] ─────< [RELATION] >───── [ENTITE_2]
     │                                    │
     └──< [ENTITE_3] >────────────────────┘
```

### Entités Principales

| Entité | Rôle | Status |
|--------|------|:------:|
| [ENTITE_1] | [DESCRIPTION] | ✅ |
| [ENTITE_2] | [DESCRIPTION] | ✅ |
| [ENTITE_3] | [DESCRIPTION] | 🔜 |

---

## Sécurité

### Authentification

<!-- PERSONNALISER: Décrire votre système d'auth -->

```
┌─────────────┐     Auth       ┌─────────────┐
│   Client    │ ────────────→  │   Serveur   │
│             │ ←──────────── │             │
│             │  Token/Session │             │
└─────────────┘                └─────────────┘
```

### Middleware/Guards

| Guard/Middleware | Rôle | Status |
|------------------|------|:------:|
| AuthGuard | Vérifie l'authentification | ✅ |
| RolesGuard | Vérifie les rôles | ✅ |
| [AUTRE_GUARD] | [DESCRIPTION] | 🔜 |

---

## Comment Ajouter une Feature

### 1. Créer la structure

```bash
mkdir -p [chemin]/features/ma-feature/__tests__
```

### 2. Créer les fichiers

```
ma-feature/
├── ma-feature.entity.ts       # Logique métier
├── ma-feature.dto.ts          # DTOs + validation
├── ma-feature.repository.ts   # Accès données
├── ma-feature.service.ts      # Orchestration
├── ma-feature.controller.ts   # Endpoints
├── ma-feature.module.ts       # Module
├── index.ts                   # Exports
└── __tests__/
    └── ma-feature.service.spec.ts
```

### 3. Enregistrer le module

<!-- PERSONNALISER: Montrer comment enregistrer un module -->

```typescript
// Dans le fichier principal
import { MaFeatureModule } from './features/ma-feature';

// Enregistrer le module
```

### 4. Tests

```bash
[COMMANDE_TEST] [chemin]/features/ma-feature
```

---

## Conventions de Fichiers

| Type | Convention | Exemple |
|------|------------|---------|
| Entity | `{name}.entity.ts` | `resource.entity.ts` |
| DTO | `{name}.dto.ts` | `resource.dto.ts` |
| Repository | `{names}.repository.ts` | `resources.repository.ts` |
| Service | `{names}.service.ts` | `resources.service.ts` |
| Controller | `{names}.controller.ts` | `resources.controller.ts` |
| Module | `{names}.module.ts` | `resources.module.ts` |
| Tests | `{name}.spec.ts` | `resources.service.spec.ts` |

---

## Documentation

### Documentation IA (.ai/)

Structure optimisée pour travail par agents IA:

```
.ai/
├── ENTRY.md              # Point d'entrée obligatoire
├── PROJECT-STATE.md      # Source de vérité unique
├── RULES.md              # Règles de code
├── ARCHITECTURE.md       # Ce fichier
├── ROADMAP.md            # Phases futures
```

**Workflow agent**: ENTRY → PROJECT-STATE → RULES → Coder → Mettre à jour PROJECT-STATE
