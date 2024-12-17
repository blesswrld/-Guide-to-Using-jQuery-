
# Using the jQuery Library on a Web Page

jQuery is a popular JavaScript library that simplifies DOM manipulation, event handling, animations, and more. This guide explains how to include jQuery in your project and utilize its features.

## Adding jQuery

### 1. Using a CDN
You can include the jQuery library via a CDN (Content Delivery Network). This is a fast and easy method.
Add the following `<script>` tag to your `<head>` or before the closing `<body>` tag:

```html
<script src="https://code.jquery.com/jquery-3.6.4.min.js"></script>
```

### 2. Local Installation
Download the jQuery library from the official website: [https://jquery.com/download/](https://jquery.com/download/).

Add the file to your project (e.g., in a `js` folder) and include it as follows:

```html
<script src="js/jquery-3.6.4.min.js"></script>
```

## Setting Up a Project with Webpack
If you're using Webpack, you can install jQuery as a module:

### Installing jQuery via npm
Run the following command in the terminal:

```bash
npm install jquery
```

### Importing jQuery in Your JavaScript File
Use the following import statement in `script.js` or any other file:

```javascript
import $ from 'jquery';
```

## Example HTML Structure

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>jQuery Example</title>
    <script src="https://code.jquery.com/jquery-3.6.4.min.js"></script>
</head>
<body>
    <div class="list">
        <button id="btn" class="list-item">First</button>
        <button class="list-item">Second</button>
        <button class="list-item">Third!</button>
        <button class="list-item">Fourth</button>
        <button class="list-item">Fifth</button>
    </div>

    <div class="wrapper">
        <img src="https://cdn.pixabay.com/photo/2018/02/13/23/41/nature-3151869_960_720.jpg" alt="1" class="image">
        <img src="https://cdn.pixabay.com/photo/2018/03/06/03/56/cyclist-3202481_960_720.jpg" alt="2" class="image">
    </div>

    <script src="dist/bundle.js"></script>
</body>
</html>
```

## Example Usage of jQuery

File `script.js`:

```javascript
import $ from 'jquery';

$(document).ready(function() {
    // Add the 'active' class when hovering over the first list item
    $('.list-item:first').hover(function() {
        $(this).toggleClass('active');
    });

    // Toggle visibility of even images when clicking the third list item
    $('.list-item:eq(2)').on('click', function() {
        $('.image:even').fadeToggle('slow');
    });

    // Animate odd images when clicking the fifth list item
    $('.list-item:eq(4)').on('click', function () {
        $('.image:odd').animate({
            opacity: 'toggle',
            height: 'toggle'
        }, 2000);
    });
});
```

### Functionality Description:
1. **Hover Effect on the First List Item:**
   When hovering over the button labeled "First," it toggles the `active` class.

2. **Toggle Visibility of Even Images:**
   Clicking on the "Third!" button toggles the visibility of even images with a `fadeToggle` effect.

3. **Animate Odd Images:**
   Clicking on the "Fifth" button animates odd images by toggling their opacity and height.

## Webpack Configuration

File `webpack.config.js`:

```javascript
'use strict';

let path = require('path');

module.exports = {
  mode: 'production',
  entry: './script.js',
  output: {
    filename: 'bundle.js'
  },
  watch: true,

  devtool: "source-map",

  module: {
    rules: [
      {
        test: /\.m?js$/,
        exclude: /(node_modules|bower_components)/,
        use: {
          loader: 'babel-loader',
          options: {
            presets: [['@babel/preset-env', {
                debug: true,
                corejs: 3,
                useBuiltIns: "usage"
            }]]
          }
        }
      }
    ]
  }
};
```

### Commands to Run the Project:

1. **Install Dependencies:**
   ```bash
   npm install
   ```

2. **Build the Project:**
   ```bash
   npx webpack
   ```

3. **Run in Development Mode:**
   ```bash
   npm run start
   ```

## Resources and Documentation
- Official jQuery Website: [https://jquery.com/](https://jquery.com/)
- Webpack Documentation: [https://webpack.js.org/](https://webpack.js.org/)
