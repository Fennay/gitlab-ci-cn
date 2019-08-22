# GitLab 持续集成/部署 (GitLab CI/CD) 

官方文档：https://docs.gitlab.com/ee/ci/README.html

（update time: 2019-08-22）

GitLab CI/CD 是GitLab内置的工具，用于通过 [连续方法](https://docs.gitlab.com/ee/ci/introduction/index.html#introduction-to-cicd-methodologies) 进行软件开发：

- 持续集成（CI）
- 持续交付（CD）
- 持续部署（CD）

## 概述

持续集成的工作原理是将小代码块推送到Git存储库中托管的应用程序代码库，并在每次推送时运行一个 `pipeline` 脚本，以便在将代码更改合并到主分支之前对代码更改进行足够地构建，测试和验证。

持续交付和部署包括进一步的CI，在每次向默认分支推送代码的时候都会持续地将应用程序部署到生产环境中去。

这些持续集成/部署的方法允许您在开发周期的早期捕获错误和错误，确保部署到生产中的所有代码都符合您为应用程序建立的代码标准。

有关这些方法和 GitLab CI/CD 的完整概述，请阅读 [Introduction to CI/CD with GitLab](https://docs.gitlab.com/ee/ci/introduction/index.html)

有关 GitLab CI/CD的视频演示，请参阅 [Demo: CI/CD with GitLab](https://www.youtube.com/watch?v=1iXFbchozdY)

## 开始

GitLab CI/CD 由位于存储库根目录的名为 `.gitlab-ci.yml` 的文件配置。此文件中设置的脚本由[GitLab Runner](https://docs.gitlab.com/runner/)执行。

要开始使用GitLab CI / CD，我们建议您阅读以下文档：

- [GitLab CI/CD的工作原理](https://docs.gitlab.com/ee/ci/introduction/index.html#how-gitlab-cicd-works)
- [GitLab CI/CD基本工作流程](https://docs.gitlab.com/ee/ci/introduction/index.html#basic-cicd-workflow)
- [第一次编写 `.gitlab-ci.yml` 的分步指南](https://docs.gitlab.com/ee/user/project/pages/getting_started_part_four.html)

如果您要从Jenkins平台迁移过来，您还可以查看我们为您提供的 [pipelines 快速改造参考](https://docs.gitlab.com/ee/ci/jenkins/index.html)。

您还可以通过以UI中提供的 `.gitlab-ci.yml` 模板之一开始使用。您可以通过选择适合您应用程序的模板创建新文件，并根据自身的需要进行调整来使用它们：

![add_file_template_11_10.png](https://docs.gitlab.com/ee/ci/img/add_file_template_11_10.png)

有关更广泛的概述，请参阅 [CI/CD入门指南](https://docs.gitlab.com/ee/ci/quick_start/README.html)。

一旦您熟悉了 GitLab CI/CD 的工作原理，可以通过查阅 [`.gitlab-ci.yml` 完整参考](https://docs.gitlab.com/ee/ci/yaml/README.html)，了解您可以设置和使用的所有属性。

> 注意：GitLab CI / CD和共享运行程序在GitLab.com中启用，可供所有用户使用，仅限于用户的 pipelines 配额。

## 配置项

GitLab CI/CD支持多种配置选项：

| 配置项                                                                                                                    | 描述                                                                  |
| ------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------- |
| [Pipelines](https://docs.gitlab.com/ee/ci/pipelines.html)                                                                 | 通过 pipelines 的 CI/CD构建流程                                       |
| [Environment variables](https://docs.gitlab.com/ee/ci/variables/README.html)                                              | 基于变量/值键对的重用值                                               |
| [Environments](https://docs.gitlab.com/ee/ci/environments.html)                                                           | 将你的应用程序部署到不同的环境（例如，分段，生产）                    |
| [Job artifacts](https://docs.gitlab.com/ee/user/project/pipelines/job_artifacts.html)                                     | 输出，使用和重用作业工件                                              |
| [Cache dependencies](https://docs.gitlab.com/ee/ci/caching/index.html)                                                    | 缓存依赖项以加快执行速度                                              |
| [Schedule pipelines](https://docs.gitlab.com/ee/user/project/pipelines/schedules.html)                                    | 根据需要安排 pipelines 运行                                           |
| [Custom path for `.gitlab-ci.yml`](https://docs.gitlab.com/ee/user/project/pipelines/settings.html#custom-ci-config-path) | 自定义 CI/CD 配置文件的路径                                           |
| [Git submodules for CI/CD](https://docs.gitlab.com/ee/ci/git_submodules.html)                                             | 配置作业以使用Git子模块。                                             |
| [SSH keys for CI/CD](https://docs.gitlab.com/ee/ci/ssh_keys/README.html)                                                  | 在CI pipelines 中使用SSH密钥                                          |
| [Pipelines triggers](https://docs.gitlab.com/ee/ci/triggers/README.html)                                                  | 通过API触发 pipelines                                                 |
| [Pipelines for Merge Requests](https://docs.gitlab.com/ee/ci/merge_request_pipelines/index.html)                          | 设计用于在合并请求中运行 pipeline 的 pipeline 结构                    |
| [Integrate with Kubernetes clusters](https://docs.gitlab.com/ee/user/project/clusters/index.html)                         | 将您的项目连接到Google Kubernetes Engine（GKE）或现有的Kubernetes集群 |
| [GitLab Runner](https://docs.gitlab.com/runner/)                                                                          | 配置您自己的GitLab Runners以执行您的脚本                              |
| [Optimize GitLab and Runner for large repositories](https://docs.gitlab.com/ee/ci/large_repositories/index.html)          | 处理大型 repo 的推荐策略                                              |
| [`.gitlab-ci.yml` full reference](https://docs.gitlab.com/ee/ci/yaml/README.html)                                         | 您可以使用的 GitLab CI/CD 所有属性。                                  |

请注意，某些操作只能根据 [user](https://docs.gitlab.com/ee/user/permissions.html#gitlab-cicd-permissions) 和 [job](https://docs.gitlab.com/ee/user/permissions.html#job-permissions) 权限执行

## 功能集

使用庞大的 GitLab CI/CD 轻松配置它以用于达成特定目标。根据DevOps阶段，将其其功能集列在下表中。

| Feature                                | Description                                                                                                                    |
| -------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| Configure                              |                                                                                                                                |
| Auto DevOps                            | Set up your app’s entire lifecycle.                                                                                            |
| ChatOps                                | Trigger CI jobs from chat, with results sent back to the channel.                                                              |
| Verify                                 |                                                                                                                                |
| Browser Performance Testing            | Quickly determine the performance impact of pending code changes.                                                              |
| CI services                            | Link Docker containers with your base image.                                                                                   |
| Code Quality                           | Analyze your source code quality.                                                                                              |
| GitLab CI/CD for external repositories | Get the benefits of GitLab CI/CD combined with repositories in GitHub and BitBucket Cloud.                                     |
| Interactive Web Terminals              | Open an interactive web terminal to debug the running jobs.                                                                    |
| JUnit tests                            | Identify script failures directly on merge requests.                                                                           |
| Using Docker images                    | Use GitLab and GitLab Runner with Docker to build and test applications.                                                       |
| **Release**                            |                                                                                                                                |
| Auto Deploy                            | Deploy your application to a production environment in a Kubernetes cluster.                                                   |
| Building Docker images                 | Maintain Docker-based projects using GitLab CI/CD.                                                                             |
| Canary Deployments                     | Ship features to only a portion of your pods and let a percentage of your user base to visit the temporarily deployed feature. |
| Deploy Boards                          | Check the current health and status of each CI/CD environment running on Kubernetes.                                           |
| Feature Flags                          | Deploy your features behind Feature Flags.                                                                                     |
| GitLab Pages                           | Deploy static websites.                                                                                                        |
| GitLab Releases                        | Add release notes to Git tags.                                                                                                 |
| Review Apps                            | Configure GitLab CI/CD to preview code changes.                                                                                |
| **Secure**                             |                                                                                                                                |
| Container Scanning                     | Check your Docker containers for known vulnerabilities.                                                                        |
| Dependency Scanning                    | Analyze your dependencies for known vulnerabilities.                                                                           |
| License Compliance                     | Search your project dependencies for their licenses.                                                                           |
| Security Test reports                  | Check for app vulnerabilities.                                                                                                 |

## 示例

在[CI示例](https://docs.gitlab.com/ee/ci/examples/README.html)页面上查找使用 GitLab CI/CD 的各种应用程序框架，语言和平台的示例项目代码和教程。

GitLab还提供了预先配置为使用 GitLab CI/CD 的[示例项目](https://gitlab.com/gitlab-examples)。

## 管理

作为GitLab管理员，您可以更改 GitLab CI/CD的默认行为：

- [一整个GitLab实例](https://docs.gitlab.com/ee/user/admin_area/settings/continuous_integration.html)。
- 具体项目，使用 [pipelines settings.](https://docs.gitlab.com/ee/user/project/pipelines/settings.html)

也可以看看：
- [如何启用或禁用GitLab CI/CD](https://docs.gitlab.com/ee/ci/enable_or_disable_ci.html)。
- 其他 [CI管理设置](https://docs.gitlab.com/ee/administration/index.html#continuous-integration-settings)

## 参考

## 为什么选择GitLab CI / CD？

以下文章解释了为 CI/CD基础结构使用GitLab CI/CD的原因：

- 为什么我们选择GitLab CI作为CI/CD解决方案
- 在GitLab CI上构建我们的Web应用程序
- 5团队切换到GitLab CI/CD

另见为 [Why CI/CD?](https://docs.google.com/presentation/d/1OGgk2Tcxbpl7DJaIOzCX4Vqg3dlwfELC3u2jEeCBbDk)介绍。

打破变化

-