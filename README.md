# How to install Sass and CSS Modules into your Create React App

This project was bootstrapped with [Create React App](https://github.com/facebookincubator/create-react-app).

`npm run eject`  
`yarn eject`

`npm i sass-loader node-sass --save`  
`yarn add sass-loader node-sass`

Modify the `webpack.config.dev.js` file

```
const ExtractTextPlugin = require('extract-text-webpack-plugin');

{
  exclude: [
    /\.html$/,
    /\.(js|jsx)$/,
    /\.css$/,
    /\.json$/,
    /\.bmp$/,
    /\.gif$/,
    /\.jpe?g$/,
    /\.png$/,
    /\.scss$/,
  ],
  loader: require.resolve('file-loader'),
  options: {
    name: 'static/media/[name].[hash:8].[ext]',
  },
},
{
  test: /\.css$/,
  use: ExtractTextPlugin.extract({
  fallback: 'style-loader',
    use: [
      {
        loader: 'css-loader',
        options: {
          modules: true,
          localIdentName: '[name]__[local]___[hash:base64:5]'
        }
      },
    'postcss-loader'
    ]
  })
},
{
  test: /\.scss$/,
  use: ExtractTextPlugin.extract({
  fallback: 'style-loader',
    use: [
      {
        loader: 'css-loader',
        options: {
          modules: true,
          sourceMap: true,
          importLoaders: 2,
          localIdentName: '[name]__[local]___[hash:base64:5]'
        }
      },
    'sass-loader'
    ]
  })
},

plugins: [
  new ExtractTextPlugin({ filename: 'styles.css', allChunks: true, disable: process.env.NODE_ENV !== 'production' }),
]  

```

* In order for hot reloading you will need to disable the Extract Text Plugin in the dev environment. This can be accomplished by adding `disable: process.env.NODE_ENV !== 'production'` in the ExtractTextPlugin options.


Create `postcss.config.js` file

```
module.exports = { plugins: [require('autoprefixer')] };
```
