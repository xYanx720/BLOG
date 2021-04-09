![image-20210304093606079](C:\Users\Mloong\AppData\Roaming\Typora\typora-user-images\image-20210304093606079.png)

## 前言

Beautify不能格式化诸如.vue 等不是原生js语法的文件  且可自定义度比较小 所以换成ESlint + Prettier + Vetur进行代码格式化



## 安装

先禁用或者卸载Beautify

 再下载以下3个插件







## 配置

Vsocde依次点开 左上角文件=>首选项=>设置=>点击右上角图标转为源码格式打开配置文件

<img src="C:\Users\Mloong\AppData\Roaming\Typora\typora-user-images\image-20210225210317019.png" alt="image-20210225210317019" style="zoom:50%;" />





在最后一个'}'前面加上以下代码,保存后退出重启vscode 

```
// 使能每一种语言默认格式化规则
  // 设置 eslint 保存时自动修复
  "eslint.autoFixOnSave": true,
  // eslint 检测文件类型
  "eslint.validate": [
    "javascript",
    "javascriptreact",
    {
      "language": "html",
      "autoFix": true
    },
    {
      "language": "vue",
      "autoFix": true
    }
  ],
  "[javascript]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[json]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[html]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode",
    "indent_size": 8
  },
  "[vue]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[less]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[css]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[jsonc]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  // vetur 的自定义设置
  "vetur.format.defaultFormatter.html": "prettier",
  "vetur.format.defaultFormatter.js": "prettier",
  "vetur.format.defaultFormatter.less": "prettier",
  "vetur.format.defaultFormatterOptions": {
    // "wrap_attributes": "force-expand-multiline",
    // "js-beautify-html": {
    //   "wrap_attributes": "force-expand-multiline",
    //   "end_with_newline": false
    // },
    "prettier": {
      "printWidth": 160,
      "singleQuote": true, // 使用单引号
      "semi": true, // 末尾使用分号
      "tabWidth": 4,
      "arrowParens": "avoid",
      "bracketSpacing": true,
      "proseWrap": "preserve" // 代码超出是否要换行 preserve保留
    }
  },
  /*  prettier的配置 */
  "prettier.printWidth": 80, // 超过最大值换行
  "prettier.tabWidth": 2, // 缩进字节数
  "prettier.useTabs": false, // 缩进不使用tab，使用空格
  "prettier.semi": true, // 句尾添加分号
  "prettier.singleQuote": true, // 使用单引号代替双引号
  "prettier.proseWrap": "preserve", // 默认值。因为使用了一些折行敏感型的渲染器（如GitHub comment）而按照markdown文本样式进行折行
  "prettier.arrowParens": "always", //  (x) => {} 箭头函数参数只有一个时是否要有小括号。avoid：省略括号
  "prettier.bracketSpacing": true, // 在对象，数组括号与文字之间加空格 "{ foo: bar }"
  "prettier.disableLanguages": ["vue"], // 不格式化vue文件，vue文件的格式化单独设置
  "prettier.endOfLine": "auto", // 结尾是 \n \r \n\r auto
  "prettier.eslintIntegration": false, //不让prettier使用eslint的代码格式进行校验
  "prettier.htmlWhitespaceSensitivity": "ignore",
  "prettier.ignorePath": ".prettierignore", // 不使用prettier格式化的文件填写在项目的.prettierignore文件中
  "prettier.jsxBracketSameLine": false, // 在jsx中把'>' 是否单独放一行
  "prettier.jsxSingleQuote": false, // 在jsx中使用单引号代替双引号
  "prettier.parser": "babylon", // 格式化的解析器，默认是babylon
  "prettier.requireConfig": false, // Require a 'prettierconfig' to format prettier
  "prettier.stylelintIntegration": false, //不让prettier使用stylelint的代码格式进行校验
  "prettier.trailingComma": "es5", // 在对象或数组最后一个元素后面是否加逗号（在ES5中加尾逗号）
  "prettier.tslintIntegration": false // 不让prettier使用tslint的代码格式进行校验
```

## 使用

格式化的时候按下Alt+Shift+f键即可