# 开始GitLab CI/CD


官方原文档：https://docs.gitlab.com/ee/ci/quick_start/README.html

> 注：从8.0版本开始，GitLab [持续集成](https://about.gitlab.com/gitlab-ci/)（CI）完全集成到GitLab中，且默认所有的项目开启。

GitLab提供[持续集成](https://about.gitlab.com/gitlab-ci/)服务。如果添加一个[`.gitlab-ci.yml`文件](https://docs.gitlab.com/ee/ci/yaml/README.html)到项目根目录，并配置GitLab项目使用某个[Runner](https://docs.GitLab.com/ee/ci/runners/README.html)，然后每一次提交或者是推送都会触发CI [pipeline](https://docs.GitLab.com/ee/ci/pipelines.html).

`.gitlab-ci.yml`文件会告诉GitLab Runner 做什么。默认情况下，它运行一个`pipeline`，分为三个阶段：`build`，`test`，`deploy`。你并不需要用到所有的阶段，没有`job`的阶段会被忽略。

如果一切运行正常(没有非零的返回值)，您将得到与commit关联的漂亮的绿色标记。这使得在查看代码之前，很容易就能看出是否有一个提交导致了测试失败。

大多数项目使用GitLab CI服务来运行测试套件，这样如果开发人员发现问题就会及时得到反馈。

因此，简而言之，CI所需要的步骤可以归结为：
```
1. 添加`.gitlab-ci.yml`到项目的根目录
2. 配置一个Runner
```
从此刻开始，在每一次push到Git仓库的过程中，Runner会自动开启pipline，pipline将显示在项目的Pipline页面中。

------

本指南要求：

- 使用版本8.0+ 的GitLab实例或者是使用[GitLab.com](https://gitlab.com/)
- 一个想使用GitLab CI的项目

让我们把它分解成碎片，并致力于解决GitLab CI之谜。

# 创建`.gitlab-ci.yml`

在创建`.gitlab-ci.yml`之前，我们先对它进行个简单的解释。

## `.gitlab-ci.yml`是什么

`.gitlab-ci.yml`是用来配置CI在我们的项目中做些什么工作。它位于项目的根目录。

在任何的push操作，GitLab都会寻找`.gitlab-ci.yml`文件，并对此次commit开始jobs，jobs的内容来源于`.gitlab-ci.yml`文件。

因为`.gitlab-ci.yml`是存在于我们的项目仓库中，并且受版本控制的，所以旧版本也可以执行成功，且使用CI可以让forks更容易，分支可也以拥有不同的pipelines和jobs，而且对于CI来说只会拥有单一的来源。你也可以在我们的博客中找到我们为什么使用`.gitlab-ci.yml`的原因。

## 创建一个简单的`.gitlab-ci.yml`

> 注意：`.gitlab-ci.yml`是一个[YAML](https://en.wikipedia.org/wiki/YAML)文件，所以必须要格外注意锁紧。使用空格，而不是tabs。

在项目的根目录创建一个名为`.gitlab-ci.yml`的文件。下面是一个Ruby on Rails项目的示例。

```yaml
before_script:
  - apt-get update -qq && apt-get install -y -qq sqlite3 libsqlite3-dev nodejs
  - ruby -v
  - which ruby
  - gem install bundler --no-ri --no-rdoc
  - bundle install --jobs $(nproc)  "${FLAGS[@]}"

rspec:
  script:
    - bundle exec rspec

rubocop:
  script:
    - bundle exec rubocop
```

这是大多数Ruby应用程序最简单的配置：

1. 定义了两个jobs，`rspec`和`rubocop`（名字可以随便取），他们执行不同的命令。
2. 在每个jobs之前，`before_script`定义的命令都将会被执行。

`.gitlab-ci.yml`定义了一系列的jobs，其中包含如何运行和何时运行的限制。jobs必须定义一个名称（在示例中分别是`rspec`和`rubocop`）作为顶级元素，而且总是必须包含`script`关键字。Jobs被用来创建任务，它们会被Runners接受和环境中的Runner执行。

重要的是，每个工作都是独立运行的。

如果你想检验`.gitlab-ci.yml`文件的语法是否正确，在GitLab实例页面中有一个命令行工具`/ci/lint`。也可以从项目中的**CI/CD ➔ Pipelines** and **Pipelines ➔ Jobs**找到此页面。

关于更多`.gitlab-ci.yml`的信息和语法，请阅读[.gitlab-ci.yml](https://docs.gitlab.com/ee/ci/yaml/README.html)参考文档。

## 推送`.gitlab-ci.yml`到GitLab

一旦创建了`.gitlab-ci.yml`，你应该及时添加到Git仓库并推送到GitLab。

```shell
git add .gitlab-ci.yml
git commit -m "Add .gitlab-ci.yml"
git push origin master
```

现在到**Pipelines**页面查看，将会看到该Pipline处于等待状态。

你也可以到**Commits**页面查看，并会发现SHA旁边的暂停按钮。

![](https://docs.gitlab.com/ee/ci/quick_start/img/new_commit.png)

点击它即可进入到该特定commit的jobs页面。

![](https://docs.gitlab.com/ee/ci/quick_start/img/single_commit_status_pending.png)

## 配置Runner

在GitLab中，Runners将会运行你在`.gitlab-ci.yml`中定义的jobs。Runner可以是虚拟机，VPS，裸机，docker容器，甚至一堆容器。GitLab和Runners通过API通信，所以唯一的要求就是运行Runners的机器可以联网。

一个Runner可以服务GitLab中的某个特定的项目或者是多个项目。如果它服务所有的项目，则被称为共享的Runner。

在[Runners](https://docs.gitlab.com/ee/ci/runners/README.html)文档中查阅更多关于不同Runners的信息。

你可以通过**Settings->CI/CD**查找是否有Runners分配到你的项目中。创建一个Runner是简单且直接的。官方支持的Runner是用GO语言写的，它的文档在这里https://docs.gitlab.com/runner/。

为了有一个功能性的Runner，你需要遵循以下步骤：

1. [安装](https://docs.gitlab.com/runner/install/)
2. [配置](https://docs.gitlab.com/ee/ci/runners/README.html#registering-a-specific-runner)

按照上面的连接设置你自己的Runner或者使用下一节介绍的共享Runner。

一旦Runner安装好，你可以从项目的**Settings->CI/CD**找到Runner页面。

## ![](https://docs.gitlab.com/ee/ci/quick_start/img/runners_activated.png)

## 共享Runners

如果你用的是GitLab.com，你可以使用GitLab公司提供的共享Runners。

这些是运行在GitLab基础设置上面的特殊虚拟机，可以构建任何项目。

你可以通过项目中的**Settings->CI/CD**找到**Shared Runners**，并点击开启它。

[阅读更多关于共享Runners](https://docs.gitlab.com/ee/ci/runners/README.html)。

## 查看pipeline和jobs的状态

成功的配置好Runner后，你应该查看最后一次提交后的状态，从*pending*、到*执行中*、*成功*或*失败*。

你可以通过项目中的Piplines页面查看所有的piplines。

![](https://docs.gitlab.com/ee/ci/quick_start/img/pipelines_status.png)

也可以通过**Piplines->Jobs**页面查看所有的jobs。

![](https://docs.gitlab.com/ee/ci/quick_start/img/builds_status.png)

通过点击jobs的状态，查看该job的日志。这对于帮助诊断job失败或者job与预期结果不同很重要。

![](https://docs.gitlab.com/ee/ci/quick_start/img/build_log.png)

你还可以查看在GitLab的各种页面中的任何提交状态，例如**Commits**和**Merge requests**。

## Examples

在[这里](https://docs.gitlab.com/ee/ci/examples/README.html)，可以查看各种语言使用GitLab CI的示例。