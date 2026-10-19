---
"@templatical/types": minor
"@templatical/editor": minor
---

Custom merge-tag syntaxes can enable autocomplete with `trigger` and `closing`

Autocomplete was only available for the built-in presets: the editor maps a preset to its opener by comparing regex sources, and a custom regex can't say which characters open and close a tag. Consumers whose platform uses its own tag format — single-brace `{first_name}`, Smarty-style `<% $email %>` — got the picker but no type-ahead.

`SyntaxPreset` gains two optional fields. `trigger` is the opener that starts autocomplete; `closing` is the closer that stops the popup reopening over a finished tag and is absorbed on insert. `getSyntaxTriggerChar()` and `getSyntaxClosingChar()` return them when set, ahead of the preset lookup, so both the rich-text and input/textarea surfaces pick them up. A custom syntax without `trigger` keeps autocomplete off, as before.

```ts
mergeTags: {
  syntax: { value: /\{[^{}\s]+\}/g, logic: /(?!)/g, trigger: "{", closing: "}" },
  tags: [{ label: "First name", value: "{first_name}" }],
}
```
