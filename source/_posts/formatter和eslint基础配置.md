---
title: 'formatter和eslint基础配置'
date: 2021-04-08 16:00
comments: true
tags:
    - eslint
---

> 对于项目来说，代码的格式化和规范很重要，特作此文章已记录学习。
<!-- more -->
### 开发工具IDE
+ IDE: vscode
+ IDE插件：prettier, eslint

### vscode配置
在项目根目录下，新建 .vscode/settings.json 文件，用于自动保存格式化，已经不同文件启用对应规则。内容如下：
```json
{
  "eslint.format.enable": true,
  "editor.formatOnSave": true,
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": true
  },
  "eslint.validate": [
    "javascript",
    "javascriptreact",
    "vue"
  ],
  "[html]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[javascript]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[css]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[json]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  // "[vue]": {
  //   "editor.defaultFormatter": "esbenp.prettier-vscode"
  // }
}
```

### prettier配置
在项目根目录下新建 .prettierrc.js 文件，用于设置格式化规则。内容如下：
```javascript
module.exports = {
  printWidth: 300,
  tabWidth: 2,
  // 单引号
  singleQuote: true,
  // 句末加分号
  semi: false,
  // 对象&数组是否追加空格
  bracketSpacing: true
}
```

### eslint配置
在项目根目录下新建 .eslintrc.js 文件，用于设置eslint规则。内容如下：
```javascript
module.exports = {
  root: true,
  parserOptions: {
    sourceType: 'module',
    parser: 'babel-eslint'
  },
  extends: ['eslint:recommended', 'plugin:vue/recommended', 'plugin:prettier/recommended'],
  env: {
    browser: true,
    es6: true,
    node: true
  },
  extends: 'eslint:recommended',
  rules: {}
}
```

> extends中'plugin:vue/recommended'，使用插件eslint-plugin-vue，用于vue中template的检测和校验。
> extends中'plugin:prettier/recommended'，使用插件eslint-plugin-prettier和eslint-config-prettier，用于vue文件的格式化。

在项目根目录下新建 .eslintignore 文件，用于eslint检查忽略的文件目录及文件。内容如下：
```txt
.vscode/
node_modules/
public/
dist/
```

### package.json中eslint相关的包
建议使用vue-cli创建项目，自动生成，以下是自动生成的相关依赖包
```json
{
    "devDependencies": {
        "@ant-design/colors": "^4.0.1",
        "@vue/cli-plugin-babel": "^4.4.0",
        "@vue/cli-plugin-eslint": "^4.4.0",
        "@vue/cli-service": "^4.4.0",
        "@vuepress/plugin-back-to-top": "^1.5.2",
        "babel-eslint": "^10.1.0",
        "babel-plugin-transform-remove-console": "^6.9.4",
        "babel-polyfill": "^6.26.0",
        "compression-webpack-plugin": "^2.0.0",
        "deepmerge": "^4.2.2",
        "eslint": "^6.7.2",
        "eslint-plugin-vue": "^6.2.2",
        "fast-deep-equal": "^3.1.3",
        "gh-pages": "^3.1.0",
        "less-loader": "^6.1.1",
        "style-resources-loader": "^1.3.2",
        "vue-cli-plugin-style-resources-loader": "^0.1.4",
        "vue-template-compiler": "^2.6.11",
        "vuepress": "^1.5.2",
        "webpack-theme-color-replacer": "^1.3.12",
        "whatwg-fetch": "^3.0.0"
  },
}
```