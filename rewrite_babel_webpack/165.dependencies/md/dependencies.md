# Организация зависимостей

Зависимости в **package.json** делятся на два види и их желательно разделять.

Кароче если что-то не так их можно вырезать и перенести в нужные зависимости.

```json
{
  "name": "exemple",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "devDependencies": {
    "@babel/cli": "^7.12.13",
    "@babel/core": "^7.12.13",
    "@babel/plugin-proposal-class-properties": "^7.12.13",
    "@babel/plugin-transform-block-scoping": "^7.12.13",
    "@babel/plugin-transform-classes": "^7.12.13",
    "@babel/plugin-transform-template-literals": "^7.12.13",
    "@babel/preset-env": "^7.12.13",
    "@babel/preset-react": "^7.12.13"
  },
  "dependencies": {
    "core-js": "^3.8.3",
    "react": "^17.0.1",
    "react-dom": "^17.0.1"
  }
}
```
