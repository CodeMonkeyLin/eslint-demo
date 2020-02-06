## ESLint

ESLint是比较新出来的工具。它被设计的容易拓展、拥有大量的自定义规则、容易的通过插件来安装。它给出准确的输出，而且包括规则名，这样可以知道哪个规则造成了错误。

ESLint文档多少有些混乱。规则容易查找，以及被分为逻辑组，但是配置指南在有些地方容易弄混。然而它可以在一个地方提供链接去编辑集成、插件和样例。

**优点**

- 灵活：任何规则都可以开启闭合，以及有些规则有些额外配置
- 很容易拓展和有需要可用插件
- 容易理解产出
- 包含了在其他检查器中不可用的规则，使得ESLint在错误检查上更有用
- 支持ES6，支持JSX的工具
- 支持自定义报告

**缺点**

- 需要一些配置
- 速度慢

> [JSCS](http://jscs.info/)已经合并到ESlint

### ESLint

ESLint是JavaScript的linting实用程序。

ESLint不依赖于特定的编码约定，用户也可以自由地启用或禁用各个编码约定。从这个意义上讲，它的一个主要特点是其高度可定制性。

用户可以通过定义原始[规则来](https://eslint.org/docs/rules/)灵活地设置编码标准，这些规则是ESLint中默认可用的编码规则。此外，第三方共享的着名编码约定，例如“Google JavaScript Style Guide”或“Airbnb JavaScript Style Guide”也可以重复使用。

您甚至可以在遵循这些编码约定的同时启用/禁用特定文件的特定规则。

如果您不知道要开始的设置，可以参考ESLint官方提供的“ [入门](https://eslint.org/docs/user-guide/getting-started) ”指南，以使用建议的编码约定。



核心概念：

- 配置文件：

  `.eslintrc`，`.eslintrc.js`，`.eslintrc.yml`

- Rules：
  - “off” 或 `0` - 关闭规则
  - “warn” 或 `1` - 开启规则，使用警告级别的错误：warn (不会导致程序退出)
  - “error” 或 `2` - 开启规则，使用错误级别的错误：error (当被触发的时候，程序会退出)

  看一个例子：

  ```json
  {
      "rules": {
          "semi": ["error", "never"],
          "quotes": ["error", "single"]
      }
  }
  ```

  也可以写成：

  ```json
  {
      "rules": {
          "semi": [2, "never"],
          "quotes": [2, "single"]
      }
  }
  ```

- Extends：

  使用别人提供的包， 如google

  ```json
  { 
      "extends"："google"，
  }
  ```

  通过使用上述说明，用户可以轻松使用Google JavaScript样式指南中的编码约定，而无需从头开始编写设置。

- Plugins:

  ESLint提供的默认规则涵盖了基本规则，但JavaScript可以使用的范围非常广泛。因此，您可能希望规则不在默认规则中。在这种情况下，可以在ESLint中开发自己的独立规则。为了让第三方开发自己的规则，ESLint允许使用[插件](https://eslint.org/docs/developer-guide/working-with-plugins)。如果你在npm中搜索eslint-plugin- *，你可以找到第三方提供的大量自定义插件。

  如果ESLint的默认规则未提供您要使用的规则，则建议您查找插件。

  与可共享配置类似，它很容易设置。例如，如果要对React代码执行静态分析，可以安装名为[eslint-plugin-react的插件](https://www.npmjs.com/package/eslint-plugin-react)，并使用以下设置来执行React语法特有的静态分析。

  ```json
  { 
      "extends": "google"，
      "plugins": [ 
          "react" 
      ]，
      "rules"": { 
          "semi": ["error", "never"],
          "quotes": ["error", "single"]
      } 
  }
  ```

  

#### 起步与安装

1. 在项目中去使用

   ```json
   // npm init 指令会在项目根目录下生成 package.json 文件。
   npm init
   
   // --save-dev 会把 eslint 安装到 package.json 文件中的 devDependencies 属性中，意思是只是开发阶段用到这个包，上线时就不需要这个包了。
   npm install eslint --save-dev
   ```

   - 使用`npm run`

   新增`package.json` 脚本，或者使用 `npx`命令

   ```javascript
"scripts": {
       "lint": "eslint src",
       "lint:create": "eslint --init"
   }
   ```
   
   然后使用`run`命令：

   ```bash
npm run lint
   ```
   
   - 直接使用`npx`命令：

   ```bash
npx eslint --init
   
   // 或者
   ./node_modules/.bin/eslint --init
   ```
   
2. 在全局使用

   ```bash
   npm install -g eslint
   ```

#### ESLint初始化

配置方法使用 `eslint --init`方法

```bash
➜ npx eslint --init
? How would you like to use ESLint? (Use arrow keys)
  To check syntax only 
❯ To check syntax and find problems 
  To check syntax, find problems, and enforce code style 
  
? What type of modules does your project use? (Use arrow keys)
❯ JavaScript modules (import/export) 
  CommonJS (require/exports) 
  None of these 
  
// 这里可以针对你的开发项目进行配置
? Which framework does your project use? 
  React 
  Vue.js 
❯ None of these 

// 可以配置代码运行的地方，是浏览器还是Node环境？
? Where does your code run? 
❯◉ Browser
 ◉ Node
 
// 最张在哪里缓存
? What format do you want your config file to be in? (Use arrow keys)
❯ JavaScript 
  YAML 
  JSON 

// 成功创建了配置文件
? What format do you want your config file to be in? JavaScript
Successfully created .eslintrc.js file in /Users/itheima/Downloads/Demo
```

配置文件`.eslintrc.js`：

> 废弃的用法：`.eslintrc`，eslint使用配置的顺序：`.eslintrc.js` > `.eslintrc.yaml` > `.eslintrc.yml` > `.eslintrc.json` > `.eslintrc` > `package.json`

`.eslintrc.js`文件：

```js
module.exports = {
    "env": {
        "browser": true,
        "es6": true,
        "node": true
    },
    "extends": "eslint:recommended",
    "globals": {
        "Atomics": "readonly",
        "SharedArrayBuffer": "readonly"
    },
    "parserOptions": {
        "ecmaVersion": 2018,
        "sourceType": "module"
    },
    "rules": {
    }
};
```

再来看看，`yaml`文件配置：

```yaml
env:
  browser: true
  es6: true
  node: true
extends: 'eslint:recommended'
globals:
  Atomics: readonly
  SharedArrayBuffer: readonly
parserOptions:
  ecmaVersion: 2018
  sourceType: module
rules: {}
```



该文件导出一个对象，对象包含属性 `env`、`extends`、`parserOptions`、`plugins`、`rules` 五个属性：

- `env`：指定脚本的运行环境。每种环境都有一组特定的预定义全局变量，（如：nodejs，browser，commonjs等）中。

- `parserOptions`：用于指定想要支持的JavaScript语言选项

  - `ecmaVersion` - 默认设置为3，5（默认）， 你可以使用 6、7、8 或 9 来指定你想要使用的 ECMAScript 版本。你也可以用使用年份命名的版本号指定为 2015（同 6），2016（同 7），或 2017（同 8）或 2018（同 9）

  - `sourceType` - 设置为 `"script"` (默认) 或 `"module"`（如果你的代码是 ECMAScript 模块)。

  - ```
    ecmaFeatures
    ```

    \- 这是个对象，表示你想使用的额外的语言特性:

    - `globalReturn` - 允许在全局作用域下使用 `return` 语句
    - `impliedStrict` - 启用全局 [strict mode](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode) (如果 `ecmaVersion` 是 5 或更高)
    - `jsx` - 启用 [JSX](http://facebook.github.io/jsx/)

- `globals`：执行代码时脚步需要访问的额外全局变量。

- `rules`：开启某些规则，也可以设置规则的等级。

- `extends`: 对默认规则进行扩展，可以使用`Airbnb`，或者`Standard`规则。



#### .eslintignore

可以在项目根目录创建，告诉ESLint忽略某些文件或者目录。相当于.gitignore都是纯文本文件。
例如

```
# 注释，忽略文件node_modules**/.jsbuild
```

常见的eslintignore内容：

```
node_modules/*
**/node_modules/*
dist/*
/build/**
/coverage/**
/docs/**
/jsdoc/**
/templates/**
/tests/bench/**
/tests/fixtures/**
/tests/performance/**
/tmp/**
/lib/rules/utils/unicode/is-combining-character.js
test.js
!.eslintrc.js
```



#### ESLint的使用方法

- 本地使用方法：

  如果你想让 ESLint 成为你项目构建系统的一部分，我们建议在本地安装。你可以使用 npm：

  ```bash
  $ npm install eslint --save-dev
  ```

  紧接着你应该设置一个配置文件：

  ```bash
  $ ./node_modules/.bin/eslint --init
  ```

  之后，你可以在你项目根目录运行 ESLint：

  ```bash
  $ ./node_modules/.bin/eslint yourfile.js
  ```

  使用本地安装的 ESLint 时，你使用的任何插件或可分享的配置也都必须在本地安装。

  

- 全局使用

  如果你想使 ESLint 适用于你所有的项目，我们建议你全局安装 ESLint。你可以使用 npm：

  ```
  $ npm install -g eslint
  ```

  紧接着你应该设置一个配置文件：

  ```
  $ eslint --init
  ```

  之后，你可以在任何文件或目录运行 ESLint：

  ```
  $ eslint yourfile.js
  ```



#### 常用ESlint配置

ESLint的规范：

Standard: https://github.com/standard/eslint-config-standard

具体地址：[eslintrc.json](https://github.com/standard/eslint-config-standard/blob/master/eslintrc.json)

Airbnb: https://github.com/airbnb/javascript

1. comma逗号

   ```js
   rules: {
   	"comma-dangle": ["error", "never"],
   }
   ```

   Bad:

   ```js
   var foo = {
   	a: '123',
   	b: '321', // wrong error
   }
   ```

   Right:

   ```js
   var foo = {
   	a: '123',
   	b: '321'
   }
   ```

2. quotes引号

3. semi分号

4. 空行

5. 驼峰命名

6. 日志输出

7. 强等判断

8. 冗余的变量

9. 空格
   - 关键字后的空格
   - 函数名后的空格
   - 缩进



#### 在IDE中的配置

配置文件：

```json
  "eslint.alwaysShowStatus": true,
  "eslint.autoFixOnSave": true,
  "editor.formatOnSave": true,
  "eslint.validate": [
    "javascriptreact",
    {
      "language": "html",
      "autoFix": true
    },
    {
      "language": "javascript",
      "autoFix": true
    }
  ],
  "eslint.options": {
    "plugins": ["html"]
  },
```

快速修复配置：

打开 `"editor.formatOnSave":  true`并且要打开`eslint.validate`如上面的配置，或者在UI界面里面设置。

![image-20190627124410671](assets/image-20190627124410671.png)

#### React中的配置资料

[Configure ESLint, Prettier, and Flow in VS Code for React Development](https://medium.com/@sgroff04/configure-eslint-prettier-and-flow-in-vs-code-for-react-development-c9d95db07213)

[React开发团队如何使用ESLint](https://blog.sideci.com/how-the-react-developer-team-uses-eslint-2828564814da)

### 完整的ESLint文件配置属性的解释

```json
/*
 * ESLint的JSON文件是允许JavaScript注释的，但在gist里显示效果不好，所以我把.json文件后缀改为了.js
 */

/*
 * ESLint 配置文件优先级：
 * .eslintrc.js(输出一个配置对象)
 * .eslintrc.yaml
 * .eslintrc.yml
 * .eslintrc.json（ESLint的JSON文件允许JavaScript风格的注释）
 * .eslintrc（可以是JSON也可以是YAML）
 *  package.json（在package.json里创建一个eslintConfig属性，在那里定义你的配置）
 */

/*
 * 你可以通过在项目根目录创建一个.eslintignore文件告诉ESLint去忽略特定的文件和目录
 * .eslintignore文件是一个纯文本文件，其中的每一行都是一个glob模式表明哪些路径应该忽略检测
 */

{
  //ESLint默认使用Espree作为其解析器
  //同时babel-eslint也是用得最多的解析器
  "parser": "espree",

  //parser解析代码时的参数
  "parserOption": {
    //指定要使用的ECMAScript版本，默认值5
    "ecmaVersion": 5,
    //设置为script(默认)或module（如果你的代码是ECMAScript模块)
    "sourceType": "script",
    //这是个对象，表示你想使用的额外的语言特性,所有选项默认都是false
    "ecmafeatures": {
      //允许在全局作用域下使用return语句
      "globalReturn": false,
      //启用全局strict模式（严格模式）
      "impliedStrict": false,
      //启用JSX
      "jsx": false,
      //启用对实验性的objectRest/spreadProperties的支持
      "experimentalObjectRestSpread": false
    }
  },

  //指定环境，每个环境都有自己预定义的全局变量，可以同时指定多个环境，不矛盾
  "env": {
    //效果同配置项ecmaVersion一样
    "es6": true,
    "browser": true,
    "node": true,
    "commonjs": false,
    "mocha": true,
    "jquery": true,
     //如果你想使用来自某个插件的环境时，确保在plugins数组里指定插件名
     //格式为：插件名/环境名称（插件名不带前缀）
    "react/node": true
  },

  //指定环境为我们提供了预置的全局变量
  //对于那些我们自定义的全局变量，可以用globals指定
  //设置每个变量等于true允许变量被重写，或false不允许被重写
  "globals": {
    "globalVar1": true,
    "globalVar2": false
  },

  //ESLint支持使用第三方插件
  //在使用插件之前，你必须使用npm安装它
  //全局安装的ESLint只能使用全局安装的插件
  //本地安装的ESLint不仅可以使用本地安装的插件还可以使用全局安装的插件
  //plugin与extend的区别：extend提供的是eslint现有规则的一系列预设
  //而plugin则提供了除预设之外的自定义规则，当你在eslint的规则里找不到合适的的时候
  //就可以借用插件来实现了
  "plugins": [
    "eslint-plugin-airbnb",
    //插件名称可以省略eslint-plugin-前缀
    "react"
  ],

  //具体规则配置
  //off或0--关闭规则
  //warn或1--开启规则，警告级别(不会导致程序退出)
  //error或2--开启规则，错误级别(当被触发的时候，程序会退出)
  "rules": {
    "eqeqeq": "warn",
    //你也可以使用对应的数字定义规则严重程度
    "curly": 2,
    //如果某条规则有额外的选项，你可以使用数组字面量指定它们
    //选项可以是字符串，也可以是对象
    "quotes": ["error", "double"],
    "one-var": ["error", {
      "var": "always",
      "let": "never",
      "const": "never"
    }],
    //配置插件提供的自定义规则的时候，格式为：不带前缀插件名/规则ID
    "react/curly": "error"
  },

  //ESLint支持在配置文件添加共享设置
  //你可以添加settings对象到配置文件，它将提供给每一个将被执行的规则
  //如果你想添加的自定义规则而且使它们可以访问到相同的信息，这将会很有用，并且很容易配置
  "settings": {
    "sharedData": "Hello"
  },

  //Eslint检测配置文件步骤：
  //1.在要检测的文件同一目录里寻找.eslintrc.*和package.json
  //2.紧接着在父级目录里寻找，一直到文件系统的根目录
  //3.如果在前两步发现有root：true的配置，停止在父级目录中寻找.eslintrc
  //4.如果以上步骤都没有找到，则回退到用户主目录~/.eslintrc中自定义的默认配置
  "root": true,

  //extends属性值可以是一个字符串或字符串数组
  //数组中每个配置项继承它前面的配置
  //可选的配置项如下
  //1.字符串eslint：recommended，该配置项启用一系列核心规则，这些规则报告一些常见问题，即在(规则页面)中打勾的规则
  //2.一个可以输出配置对象的可共享配置包，如eslint-config-standard
    //可共享配置包是一个导出配置对象的简单的npm包，包名称以eslint-config-开头，使用前要安装
    //extends属性值可以省略包名的前缀eslint-config-
  //3.一个输出配置规则的插件包，如eslint-plugin-react
    //一些插件也可以输出一个或多个命名的配置
    //extends属性值为，plugin：包名/配置名称
  //4.一个指向配置文件的相对路径或绝对路径
  //5.字符串eslint：all，启用当前安装的ESLint中所有的核心规则
    //该配置不推荐在产品中使用，因为它随着ESLint版本进行更改。使用的话，请自己承担风险
  "extends": [
    "eslint:recommended",
    "standard",
    "plugin:react/recommended",
    "./node_modules/coding-standard/.eslintrc-es6",
    "eslint:all"
  ]
}
```

