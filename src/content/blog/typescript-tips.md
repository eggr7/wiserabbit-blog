---
title: TypeScript Tips for Better Code
description: Essential TypeScript tips and tricks to write more maintainable and type-safe code.
pubDate: 2025-08-06
tags: [typescript, javascript, programming]
---

# TypeScript Tips for Better Code

TypeScript has become an essential tool for modern web development. Here are some practical tips to help you write better, more maintainable TypeScript code.

## 1. Use Strict Mode

Always enable strict mode in your `tsconfig.json`:

```json
{
  "compilerOptions": {
    "strict": true,
    "noImplicitAny": true,
    "strictNullChecks": true
  }
}
```

This catches more potential errors at compile time.

## 2. Leverage Union Types

Union types are powerful for representing values that can be one of several types:

```typescript
type Status = 'loading' | 'success' | 'error';
type ID = string | number;

function handleStatus(status: Status) {
  switch (status) {
    case 'loading':
      return 'Loading...';
    case 'success':
      return 'Success!';
    case 'error':
      return 'Error occurred';
  }
}
```

## 3. Use Type Guards

Type guards help narrow down types safely:

```typescript
function isString(value: unknown): value is string {
  return typeof value === 'string';
}

function processValue(value: unknown) {
  if (isString(value)) {
    // TypeScript knows value is string here
    console.log(value.toUpperCase());
  }
}
```

## 4. Utility Types

TypeScript provides many useful utility types:

```typescript
interface User {
  id: number;
  name: string;
  email: string;
  password: string;
}

// Pick only certain properties
type PublicUser = Pick<User, 'id' | 'name' | 'email'>;

// Make all properties optional
type PartialUser = Partial<User>;

// Omit certain properties
type UserWithoutPassword = Omit<User, 'password'>;
```

## 5. Generic Constraints

Use constraints to limit generic types:

```typescript
interface Lengthwise {
  length: number;
}

function logLength<T extends Lengthwise>(arg: T): T {
  console.log(arg.length);
  return arg;
}

logLength('hello'); // Works
logLength([1, 2, 3]); // Works
// logLength(123); // Error: number doesn't have length
```

## 6. Mapped Types

Create new types by transforming existing ones:

```typescript
type Readonly<T> = {
  readonly [P in keyof T]: T[P];
};

type Optional<T> = {
  [P in keyof T]?: T[P];
};

interface User {
  name: string;
  age: number;
}

type ReadonlyUser = Readonly<User>;
type OptionalUser = Optional<User>;
```

## 7. Conditional Types

Create types that depend on conditions:

```typescript
type ApiResponse<T> = T extends string
  ? { message: T }
  : { data: T };

type StringResponse = ApiResponse<string>; // { message: string }
type DataResponse = ApiResponse<User[]>; // { data: User[] }
```

## 8. Template Literal Types

Create string literal types with patterns:

```typescript
type EventName<T extends string> = `on${Capitalize<T>}`;
type ButtonEvent = EventName<'click'>; // 'onClick'
type InputEvent = EventName<'change'>; // 'onChange'

type CSSProperty = `--${string}`;
const customProperty: CSSProperty = '--primary-color'; // Valid
```

## Best Practices

1. **Start with strict mode** - Catch errors early
2. **Use meaningful type names** - Make code self-documenting
3. **Prefer interfaces over types** - For object shapes
4. **Use enums sparingly** - Consider union types instead
5. **Don't use `any`** - Use `unknown` when type is truly unknown

## Conclusion

These TypeScript features help you write more robust, maintainable code. Start incorporating them into your projects to catch bugs early and improve your development experience.

Remember: TypeScript is about making JavaScript development more predictable and enjoyable!