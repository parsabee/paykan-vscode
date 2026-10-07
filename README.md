# PaykanLang for Visual Studio Code

Syntax highlighting for [PaykanLang](https://github.com/parsabee/PaykanLang) (`.pkn` files).

## Features

- Highlighting for keywords, declarations (`fn`, `class`, `enum`), generics, built-in types
  (`int`, `float`, `bool`, `char`, `Str`, `Obj`, `File`, …) and built-in functions
  (`println`, `printerr`, `open`, …).
- Literals: strings and characters with their escapes, integers, floats, `True`/`False`,
  `None`, and tuple indices (`t.0.1`).
- Module paths in `import` declarations, `mod::name` qualifiers, and `Enum::Variant`.
- `mov` is marked as invalid, because the language removed it.
- `//` comment toggling, bracket matching, auto-closing pairs and indentation after `{`.

There is no language server yet, so there are no diagnostics, completion or go-to-definition.

## Installing

The extension isn't on the Marketplace yet. Build a `.vsix` and install it:

```sh
npm install
npx vsce package
code --install-extension paykan-0.0.1.vsix
```

Or, in VS Code, run **Extensions: Install from VSIX…** and pick the file.

## Development

The grammar is [`syntaxes/paykan.tmLanguage.json`](syntaxes/paykan.tmLanguage.json). It follows
the lexical rules in PaykanLang's
[`docs/grammar.md`](https://github.com/parsabee/PaykanLang/blob/develop/docs/grammar.md); when the
language gains or loses a keyword, update both.

Tests are [`vscode-tmgrammar-test`](https://github.com/PanAeon/vscode-tmgrammar-test) files in
`tests/`. Each source line is followed by assertion lines that name the scopes a token must have:

```
  x = t.0;
//      ^ constant.numeric.integer.tuple-index.paykan
```

Run them with `npm test`. CI runs the tests and packages the extension on every push and pull
request.

To try a change in VS Code, open this folder and press F5. That starts an Extension Development
Host with the extension loaded; open any `.pkn` file there. **Developer: Inspect Editor Tokens
and Scopes** shows the scopes under the cursor.

## License

MIT
