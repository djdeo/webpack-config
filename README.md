# webpack demo

## folder structure
  
- dist
- src
  + index.html
  + main.js
  + /img/
  + /js/
  + /css/
    - style.css
    - style.scss
  + webpack.config.js
- package.json

## auto pack

`npm i webpack-dev-server -D` auto pack on Save
`npm i webpack -D`

## html-webpack-plugin

generate a index.html in ROM
`npm i html-webpack-plugin -D`

## style-loader

`npm i style-loader css-loader sass-loader node-sass -D`
for image url in style files, another loader is required
`npm i url-loader file-loader -D`

## webpack.config.js

```js
const path = require('path')
const htmlWebpackPlugin = require('html-webpack-plugin')

module.exports = {
  entry: path.join(__dirname, './src/main.js'),
  output:{
    path: path.join(__dirname, './dist'),
    filename: 'bundle.js'
  },
  plugins:[ // configs of all plugins
    new htmlWebpackPlugin({
      template: path.join(__dirname, './src/index.html'), // target temp file path
      filename: 'index.html' // setting ROM page name
    })
  ],
  module: { // configs of all third-party loaders
    rules: [
      { test: /\.css$/, use: ['style-loader', 'css-loader'] }, // loaders for css handling
      { test: /\.scss$/, use: ['style-loader', 'css-loader', 'sass-loader'] }, 
      { test: /\.(jpg|png|gif|bmp|jpeg)$/, use: 'url-loader?limit=7632?name=[hash:8]-[name].[ext]'}, 
      // handle url path in css file  
      // limit(byte): when value is greater than the image size, won't convert it to Base64 format
      // name: use the same filename, no hash name  '=[name].[ext]'; [hash:8] use 8 hash char
      { test: /\.(ttf|eot|svg|woff|woff2)$/, use: 'url-loader'}, // handle font file

    ]

  }
}
```

## package.json

```json
"script": {
  "dev": "webpack-dev-server --open --port 3000 --contentBase src --hot"
}

```

```js
//main.js
import './css/style.css'
import './css/style.scss'
```

