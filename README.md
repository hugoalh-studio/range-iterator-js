# Range Iterator (JavaScript)

[**⚖️** MIT](./LICENSE.md)

**🗂️**
[![GitHub: hugoalh-studio/range-iterator-js](https://img.shields.io/badge/hugoalh--studio/range--iterator--js-181717?logo=github&logoColor=ffffff&style=flat "GitHub: hugoalh-studio/range-iterator-js")](https://github.com/hugoalh-studio/range-iterator-js)
[![NPM: @hugoalh/range-iterator](https://img.shields.io/badge/@hugoalh/range--iterator-CB3837?logo=npm&logoColor=ffffff&style=flat "NPM: @hugoalh/range-iterator")](https://www.npmjs.com/package/@hugoalh/range-iterator)

**🆙** ![Latest Release Version](https://img.shields.io/github/release/hugoalh-studio/range-iterator-js?sort=semver&color=2187C0&label=&style=flat "Latest Release Version") (![Latest Release Date](https://img.shields.io/github/release-date/hugoalh-studio/range-iterator-js?color=2187C0&label=&style=flat "Latest Release Date"))

A JavaScript module to iterate between range.

## 🎯 Target

- Bun ^ v1.0.0
- Cloudflare Workers
- Deno >= v1.34.0
  > **🛡️ Require Permission**
  >
  > *N/A*
- NodeJS >= v16.13.0

### 🔗 Other Edition

- [TypeScript](https://github.com/hugoalh-studio/range-iterator-ts)

## 🔰 Usage

### Via Installation

> **🎯 Supported Target**
>
> - Cloudflare Workers
> - NodeJS

1. Install via console/shell/terminal:
    - Via NPM
      ```sh
      npm install @hugoalh/range-iterator[@<Tag>]
      ```
    - Via PNPM
      ```sh
      pnpm add @hugoalh/range-iterator[@<Tag>]
      ```
    - Via Yarn
      ```sh
      yarn add @hugoalh/range-iterator[@<Tag>]
      ```
2. Import at the script (`<ScriptName>.js`):
    ```js
    import ... from "@hugoalh/range-iterator";
    ```
    > **ℹ️ Note**
    >
    > Although it is recommended to import the entire module, it is also able to import part of the module with sub path if available, please visit [file `package.json`](./package.json) property `exports` for available sub paths.

### Via NPM Specifier

> **🎯 Supported Target**
>
> - Bun
> - Deno

1. Import at the script (`<ScriptName>.js`):
    ```js
    import ... from "npm:@hugoalh/range-iterator[@<Tag>]";
    ```
    > **ℹ️ Note**
    >
    > Although it is recommended to import the entire module, it is also able to import part of the module with sub path if available, please visit [file `package.json`](./package.json) property `exports` for available sub paths.

## 🧩 API

- ```ts
  function rangeIterator(start: bigint, end: bigint, step?: RangeIteratorOptions<bigint>["step"]): Generator<bigint>;
  function rangeIterator(start: number, end: number, step?: RangeIteratorOptions<number>["step"]): Generator<number>;
  function rangeIterator(start: string, end: string, step?: RangeIteratorOptions<string>["step"]): Generator<string>;
  function rangeIterator(start: bigint, end: bigint, options?: RangeIteratorOptions<bigint>): Generator<bigint>;
  function rangeIterator(start: number, end: number, options?: RangeIteratorOptions<number>): Generator<number>;
  function rangeIterator(start: string, end: string, options?: RangeIteratorOptions<string>): Generator<string>;
  ```
- ```ts
  interface RangeIteratorOptions<T extends RangeIteratorAcceptType> {
    /**
    * Whether to exclusive end.
    * @default false
    */
    endExclusive?: boolean;
    /**
    * Step of the decrement/increment of the iterate.
    * @default 1n // Big integer.
    * @default 1 // Number/String.
    */
    step?: RangeIteratorIndexType<T>;
  }
  ```
- ```ts
  type RangeIteratorAcceptType = bigint | number | string;
  ```
- ```ts
  type RangeIteratorIndexType<T extends RangeIteratorAcceptType> = T extends bigint ? bigint : number;
  ```

## ✍️ Example

- ```js
  Array.from(rangeIterator(1, 9));
  //=> [1, 2, 3, 4, 5, 6, 7, 8, 9]
  ```
- ```js
  Array.from(rangeIterator(1n, 9n, { endExclusive: true }));
  //=> [1n, 2n, 3n, 4n, 5n, 6n, 7n, 8n]
  ```
- ```js
  Array.from(rangeIterator(1, 9, { step: 0.5 }));
  //=> [1, 1.5, 2, 2.5, 3, 3.5, 4, 4.5, 5, 5.5, 6, 6.5, 7, 7.5, 8, 8.5, 9]
  ```
- ```js
  Array.from(rangeIterator("a", "z"));
  //=> ["a", "b", "c", ... +20 ..., "x", "y", "z"]
  ```
- ```js
  Array.from(rangeIterator(9, 1));
  //=> [9, 8, 7, 6, 5, 4, 3, 2, 1]
  ```
- ```js
  Array.from(rangeIterator(9n, 1n, { endExclusive: true }));
  //=> [9n, 8n, 7n, 6n, 5n, 4n, 3n, 2n]
  ```
- ```js
  Array.from(rangeIterator(9, 1, { step: 0.5 }));
  //=> [9, 8.5, 8, 7.5, 7, 6.5, 6, 5.5, 5, 4.5, 4, 3.5, 3, 2.5, 2, 1.5, 1]
  ```
- ```js
  Array.from(rangeIterator("z", "a"));
  //=> ["z", "y", "x", ... +20 ..., "c", "b", "a"]
  ```
