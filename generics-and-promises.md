# TypeScript Generics Made Easy: Working with Promise<T>

## Introduction

Imagine a delivery box that can hold anything, but nobody knows what is inside until it is opened. That is what happens when we use `any` in TypeScript. Generics fix this by letting us say, "this box holds _this_ type." In this post, you will learn what generics are, how they work with functions, and how they make asynchronous `Promise<T>` code safer. We will also compare code with and without generics.

## What Are Generics?

A generic is a placeholder for a type. We write it as `<T>`, and TypeScript replaces `T` with a real type when the function is used.

```ts
function getFirst<T>(items: T[]): T {
  return items[0];
}

const firstNumber = getFirst([10, 20, 30]); // type: number
const firstName = getFirst(["Henry", "Oliver"]); // type: string
```

The same function works for numbers and strings, and TypeScript remembers which one you used.

## What Is Promise<T>?

A Promise is a value that will arrive later, such as data from a server. `Promise<T>` tells TypeScript what type of value will arrive.

```ts
function wait<T>(value: T, ms: number): Promise<T> {
  return new Promise((resolve) => {
    setTimeout(() => resolve(value), ms);
  });
}

const result = await wait("Hello!", 1000); // type: string
const count = await wait(42, 500); // type: number
```

Here, `wait` returns whatever value you give it, after a delay. The type is never lost.

## A Real Example: Fetching Data

```ts
interface Product {
  id: number;
  title: string;
  price: number;
}

async function getData<T>(url: string): Promise<T> {
  const response = await fetch(url);
  return response.json();
}

const product = await getData<Product>("/api/product/1");
console.log(product.title); // autocomplete works
// console.log(product.color); // Error: 'color' does not exist
```

One function can now fetch products, users, or orders safely.

## Comparison: Without vs With Generics

**Without generics (using `any`):**

```ts
async function getDataAny(url: string): Promise<any> {
  const response = await fetch(url);
  return response.json();
}

const item = await getDataAny("/api/product/1");
console.log(item.colour); // No error, but it is a typo!
```

**With generics:**

```ts
const item = await getData<Product>("/api/product/1");
console.log(item.colour); // Error caught immediately
```

| Feature      | Without Generics (`any`) | With Generics (`<T>`) |
| ------------ | ------------------------ | --------------------- |
| Type safety  | None                     | Strong                |
| Autocomplete | Not available            | Available             |
| Typos caught | At runtime (too late)    | While coding          |
| Reusability  | Reusable but unsafe      | Reusable and safe     |
| Code clarity | Unclear return type      | Clear return type     |

## Conclusion

Generics are like labeled boxes: you choose what goes inside, and TypeScript makes sure you use it correctly. When combined with `Promise<T>`, they make asynchronous code predictable, reusable, and safe. Compared with `any`, generics give you the same flexibility without losing protection. Start by adding `<T>` to your next async function, and you will quickly see the benefits.
