# 开始GitLab CI

官方原文档：https://docs.gitlab.com/ee/ci/quick_start/README.html

> 注：从8.0版本开始，GitLab持续集成（CI）完全集成到GitLab中，且所有的项目默认开启。

GitLab提供持续集成服务。如果添加一个`.gitlab-ci.yml`[文件](https://docs.GitLab.com/ee/ci/yaml/README.html)到项目根目录，并配置GitLab项目使用某个[Runner](https://docs.GitLab.com/ee/ci/runners/README.html),然后每一次提交或者是推送都会触发CI [pipeline](https://docs.GitLab.com/ee/ci/pipelines.html).

`.gitlab-ci.yml`文件会告诉GitLab Runner 该怎么做。默认情况下，它运行一个`pipeline`，分为三个阶段：`build`,`test`,`deploy`.你并不需要用到所有的阶段，没有`job`的阶段会被忽略。

如果所有的运行都正常（没有非0返回值），此次的commit将得到一个绿色的复选标记。