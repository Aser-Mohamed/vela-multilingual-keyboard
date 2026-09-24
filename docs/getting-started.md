# Getting started

This guide takes you from nothing to a working keyboard in five steps.

## 1. Copy the component

Put `Keyboard.ux` and the `keyboard-assets/` folder side by side under your app's `src/`:

```
src/components/
├── Keyboard.ux
└── keyboard-assets/   (21 PNG files)
```

`Keyboard.ux` loads its images from `./keyboard-assets/`. If they are separated, every key will be blank.

## 2. Declare features

Add these to `manifest.json` if they are not already there:

```json
"features": [
  { "name": "system.storage" },
  { "name": "system.device" }
]
```

- `system.device` detects the screen shape and size.
- `system.storage` remembers the last language.

## 3. Import the component

```html
<import name="custom-keyboard" src="../../components/Keyboard.ux"></import>
```

Adjust the path to match where your page lives.

## 4. Add it to your page

```html
<stack class="page">
  <!-- your content -->
  <custom-keyboard
    is-visible="{{ kbVisible }}"
    @keypress="onKeyPress"
    @delete="onDelete"
    @heightchange="onKeyboardHeight"
    @close="onClose"
  ></custom-keyboard>
</stack>
```

The keyboard is fixed to the bottom of its parent and fills the full width. Wrapping your page in `<stack>` is the easiest way to get that.

## 5. Handle the events

The keyboard never stores text. Your page keeps the string:

```js
export default {
  private: { text: "", kbVisible: true, barBottom: 220 },

  onKeyPress(e) {
    const value = e && e.detail ? e.detail.value : ""
    if (value) this.text += value
  },

  onDelete() {
    this.text = this.text.slice(0, -1)
  },

  onKeyboardHeight(e) {
    const h = e && e.detail ? e.detail.value : 0
    if (h) this.barBottom = h + 8
  },

  onClose() {
    this.kbVisible = false
  }
}
```

The space bar also arrives as `keypress`, with `value` set to `" "`.

## What you get

- Tap the language pill on the toolbar to switch between EN, AR, ES, DE, RU and FR. The choice is saved.
- Tap the symbols key for digits and punctuation.
- Tap the down chevron to fire `close`.

## Next steps

- Runnable page: [`examples/basic/index.ux`](../examples/basic/index.ux)
- All props and events: [api.md](api.md)
- Add a language: [languages.md](languages.md)
