---
title: 初识git-hook01
toc: true
mathjax: true
date: 2019-02-14 16:48:15
tags: [git]
categories: git
---
## git hook 简介
git hook可以在特定操作之前或者之后执行自定义的脚本

## 待研究
在提交代码后，自动部署静态页面
主要使用post-receive实现

## 客户端钩子
commit-msg
pre-commit 提交之前
post-commit 提交之后

## 服务器钩子
pre-receive 接受之前
update 更新之前
post-update 更新之后
post-receive 接受之后

pre-commit hook
检查提交信息
```bash
#!/usr/bin/env bash
regularExpression="^\s?\[(feature|bugfix|refactor|other)\]\s?\[.+\]\s?.+"
error_msg="
-----------------------------------------------
提交信息首行请按照如下格式书写:
[commitType][module] description
detail ...
1. commitType只能是feature（新功能）、bugfix（修复bug）、refactor（重构）、other（其他）
2. module 则为对应的功能模块，如: lvsfullnat pa_nat 等
3. description 简单描述改动。
4. detail 详细描述改动。
-----------------------------------------------
例如：
[feature][lvsfullnat-2.17] 自动解绑pool
1.neutron_lbass/service/pa_lvs/pa_lvs_plugin.py
  删除时判断，如果是最后一个member，自动解绑pool。
2.neutron_lbass/db/loadbalancer_lvsdb.py
  修改对应的 orm 函数 delete_pool_member"
  
#获取提交信息
firstLine=`head -n1 "$1"`
echo -e "你的提交信息如下: \n$firstLine"
if [[ "$firstLine" =~ $regularExpression ]]; then
    echo "commit success"
    exit 0
fi
echo "commit fail"
echo -e "你的提交信息如下：\n`cat .git/COMMIT_EDITMSG`"
echo "$error_msg" >&2
exit 1
```