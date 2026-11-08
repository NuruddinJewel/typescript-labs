# Type vs Interface in TypeScript: What's the Difference?

## Introduction

When you start learning TypeScript, you quickly meet two ways to describe the shape of data: `type` aliases and `interface`. They look very similar, so many beginners wonder which one to use. The good news is that both work well for most everyday tasks. However, they have a few important differences. Let's understand them in a simple way.

## Core Differences

### 1. Describing Objects

Both can describe an object in almost the same way:

```typescript
interface User {
  name: string;
  age: number;
}

type Person = {
  name: string;
  age: number;
};
```

### 2. Extending

An `interface` uses the `extends` keyword, while a `type` uses the `&` (intersection) symbol:

```typescript
interface Animal { name: string; }
interface Dog extends Animal { breed: string; }

type Cat = Animal & { color: string };
```

### 3. Declaration Merging

If you declare the same `interface` twice, TypeScript merges them into one. A `type` cannot do this and will show an error:

```typescript
interface Car { brand: string; }
interface Car { year: number; }
// Car now has both brand and year
```

### 4. Flexibility

A `type` can describe more than objects, such as unions, primitives, and tuples. An `interface` cannot:

```typescript
type Id = string | number;
type Point = [number, number];
```

## When to Choose Which

Use `interface` for objects and class shapes, especially in libraries where others may extend them. Use `type` when you need unions, tuples, or other advanced combinations.

## Conclusion

Both `type` and `interface` are powerful tools. Choose `interface` for simple object shapes and `type` for anything more flexible. Most importantly, stay consistent within your project, and your code will stay clean and easy to read.