# API reference

Tag name is your choice at import. These docs use `custom-keyboard`.

## Props

| Prop | Type | Default | Description |
| --- | --- | --- | --- |
| `is-visible` | boolean | `false` | Shows the keyboard when `true`. Hiding it also closes the language picker. |
| `cancel-label` | string | `"Cancel"` | Text of the Cancel button in the language picker. This is the only UI text in the component. |

The keyboard appears once it has detected the screen, so the first frame after it becomes visible can be a few milliseconds late.

## Events

| Event | Payload | Fired when |
| --- | --- | --- |
| `keypress` | `{ detail: { value: string } }` | A character key or the space bar is pressed |
| `delete` | none | The delete key is pressed |
| `heightchange` | `{ detail: { value: number } }` | The keyboard's height in px is known or changes |
| `close` | none | The dismiss chevron is pressed |

### Reading the payload

Read it defensively so the same handler works in either event shape:

```js
const value = e && e.detail ? e.detail.value : e ? e.value : ""
```

### Notes

- `keypress` gives the exact character, already upper-cased when shift is on.
- `heightchange` fires more than once (after screen detection, and after shift, symbols and language changes). Keep the handler safe to run repeatedly.

## Storage

| Key | Values | Purpose |
| --- | --- | --- |
| `KBD_LANG` | `EN` `AR` `ES` `DE` `RU` `FR` | Last selected layout. Read on start, written when the user picks a layout. |

It is independent of your app's own language setting. A user can type Arabic while your UI is in English.

## Requirements

| Feature | Used for |
| --- | --- |
| `@system.device` | Screen shape and width |
| `@system.storage` | Remembering the layout |
