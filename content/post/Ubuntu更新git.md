---
title: "Ubuntu更新git源"
date: 2020-12-31T21:29:55+08:00
images:
tags: 
  - Linux、git
---

### Ubuntu更新git源，免密登录

Ubuntu 自带的 Git 版本，比最新的 Git 版本低，会导致一系列问题，解决方案：

1. 增加软件源：

   ```shell
   sudo add-apt-repository ppa:git-core/ppa
   ```

2. 更新安装列表：

   ```shell
   sudo apt-get update
   ```

3. 升级git：

   ```shell
   sudo apt-get install git
   ```

4. 获取版本：

   ```shell
   git --version
   ```

5. 获取代码不用每次输入密码：

   ```shell
   git config --global credential.helper store
   ```

   