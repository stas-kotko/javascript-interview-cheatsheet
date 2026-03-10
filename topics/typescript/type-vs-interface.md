# type VS interface

## Similarities

For object shapes, they are mostly equivalent. Both:
- Are structural
- Support generics
- Can describe functions
- Can be extended

## Key Differences

### 1. Declaration merging

Only `interface` supports merging:
```ts
interface User { id: string }
interface User { name: string } 
// merged
```

`type` cannot be re-declared.

### 2. Unions & primitives

Type can represent unions, primitives, tuples. Interface cannot.

```ts
type ID = string | number;
type Point = [number, number];
```

### 3. Extending

Interface uses extends. Type uses intersection:
```ts
interface Admin extends User { role: string }
type Admin = User & { role: string }
```

Subtle difference:
- Interface conflicts → compile error.
- Type intersections can produce impossible types silently.

### 4. Computed / mapped types

Only type supports mapped/conditional types:

```typescript
type PartialUser = Partial<User>;
type Keys<T> = keyof T;
```

You cannot express this with interface.

## What should you use?

For application code:
- Use interface for object shapes meant to be extended/implemented (OOP style, public contracts).
- Use type for unions, utility types, transformations, complex compositions.

Do not follow the “always use type” or “always use interface” dogma — they solve slightly different problems.

## Interview-ready summary
- interface is best for object contracts and extensibility (supports declaration merging).
- type is more powerful (unions, mapped types, conditional types).
- In practice: interfaces for public object shapes, types for everything else.
