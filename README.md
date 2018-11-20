# ts-types-utils

[![npm version](https://img.shields.io/npm/v/ts-types-utils.svg)](https://www.npmjs.com/package/ts-types-utils)
[![Conventional Commits](https://img.shields.io/badge/Conventional%20Commits-1.0.0-yellow.svg)](https://conventionalcommits.org)
[![code style: prettier](https://img.shields.io/badge/code_style-prettier-ff69b4.svg?style=flat-square)](https://github.com/prettier/prettier)

Type utilities for typescript

## Usage

Import types and use them ;-)

### ArgsType<F> // F is function

Like built-in `ReturnType` but for the args of a function, works for any number of arguments

```ts
import { ArgsType } from "ts-types-utils";
function myFunc(a: string, b: number) {}
const all: ArgsType<typeof myFunc>; // [string, number]
const first: ArgsType<typeof myFunc>[0]; // string
const second: ArgsType<typeof myFunc>[1]; // number
```

### Match<T, M, N> // T is object, M is what to match to, N negate

Pick from T all properties that match M, or not match M if N is false

```ts
import { Match } from "ts-types-utils";

type FunctionProperties<T> = Match<T, Function>; // Match<T, Function, true>
type NonFunctionProperties<T> = Match<T, Function, false>;

const foo = {
    a: string;
    b: number;
    c: () => void;
    d: (hello:string) => number;
}

const funcs: NonFunctionProperties<typeof foo> // { a: string, b: number }
const funcs: FunctionProperties<typeof foo> // { c: () => void; d: (hello: string) => number }
```