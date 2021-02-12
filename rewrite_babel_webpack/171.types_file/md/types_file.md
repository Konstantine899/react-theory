# Loader`ы для разных типов файлов

```js
//webpack.config.js
module.exports = {
  mode: 'development',

  module: {
    rules: [
      {
        test: /\.(png|jpg|jpeg|gif|ico)$/,
        use: [
          {
            loader: 'file-loader',
            options: {
              outputPath: 'images',
              name: '[name]-[sha1:hash:7].[ext]',
            },
          },
        ],
      },
    ],
  },
};
```

Это новое регулярное выражение говорит что будет обрабатывать любой файл который заканчивается но точку после которого идет любое из этих рассширений.

Примерно так же можно обрабатывать и шрифты.

```js
//webpack.config.js
module.exports = {
  mode: 'development',

  module: {
    rules: [
      // картинки
      {
        test: /\.(png|jpg|jpeg|gif|ico)$/,
        use: [
          {
            loader: 'file-loader',
            options: {
              outputPath: 'images',
              name: '[name]-[sha1:hash:7].[ext]',
            },
          },
        ],
      },
      // Шрифты
      {
        test: /\.(ttf|otf|eot|woff|woff2)$/,
        use: [
          {
            loader: 'file-loader',
            options: {
              outputPath: 'fonts',
              name: '[name].[ext]',
            },
          },
        ],
      },
    ],
  },
};
```

Если бы мне нужно было бы добавить еще один тип файлов к примру файлы со звуками **mp3** и т.д. я бы снова создал отдельное правило в блоке rules и не смешивал бы эту конфигурацию с файлами других видов.
