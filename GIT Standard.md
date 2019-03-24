# 1、说明
项目是一个多人协同完成同一个目标的团队组织形式，在多人协作项目中，如果代码风格统一（前端代码规范和静态代码检查约束）、代码提交信息的说明准确规范（本章介绍），那么在项目开发过程及后期协作以及Bug处理时会更加方便。

在本文中，我将介绍大家如何利用工具及约定保证大家代码提交的统一性，从而提高大家的协同效率：

- **commitlint**: git 提交信息规范与验证
> 添加如ESLint的格式规范校验，规范comiit的格式，达到团队每个人的提交风格保持一直，保证提交信息的完整和准确性
风格如下：

```
<type>(<scope>): <subject> // Header
// 空一行
<body> // 72
// 空一行
<footer> // 72

// 例
fix(登陆模块): 修复登录密码错误的提示

登录没有做友好型提示

修正后不存在此问题
```

- **husky**: 使git-hook更容易
> husky继承了Git下所有的钩子，在触发钩子的时候，husky可以阻止不合法的commit,push等等。注意使用husky之前，必须先将代码放到git 仓库中，否则本地没有.git文件，就没有地方去继承钩子了。
- standard-version: 自动生成CHANGELOG 并发布版本

# 2、git commit message 规范
## commit message格式

```
类型(影响范围): 描述

问题描述

修复方式结果
```


注意：
1.冒号后面有空格。
2.英文小括号。
3.正文和注脚前都要加空行。
## type 类型
用于说明 commit 的类别，只允许使用下面13个标识。

```
'feat', // feat：新增功能
'fix', // fix：bug 修复
'docs', // docs：文档更新
'style', // style：不影响程序逻辑的代码修改(修改空白字符，格式缩进，补全缺失的分号等，没有改变代码逻辑)
'refactor', // refactor：重构代码(既没有新增功能，也没有修复 bug)
'test', // test：新增测试用例或是更新现有测试
'chore', // revert：回滚某个更早之前的提交
'revert', // build：主要目的是修改项目构建系统(例如 glup，webpack，rollup 的配置等)的提交
'build', // build：打包生产环境代码
'ci', // ci：主要目的是修改项目继续集成流程(例如 Travis，Jenkins，GitLab CI，Circle等)的提交
'merge', // merge：分支合并 Merge branch ? of ?
'perf', // perf：性能, 体验优化
'chore' // chore：不属于以上类型的其他类型(构建过程或辅助工具的变动)
```

如果type为feat和fix，则该 commit 将肯定出现在 Change log 之中。
## scope 影响范围
可根据项目组需要进行定制化设置，也可不做强制要求
## subject 描述
subject是 commit 目的的简短描述，不超过50个字符，且结尾不加句号（.）。
## body 详细描述
body 部分是对本次 commit 的详细描述，可以分成多行。下面是一个范例。

```
此次提交内容包括如下信息：
- 登录为空校验
- 密码错误提示
```
## footer
Footer 部分只用于两种情况。
- 不兼容变动（改变解决方案）
- 关闭 Issue（回复bug）

# 3、使用工具校验commit是否符合规范

## commitlint
### 3.1 commitlint安装

```
// npm 安装
npm install --save-dev @commitlint/{cli,config-conventional}
```

## 3.2 生成commitlint.config.js配置文件
执行echo命令创建配置文件，也可以手动创建配置文件，或者从已有的配置文件进行拷贝。

```
// 项目根目录创建commitlint.config.js
echo "module.exports = {extends: ['@commitlint/config-conventional']}" > commitlint.config.js
```


## 3.3 在commitlint.config.js制定提交message规范

```
// type(scope?): subject

// body?

// footer?
module.exports = {
  // 继承自默认规则
  extends: ['@commitlint/config-conventional'],
  // 这里写自定义规则
  rules: {
    // 等级 [0 1 2]: 0 不使用规则 1 警告 2 错误
    // 启用范围 always|never: 总是或者永不.
    // 规则值: 规则对应的值

    // 头部（包含type、scope、subject）
    'header-case': [0, 'always', 'lower-case'],
    'header-full-stop': [0, 'never', '.'],
    'header-max-length': [0, 'always', 72],
    'header-min-length': [0, 'always', 0],

    // 提交类型
    'type-case': [0, 'never'],
    'type-empty': [2, 'never'],
    'type-max-length': [0, 'always', Infinity],
    'type-min-length': [0, 'always', 0],
    'type-enum': [
      2,
      'always',
      [
        'feat', // feat：新增功能
        'fix', // fix：bug 修复
        'docs', // docs：文档更新
        'style', // style：不影响程序逻辑的代码修改(修改空白字符，格式缩进，补全缺失的分号等，没有改变代码逻辑)
        'refactor', // refactor：重构代码(既没有新增功能，也没有修复 bug)
        'test', // test：新增测试用例或是更新现有测试
        'revert', // revert：回滚某个更早之前的提交
        'build', // build：build：主要目的是修改项目构建系统(例如 glup，webpack，rollup 的配置等)的提交，打包生产环境代码
        'ci', // ci：主要目的是修改项目继续集成流程(例如 Travis，Jenkins，GitLab CI，Circle等)的提交
        'merge', // merge：分支合并 Merge branch ? of ?
        'perf', // perf：性能, 体验优化
        'chore' // chore：不属于以上类型的其他类型(构建过程或辅助工具的变动)
      ]
    ],

    // 影响范围
    'scope-case': [0, 'always', 'lower-case'], // 书写格式
    'scope-max-length': [0, 'always', Infinity], // 最长
    'scope-min-length': [0, 'always', 0], // 最短
    'scope-empty': [2, 'never'], // 影响范围：为空|永不
    'scope-enum': [0, 'always', ['a', 'b']], // 影响范围：给出范围但是不在给定的列表内

    // 简介
    'subject-empty': [2, 'never'], // 简介不能为空
    'subject-full-stop': [0, 'never', '.'], // 简介结尾以.结束
    'subject-case': [0, 'never'],
    'subject-max-length': [0, 'always', Infinity],
    'subject-min-length': [0, 'always', 1],

    // 正文
    'body-leading-blank': [2, 'always'],
    'body-max-length': [0, 'always', Infinity],
    'body-max-line-length': [0, 'always', Infinity],
    'body-min-length': [0, 'always', 1],

    // 注脚
    'footer-leading-blank': [2, 'always'],
    'footer-max-length': [0, 'always', Infinity],
    'footer-max-line-length': [0, 'always', Infinity],
    'footer-min-length': [0, 'always', 1],

    // 其他
    'references-empty': [0, 'never'],
    'signed-off-by': [0, 'always', 'Signed-off-by']
  }
}
```

上面我们就完成了commitlint的安装与提交规范的制定。检验commit message的最佳方式是结合git hook，所以需要配合Husky

## husky
### 3.4 husky安装

```
npm install husky --save-dev
```
### 3.5 husky 配置
安装成功后需要在项目下的package.json中配置

```
// package.json
{
  "husky": {
    "hooks": { // husky的钩子
      "pre-commit": "npm run lint" // 提交前进行代码静态校验
      "commit-msg": "commitlint -E HUSKY_GIT_PARAMS" // 进行提交信息格式校验
    }  
  },
  "scripts": {}
  ...
}
```

### 3.5 husky 执行测试
最后我们可以正常的git操作

```
git add .
git commit -m ""
```

git commit的时候会触发commlint。下面演示下不符合规范提交示例：

```
C:\lixg\git>git commit -m "thunisoft: abcde"

husky > npm run -s commitmsg (node v8.2.1)

⧗   input:
thunisoft(all): abcde

✖   type must be one of [feat, fix, docs, style, refactor, perf, test, build, ci, chore, revert] [type-enum]
✖   found 1 problems, 0 warnings

husky > commit-msg hook failed (add --no-verify to bypass)

C:\lixg\git>
```

上面的提交看反馈消息得知是type格式没有符合限制的提交类型列表，所以提交失败，虾米啊我们把type改为feat再试一下


```
C:\lixg\git>git commit -m "feat(all): 新功能"

husky > npm run -s commitmsg (node v8.2.1)

⧗   input: feat: 新功能
✔   found 0 problems, 0 warnings

[develop 19dfhe] feat: 新功能
 1 file changed, 1 insertion(+)

C:\lixg\git>
```

修改后格式符合规范，提交成功。

# 参考来源
- commitlint 
> https://conventional-changelog.github.io/commitlint/#/
- husky
> https://github.com/typicode/husky
- 阮一峰
> http://www.ruanyifeng.com/blog/2016/01/commit_message_change_log.html

# 版权声明
Copyright by lixuguang
未经授权，严禁转载。如需转载，请[联系作者](mailto:lixuguang316@gmail.com)。