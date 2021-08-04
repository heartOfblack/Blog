---
title: 1 初始化项目
date: 2021-4-6
categories:
 - vue从零搭建业务管理 
---

# 创建项目

通过vue-cli脚手架，可以快速创建一个项目原型，在原型基础上，根据自身需求添加额外配置

1. 全局安装vue-cli   ```npm install -g @vue/cli```
2. vue create hello-world (根据交互提示，选择自己需要的基础配置，主要是eslint选择standard配置，他有命令行可以用)

>如果你在 Windows 上通过 minTTY 使用 Git Bash，交互提示符并不工作。你必须通过 `winpty vue.cmd create hello-world` 启动这个命令。不过，如果你仍想使用 `vue create hello-world`，则可以通过在 `~/.bashrc` 文件中添加以下行来为命令添加别名。 `alias vue='winpty vue.cmd'` 你需要重新启动 Git Bash 终端会话以使更新后的 bashrc 文件生效。

3. npm run serve 即可运行初始项目



vue-cli版本为4.x，则项目不会自动生成vue.config.js配置文件，如有需要更改选项，可以手动创建并更改。

