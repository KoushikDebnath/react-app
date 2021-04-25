# react-app
React app setup done without create-react-app

#Process

Step 1: Initialize NPM (Node Package Manager)

mkdir react-app
cd react-app
npm init


Step 2: Install React, Webpack, and Babel

npm install react react-dom 
npm install --save-dev webpack webpack-cli webpack-dev-server html-webpack-plugin @babel/core babel-loader @babel/preset-env @babel/preset-react

Here's what each package does:
react: UI library for creating modular components
react-dom: enables us to render the React within the browser DOM
webpack: bundler that converts your source code into production-ready output
webpack-cli: allows webpack to work with CLI commands
webpack-dev-server: transforms our source code and serves it on a web server as we develop it continuously. This helps use see the output of your code in the browser.
html-webpack-plugin: an extension to webpack that adds the basic index html file
@babel/core: a JavaScript transpiler to converts modern JavaScript into a production-ready version that's compatible with all browsers.
babel-loader: connects Babel to webpack's build process
@babel/preset-env: group of commonly used Babel plugins bundled into a preset that converts modern JavaScript features into widely compatible syntax
@babel/preset-react: React-specific Babel plugins that convert JSX syntax into plain old JavaScript that browsers can understand

Step 3: Create the files

touch webpack.config.js
mkdir src
cd src
touch index.js
touch index.html

 webpack.config.js ----
 const path = require('path');
const HtmlWebpackPlugin = require('html-webpack-plugin');

module.exports = {
  // the output bundle won't be optimized for production but suitable for development
  mode: 'development',
  // the app entry point is /src/index.js
  entry: path.resolve(__dirname, 'src', 'index.js'),
  output: {
  	// the output of the webpack build will be in /dist directory
    path: path.resolve(__dirname, 'dist'),
    // the filename of the JS bundle will be bundle.js
    filename: 'bundle.js'
  },
  module: {
    rules: [
      {
      	// for any file with a suffix of js or jsx
        test: /\.jsx?$/,
        // ignore transpiling JavaScript from node_modules as it should be that state
        exclude: /node_modules/,
        // use the babel-loader for transpiling JavaScript to a suitable format
        loader: 'babel-loader',
        options: {
          // attach the presets to the loader (most projects use .babelrc file instead)
          presets: ["@babel/preset-env", "@babel/preset-react"]
        }
      }
    ]
  },
  // add a custom index.html as the template
  plugins: [new HtmlWebpackPlugin({ template: path.resolve(__dirname, 'src', 'index.html') })]
};


src/index.js----------------
   import React from 'react';
  import ReactDOM from 'react-dom';

  ReactDOM.render(<h1>Helloworld React!</h1>, document.getElementById('root'));
  
  src/index.html--------------------
  <html>
  <head>
    <title>Hello world App</title>
  </head>
  <body>
  <div id="root"></div>
  <script src="bundle.js"></script>
  </body>
</html>

 Step 4: Create NPM run scripts
 
  #package.json
    ...
  "scripts": {
    "start": "webpack-dev-server --open",
    "build": "webpack"
  },
  ...
  
  
  

