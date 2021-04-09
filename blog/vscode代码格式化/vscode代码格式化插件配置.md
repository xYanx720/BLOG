---
title: vscode代码格式化插件配置
date: 2021-02-25 20:49:55
tags: vscode
---

不要再用 Beautify 代码格式化插件了 当开始写vue、nodejs、less时Beautify带来得体验及其不佳，换个新插件？

## 前言

Beautify不用配置就可以直接用但是会可能出现一系列奇怪得问题 

例如：

![image-20210225210845969](C:\Users\Mloong\AppData\Roaming\Typora\typora-user-images\image-20210225210845969.png)

或者：

![image-20210225211117596](C:\Users\Mloong\AppData\Roaming\Typora\typora-user-images\image-20210225211117596.png)

**最好得情况下应该是**

![image-20210225211148324](C:\Users\Mloong\AppData\Roaming\Typora\typora-user-images\image-20210225211148324.png)

![image-20210225211202414](C:\Users\Mloong\AppData\Roaming\Typora\typora-user-images\image-20210225211202414.png)

所以先把beautify卸载吧  或者全局禁用插件也可以  然后接下来安装3个插件

### 安装插件

- ESlint
- Vetur
- Prettier

![image-20210225205810152](C:\Users\Mloong\AppData\Roaming\Typora\typora-user-images\image-20210225205810152.png)

![image-20210225205831881](C:\Users\Mloong\AppData\Roaming\Typora\typora-user-images\image-20210225205831881.png)

![image-20210225205741458](C:\Users\Mloong\AppData\Roaming\Typora\typora-user-images\image-20210225205741458.png)

#### 打开 settings 文件

打开方式：

VsCode => preferences => setting (Vscode 左上角 ‘文件’ > '首选项' > ‘设置’)

<img src="C:\Users\Mloong\AppData\Roaming\Typora\typora-user-images\image-20210225210317019.png" alt="image-20210225210317019" style="zoom:50%;" />

右上角点开可以看到

<img src="C:\Users\Mloong\AppData\Roaming\Typora\typora-user-images\image-20210225210348779.png" alt="image-20210225210348779" style="zoom:50%;" />

滑到末尾在最后一个 ‘}’ 前加入以下配置 保存即可（基本上已经符合大多数得开发）

```
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

至此教程结束

佛系更新哈哈