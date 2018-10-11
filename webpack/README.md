# Webpack

## Guides

[Getting starting (official docs)](https://webpack.js.org/guides/getting-started/)
[Webpack 4 Fundamentals](https://frontendmasters.com/courses/webpack-fundamentals/)

## Installation

`npm init`
Starts an npm project, creates a package.json file

`npm install webpack webpack-cli --save-dev`
Creates nod_modules where npm libraries will be stored

`touch webpack.config.js`
Create a config file for webpack
Add the following:
```js
const path = require('path');

module.exports = {
  entry: './src/index.js',
  output: {
    filename: 'main.js',
    path: path.resolve(__dirname, 'dist')
  }
};
```

create a `src` and `dist` folders

Add index.js to source and get it to do something trivial like console log hell from index.js
Add a index.html file to dist and link it:

```html
<!doctype html>
<html>
  <head>
    <title>Getting Started</title>
    <script src="https://unpkg.com/lodash@4.16.6"></script>
  </head>
  <body>
    <script src="main.js"></script>
  </body>
</html>
```

Then run `npx webpack` to create main.js in dist

### Add an automation script

In package.json you can add script commands. For example:
```json
"scripts": {
    "webpack": "webpack",
    "dev": "npm run webpack"
}
```

## Combining JS files

Let's create two further JS files in the `src` directory:

```console
cd src
echo "console.log('Hello from header');" > header.js
echo "console.log('Hello from footer');" > footer.js
```

Then lets's require those files in the index.js

```js
import './header';
console.log("Working");
import './footer';
```

Then run webpack:
`npm run webpack`

Gotcha: You should get the console output:

```console
Hello from header
Hello from footer
Working
```

The import statements are hoisted

## Adding JQuery

Let's add JQuery.

First add the following to index.html:
`<div id="app"></div>`

Then add the following to index.js:

```js
$("#app").append("<p>Hello from JQuery!</p>");
```

This line will throw an error in the console because it is dependent on JQuery. We need to add JQuery as a dependency.
First install JQuery from npm:

`npm install --save jquery`

Then import it at the top of index.js:

`import $ from 'jquery';`

Then run the code and "Hello from JQuery" should appear on the page.

## ES6

Let's try out an ES6 command
```js
# Using both ES6 and JQuery!
let foo = () => "bar!";
$("#app").append("<p>" + foo() + "</p>");
```

In order to transpile it first install babel:

`npm install -D babel-loader @babel/core @babel/preset-env`

Then add it to the webpack config:

```js
module: {
    rules: [
      {
        test: /\.m?js$/,
        exclude: /(node_modules|bower_components)/,
        use: {
          loader: 'babel-loader',
          options: {
            presets: ['@babel/preset-env'],
            plugins: [require('@babel/plugin-proposal-object-rest-spread')]
          }
        }
      }
    ]
}
```

## Add watch mode

Add the following to scripts:

```js
"dev": "npm run webpack -- --mode development --watch"
```

## Adding CSS

Let's create a CSS file:

`touch src/styles.css`

Add some sorta style:

```css
#app {
    background-color: brown;
}
```

And include it in `index.js`:

`import './styles.css';`

This will throw an error because there is no loader for css yet.
We can fix that. First by installing css-loader AND style-loader:

`npm install --save-dev css-loader`

`npm install style-loader --save-dev`

Then we can add it to module rules:

```js
{
    test: /\.css$/,
    use: [
        "style-loader",
        "css-loader"
    ]
}
```
