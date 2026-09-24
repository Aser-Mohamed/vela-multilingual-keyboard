# Troubleshooting

## Keys are blank or images are missing

`keyboard-assets/` is not next to `Keyboard.ux`. The component loads images from `./keyboard-assets/`, so keep the folder beside the file.

## Nothing appears

- Check `is-visible` is `true`.
- Put the keyboard inside a `<stack>` (or any positioned parent), because it anchors to the bottom of its parent.
- Confirm `system.device` is declared in `manifest.json`. The keyboard renders only after it has detected the screen.

## The language is not remembered

Declare `system.storage` in `manifest.json`. The value is saved under `KBD_LANG`.

## I press keys but no text shows

The keyboard only sends events. Append `e.detail.value` to your own string in the `keypress` handler and clear or trim it in the `delete` handler.

## Language or delete key is missing on a Xiaomi Band

This is a known limitation of pill-shaped screens. See [Pill-shaped screens](screens.md#pill-shaped-screens).

## Arabic text looks reversed or misaligned

Vela has no `direction` property. The keyboard sends characters in the order they are typed, so align your text element yourself (for example `text-align: right`).

## Shifted `ß` stays `ß`

This is intended. In JavaScript `"ß".toUpperCase()` is `"SS"`, two characters, so the key keeps its lowercase form.

## Everything is twice as large as expected

Check `designWidth` in `manifest.json`. See [Design width](screens.md#design-width).

## Upgrading from an older copy that imported `../common/i18n/index.js`

That import is gone. The one string it supplied is now the `cancel-label` prop. Remove the i18n import from any copy of `Keyboard.ux` you patched yourself.
