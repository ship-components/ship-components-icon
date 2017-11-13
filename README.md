# ship-components-icon
Material Design icons in css module format. Exports a css module that can be used with [webpack](http://webpack.github.io/).

## Usage

### CSS Modules
The component is a css file that imports fonts and images, therefore some [webpack](http://webpack.github.io/) configuration is needed to use it this way. Below is an example of usage as a CSS Module in a ES2015 class.

```js
import icon from 'ship-components-icon';

class Example extends React.Component {
  render() {
    return (
      <div>
        <span className={icon.games} />
      </div>
    );
  }
}
```

### Webpack Configuration
This module is designed to be used with webpack but requires a few loaders. PostCSS + Autoprefixer is not actually required, but is recommended.

```shell
npm install webpack css-loader style-loader file-loader extract-text-webpack-plugin postcss-loader autoprefixer --save-dev
```

Below are is a sample of how to setup the loaders:

```js
/**
 * Relevant Webpack Configuration
 */
{
  [...]
  module: {
    loaders: [
      // File loader for images (application icons)
      {
        test: /\.(png|svg|jpeg|jpg)/,
        include: [/ship-components-icon\/src/],
        loader: "file-loader?name=images/[name].[ext]"
      }
      // CSS loader with CSS Modules + PostCSS
      {
        test: /\.css$/,
        include: [/ship-components-icon\/src/],
        loader: ExtractTextPlugin.extract('style-loader', 'css-loader?modules&importLoaders=1&localIdentName=[name]__[local]___[hash:base64:5]!postcss-loader')
      }
    ]
  },
  plugins: [
    // Extract the css and put it in one file. Path is relative to output path
    new ExtractTextPlugin('../css/[name]-modules.css', { allChunks: true })
  ],
  [...]
}
```

## Tests

*There's currently a bug in Jest, so the units tests and they will not run.*

1. `npm install`
2. `npm test`

## License
The MIT License (MIT)

Copyright (c) 2015

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
