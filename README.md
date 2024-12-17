# jQuery Documentation
 Guide to Using jQuery with Webpack Setup✨


# Использование библиотеки jQuery на веб-странице

jQuery — это популярная библиотека JavaScript, которая упрощает работу с DOM, обработку событий, анимации и многое другое. В данном руководстве описано, как подключить jQuery к вашему проекту и использовать её возможности.

## Подключение jQuery

### 1. Использование CDN
Вы можете подключить библиотеку jQuery с помощью CDN (Content Delivery Network). Это быстрый и простой способ.
Добавьте следующий тег `<script>` в `<head>` или перед закрывающим тегом `<body>`:

```html
<script src="https://code.jquery.com/jquery-3.6.4.min.js"></script>
```

### 2. Локальное подключение
Скачайте файл библиотеки jQuery с официального сайта: [https://jquery.com/download/](https://jquery.com/download/).

Добавьте файл в ваш проект (например, в папку `js`) и подключите его:

```html
<script src="js/jquery-3.6.4.min.js"></script>
```

## Настройка проекта с использованием Webpack
Если вы работаете с Webpack, вы можете установить jQuery как модуль:

### Установка jQuery через npm
Выполните следующую команду в терминале:

```bash
npm install jquery
```

### Импорт jQuery в вашем JavaScript-файле
Используйте следующий импорт в `script.js` или любом другом файле:

```javascript
import $ from 'jquery';
```

## Пример HTML-структуры

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
        <button id="btn" class="list-item">Первый</button>
        <button class="list-item">Второй</button>
        <button class="list-item">Третий!</button>
        <button class="list-item">Четвёртый</button>
        <button class="list-item">Пятый</button>
    </div>

    <div class="wrapper">
        <img src="https://cdn.pixabay.com/photo/2018/02/13/23/41/nature-3151869_960_720.jpg" alt="1" class="image">
        <img src="https://cdn.pixabay.com/photo/2018/03/06/03/56/cyclist-3202481_960_720.jpg" alt="2" class="image">
    </div>

    <script src="dist/bundle.js"></script>
</body>
</html>
```

## Пример использования jQuery

Файл `script.js`:

```javascript
import $ from 'jquery';

$(document).ready(function() {
    // Добавление класса active при наведении на первый элемент списка
    $('.list-item:first').hover(function() {
        $(this).toggleClass('active');
    });

    // Переключение видимости чётных изображений при нажатии на третий элемент списка
    $('.list-item:eq(2)').on('click', function() {
        $('.image:even').fadeToggle('slow');
    });

    // Анимация нечётных изображений при нажатии на пятый элемент списка
    $('.list-item:eq(4)').on('click', function () {
        $('.image:odd').animate({
            opacity: 'toggle',
            height: 'toggle'
        }, 2000);
    });
});
```

### Описание функционала:
1. **Hover-эффект на первый элемент списка:**
   При наведении мыши на кнопку с текстом "Первый" она получает или теряет класс `active`.

2. **Переключение видимости чётных изображений:**
   При клике на кнопку "Третий!" чётные изображения переключают свою видимость с эффектом `fadeToggle`.

3. **Анимация нечётных изображений:**
   При клике на кнопку "Пятый" нечётные изображения анимируются, изменяя прозрачность и высоту.

## Настройка Webpack

Файл `webpack.config.js`:

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

### Команды для запуска проекта:

1. **Установка зависимостей:**
   ```bash
   npm install
   ```

2. **Сборка проекта:**
   ```bash
   npx webpack
   ```

3. **Запуск в режиме разработки:**
   ```bash
   npm run start
   ```

## Ресурсы и документация
- Официальный сайт jQuery: [https://jquery.com/](https://jquery.com/)
- Документация Webpack: [https://webpack.js.org/](https://webpack.js.org/)
