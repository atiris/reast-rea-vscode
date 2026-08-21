# Rea Language — VS Code Extension

Syntax highlighting for the [Rea interactive fiction language](https://rea.st) used by the Reast platform.

## Features

- Full syntax highlighting for `.rea` files and `.rext` extension modules
- All Rea constructs: commands `{ }`, references `[ ]`, formatting, choices, diverts
- Code folding on headings and block commands (`begin`/`end`)
- Auto-closing pairs for brackets, quotes, and formatting markers
- Comment toggling (`{comment ...}` and `{comment begin}...{end comment}`)

## Installation

### From VSIX (local build)

```bash
cd tools/vscode-rea
npx @vscode/vsce package
code --install-extension rea-language-0.1.0.vsix
```

### From source (development)

1. Open `tools/vscode-rea/` in VS Code
2. Press `F5` to launch Extension Development Host
3. Open any `.rea` or `.rext` file to see highlighting

## Highlighted Elements

| Element      | Example             | Color Category     |
| ------------ | ------------------- | ------------------ |
| Headings     | `## Chapter`        | Heading (markup)   |
| Commands     | `{set x = 1}`       | Keyword + variable |
| Control flow | `{if x begin}`      | Keyword (control)  |
| Choices      | `* [Open door]`     | Keyword + string   |
| Dialogue     | `@elena: "Hi"`      | Entity + string    |
| Diverts      | `-> forest`         | Keyword + label    |
| Variables    | `{player.name}`     | Variable           |
| Functions    | `{random(1,6)}`     | Function call      |
| Card refs    | `[@elena]` `[$key]` | Entity (card)      |
| Comments     | `{comment note}`    | Comment            |
| Media        | `[!alt < src]`      | Link + string      |
| Formatting   | `_italic_ *bold*`   | Markup             |
| Varying text | `{first\|second}`   | String (varying)   |

## Reuse in Other Editors

The `syntaxes/rea.tmLanguage.json` TextMate grammar is compatible with:

- **VS Code** (this extension)
- **Sublime Text** (copy to Packages/User/)
- **JetBrains IDEs** (via TextMate Bundles plugin)
- **GitHub Linguist** (for repository syntax highlighting)
- **Shiki / VitePress** (already used in project docs)
- **Any editor** supporting TextMate grammars

## Development

`syntaxes/rea.tmLanguage.json` is the canonical grammar. The docs site needs the file inside its own package (VitePress imports it from `.vitepress/config.ts`, and the two live in separate submodules), so it keeps a mirror. When Rea syntax evolves:

1. Update `syntaxes/rea.tmLanguage.json`
2. Copy it over `modules/docs/.vitepress/rea.tmLanguage.json` — never edit that copy directly
3. Rebuild VSIX for distribution

The orchestrator's `scripts/check-grammar-sync.mjs` compares the two as normalized JSON in pre-commit and in CI, so a forgotten step 2 fails the next commit instead of drifting quietly.

## License

MIT
