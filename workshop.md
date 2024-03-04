# Typescript Introduction:

## Prerequisites:

### Setting up the environment

To get started with Typescript, you need to install Node.js and npm.
You can download and install Node.js from the official website. Once you have installed Node.js, you can install Typescript using npm.

```bash
npm install -g typescript
```

Copy and paste the following helpers at the top of your file before getting started with the exercises.
These helpers will be used to implement "unit tests" for the exercises and to check if your solution is correct.

**Important:**
 - You should not modify these helpers.
 - You should not write any unit tests. They will be provided for you.
 - You **don't** have to understand how these helpers work to complete the exercises. They are just here for testing purposes.

```typescript
//This helper checks weather two types are equal or not and returns a boolean.
type Equals<A, B> =
    (<T>() => T extends A ? 1 : 2) extends
    (<T>() => T extends B ? 1 : 2) ? true : false;

//This helper will prevent compilation if the provided type is not true.
type Expect<T extends true> = T;
```

## Diving into the type system

### Warm-up
#### Exercice 0
Notions:
- Type
- Literal type

```typescript
// Make the following code compile by changing only the "HelloWorld" type.
type HelloWorld = any

type test = Expect<Equals<HelloWorld, "Hello World">>
```

### Easy
#### Exercise 1 (Hello World)
Notions:
- Union type

```typescript
// Make the following code compile by changing only the "Result" type. 

type Result = any

type test = Expect<Equals<Result, "Hello" | "World">>
```

#### Exercice 2 (Your first generic)
Notions:
- Generic type

```typescript
// Make the following code compile by changing only the "Result" type.

type Result = any

type test = Expect<Equals<Result<number>, number>>
```

### Medium
#### Exercice 3 (Conditional type)
Notions:
- Conditional type

```typescript
// Make the following code compile by changing only the "Result" type.

type Result = any

type test = Expect<Equals<Result<true>, "true">>
type test2 = Expect<Equals<Result<false>, "false">>
```

#### Exercice 4 (First of array)
Notions:
- Index type

```typescript
// Make the following code compile by changing only the "First" type.

type First = any

type test = Expect<Equals<First<["Hello", "World"]>, "Hello">>
type test2 = Expect<Equals<First<[3, 2, 1]>, 3>>
type test3 = Expect<Equals<First<[]>, never>>
```

#### Exercice 5 (Concat)
Notions:
- Spread operator

```typescript
// Make the following code compile by changing only the "Concat" type.

type Concat = any

type test = Expect<Equals<Result<["Hello", "World"], ["Hello", "World"]>, ["Hello", "World", "Hello", "World"]>>
type test2 = Expect<Equals<Result<[], []>, []>>
type test3 = Expect<Equals<Result<["Hello"], ["World"]>, ["Hello", "World"]>>
```

### Hard
#### Exercice 6 (Deep Readonly)
Notions:
- Recursive type

```typescript
// Make the following code compile by changing only the "DeepReadonly" type.

type DeepReadonly = any

type TestCase1 = {
    foo: {
        bar: {
            value: "Hello World"
        }
    }
    hello: "world"
}

type TestCase2 = {
    a: {
        readonly b: {
            c: {
                d: {
                    e: string
                }
            }
        }
    }
}

type Expected1 = {
    readonly foo: {
        readonly bar: {
            readonly value: "Hello World"
        }
    }
    readonly hello: "world"
}

type Expected2 = {
    readonly a: {
        readonly b: {
            readonly c: {
                readonly d: {
                    readonly e: string
                }
            }
        }
    }
}

type test = Expect<Equals<DeepReadonly<TestCase1>, Expected1>>
type test2 = Expect<Equals<DeepReadonly<TestCase2>, Expected2>>
```

#### Exercice 7 (Get return type)
Notions:
- Type
- Function type

```typescript
// Make the following code compile by changing only the "GetReturnType" type.

type GetReturnType = any

const f2 = (a: number, b: number) => a + b;

type test = Expect<Equals<GetReturnType<() => "Hello World">, "Hello World">>
type test2 = Expect<Equals<GetReturnType<typeof f2>, number>>
type test3 = Expect<Equals<GetReturnType<(a: string) => void>, void>>
type test4 = Expect<Equals<GetReturnType<never>, never>>
```

### Painful
#### Exercice 8 (String with spaces to camel case)
Notions:
- String manipulation
- Capitalize

```typescript
// Make the following code compile by changing only the "CamelCase" type.

type CamelCase = any

type test = Expect<Equals<CamelCase<"foo bar">, "fooBar">>
type test2 = Expect<Equals<CamelCase<"foo bar hello world">, "fooBarHelloWorld">>
type test3 = Expect<Equals<CamelCase<"foo">, "foo">>
type test4 = Expect<Equals<CamelCase<"">, "">>
type test5 = Expect<Equals<CamelCase<never>, never>>
```

#### Exercice 9 (My str to word array)
Notions:
- String manipulation

```typescript
// Make the following code compile by changing only the "StringToWordArray" type.

type StringToWordArray = any

type test = Expect<Equals<StringToWordArray<"foo bar">, ["foo", "bar"]>>
type test2 = Expect<Equals<StringToWordArray<"foo bar hello world">, ["foo", "bar", "hello", "world"]>>
type test3 = Expect<Equals<StringToWordArray<"foo">, ["foo"]>>
type test4 = Expect<Equals<StringToWordArray<"">, []>>
type test5 = Expect<Equals<StringToWordArray<never>, never>>
```
