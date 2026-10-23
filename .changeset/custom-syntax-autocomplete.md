---
"@templatical/types": minor
"@templatical/editor": minor
---

Custom merge-tag syntaxes get autocomplete through `opener` and `closer`

`SyntaxPreset` takes two optional fields, `opener` and `closer`: the characters that open and close a data tag. With an `opener`, a custom syntax gets the same type-ahead as the built-in presets, in rich text and in every merge-tag field. Without one it has none, as before. `getSyntaxTriggerChar()` and `getSyntaxClosingChar()` return them ahead of the preset lookup.

```ts
mergeTags: {
  syntax: { value: /\{[^{}\s]+\}/g, logic: /(?!)/g, opener: "{", closer: "}" },
  tags: [{ label: "First name", value: "{first_name}" }],
}
```

The opener and closer can be the same characters, as in `%FIRSTNAME%`: a field skips every tag the `value` regex matches before it looks for an opener, so the popup stays closed right after a finished tag. A whitespace-only `opener` or `closer` counts as unset, and the editor warns once about it, and about a `closer` on a custom syntax that has no `opener`.
