# esutils

[
![NPM version](https://img.shields.io/npm/v/esutils.svg)
](https://www.npmjs.com/package/esutils)
[
![Build Status](https://travis-ci.org/estools/esutils.svg?branch=master)
](https://travis-ci.org/estools/esutils)
[
![License](https://img.shields.io/npm/l/esutils.svg)
](LICENSE.BSD)

ECMAScript言語ツール向けのユーティリティライブラリです。ASTノードの検証、文字コードのチェック、キーワードや識別子の分析を行う関数を提供します。

## インストール

```bash
npm install esutils
```

## 使い方

```javascript
import { ast, code, keyword } from 'esutils';

// 例: ASTノードが式であるかを確認する
const node = { type: 'Literal', value: 42 };
if (ast.isExpression(node)) {
  console.log('It is an expression!');
}

// 例: 文字列が有効なES6の識別子であるかを確認する
if (keyword.isIdentifierES6('myVar')) {
  console.log('Valid identifier.');
}
```

## API

### `ast`

ECMAScriptのASTノードを扱うためのユーティリティです。

*   `ast.isExpression(node)`: `node`がECMA-262 5.1の第11章で定義されている`Expression`（式）である場合に`true`を返します。
*   `ast.isStatement(node)`: `node`がECMA-262 5.1の第12章で定義されている`Statement`（文）である場合に`true`を返します。
*   `ast.isIterationStatement(node)`: `node`が`IterationStatement`（反復文、例: `ForStatement`、`WhileStatement`）である場合に`true`を返します。
*   `ast.isSourceElement(node)`: `node`が`SourceElement`（ソース要素、つまり`Statement`または`FunctionDeclaration`）である場合に`true`を返します。
*   `ast.trailingStatement(node)`: 指定されたノードの末尾にある`Statement`（例: `ForStatement`の`body`や、`IfStatement`の`consequent`）を返します。
*   `ast.isProblematicIfStatement(node)`: `node`が「dangling else（ぶら下がりelse）」の曖昧さを引き起こす可能性のある、問題のある`IfStatement`（別の`if`の`consequent`内に、`else`を持たない`if`がネストされている状態）である場合に`true`を返します。

### `code`

文字コードをチェックするためのユーティリティです。

*   `code.isDecimalDigit(code)`: 10進数の数字（`0-9`）であるかを確認します。
*   `code.isHexDigit(code)`: 16進数の数字（`0-9`、`a-f`、`A-F`）であるかを確認します。
*   `code.isOctalDigit(code)`: 8進数の数字（`0-7`）であるかを確認します。
*   `code.isWhiteSpace(code)`: ECMAScript標準で定義されている空白文字であるかを確認します。
*   `code.isLineTerminator(code)`: 行終端文字であるかを確認します。
*   `code.isIdentifierStartES5(code)` / `code.isIdentifierStartES6(code)`: 文字コードが、指定されたECMAScriptバージョンにおいて識別子の最初の文字として有効であるかを確認します。
*   `code.isIdentifierPartES5(code)` / `code.isIdentifierPartES6(code)`: 文字コードが、指定されたECMAScriptバージョンにおいて識別子の一部として有効であるかを確認します。

### `keyword`

識別子とキーワードを検証するためのユーティリティです。`strict`という真偽値パラメータを受け取る関数は、Strictモード（厳格モード）で予約されているキーワードかどうかも考慮してチェックします。

*   `keyword.isKeywordES5(id, strict)` / `keyword.isKeywordES6(id, strict)`
*   `keyword.isReservedWordES5(id, strict)` / `keyword.isReservedWordES6(id, strict)`
*   `keyword.isRestrictedWord(id)`: `eval`および`arguments`であるかを確認します。
*   `keyword.isIdentifierNameES5(id)` / `keyword.isIdentifierNameES6(id)`: 文字列が有効な識別子名であるかを確認します（予約語のチェックは行いません）。
*   `keyword.isIdentifierES5(id, strict)` / `keyword.isIdentifierES6(id, strict)`: 文字列が有効な識別子であるか（かつ予約語ではないか）を確認します。

## ライセンス

[BSD-2-Clause](LICENSE.BSD)
