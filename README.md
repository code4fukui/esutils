# esutils

> 日本語のREADMEはこちらです: [README.ja.md](README.ja.md)

[
![NPM version](https://img.shields.io/npm/v/esutils.svg)
](https://www.npmjs.com/package/esutils)
[
![Build Status](https://travis-ci.org/estools/esutils.svg?branch=master)
](https://travis-ci.org/estools/esutils)
[
![License](https://img.shields.io/npm/l/esutils.svg)
](LICENSE.BSD)

A utility library for ECMAScript language tools, providing functions for AST node validation, character code checks, and keyword/identifier analysis.

## Installation

```bash
npm install esutils
```

## Usage

```javascript
import { ast, code, keyword } from 'esutils';

// Example: Check if an AST node is an expression
const node = { type: 'Literal', value: 42 };
if (ast.isExpression(node)) {
  console.log('It is an expression!');
}

// Example: Check if a string is a valid ES6 identifier
if (keyword.isIdentifierES6('myVar')) {
  console.log('Valid identifier.');
}
```

## API

### `ast`

Utilities for working with ECMAScript AST nodes.

*   `ast.isExpression(node)`: Returns `true` if `node` is an `Expression` as defined in ECMA-262, 5.1, Section 11.
*   `ast.isStatement(node)`: Returns `true` if `node` is a `Statement` as defined in ECMA-262, 5.1, Section 12.
*   `ast.isIterationStatement(node)`: Returns `true` if `node` is an `IterationStatement` (e.g., `ForStatement`, `WhileStatement`).
*   `ast.isSourceElement(node)`: Returns `true` if `node` is a `SourceElement` (a `Statement` or `FunctionDeclaration`).
*   `ast.trailingStatement(node)`: Returns the trailing `Statement` of a given node (e.g., the `body` of a `ForStatement` or the `consequent` of an `IfStatement`).
*   `ast.isProblematicIfStatement(node)`: Returns `true` if `node` is a problematic `IfStatement` that could cause a "dangling else" ambiguity (a nested `if` without an `else` inside another `if`'s `consequent`).

### `code`

Utilities for checking character codes.

*   `code.isDecimalDigit(code)`: Checks for decimal digits (`0-9`).
*   `code.isHexDigit(code)`: Checks for hexadecimal digits (`0-9`, `a-f`, `A-F`).
*   `code.isOctalDigit(code)`: Checks for octal digits (`0-7`).
*   `code.isWhiteSpace(code)`: Checks for whitespace characters as defined by the ECMAScript standard.
*   `code.isLineTerminator(code)`: Checks for line terminator characters.
*   `code.isIdentifierStartES5(code)` / `code.isIdentifierStartES6(code)`: Checks if a character code is a valid start of an identifier for the specified ECMAScript version.
*   `code.isIdentifierPartES5(code)` / `code.isIdentifierPartES6(code)`: Checks if a character code is a valid part of an identifier for the specified ECMAScript version.

### `keyword`

Utilities for validating identifiers and keywords. Functions that accept a `strict` boolean parameter check against keywords reserved in strict mode.

*   `keyword.isKeywordES5(id, strict)` / `keyword.isKeywordES6(id, strict)`
*   `keyword.isReservedWordES5(id, strict)` / `keyword.isReservedWordES6(id, strict)`
*   `keyword.isRestrictedWord(id)`: Checks for `eval` and `arguments`.
*   `keyword.isIdentifierNameES5(id)` / `keyword.isIdentifierNameES6(id)`: Checks if a string is a valid identifier name (before checking for reserved words).
*   `keyword.isIdentifierES5(id, strict)` / `keyword.isIdentifierES6(id, strict)`: Checks if a string is a valid identifier (and not a reserved word).

## License

[BSD-2-Clause](LICENSE.BSD)