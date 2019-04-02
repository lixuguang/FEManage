# 插件安装
## Prettier - Code formatter
格式化工具
## ESLint
校验规则
## Vetur
vue代码片段及代码美化
## Vue 2 Snippets
vue2 代码片段
## vscode-fileheader
文件注释

# 配置项
```
{
    "workbench.startupEditor": "newUntitledFile",
    "terminal.integrated.shell.windows": "C:\\Program Files\\Git\\bin\\bash.exe", \\ 自行配置自己的环境地址
    "javascript.updateImportsOnFileMove.enabled": "always",
    "editor.tabSize": 2,
    "search.exclude": {
        "**/node_modules": true,
        "**/bower_components": true
    },
    "sync.gist": "748b4cae5eb6e56d6997978ead096e8f",
    "breadcrumbs.enabled": true,
    "todohighlight.isEnable": false,
    "liveServer.settings.donotShowInfoMsg": true,
    "search.location": "sidebar",
    "workbench.activityBar.visible": true,
    "window.menuBarVisibility": "default",
    "workbench.statusBar.visible": true,
    "editor.snippetSuggestions": "top",
    "editor.formatOnPaste": true,
    "workbench.colorTheme": "Tiny Light",
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
    "prettier.eslintIntegration": true,
    "files.autoSave": "onWindowChange",
    "code-runner.saveAllFilesBeforeRun": true,
    "vetur.format.defaultFormatter.html": "js-beautify-html",
    "vetur.format.defaultFormatter.js": "vscode-typescript",
    "prettier.jsxSingleQuote": true,
    "prettier.requireConfig": false,
    "prettier.arrowParens": "always",
    "typescript.format.insertSpaceAfterSemicolonInForStatements": false,
    "prettier.stylelintIntegration": true,
    "prettier.singleQuote": true,
    "prettier.tslintIntegration": true,
    "eslint.provideLintTask": true,
    "eslint.autoFixOnSave": true,
    "editor.mouseWheelZoom": true,
    "editor.tabCompletion": "on",
    "editor.formatOnType": true,
    "eslint.alwaysShowStatus": true,
    "eslint.options": {
        "configFile": "E:/project/xxjs/fore-core/.eslintrc.js" // 自行配置自己的项目地址
    },
    "fileheader.Author": "Li.Xg", // 自行配置自己的名称
    "fileheader.LastModifiedBy": "Li.Xg" // 自行配置自己的名称
}
```
