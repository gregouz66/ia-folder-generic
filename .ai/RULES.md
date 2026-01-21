# Règles de Code

> **Ces règles sont NON-NÉGOCIABLES.**  
> **Tout code qui ne les respecte pas sera rejeté.**

---

## Table des Matières

1. [Langue et Commentaires](#1-langue-et-commentaires)
2. [Typage et Sécurité](#2-typage-et-sécurité)
3. [Architecture](#3-architecture)
4. [Code Propre](#4-code-propre)
5. [Nommage](#5-nommage)
6. [Dette Technique](#6-dette-technique)
7. [Tests](#7-tests)
8. [Sécurité](#8-sécurité)
9. [Git](#9-git)

---

## 1. Langue et Commentaires

### Langue des Commentaires

> **À DÉFINIR**: Choisir la langue des commentaires pour le projet

| Option | Quand l'utiliser |
|--------|------------------|
| **Français** | Équipe francophone, projet interne |
| **Anglais** | Équipe internationale, projet open-source |

### Quand Commenter

| Commenter | Ne Pas Commenter |
|-----------|------------------|
| Début de fichier (but du fichier) | Chaque fonction évidente |
| Logique métier complexe | Getters/setters simples |
| Décisions d'architecture | Code auto-explicatif |
| Workarounds et leurs raisons | Imports |
| Algorithmes non-triviaux | Types évidents |

### Interdit dans les Commentaires

- ❌ Commentaires qui répètent le code
- ❌ TODO sans ticket associé
- ❌ Code commenté (supprimer ou versionner)
- ❌ Commentaires obsolètes

---

## 2. Typage et Sécurité

### Règles Strictes (TypeScript)

| Règle | Bon | Mauvais |
|-------|-----|---------|
| Pas de `any` | `data: unknown` + type guard | `data: any` |
| Pas de `@ts-ignore` | Corriger l'erreur | `// @ts-ignore` |
| Types explicites | `function get(): string` | `function get()` |
| Pas de cast forcé | Type guard ou validation | `data as User` |

### Validation des Données

```typescript
// ✅ BON: Validation à l'entrée
const validated = Schema.parse(input);

// ❌ MAUVAIS: Faire confiance aux données externes
processData(input); // Pas de validation!
```

---

## 3. Architecture

### Principes

| Principe | Description |
|----------|-------------|
| **Séparation des responsabilités** | Chaque module a une seule raison de changer |
| **Dépendances unidirectionnelles** | Pas de cycles, dépendances vers le bas |
| **Isolation des features** | Features auto-contenues |

### WET > DRY (Write Everything Twice)

| Situation | Action |
|-----------|--------|
| 1ère utilisation | Garde dans le module |
| 2ème utilisation similaire | **Duplique** (WET) |
| 3ème utilisation identique | **Extrait** vers shared |

> L'abstraction prématurée crée plus de dette que la duplication.

### Pas d'Interface pour une Seule Implémentation

```typescript
// ❌ MAUVAIS: Interface inutile
interface IUserRepository { ... }
class UserRepository implements IUserRepository { ... }

// ✅ BON: Classe directe (YAGNI)
class UserRepository { ... }

// Note: Ajouter l'interface quand tu as une 2ème implémentation
```

---

## 4. Code Propre

### Fonctions

| Règle | Description |
|-------|-------------|
| **Courtes** | Max ~20 lignes, sinon découper |
| **Un seul but** | Une fonction = une responsabilité |
| **Nommage explicite** | Le nom décrit ce que ça fait |
| **Pas d'effets de bord cachés** | Effets visibles dans le nom |

### Early Return

```typescript
// ✅ BON: Early return
async function findUser(id: string): Promise<User> {
  const user = await repository.findById(id);
  if (!user) {
    throw new NotFoundException('User not found');
  }
  return user;
}

// ❌ MAUVAIS: Imbrication profonde
async function findUser(id: string): Promise<User> {
  const user = await repository.findById(id);
  if (user) {
    return user;
  } else {
    throw new NotFoundException('User not found');
  }
}
```

### Pas de Magic Numbers/Strings

```typescript
// ✅ BON: Constantes nommées
const MAX_NAME_LENGTH = 100;
const DEFAULT_PAGE_SIZE = 20;

// ❌ MAUVAIS: Nombres magiques
if (name.length > 100) { ... }
```

---

## 5. Nommage

### Conventions

| Type | Convention | Exemple |
|------|------------|---------|
| Fichiers composants | PascalCase | `UserCard.tsx` |
| Fichiers autres | kebab-case | `user-utils.ts` |
| Classes/Types | PascalCase | `UserService` |
| Fonctions/Variables | camelCase | `getUsers` |
| Constantes | UPPER_SNAKE | `MAX_RETRIES` |
| Booléens | Préfixe is/has/can | `isActive` |

### Noms Explicites

```typescript
// ✅ BON: Noms descriptifs
const activeUsers = users.filter(u => u.isActive);
async function validateUserPermission(userId, action): Promise<boolean>

// ❌ MAUVAIS: Noms vagues
const data = users.filter(u => u.isActive);
async function check(uid, a): Promise<boolean>
```

---

## 6. Dette Technique

### Signes de Dette

| Signe | Action |
|-------|--------|
| Code dupliqué 3+ fois | Extraire vers shared |
| Fonction > 50 lignes | Découper |
| Fichier > 300 lignes | Séparer responsabilités |
| TODO sans ticket | Créer ticket ou supprimer |
| Suppression de type | Corriger le type |

### Règle du Boy Scout

> "Laisse le code plus propre que tu l'as trouvé"

---

## 7. Tests

### Stratégie de Test

```
┌─────────────────────────────────────────────────────────────────────┐
│                    STRATÉGIE DE TEST                                 │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│  NIVEAU 1: UNITAIRE/INTÉGRATION                                     │
│  ├── Services, hooks, composants                                    │
│  ├── À chaque développement                                         │
│  └── Commande: [TEST_COMMAND]                                       │
│                                                                     │
│  NIVEAU 2: E2E                                                      │
│  ├── Parcours utilisateur complets                                  │
│  ├── Avant merge/deploy                                             │
│  └── Commande: [E2E_COMMAND]                                        │
│                                                                     │
└─────────────────────────────────────────────────────────────────────┘
```

### Pattern AAA (Arrange-Act-Assert)

```typescript
it('should create user with valid data', async () => {
  // Arrange
  const request = { name: 'John', email: 'john@test.com' };
  
  // Act
  const result = await service.create(request);
  
  // Assert
  expect(result.name).toBe('John');
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
| Y a-t-il une faille potentielle ? | Injection, XSS, CSRF |
| Les données sensibles sont-elles protégées ? | Mots de passe, tokens |
| Les permissions sont-elles vérifiées ? | Chaque endpoint |
| Les entrées sont-elles validées ? | Jamais faire confiance |

### Règles Non-Négociables

| Règle | Détail |
|-------|--------|
| Jamais de secrets dans le code | Variables d'environnement |
| Valider TOUTES les entrées | Schema validation |
| Hasher les mots de passe | bcrypt ou équivalent |
| Vérifier les permissions | À chaque action |

### Multi-Tenant (si applicable)

```typescript
// ✅ BON: Toujours filtrer par tenant
async findItems(tenantId: string): Promise<Item[]> {
  return db.items.findMany({
    where: { tenantId } // OBLIGATOIRE
  });
}

// ❌ CRITIQUE: Pas de filtre tenant
async findItems(): Promise<Item[]> {
  return db.items.findMany(); // FAILLE!
}
```

---

## 9. Git

### Branches

```
feature/TICKET-123-add-user-filters
fix/TICKET-456-login-timeout
refactor/TICKET-789-extract-validation
docs/update-readme
```

### Commits

```bash
# ✅ BON: Message clair avec ticket
git commit -m "feat(users): add email validation TICKET-123"
git commit -m "fix(auth): handle token expiration TICKET-456"

# ❌ MAUVAIS: Messages vagues
git commit -m "fix bug"
git commit -m "update code"
```

### Avant de Committer

```bash
[TYPECHECK_COMMAND]  # 0 erreurs
[TEST_COMMAND]       # Tous passent
[LINT_COMMAND]       # Pas d'erreurs
```

---

## Checklist Avant de Soumettre

- [ ] Commentaires dans la bonne langue
- [ ] Pas de suppressions de typage
- [ ] Fonctions courtes (< 20 lignes)
- [ ] Noms explicites
- [ ] Entrées validées
- [ ] Tests couvrent les cas importants
- [ ] Vérifications passent (types, tests, lint)
- [ ] Pas de code debug oublié
- [ ] Code plus propre qu'avant (Boy Scout)
- [ ] Sécurité vérifiée
