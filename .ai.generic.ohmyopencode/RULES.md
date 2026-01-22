# Règles de Code

> **Ces règles sont NON-NÉGOCIABLES.**  
> **Tout code qui ne les respecte pas sera rejeté.**

---

## Table des Matières

1. [Langue et Commentaires](#1-langue-et-commentaires)
2. [TypeScript](#2-typescript)
3. [Architecture](#3-architecture)
4. [Code Propre](#4-code-propre)
5. [Nommage](#5-nommage)
6. [Éviter la Dette Technique](#6-éviter-la-dette-technique)
7. [Tests](#7-tests)
8. [Sécurité](#8-sécurité)
9. [Git](#9-git)

---

## 1. Langue et Commentaires

### Règle Absolue: Langue des Commentaires

<!-- PERSONNALISER: Choisir la langue des commentaires -->

```typescript
// ✅ BON - Commentaires dans la langue choisie
/** Service de gestion des ressources */
export class ResourceService {
  /** Crée une nouvelle ressource */
  async create(request: CreateResourceRequest): Promise<Resource> {
    // Valide les données
    ...
  }
}

// ❌ MAUVAIS - Mélange de langues
/** Resource management service */
export class ResourceService {
  // Creates a new resource
  ...
}
```

### Quand Commenter (Juste le Nécessaire)

| Commenter | Ne Pas Commenter |
|-----------|------------------|
| Début de fichier (1-2 lignes: but du fichier) | Chaque fonction évidente |
| Logique métier complexe | Getters/setters simples |
| Décisions d'architecture non-évidentes | Code auto-explicatif |
| Workarounds et leurs raisons | Imports |
| Algorithmes non-triviaux | Types évidents |

### Ce Qui est INTERDIT dans les Commentaires

```typescript
// ❌ Commentaires inutiles
const count = items.length; // Récupère le nombre d'items

// ❌ Commentaires qui répètent le code
// Incrémente i de 1
i++;

// ❌ Commentaires obsolètes (TODO sans ticket)
// TODO: à refactorer plus tard

// ❌ Code commenté
// const oldImplementation = () => { ... };
```

---

## 2. TypeScript

<!-- PERSONNALISER: Adapter si vous n'utilisez pas TypeScript -->

### Règles Strictes

| Règle | Exemple BON | Exemple MAUVAIS |
|-------|-------------|-----------------|
| Pas de `any` | `data: unknown` puis type guard | `data: any` |
| Pas de `@ts-ignore` | Corriger l'erreur | `// @ts-ignore` |
| Pas de `@ts-expect-error` | Corriger l'erreur | `// @ts-expect-error` |
| Types explicites | `function get(): string` | `function get()` |
| Pas de `as` sans validation | Type guard ou validation | `data as User` |

### Type Guards

```typescript
// ✅ BON: Type guard avec validation
function isUser(data: unknown): data is User {
  return (
    typeof data === 'object' &&
    data !== null &&
    'id' in data &&
    'email' in data
  );
}

// Utilisation
if (isUser(response)) {
  console.log(response.email); // Type-safe
}

// ❌ MAUVAIS: Cast forcé
const user = response as User; // Dangereux!
```

### Null Safety

```typescript
// ✅ BON: Gestion explicite de null
async findUser(id: string): Promise<User | null> {
  const user = await this.repository.findById(id);
  return user; // Peut être null
}

// Utilisation
const user = await this.findUser(id);
if (!user) {
  throw new NotFoundException('Utilisateur non trouvé');
}
// Ici user est garanti non-null

// ❌ MAUVAIS: Ignorer la possibilité de null
const user = await this.findUser(id);
console.log(user.email); // Erreur si user est null!
```

---

## 3. Architecture

### Organisation du Code

<!-- PERSONNALISER: Adapter à votre architecture -->

```
features/[feature]/
├── [feature].entity.ts       # Logique métier + validation
├── [feature].dto.ts          # DTOs + schemas de validation
├── [feature].repository.ts   # Accès données
├── [feature].service.ts      # Orchestration
├── [feature].controller.ts   # Endpoints HTTP
├── [feature].module.ts       # Module
└── __tests__/                # Tests de la feature
```

### Règle d'Isolation des Features

```typescript
// ❌ INTERDIT: Importer une feature depuis une autre
import { OtherService } from '../other-feature/other.service';

// ✅ AUTORISÉ: Importer depuis core/shared
import { CommonService } from '../../core/common.service';
```

### WET > DRY (Write Everything Twice)

| Situation | Action |
|-----------|--------|
| 1ère utilisation | Garde dans la feature |
| 2ème utilisation similaire | **Duplique** (WET) |
| 3ème utilisation identique | **Extrait** vers `core/` ou `shared/` |

### Pas d'Interface pour une Seule Implémentation

```typescript
// ❌ MAUVAIS: Interface inutile
interface IResourceRepository {
  findAll(): Promise<Resource[]>;
}

class ResourceRepository implements IResourceRepository {
  findAll(): Promise<Resource[]> { ... }
}

// ✅ BON: Classe directe (YAGNI)
class ResourceRepository {
  findAll(): Promise<Resource[]> { ... }
}

// Note: Ajouter l'interface quand tu as une 2ème implémentation
```

---

## 4. Code Propre

### Fonctions

| Règle | Description |
|-------|-------------|
| Courtes | Max ~20 lignes, sinon découper |
| Un seul but | Une fonction = une responsabilité |
| Nommage explicite | Le nom décrit ce que ça fait |
| Pas d'effets de bord cachés | Si modifie l'état, c'est clair |

```typescript
// ✅ BON: Fonctions courtes et claires
async createResource(request: CreateRequest): Promise<Resource> {
  await this.validateAccess(request.parentId);
  const resource = Resource.create(request);
  return this.repository.save(resource);
}

// ❌ MAUVAIS: Fonction trop longue et fait trop de choses
async createResource(request: CreateRequest): Promise<Resource> {
  // 50 lignes de code mélangeant validation, création, logging, etc.
}
```

### Early Return

```typescript
// ✅ BON: Early return (évite l'imbrication)
async findResource(id: string): Promise<Resource> {
  const resource = await this.repository.findById(id);
  if (!resource) {
    throw new NotFoundException('Ressource non trouvée');
  }
  
  if (!resource.isActive) {
    throw new ForbiddenException('Ressource désactivée');
  }
  
  return resource;
}

// ❌ MAUVAIS: Imbrication profonde
async findResource(id: string): Promise<Resource> {
  const resource = await this.repository.findById(id);
  if (resource) {
    if (resource.isActive) {
      return resource;
    } else {
      throw new ForbiddenException('Ressource désactivée');
    }
  } else {
    throw new NotFoundException('Ressource non trouvée');
  }
}
```

### Éviter les Magic Numbers/Strings

```typescript
// ✅ BON: Constantes nommées
const MAX_NAME_LENGTH = 100;
const DEFAULT_PAGE_SIZE = 20;

if (name.length > MAX_NAME_LENGTH) {
  throw new BadRequestException('Nom trop long');
}

// ❌ MAUVAIS: Nombres magiques
if (name.length > 100) { // C'est quoi 100?
  throw new BadRequestException('Nom trop long');
}
```

---

## 5. Nommage

### Conventions

| Type | Convention | Exemple |
|------|------------|---------|
| Fichiers composants | PascalCase | `ResourceCard.tsx` |
| Fichiers autres | kebab-case | `resource-utils.ts` |
| Classes/Types/Interfaces | PascalCase | `ResourceService` |
| Fonctions/Variables | camelCase | `getResources` |
| Constantes | UPPER_SNAKE | `MAX_RETRIES` |
| Booléens | Préfixe is/has/can | `isActive`, `hasPermission` |

### Noms Explicites

```typescript
// ✅ BON: Noms qui décrivent l'intention
const activeUsers = users.filter(u => u.isActive);

async function validateUserHasAccess(
  userId: string, 
  resourceId: string
): Promise<boolean> { ... }

// ❌ MAUVAIS: Noms vagues ou abrégés
const data = users.filter(u => u.isActive);

async function check(uid: string, rid: string): Promise<boolean> { ... }
```

---

## 6. Éviter la Dette Technique

### Signes de Dette Technique

| Signe | Action |
|-------|--------|
| Code dupliqué 3+ fois | Extraire vers shared |
| Fonction > 50 lignes | Découper |
| Fichier > 300 lignes | Séparer responsabilités |
| TODO sans ticket | Créer ticket ou supprimer |
| `@ts-ignore` | Corriger le type |
| `console.log` en prod | Utiliser logger approprié |

### Règle du Boy Scout

> "Laisse le code plus propre que tu l'as trouvé"

### Quand NE PAS Refactorer

- Si c'est hors du scope de ta tâche actuelle
- Si ça nécessite des changements dans d'autres features
- Si c'est un changement architectural majeur

→ **Créer un ticket à la place et continuer**

---

## 7. Tests

### Stratégie de Test

```
┌─────────────────────────────────────────────────────────────────────┐
│                    STRATÉGIE DE TEST                                 │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│  NIVEAU 1: TESTS UNITAIRES/INTÉGRATION (Chaque développement)       │
│  ├── Tests unitaires (services, hooks, composants)                  │
│  ├── Tests d'intégration (modules, features)                        │
│  └── Commande: [COMMANDE_TEST]                                      │
│                                                                     │
│  NIVEAU 2: TESTS E2E (Avant merge/deploy)                           │
│  ├── Tests E2E (parcours utilisateur complets)                      │
│  └── Commande: [COMMANDE_TEST_E2E]                                  │
│                                                                     │
└─────────────────────────────────────────────────────────────────────┘
```

### Pattern AAA (Arrange-Act-Assert)

```typescript
describe('ResourceService', () => {
  describe('create', () => {
    it('crée une ressource avec les données valides', async () => {
      // Arrange (prépare)
      const request = { name: 'Ma Ressource', parentId: 'parent-1' };
      mockRepository.findById.mockResolvedValue(mockParent);
      
      // Act (exécute)
      const result = await service.create(request, 'user-1');
      
      // Assert (vérifie)
      expect(result.name).toBe('Ma Ressource');
      expect(mockRepository.save).toHaveBeenCalledWith(
        expect.objectContaining({ name: 'Ma Ressource' })
      );
    });

    it('échoue si le parent n\'existe pas', async () => {
      // Arrange
      mockRepository.findById.mockResolvedValue(null);
      
      // Act & Assert
      await expect(
        service.create({ name: 'Test', parentId: 'invalid' }, 'user-1')
      ).rejects.toThrow(NotFoundException);
    });
  });
});
```

### Ce Qui Doit Être Testé

| Tester | Ne Pas Tester |
|--------|---------------|
| Logique métier | Getters/setters triviaux |
| Cas limites | Code framework |
| Gestion d'erreurs | Librairies tierces |
| Intégrations critiques | UI statique |

---

## 8. Sécurité

### Mentalité Sécurité-First

> **Règle d'Or**: À chaque ligne de code, se poser la question :  
> **"Est-ce que ce code introduit une faille de sécurité ?"**

### Questions Obligatoires

| Question | Contexte |
|----------|----------|
| **Y a-t-il une faille potentielle ?** | Injection, XSS, CSRF, auth bypass |
| **Les données sensibles sont-elles protégées ?** | Mots de passe, tokens, credentials |
| **Les permissions sont-elles vérifiées ?** | Chaque endpoint, chaque action |
| **Les entrées sont-elles validées ?** | Jamais faire confiance aux données externes |

### Règles Non-Négociables

| Règle | Détail |
|-------|--------|
| Jamais de secrets dans le code | Utiliser variables d'environnement |
| Valider TOUTES les entrées | Validation sur chaque DTO/input |
| Hasher les mots de passe | bcrypt ou équivalent, jamais en clair |
| Vérifier les permissions | Guards/middleware sur chaque endpoint |
| Échapper les données | Pas d'injection SQL/XSS |

### Gestion des Erreurs

```typescript
// ✅ BON: Messages génériques pour la sécurité
if (!user || !await verifyPassword(password, user.passwordHash)) {
  throw new UnauthorizedException('Email ou mot de passe incorrect');
  // Note: Ne pas dire "utilisateur non trouvé" vs "mauvais mot de passe"
}

// ❌ MAUVAIS: Fuite d'information
if (!user) {
  throw new UnauthorizedException('Utilisateur non trouvé'); // Révèle l'existence
}
```

---

## 9. Git

### Branches

```
feature/TICKET-123-add-filters
fix/TICKET-456-connection-timeout
refactor/TICKET-789-extract-validation
docs/update-readme
```

### Commits

```bash
# ✅ BON: Message clair avec ticket
git commit -m "feat(resources): ajoute filtres par date TICKET-123"
git commit -m "fix(auth): corrige expiration token TICKET-456"

# ❌ MAUVAIS: Messages vagues
git commit -m "fix bug"
git commit -m "update code"
git commit -m "WIP"
```

### Avant de Committer

```bash
[COMMANDE_TYPECHECK]   # 0 erreurs
[COMMANDE_TEST]        # Tous les tests passent
[COMMANDE_LINT]        # Pas d'erreurs lint
```

---

## Checklist Avant de Soumettre du Code

- [ ] Commentaires dans la langue définie
- [ ] Pas de `any`, `@ts-ignore`, ou `@ts-expect-error`
- [ ] Les fonctions sont courtes (< 20 lignes idéalement)
- [ ] Les noms sont explicites
- [ ] Les entrées sont validées
- [ ] Les tests couvrent les cas importants
- [ ] Les commandes de vérification passent
- [ ] Pas de `console.log` oublié
- [ ] Le code est plus propre qu'avant (Boy Scout)
- [ ] **SÉCURITÉ**: Pas de faille identifiée
