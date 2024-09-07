# 包管理器 Npm And Yarn


## 软件包管理器

**包管理器**：是开发人员用来自动寻找、下载、安装、配置、升级和删除系统包的工具。

软件包管理器--如 [NPM](https://www.npmjs.com/)、[pNPM](https://pnpm.io/)、[Bower](https://bower.io/) 和 [Yarn](https://yarnpkg.com/)--有助于自动化并消除手动管理所有包的繁琐过程。

**NPM**(Node Package Manager)和 **Yarn**(Yet Another Resource Negotiator)是两个常用的软件包管理器。

## Package Registry

**Package Registry**是一个数据库（存储），用于存储成千上万的包（库、插件、框架或工具）。

[NPM Registry](https://www.npmjs.com/)和[GitHub Packages](https://github.com/features/packages)是两个普遍使用的 package registrys;

## NPM 和 Yarn

NPM 会在安装[Node.js](https://nodejs.org/en/)时自动安装。

### Node.js

-   检查已安装的 Node 版本
    ```bash
    node -v
    ```
-   升级 Node
    1. 前往 [Node.js 官网](https://nodejs.org/en) 下载最新版本，这会替换旧版本并保留全局包。
    2. 使用 [n](https://github.com/tj/n) 或 [nvm](https://github.com/nvm-sh/nvm)

### NPM

-   检查已安装的 NPM 版本

    ```bash
    # -v 是 --version 的缩写。
    npm -v
    ```

-   升级 NPM
    ```bash
    npm install npm@latest -g
    ```

### Yarn

Yarn 可以通过 NPM 安装

```bash
npm install -g yarn
```

升级 Yarn：

```bash
yarn set version latest
```

## Package（包）

**包**是一个**目录**或**项目**，它有一个 `package.json` 文件用来记录它的信息。

{{< admonition >}}
你只能将包（由 `package.json` 文件描述的项目）发布到 NPM Registry
{{< /admonition >}}

### 安装包

安装包有两种方法：本地、全局

本地安装只能在被安装的项目中使用，安装步骤：

1. 进入项目根目录
2. 使用 NPM 或 Yarn 安装命令安装

#### NPM 安装命令

```bash
# 1. 安装单个包
npm install <package-name>
# 例
npm install express
# 2. 安装指定版本的包
npm install <package-name>@<version>
# 例
npm install express@4.17.1
# 3. 安装全局包
npm install -g <package-name>
# 例
npm install -g nodemon
# 4. 安装开发依赖（Development Dependencies）
# --save-dev 表示将该包作为开发依赖（devDependencies）添加到 package.json 中，仅在开发环境中使用，不会再生产环境中安装
npm install <package-name> --save-dev
# 例
npm install eslint --save-dev
# 5. 安装生产依赖（Production Dependencies）
# 默认情况下，npm install 会把包加入到 dependencies 中，但 --save选项会明确的将包安装为生产依赖
npm install <package-name> --save
# 例
npm install lodash --save
# 6. 安装 package.json 中的所有依赖
# 如果你的项目已经有 package.json ，这个命令会安装文件中所有的依赖
npm install
# 7. 安装并避免修改 package.json
npm install <package-name> --no-save
# 例
npm install lodash --no-save
# 8. 更新已安装的包
npm update <package-name>
```

#### Yarn 安装命令

```bash
# 安装包并添加到 dependencies。
yarn add <package-name>
# 安装包并添加到 devDependencies。
yarn add <package-name> --dev
# 全局安装包。
yarn global add <package-name>
# 安装 package.json 中的所有依赖。
yarn install
```

### 软件包的[本地安装和全局安装](https://nodejs.org/en/blog/npm/npm-1-0-global-vs-local-installation/#when-you-can-t-choose)

一般来说，最好使用本地安装。

区别：

-   安装位置

    -   本地安装会被安装在执行 `npm install package-name`（或 `yarn add package-name`）命令的目录下。
    -   全局安装会被安装在系统中的一个位置。

-   软件包版本

    -   本地安装，你可以在不同项目中使用同一个包的不同版本。
    -   全局安装，所有的项目只能使用同一个版本的软件包。

-   使用建议

    -   本地安装适合打算只在命令行上使用的软件包--特别是当它们提供了可在不同项目中重复使用的可执行命令，例如：[NPM](https://www.npmjs.com/)、[React Native CLI](https://reactnative.dev/docs/environment-setup)、[Gatsby CLI](https://www.gatsbyjs.com/docs/reference/gatsby-cli/)、[Grunt CLI](https://gruntjs.com/getting-started) 和 [Vue CLI](https://cli.vuejs.org/)
    -   全局安装适合于在程序中使用的软件包--通过 `import` 或 `require()` 函数，例如：[Webpack](https://webpack.js.org/)、[Lodash](https://lodash.com/)、[Jest](https://jestjs.io/) 和 [MomentJS](https://momentjs.com/)。

## node_modules 文件夹

node_modules 目录是 NPM 放置为你的项目下载的本地软件包的文件夹。

## package.json 文件

package.json 文件是一个 JSON 文件，包管理器（如 NPM 和 Yarn）使用它来存储项目信息，它是一个项目的元数据文件。

package.json 文件的优点：

-   可以将你的项目发布到 NPM Registry
-   使得其他人可以轻松管理和安装你的软件包
-   帮助 NPM 轻松管理[模块](https://www.codesweetly.com/javascript-modules-tutorial/)的依赖关系
-   使得你的软件包可以重现并与其他开发者共享

### package.json 文件

创建：进入项目根目录，初始化一个 package.json 文件

```bash
# npm
npm init
# yarn
yarn init
```

执行命令后，软件包管理器会询问你一些关于项目的信息来创建 package.json 文件，或者跳过提问：

```bash
npm init -y
# 或
yarn init -y
```

这将使用从[当前目录获得默认值](https://docs.npmjs.com/creating-a-package-json-file#default-values-extracted-from-the-current-directory)来创建 package.json

**注意**： `-y`标志是 `--yes` 的简写。

当软件包管理器完成初始化过程后，package.json 将包含一个具有一系列属性的对象：

```json
{
    "name": "codesweetly-project",
    "version": "1.0.0",
    "main": "index.js"
}
```

假设你想把你的包发布到 NPM Registry，package.json 文件必须含有 `name` 和 `version` 字段，如果不发布，所有字段--包括 `name` 和 `version` 都是可选的。

**name**

`name` 字段用于记录项目名称。
`name`属性的值必须是：

-   一个单字
-   小写字母
-   小于或等于 214 个字符

可以使用连字符和下划线将单词连接起来。

【例】

```json
{
    "name": "code_sweetly-project"
}
```

**description**

`description` 用于简要描述项目目的，NPM 建议有一个 `description` 属性，使你的包在 NPM 网站上更容易被找到。当人们使用 `npm search` 命令时，你的描述将被显示出来。

【例】

```json
{
    "description": "A brief description about this package (project)"
}
```

**main**

`main` 字段表示项目的入口点。当运行 `require()` 函数时，Node 会把调用解析为 `require(<package.json:main>)`。

【例】

```json
{
    "main": "./src/index.js"
}
```

**private**
`private`字段控制是否将项目发布到 NPM registry。
【例】

```json
{
    // 不进行发布
    "private": true
}
```

**scripts**
`scripts`字段定义项目在不同生命周期时运行的脚本命令

```json
{
    "scripts": {
        "test": "jest",
        "dev": "webpack --mode development",
        "build": "webpack --mode production",
        "predeploy": "npm run build",
        "deploy": "gh-pages -d build"
    }
}
```

例如，运行 `npm run dev` 时执行 `webpack --mode development`

**keywords**
`keywords`指定关键字，帮助人们搜索发现你的包

```json
{
    "keywords": ["drag", "drop", "drag and drop", "dragndrop", "draggable"]
}
```

**author**
`author`描述项目作者的详细资料

```json
{
    "author": "Oluwatobi Sofela <oluwatobiss@codesweetly.com> (https://www.codesweetly.com)"
}
```

或者

```json
{
    "author": {
        "name": "Oluwatobi Sofela",
        // 可选
        "email": "oluwatobiss@codesweetly.com",
        // 可选
        "url": "https://www.codesweetly.com"
    }
}
```

**dependencies**
`dependencies`列出了项目在生产中依赖的所有软件包

```json
{
    "dependencies": {
        "first-package": "^1.0.4",
        "second-package": "~2.1.3"
    }
}
```

可以通过两种方式一个包添加到 `dependencies` 字段中：

-   手动添加软件包的名称和[语义版本](https://docs.npmjs.com/about-semantic-versioning)
-   运行 `npm install package-name --save-prod` 或 `yarn add package-name`

**devDependencies**
`devDependencies` 列出了在生产中不需要，在本地开发和测试中需要的依赖

```json
{
    "devDependencies": {
        "first-dev-package": "^5.8.1",
        "second-dev-package": "3.2.2—4.0.0"
    }
}
```

即用户使用 `npm install` 或 `yarn add` 时，软件包管理器将找到并下载所有列出的 devDependencies 到项目的 node_modules 目录。

