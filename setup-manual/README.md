## Environment Setup Lesson 1

@babel/preset-env - helps babel to convert ES6, ES7 and ES8 code to ES5.
@babel/preset-react - transforms JSX to JavaScript.

Create directories with these commands:
$ mkdir setup-manual
$ cd setup-manual
$ mkdir public src
$ touch public/index.html src/app.js

public/index.html
```
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>React App</title>
  </head>

  <body>
    <div id="root"></div>

    <script src="./bundle.js"></script>
  </body>
</html>
```

Install Webpack & React:
```
npm install webpack webpack-cli --save-dev
```

Add the webpack command inside package.json:
```
"scripts": {
    "start": "webpack --mode=development",
    "build": "webpack --mode=production"
}
```

Intall React
```
npm install react react-dom
```

Import react and react-dom inside our app.js file and add react code.
```
import React from 'react';
import ReactDOM from 'react-dom';

const template = React.createElement('p', {}, 'Hello from react');

ReactDOM.render(template, document.getElementById('root'));
```

JSX
```
import React from 'react';
import ReactDOM from 'react-dom';

const template = <p>Hello from react</p>;

ReactDOM.render(template, document.getElementById('root'));
```
Note: Error

Install and configure Babel
```
npm install @babel/core @babel/preset-env @babel/preset-react babel-loader --save-dev
```

Configure .babelrc
```
{
  "presets": ["@babel/preset-env", "@babel/preset-react"]
}
```

webpack.config.js
```
const path = require('path');

module.exports = {
  entry: './src/app.js',
  output: {
    path: path.join(__dirname, 'public'),
    filename: 'bundle.js'
  },
  module: {
    rules: [
      {
        test: /\.js$/,
        exclude: /node_modules/,
        loader: 'babel-loader'
      }
    ]
  }
};
```

Install DevServer
```
npm install webpack-dev-server --save-dev
```

Add webpack.config.server
```
devServer: {
  contentBase: path.join(__dirname, 'public')
}
```

Add webpack-dev-server package.json
```
"dev-server": "webpack-dev-server"
```

Loading the Styles
```
mkdir src/styles && touch src/styles/styles.css
```

src/styles/styles.css
```
* {
  color: blue;
}
```

```
npm install css-loader style-loader --save-dev
```

css-loader: Allows webpack to load our CSS assets.
style-loader: Take CSS and adds it to the DOM by injecting a <style> tag.

webpack.config.js
```
const path = require('path');

module.exports = {
  entry: './src/app.js',
  output: {
    path: path.join(__dirname, 'public'),
    filename: 'bundle.js'
  },
  module: {
    rules: [
      {
        test: /\.js$/,
        exclude: /node_modules/,
        loader: 'babel-loader'
      },
      // New rules to load css
      {
        test: /\.css$/,
        use: ['style-loader', 'css-loader']
      }
    ]
  },
  devtool: 'cheap-module-eval-source-map',
  devServer: {
    contentBase: path.join(__dirname, 'public')
  }
};
```

Import style.css inside app.js file and run dev-server to see the effect.
```
import React from 'react';
import ReactDOM from 'react-dom';
import './styles/styles.css';

const template = <p>Hello from react</p>;

ReactDOM.render(template, document.getElementById('root'));
```http://localhost:3000/
