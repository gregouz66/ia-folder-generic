# Architecture Technique

> **Ce document décrit la structure technique du projet.**
>
> **Dernière mise à jour**: [DATE]

---

## Stack Technique

| Domaine | Technologie | Statut |
|---------|-------------|:------:|
| **Langage** | [Ex: TypeScript 5.x] | ✅ |
| **Frontend** | [Ex: React 18 + Vite] | ✅ |
| **State Management** | [Ex: Zustand + TanStack Query] | ✅ |
| **UI** | [Ex: shadcn/ui + Tailwind] | ✅ |
| **Backend** | [Ex: NestJS] | ✅ |
| **ORM** | [Ex: Prisma] | ✅ |
| **Base de données** | [Ex: PostgreSQL] | ✅ |
| **Monorepo** | [Ex: NX + pnpm] | ✅ |
| **Testing** | [Ex: Vitest + Playwright] | ✅ |
| **Auth** | [Ex: Better Auth] | ✅ |

---

## Vue d'Ensemble

```
projet/
├── .ai/                    # Documentation IA
├── docs/                   # Documentation humains
├── src/                    # Code source (adapter selon structure)
│   ├── features/           # Features (Vertical Slice)
│   ├── core/               # Code partagé
│   └── ...
└── tests/                  # Tests E2E
```

> **Adapter cette structure** selon l'organisation réelle du projet.

---

## Organisation du Code

### Pattern: Vertical Slice Architecture

Chaque feature est auto-contenue :

```
features/[feature-name]/
├── [feature].entity.ts       # Logique métier
├── [feature].dto.ts          # DTOs + validation
├── [feature].repository.ts   # Accès données
├── [feature].service.ts      # Orchestration
├── [feature].controller.ts   # Endpoints
├── [feature].module.ts       # Module
└── __tests__/                # Tests
```

### Flux d'une Requête (Backend)

```
HTTP Request
    ↓
Controller (validation, auth)
    ↓
Service (logique métier)
    ↓
Repository (accès données)
    ↓
Database
```

---

## Règles de Dépendances

### Matrice de Dépendances

| Module | Peut importer |
|--------|---------------|
| Core/Shared | Rien (standalone) |
| Features | Core, pas d'autres features |
| UI Components | Core, UI libs |

### Ce Qui est INTERDIT

```typescript
// ❌ Feature qui importe une autre feature
import { UserService } from '../users/user.service';

// ✅ Utiliser le module (injection de dépendances)
// ou extraire vers core/ si vraiment partagé
```

---

## Base de Données

### Schéma Principal

> **Adapter** selon le projet

```
[Entity A] ───< [Entity B] >─── [Entity C]
     │              │
     └──< [Entity D]
```

### Conventions

| Aspect | Convention |
|--------|------------|
| Noms de tables | snake_case pluriel |
| Noms de colonnes | snake_case |
| Clés primaires | `id` (UUID ou auto-increment) |
| Clés étrangères | `[table]_id` |
| Timestamps | `created_at`, `updated_at` |

---

## Sécurité

### Authentification

> **Décrire** le système d'auth utilisé

```
┌─────────────┐     Login      ┌─────────────┐
│   Frontend  │ ────────────→  │   Backend   │
│             │ ←──────────── │             │
│             │  Access Token  │             │
└─────────────┘                └─────────────┘
```

### Guards/Middleware

| Guard | Rôle | Statut |
|-------|------|:------:|
| Auth Guard | Vérifie le token | ✅ |
| Roles Guard | Vérifie les rôles | ✅ |
| [Autre Guard] | [Description] | ✅ |

---

## Comment Ajouter une Feature

### 1. Créer la structure

```bash
mkdir -p src/features/ma-feature/__tests__
```

### 2. Créer les fichiers

```
ma-feature/
├── ma-feature.entity.ts
├── ma-feature.dto.ts
├── ma-feature.repository.ts
├── ma-feature.service.ts
├── ma-feature.controller.ts
├── ma-feature.module.ts
└── __tests__/
    └── ma-feature.service.spec.ts
```

### 3. Enregistrer le module

```typescript
// app.module.ts ou équivalent
import { MaFeatureModule } from './features/ma-feature';

@Module({
  imports: [MaFeatureModule],
})
export class AppModule {}
```

### 4. Tester

```bash
[TEST_COMMAND] src/features/ma-feature
```

---

## Conventions de Fichiers

| Type | Convention | Exemple |
|------|------------|---------|
| Entity | `{name}.entity.ts` | `user.entity.ts` |
| DTO | `{name}.dto.ts` | `user.dto.ts` |
| Repository | `{names}.repository.ts` | `users.repository.ts` |
| Service | `{names}.service.ts` | `users.service.ts` |
| Controller | `{names}.controller.ts` | `users.controller.ts` |
| Tests | `{name}.spec.ts` | `users.service.spec.ts` |
| Composants | `{Name}.tsx` | `UserCard.tsx` |

---

## Environnements

| Environnement | URL | Description |
|---------------|-----|-------------|
| Local | `http://localhost:XXXX` | Développement |
| Staging | [URL] | Tests |
| Production | [URL] | Live |

---

## Diagrammes

> **Ajouter** des diagrammes selon les besoins :
> - Diagramme de composants
> - Diagramme de séquence pour les flux critiques
> - Diagramme de déploiement
