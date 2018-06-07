---
title: tslint 与 git pre-commit 配置教程
date: 2018-06-07 16:30:11
categories: "tslint"
tags:
     - git
     - tslint
---

> ***

## tslint 配合pre-commit的意义

为什么用pre-commit 加 tslint（jshint，eslint原理都类似），因为在项目中我们会经常忘记主动的去做代码检查，虽然结合webpack各种构建工具下，存在*slint报错，项目会跑不起来。但在某些情况下，可能会因为着急，或者其他原因，没有去观察项目运行的情况就仓促提交。团队开发的情景下，可能会成为别人的麻烦。而pre-commit tslint解决的需求既是：拒绝向仓库提交错误代码。

## git hooks

在配置tslint pre commit之前，首先需要了解git hooks，正如它的名字所示，这是一个关于git 操作的钩子，比如我们想要在做远程仓库推送时，那就会触发pre-push这个钩子，然后在这个钩子中写下自己想做的事。git hooks的配置就在项目.git文件夹下面的hooks文件夹中。

在写相关的钩子函数时，需要注意的是，将钩子后面的sample后缀去掉，代码才会生效。

比如，本文中用到的pre-commit这个钩子。 

更多关于git hooks的介绍，请参考：https://git-scm.com/book/en/v2/Customizing-Git-Git-Hooks

下面介绍如何配置：

 ***

 <!-- more -->

## 配置步骤

1. 打开项目中的.git/hooks文件夹，找到pre-commit.sample文件，将以下代码替换到文件中。

```
#!/bin/bash
TSLINT="$(git rev-parse --show-toplevel)/node_modules/.bin/tslint"
for file in $(git diff --cached --name-only | grep -E '\.ts$')
do
        git show ":$file" | "$TSLINT" "$file"
        if [ $? -ne 0 ]; then
                exit 1
        fi
done
```

2. 将pre-commit.sample文件名修改为pre-commit。

此时再打开项目运行git commit -m"xxx"命令时，tslint会做自动的检查，如果没有错误的话，才会提交成功。而存在tslint报错的话，会终止提交。 
![tslint-error.png](https://upload-images.jianshu.io/upload_images/3100736-33f7c7ab5dc22071.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

* 注意： 日常开发中，有时为了方便会直接使用git commit -am"xxx"（即add+commit）的指令。而pre-commit 只是单独commit 钩子，因此还需要在pre-applypatch这个钩子下去做相同的配置。