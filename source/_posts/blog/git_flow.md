---
title: 工作流设计
date: 2024-01-02 21:35:56
tags:
- git
- git flow
---

## 什么是工作流

## 集中式工作流

定义：都使用 master 分支或者特定的某一分支进行开发。
适用场景：团队人数少、开发不频繁、不需要同时维护多个版本的小项目。

## 功能分支工作流

定义：开发新功能时基于 master 新建一个分支，在新分支上开发测试，测试完成之后合并回 master 分支。最后的合并不能直接合并需要提 Pull Request。
适用场景：开发团队相对固定，规模较小的项目中。

## Git Flow 工作流

定义：Git Flow 中定义了 5 种分支，分别是 master、develop、feature、release 和 hotfix，其中 master 和 develop 为常驻分支，不同研发阶段回用到不同的分支。
|分支|描述|
|--|--|
|master|该分支上的最新代码永远是发布状态，不能直接在该分支上开发。master 每合并一个 hotfix/release 都会打上版本标签|
|develop|该分支上的代码是开发中的最新版本，该分支只做合并操作，不能直接在该分支上开发|
|feature|在研发阶段用来做功能开发，一个新功能会基于 develop 创建一个 feature 分支。功能开发完成后合并到 develop 分支并删除 feature 分支|
|release|在发布阶段用作版本发布的预发布分支，基于 develop 分支创建，分支名建议命名为 release/xxx-xxx 测试后合并回 master 和 develop|
|hotfix|在维护阶段用来做 bug 修复|
适用场景：开发团队相对固定，项目较大的项目

## Git Forking 工作流

定义：fork 仓库到自己账号下，功能分支开发，推入自己仓库远端分支，对源仓库提交 PR。
适用场景：开源项目、开发者有衍生版本的需求、开发人员可能是可以访问到项目的任何人。

