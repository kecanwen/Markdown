下面是一些简单的步骤来在项目中加入 ESLint：

1. 在项目中安装 ESLint

   ```
   npm install eslint --save-dev
   ```

2. 初始化 ESLint 配置文件

   ```
   ./node_modules/.bin/eslint --init
   ```

3. 根据提示回答问题，
   在处理与其他工具的集成时，可选择插件样式，如 Prettier 和 TypeScript 插件。

4. 配置 eslintignore 文件，来忽略一些文件，这个文件与 gitignore 类似，目的是避免运行 ESLint 检查一些不必要的文件和目录。

5. 在 package.json 文件中添加脚本命令，如下所示：

   ```
    "scripts": {
        "lint": "eslint ."
    }
   ```

   上面的代码中，我们添加了一个名为 lint 的脚本命令，并使用 ESLint 对整个项目进行 lint 检查。

6. 运行 ESLint，可以运行以下命令：

   ```
   npm run lint
   ```

   如果你不想在命令行中每次运行 ESLint 时输入 `./node_modules/.bin/eslint`，也可以将其添加到 package.json 文件中的 scripts 标签下，然后使用 `npm run your-script-name` 命令来运行脚本。

以上是一些基本的步骤，当然，ESLint 可以通过更多的配置来满足不同的开发环境和需求。
