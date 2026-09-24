# Languages and layouts

## Built-in layouts

| Code | Language | Letter rows | Shift | Notes |
| --- | --- | --- | --- | --- |
| `EN` | English | 10 / 9 / 7 | Yes | QWERTY |
| `AR` | Arabic | 13 / 11 / 9 | No | Uses the Arabic comma `،` |
| `RU` | Russian | 12 / 11 / 10 | Yes | ЙЦУКЕН, includes `ё` |
| `ES` | Spanish | 10 / 10 / 7 | Yes | Has `ñ`; `¿ ¡` are on the symbols layer |
| `DE` | German | 11 / 11 / 8 | Yes | QWERTZ with `ü ö ä ß` |
| `FR` | French | 10 / 10 / 6 | Yes | AZERTY; `é è ç à ù` are on the symbols layer |

Letters that do not fit on a row go on the symbols layer, because the keyboard has no long-press for accents.

Users switch layouts from the language pill on the toolbar. The choice is saved as `KBD_LANG`.

## Add a language

All settings are at the top of the `<script>` block in `Keyboard.ux`.

**Step 1.** Add exactly three rows to `LAYOUTS`:

```js
IT: [
  ["q","w","e","r","t","y","u","i","o","p"],
  ["a","s","d","f","g","h","j","k","l"],
  ["z","x","c","v","b","n","m"]
],
```

**Step 2.** Add the code to `langCodes`. The order here is the order in the picker:

```js
langCodes: ["EN", "AR", "ES", "DE", "RU", "FR", "IT"],
```

That is enough. The toolbar label is derived from the code (`IT` shows as `It`) and the key artwork is blank, so letters are drawn on top of any layout.

## Optional tweaks

**Extra symbols for a language.** Add nine keys for the third symbols row:

```js
const SYM_ROW3 = {
  // ...
  IT: ["à", "è", "é", "ì", "ò", "ù", "!", "?", "."]
}
```

**A script with no upper and lower case.** Add it to `CASELESS` with its own comma character. Shift is then disabled:

```js
const CASELESS = { AR: "،", HE: "," }
```

## Good to know

- **Row width.** Arabic's 13 keys on the first row is close to the practical maximum on a round screen. Keep new rows at or below that.
- **Uppercase.** Each key is upper-cased with `toUpperCase()`. If that produces more than one character (`ß` becomes `SS`), the key stays lowercase so one press always types one character.
