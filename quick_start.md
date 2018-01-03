# 开始GitLab CI/CD

[TOC]

官方原文档：https://docs.gitlab.com/ee/ci/quick_start/README.html

> 注：从8.0版本开始，GitLab [持续集成](https://about.gitlab.com/gitlab-ci/)（CI）完全集成到GitLab中，且默认所有的项目开启。

GitLab提供[持续集成](https://about.gitlab.com/gitlab-ci/)服务。如果添加一个[`.gitlab-ci.yml`文件](https://docs.gitlab.com/ee/ci/yaml/README.html)到项目根目录，并配置GitLab项目使用某个[Runner](https://docs.GitLab.com/ee/ci/runners/README.html)，然后每一次提交或者是推送都会触发CI [pipeline](https://docs.GitLab.com/ee/ci/pipelines.html).

`.gitlab-ci.yml`文件会告诉GitLab Runner 做什么。默认情况下，它运行一个`pipeline`，分为三个阶段：`build`，`test`，`deploy`。你并不需要用到所有的阶段，没有`job`的阶段会被忽略。

如果一切运行正常(没有非零的返回值)，您将得到与commit关联的漂亮的绿色标记。这使得在查看代码之前，很容易就能看出是否有一个提交导致了测试失败。

大多数项目使用GitLab CI服务来运行测试套件，这样如果开发人员发现问题就会及时得到反馈。

因此，简而言之，CI所需要的步骤可以归结为：

 	1. 添加`.gitlab-ci.yml`到项目的根目录
 	2. 配置一个Runner

从此刻开始，在每一次push到Git仓库的过程中，Runner会自动开启pipline，pipline将显示在项目的Pipline页面中。

------

本指南要求：

- 使用版本8.0+ 的GitLab实例或者是使用[Gitlab.com](https://gitlab.com/)
- 一个想使用GitLab CI的项目

让我们把它分解成碎片，并致力于解决GitLab CI之谜。