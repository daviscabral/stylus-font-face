[![NPM version](https://img.shields.io/npm/v/stylus-font-face.svg)](http://badge.fury.io/js/stylus-font-face)
[![Dependency Status](https://img.shields.io/gemnasium/pirxpilot/stylus-font-face.svg)](https://gemnasium.com/pirxpilot/stylus-font-face)

# stylus-font-face

[Stylus] plugin that generates [bulletproot @font-face syntax][1] optionally with data url.

## Usage


Install using `npm`

    npm install -S stylus-font-face

See [Nib] usage and installation.

First you have to tell stylus about the plugin:

```js
var fontFace = require('stylus-font-face');
stylus.use(fontFace());
```

or if you are using command line:

    stylus --use ./node_modules/stylus-font-face

Then you can use it in your stylus files

```stylus
@import 'font-face'

font-face(family-name, font-name)
font-face-inline(family-name, font-name)
```

## API

Both `font-face` and `font-face-inline` take the same parameters:

- `family` - font family name that you want to use in CSS
- `file` - base name of the file - optional defaults to `family`
- `path` - defaults to `fonts` - assumes that font files are located in `fonts` directory relative to
  your `.styl` file
- `weight` - font weight - defaults to `normal`
- `style` - font style - defaults to `normal`

## Generated CSS

`font-face` generates:

```css
@font-face {
  font-family: 'font-icon';
  src:url('fonts/iconfont.eot');
  src:url('fonts/iconfont.eot?#iefix') format('embedded-opentype'),
    url('fonts/iconfont.woff') format('woff'),
    url('fonts/iconfont.ttf') format('truetype'),
    url('fonts/iconfont.svg#font-icon') format('svg');
  font-weight: normal;
  font-style: normal;
}

```

`font-face-inline` attempts to inline fonts directly in CSS as BASE64 data:

```css
@font-face {
  font-family: 'font-icon';
  src: url('iconfont.eot?') format('embedded-opentype');
  }

@font-face {
  font-family: 'font-icon';
    url(data:font/truetype;charset=utf-8;base64,BASE64_ENCODED_DATA_HERE)  format('truetype'),
    url(data:font/woff;charset=utf-8;base64,BASE64_ENCODED_DATA_HERE)  format('woff'),
    url('iconfont.svg#font-icon') format('svg');
}
```

Only `.woff` and `.ttf` are inlined and only. By default only files smaller than 10000k are inlined, but that can be changed by passing a `limit` option to stylus.

    stylus --use ./node_modules/stylus-font-face --with {limit:80000}

You can run `make check` and examine `test/main.css' file to see the how the macros work with real fonts.
Example fonts were generated by [Icomoon] app.

## License

MIT


[Stylus]: http://learnboost.github.io/stylus/
[Nib]: http://visionmedia.github.io/nib/
[Icomoon]: http://icomoon.io/

[1]: http://www.fontspring.com/blog/the-new-bulletproof-font-face-syntax
