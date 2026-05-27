# Rea Language — VS Code Extension

Syntax highlighting for the [Rea interactive fiction language](https://rea.st) used by the Reast platform.

## Features

- Full syntax highlighting for `.rea` files
- All Rea constructs: commands `{ }`, references `[ ]`, formatting, choices, diverts
- Code folding on headings and block commands (`begin`/`end`)
- Auto-closing pairs for brackets, quotes, and formatting markers
- Comment toggling (`{// ...}` and `{comment begin}...{end comment}`)

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
3. Open any `.rea` file to see highlighting

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
| Comments     | `{// note}`         | Comment            |
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

The grammar is the single source of truth. When Rea syntax evolves:

1. Update `syntaxes/rea.tmLanguage.json`
2. Copy to `modules/docs/.vitepress/rea.tmLanguage.json` for docs
3. Rebuild VSIX for distribution

## License

MIT
