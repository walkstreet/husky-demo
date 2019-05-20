# husky-demo
目前规范使用较多的是 Angular 团队的规范, 继而衍生了 Conventional Commits specification. 很多工具也是基于此规范, 它的 message 格式如下:
<type>(<scope>): <subject>
<BLANK LINE>
<body>
<BLANK LINE>
<footer>
复制代码我们通过 git commit 命令带出的 vim 界面填写的最终结果应该类似如上这个结构, 大致分为三个部分(使用空行分割):

标题行: 必填, 描述主要修改类型和内容
主题内容: 描述为什么修改, 做了什么样的修改, 以及开发的思路等等
页脚注释: 放 Breaking Changes 或 Closed Issues

分别由如下部分构成:

+ type: commit 的类型
+ feat: 新特性
+ fix: 修改问题
+ refactor: 代码重构
+ docs: 文档修改
+ style: 代码格式修改, 注意不是 css 修改
+ test: 测试用例修改
+ chore: 其他修改, 比如构建流程, 依赖管理.
+ scope: commit 影响的范围, 比如: route, component, utils, build...
+ subject: commit 的概述, 建议符合  50/72 formatting
+ body: commit 具体修改内容, 可以分为多行, 建议符合 50/72 formatting
+ footer: 一些备注, 通常是 BREAKING CHANGE 或修复的 bug 的链接.

这样一个符合规范的 commit message, 就好像是一份邮件.

## 集成步骤
1. npm install -D commitizen cz-conventional-changelog
2. package.json中配置：  

```
"script": {
    "commit": "git-cz",
},
"config": {
    "commitizen": {
      "path": "node_modules/cz-conventional-changelog"
    }
}
```

## 校验你的message
1. npm i -D @commitlint/config-conventional @commitlint/cli
2. 同时需要在项目目录下创建配置文件 .commitlintrc.js, 写入:

```
module.exports = {
  extends: [
    ''@commitlint/config-conventional''
  ],
  rules: {
  }
};
```

### 结合Husky
校验 commit message 的最佳方式是结合 git hook, 所以需要配合 Husky.
1. npm i husky@next
2. package.json 中添加:   

```
"husky": {
    "hooks": {
      "commit-msg": "commitlint -e $GIT_PARAMS"
    }
},
```

### standard-version: 自动生成 CHANGELOG
1. npm i -S standard-version
2. package.json 配置:

```
"scirpt": {
    "release": "standard-version"
}
```


## 参考文档
https://juejin.im/post/5afc5242f265da0b7f44bee4

### 标准流程
```
git add .
npm run commit
git push
```