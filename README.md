# Rollup plugin postcss lit

Rollup plugin to load PostCSS-processed stylesheets in LitElement components

![](https://github.com/umbopepato/rollup-plugin-postcss-lit/workflows/Node.js%20CI/badge.svg)
[![](https://img.shields.io/npm/v/rollup-plugin-postcss-lit.svg)](https://npmjs.org/package/rollup-plugin-postcss-lit)
[![](https://img.shields.io/badge/license-MIT-brightgreen)](LICENSE)

## Install

```bash
$ npm i -D rollup-plugin-postcss-lit
```

## Usage

Add `postcssLit` plugin _after_ `postcss`. This wraps PostCSS-processed styles in LitElement's `css`
template literal tag so you can import them directly in your components. 

```javascript
// rollup.config.js
import postcss from 'rollup-plugin-postcss';
import postcssLit from 'rollup-plugin-postcss-lit';

export default {
  input: 'entry.js',
  output: {
    // ...
  },
  plugins: [
    postcss({
      // ...
    }),
    postcssLit(),
  ],
}
```

Add PostCSSed stylesheets to your LitElement components:

```typescript
import {customElement, LitElement, css} from 'lit-element';
import myStyles from './styles.css';
import otherStyles from './other-styles.scss';

@customElement('my-component')
export class MyComponent extends LitElement {
  
  // Add a single style
  static styles = myStyles;
  
  // Or more!
  static styles = [myStyles, otherStyles, css`
    .foo {
      color: ${...};
    }
  `];
  
  render() {
    // ...
  }
}
```

<details>
<summary>JS version</summary>

```javascript
import {LitElement, css} from 'lit-element';
import myStyles from './styles.css';
import otherStyles from './other-styles.scss';

export class MyComponent extends LitElement {
  
  // Add a single style
  static get styles() {
    return myStyles;
  }
  
  // Or more!
  static get styles() {
    return [myStyles, otherStyles, css`
      .foo {
        color: ${...};
      }
    `];
  }
  
  render() {
    // ...
  }
}

customElements.define('my-component', MyComponent);
```

</details>

## Options

```javascript
postcssLit({

  // A glob (or array of globs) of files to include.
  // Default: **/*.{css,sss,pcss,styl,stylus,sass,scss,less}
  include: ...,

  // A glob (or array of globs) of files to exclude.
  // Default: null
  exclude: ...,

}),
```

## When should I use it?

This plugin is meant to be used with [`rollup-plugin-postcss`](https://github.com/egoist/rollup-plugin-postcss).
If you only need to load plain css files in your LitElement components,
consider using [`rollup-plugin-lit-css`](https://github.com/bennypowers/rollup-plugin-lit-css).

### Contributors

<a href="https://github.com/umbopepato/rollup-plugin-postcss-lit/graphs/contributors">
  <img src="https://contributors-img.web.app/image?repo=umbopepato/rollup-plugin-postcss-lit" height="40"/>
</a>


### License

This project is licensed under the MIT License, see [LICENSE](./LICENSE) for details. 
