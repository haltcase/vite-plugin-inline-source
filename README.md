# vite-plugin-inline-source

[![ci](https://github.com/bienzaaron/vite-plugin-inline-source/workflows/Node.js%20CI/badge.svg)](https://github.com/bienzaaron/vite-plugin-inline-source/actions/workflows/ci.yml)
[![npm version](https://img.shields.io/npm/v/vite-plugin-inline-source.svg?style=flat)](https://www.npmjs.com/package/vite-plugin-inline-source)


A Vite plugin which inlines source files in HTML files where the `inline-source` attribute is present. This is similar in premise to [vite-plugin-singlefile](https://github.com/richardtallent/vite-plugin-singlefile), but allows you to control which assets are inlined.

This plugin was heavily influenced by [markup-inline-loader](https://github.com/asnowwolf/markup-inline-loader) for webpack. I wanted the same functionality, but couldn't find a suitable replacement in the Vite ecosystem.

## Example Usage

Check out the interactive demo on [StackBlitz](https://stackblitz.com/edit/vite-cc3cbk?file=vite.config.js)!

**vite.config.ts**
```typescript
import { defineConfig } from "vite";
import inlineSource from "vite-plugin-inline-source";

export default defineConfig({
  plugins: [
    inlineSource(),
  ],
});
```

**style.css**
```css
body {
  background-color: red;
}
```

**index.html**
```html
<html>
  <style inline-source src="style.css"></style>
</html>
```

**Resulting index.html after build**
```html
<html>
  <style inline-source>body {
  background-color: red;
}
  </style>
</html>
```

## Options

### replaceTags

Tags that should be replaced in the HTML file.

For example, `style` and `script` tags are not replaced by default because the corresponding css/js file would not contain the `style` or `script` tag. However, with `svg` tags, the corresponding svg file would contain the `svg` tag, so the `svg` tags in the HTML file are replaced. See the unit tests for more explicit examples.

- **type**: `string[]`
- **default**: `['svg', 'math']`

### optimizeSvgs

Whether or not to optimize SVGs using [svgo](https://github.com/svg/svgo).

- **type**: `boolean`
- **default**: `true`

### svgoOptions

Options to pass to [svgo](https://github.com/svg/svgo). Only used if `optimizeSvgs` is `true`.

- **type**: `OptimizeOptions`
- **default**: `{}`
