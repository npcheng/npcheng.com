---
title: gitlab的持续集成runner (一)
date: 2019-01-06 19:58:39
tags:
---

持续集成是啥？ 就是软件工程的一种具体实践方式， 比较频繁的通过自动化的方式来验证（编译，发布，自动化测试）各个阶段的错误。
![ci/cd pic](https://img.npcheng.com/cicd_pipeline_infograph.png)

gitlab在8.0及以后版本集成了持续集成工具:Runners，  

Runners三个特定的runner:

1. Shared Runners
2. Specific Runners
3. Group Runners

现在我gitlab使用的是gitlab.com没有自己搭建，所以我的理解：shared runner是gitalb提供的runners,  Specific Runnders是运行在自己的服务器上的runner, Group Runners没有使用过暂时未知。

shared Runners是使用Docker做为开发环境，现在主要用它发布hexo page. 因为开发需要最近主要在测试Spicific Runners.

### 安装

Spicfic Runners 支持多平台主流的linux/macos/Windows都支持，具体可参考[runners install](https://docs.gitlab.com/runner/install/index.html)

我的环境是ubuntu linux

```bash
 curl -L https://packages.gitlab.com/install/repositories/runner/gitlab-runner/script.deb.sh | sudo bash
 ```

 查看gitlab projects ->选择项目-> settings->CI/CD -> Runners -> Expand 记住Set up a specific Runner manually 的URL 和gitlab-token大致信息如下
 [specific runner set up](https://img.npcheng.com/20190107161101.png)

### 注册

 ```bash
 sudo gitlab-runner register
 ```

 然后根据以下交互信息输入相关内容

```bash
  Please enter the gitlab-ci coordinator URL (e.g. https://gitlab.com )
 https://gitlab.com
 Please enter the gitlab-ci token for this runner # gitlab-ci token
 xxx
 Please enter the gitlab-ci description for this runner #自己定义
 [hostame] my-runner
 Please enter the gitlab-ci tags for this runner (comma separated): #指定tag, 根据tag决定否出发此runner, 可以不指定
 my-tag,another-tag
 Please enter the executor: ssh, docker+machine, docker-ssh+machine, kubernetes, docker, parallels, virtualbox, docker-ssh, shell:
 docker
 ```

 注册完成之后再项目的settings -> CI/CD ->  Set up a specific Runner manually 下面会出现一个runner.

### 测试

注册成功之后，我们进入测试阶段， gitlab的Runners 继承仅仅需要在项目的根目录配置.gitlab-ci.yml即可。提交代码后，Runners会根据.gitlab-ci.yml的配置信息决定做CI/CD
现在我们写一个简单的测试

```bash
before_script:
  - echo "Before script section"
  - echo "For example you might run an update here or install a build dependency"
  - echo "Or perhaps you might print out some debugging details"
   
after_script:
  - echo "After script section"
  - echo "For example you might do some cleanup here"
   
build1:
  stage: build
  script:
    - echo "Do your build here"
   
test1:
  stage: test
  script: 
    - echo "Do a test here"
    - echo "For example run a test suite"
   
test2:
  stage: test
  script: 
    - echo "Do another parallel test here"
    - echo "For example run a lint test"
   
deploy1:
  stage: deploy
  script:
    - pwd
    - ls
    - echo "Do your deploy here"
```

其实这个脚本啥也没干就是打印一下测试信息。 通过git 提交代码后在CI/CD -> Pipelines下面会看到执行结果。
大致结果如下

Pipline 状态

![runner_Pipeline](https://img.npcheng.com/20190107162918_1.png)

stage 状态

![runner_stage](https://img.npcheng.com/20190107162949_2.png)

runner执行结果

![runner_info](https://img.npcheng.com/20190107163001_3.png)

### 参考资料

- [https://docs.gitlab.com/ee/ci/yaml/README.html](https://docs.gitlab.com/ee/ci/yaml/README.html)
- [https://gitlab.com/ayufan/python-getting-started/blob/master/.gitlab-ci.yml](https://gitlab.com/ayufan/python-getting-started/blob/master/.gitlab-ci.yml)
- [https://docs.gitlab.com/ee/ci/](https://docs.gitlab.com/ee/ci/)
