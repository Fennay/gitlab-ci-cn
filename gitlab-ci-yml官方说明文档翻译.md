# 通过 .gitlab-ci.yml配置任务

[TOC]

此文档用于描述.gitlab-ci.yml语法，.gitlab-ci.yml文件被用来管理项目的runner 任务。

如果想要快速的了解GitLab CI ，可移步[快速引导](https://docs.gitlab.com/ce/ci/quick_start/README.html)。

## .gitlab-ci.yml

从7.12版本开始，GitLab CI使用[YAML](https://en.wikipedia.org/wiki/YAML)文件(.gitlab-ci.yml)来管理项目配置。该文件存放于项目仓库的根目录，它定义该项目如何构建。

开始构建之前YAML文件定义了一系列带有约束说明的任务。这些任务都是以任务名开始并且至少要包含`script`部分：

```shell
job1:
  script: "execute-script-for-job1"
  
job2:
  script: "execute-script-for-job2"
```

上面这个例子就是一个最简单且带有两个独立任务的CI配置，每个任务分别执行不同的命令。

`script`可以直接系统命令(例如：./configure;make;make install)或者是直接执行脚本(test.sh)。

任务是由[Runners](https://docs.gitlab.com/ce/ci/runners/README.html)接管并且由服务器中runner执行。更重要的是，每一个任务的执行过程都是独立运行的。

用下面这个例子来说明YAML语法还有更多复杂的任务：

```shell
image: ruby:2.1
services:
  - postgres

before_script:
  - bundle install

after_script:
  - rm secrets

stages:
  - build
  - test
  - deploy

job1:
  stage: build
  script:
    - execute-script-for-job1
  only:
    - master
  tags:
    - docker
```

下面列出保留字段，这些保留字段是无法作为`job`名称：

| 关键字           | 是否必须 | 描述                                       |
| ------------- | ---- | ---------------------------------------- |
| image         | 否    | 用于docker镜像，查看[docker](https://docs.gitlab.com/ce/ci/docker/README.html)文档 |
| services      | 否    | 用于docker服务，查看[docker](https://docs.gitlab.com/ce/ci/docker/README.html)文档 |
| stages        | 否    | 定义构建阶段                                   |
| types         | 否    | `stages` 的别名(已废除)                        |
| before_script | 否    | 定义在每个job之前运行的命令                          |
| after_script  | 否    | 定义在每个job之后运行的命令                          |
| variable      | 否    | 定义构建变量                                   |
| cache         | 否    | 定义一组文件列表，可在后续运行中使用                       |

### image和services

这两个关键字允许使用一个自定义的Docker镜像和一系列的服务，并且可以用于整个job周期。详细配置文档请查看[a separate document](https://docs.gitlab.com/ce/ci/docker/README.html)。

### before_script

`before_script`用来定义所有job之前运行的命令，包括deploy(部署) jobs，但是在修复artifacts之后。它可以是一个数组或者是多行字符串。

### after_script

> GitLab 8.7 开始引入，并且要求Gitlab Runner v1.2

`after_script`用来定义所有job之后运行的命令。它必须是一个数组或者是多行字符串

### stages

`stages`用来定义可以被job调用的stages。stages的规范允许有灵活的多级pipelines。

stages中的元素顺序决定了对应job的执行顺序：

	1. 相同stage的job可以平行执行。
	2. 下一个stage的job会在前一个stage的job成功后开始执行。

接下仔细看看这个例子，它包含了3个stage：

```
stages:
 - build
 - test
 - deploy
```

1. 首先，所有`build`的jobs都是并行执行的。
2. 所有`build`的jobs执行成功后，`test`的jobs才会开始并行执行。
3. 所有`test`的jobs执行成功，`deploy`的jobs才会开始并行执行。
4. 所有的`deploy`的jobs执行成功，commit才会标记为`success`
5. 任何一个前置的jobs失败了，commit会标记为`failed`并且下一个stages的jobs都不会执行。

这有两个特殊的例子值得一提：

1. 如果`.gitlab-ci.yml`中没有定义`stages`，那么job's stages 会默认定义为 `build`，`test` 和 `deploy`。
2. 如果一个job没有指定`stage`，那么这个任务会分配到`test` stage。

### types

> 已废除，将会在10.0中移除。用stages替代。

与[stages](#)同义

### variables

> GitLab Runner V0.5.0. 开始引入

GItLab CI 允许在`.gitlab-ci.yml`文件中添加变量，并在job环境中起作用。因为这些配置是存储在git仓库中，所以最好是存储项目的非敏感配置，例如：

```shell
variables:
  DATABASE_URL:"postgres://postgres@postgres/my_database"
```

这些变量可以被后续的命令和脚本使用。服务容器也可以使用YAML中定义的变量，因此我们可以很好的调控服务容器。变量也可以定义成[job level](https://docs.gitlab.com/ce/ci/yaml/README.html#job-variables)。

出来用户自定义的变量外，Runner也可以定义它自己的变量。`CI_COMMIT_REG_NAME`就是一个很好的例子，

### cache

> Gitlab Runner v0.7.0 开始引入



##### 缓存key

### 任务

#### 脚本

#### 阶段

#### 唯一和排除

#### 任务变量

#### 标签

#### 允许的失败

#### when

##### 手动执行

#### 环境



官方文档地址：https://docs.gitlab.com/ce/ci/yaml/README.html