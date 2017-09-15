Once you install Lektor and want to add Webpack, follow the instructions here: https://github.com/lektor/lektor-webpack-support

And then make following changes:

### webpack.config.js

**modules**

change
```js
  resolve: {
    modulesDirectories: ['node_modules'],
    extensions: ['', '.js']
  },
...
```
for
```
  resolve: {
    modules: ['node_modules'],
    extensions: ['.js']
  },
...
```
**scss-loader**

change
```js
 {
    test: /\.scss$/,
    loader: ExtractTextPlugin.extract('style-loader', 'css-loader!sass-loader')
 },
...
```
for
```js
 {
    test: /\.scss$/,
    use: ExtractTextPlugin.extract({fallback:"style-loader",use:["css-loader","sass-loader"]})
  },
...
```
**DedupePlugin**

remove
```js
new webpack.optimize.DedupePlugin()
```

### layout.html
link stylesheet with
```html
<link rel="stylesheet" href="{{ '/static/gen/styles.css'|url }}">
```
