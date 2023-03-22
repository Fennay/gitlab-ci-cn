# GitLab 持续集成 (GitLab CI) 

![ss](https://docs.gitlab.com/ee/ci/img/cicd_pipeline_infograph.png)

当自动化在你的工作中扮演一个不可或缺的角色时，持续集成带来的收益是巨大的。GitLab具有内置的持续集成、持续部署和持续交付来构建、测试和部署应用程序。

这里有一些我们收集到的信息带你开始持续集成。

## 开始

向你的GitLab CI旅程迈出的第一步。

- [开始使用GitLab CI](https://fennay.github.io/gitlab-ci-cn/quick_start.html)
- [Pipelines and jobs](https://docs.gitlab.com/ee/ci/pipelines.html)
- [配置Runner，让它运行你的程序](https://docs.gitlab.com/ee/ci/runners/README.html)
- 参考文章
  - [Getting started with GitLab and GitLab CI - Intro to CI](https://about.gitlab.com/2015/12/14/getting-started-with-gitlab-and-gitlab-ci/)
  - [Continuous Integration, Delivery, and Deployment with GitLab - Intro to CI/CD](https://about.gitlab.com/2016/08/05/continuous-integration-delivery-and-deployment-with-gitlab/)
  - [GitLab CI: Run jobs sequentially, in parallel, or build a custom pipeline](https://about.gitlab.com/2016/07/29/the-basics-of-gitlab-ci/)
  - [Setting up GitLab Runner For Continuous Integration](https://about.gitlab.com/2016/03/01/gitlab-runner-with-docker/)
  - [GitLab CI: Deployment & environments](https://about.gitlab.com/2016/08/26/ci-deployment-and-environments/)
- 视频：
  -  [Demo (Streamed live on Jul 17, 2017): GitLab CI/CD Deep Dive](https://youtu.be/pBe4t1CD8Fc?t=195)
  -  [Demo (March, 2017): how to get started using CI/CD with GitLab](https://about.gitlab.com/2017/03/13/ci-cd-demo/)
  -  [Webcast (April, 2016): getting started with CI in GitLab](https://about.gitlab.com/2016/04/20/webcast-recording-and-slides-introduction-to-ci-in-gitlab/)
- 第三方视频
  - [Intégration continue avec GitLab (September, 2016)](https://www.youtube.com/watch?v=URcMBXjIr24&t=13s)
  - [GitLab CI for Minecraft Plugins (July, 2016)](https://www.youtube.com/watch?v=Z4pcI9F8yf8)

## 参考指南

一旦你熟悉了入门指南，你就会发现自己会去查阅特定的参考指南。

- [`.gitlab-ci.yml`指南](https://fennay.github.io/gitlab-ci-cn/quick_start.html) - 了解关于`.gitlab-ci.yml`的所有细节和参数设置。
- CI Variables - 了解如何在你的`.gitlab-ci.yml`中使用变量或者保证项目中变量安全。
- 权限模型 - 了解用户执行某些CI操作的访问级别
  - [用户权限](https://docs.gitlab.com/ee/user/permissions.html#gitlab-ci)
  - [Job权限](https://docs.gitlab.com/ee/user/permissions.html#job-permissions)

## Auto DevOps 

- [Auto DevOps](https://docs.gitlab.com/ee/topics/autodevops/index.html)

## GitLab CI + Docker 

利用Docker的力量来运行CI piplis。

- 使用docker 镜像执行GitLab Runner。
- 使用CI构建docker镜像
- CI 服务（链接docker容器）
- 文章
  - [Setting up GitLab Runner For Continuous Integration](https://about.gitlab.com/2016/03/01/gitlab-runner-with-docker/)

## 高级使用

一旦你熟悉了GitLab CI的基础知识，就该开始学习如何利用它的潜能了。

- [Environments and deployments](https://docs.gitlab.com/ee/ci/environments.html) - 将你的工作分成不同的环境，并将它们用于不同的目的，如测试、构建和部署。
- [Job artifacts](https://docs.gitlab.com/ee/user/project/pipelines/job_artifacts.html)
- [Git submodules](https://docs.gitlab.com/ee/ci/git_submodules.html) - 在涉及Git子模块时如何运行CI jobs
- [Auto deploy](https://docs.gitlab.com/ee/ci/autodeploy/index.html)
- [Use SSH keys in your build environment](https://docs.gitlab.com/ee/ci/ssh_keys/README.html) and status of each CI environment running on Kubernetes
- [Trigger pipelines through the GitLab API](https://docs.gitlab.com/ee/ci/triggers/README.html)
- [Trigger pipelines on a schedule](https://docs.gitlab.com/ee/user/project/pipelines/schedules.html)
- [Deploy Boards](https://docs.gitlab.com/ee/user/project/deploy_boards.html) - 检查当前状况
- [Kubernetes clusters](https://docs.gitlab.com/ee/user/project/clusters/index.html) - 将一个或多个Kubernetes集群集成到项目中。

## Review Apps

- [Review Apps](https://docs.gitlab.com/ee/ci/review_apps/index.html)
- 参考文章:
  - [Introducing Review Apps](https://about.gitlab.com/2016/11/22/introducing-review-apps/)
  - [Example project that shows how to use Review Apps](https://gitlab.com/gitlab-examples/review-apps-nginx/)

## GitLab CI for GitLab Pages 

See the topic on [GitLab Pages](https://docs.gitlab.com/ee/user/project/pages/index.html).

## 特殊配置

你可以在你的整个GitLab实例以及每个项目中更改GitLab CI的默认行为。

- Project specific
  - [Pipelines settings](https://docs.gitlab.com/ee/user/project/pipelines/settings.html)
  - [Learn how to enable or disable GitLab CI](https://docs.gitlab.com/ee/ci/enable_or_disable_ci.html)
- Affecting the whole GitLab instance
  - [Continuous Integration admin settings](https://docs.gitlab.com/ee/user/admin_area/settings/continuous_integration.html)

## 示例

> 注意：[GitLab CI Yml 项目](https://gitlab.com/gitlab-org/gitlab-ci-yml)是官方维护的`.gitlab-ci.yml`文件集合。如果你最爱的编程语言或框架没有`.gitlab-ci.yml`文件，我们非常欢迎你通过提交merge request来帮忙。

这里有一些关于设置CI pipline的教程和指南。

- [GitLab CI示例](https://docs.gitlab.com/ee/ci/examples/README.html)：
  - [PHP](https://docs.gitlab.com/ee/ci/examples/php.html)
  - [Ruby](https://docs.gitlab.com/ee/ci/examples/test-and-deploy-ruby-application-to-heroku.html)
  - [Python](https://docs.gitlab.com/ee/ci/examples/test-and-deploy-python-application-to-heroku.html)
  - [Clojure](https://docs.gitlab.com/ee/ci/examples/test-clojure-application.html)
  - [Scala](https://docs.gitlab.com/ee/ci/examples/test-scala-application.html)
  - [Phoenix](https://docs.gitlab.com/ee/ci/examples/test-phoenix-application.html)
  - [Run PHP Composer & NPM scripts then deploy them to a staging server](https://docs.gitlab.com/ee/ci/examples/deployment/composer-npm-deploy.html)
  - [Analyze code quality with the Code Climate CLI](https://docs.gitlab.com/ee/ci/examples/code_climate.html)
- 参考文章：
  - [How to test and deploy Laravel/PHP applications with GitLab CI/CD and Envoy](https://docs.gitlab.com/ee/articles/laravel_with_gitlab_and_envoy/index.html)
  - [How to deploy Maven projects to Artifactory with GitLab CI/CD](https://docs.gitlab.com/ee/ci/examples/artifactory_and_gitlab/index.html)
  - [Automated Debian packaging](https://about.gitlab.com/2016/10/12/automated-debian-package-build-with-gitlab-ci/)
  - [Spring boot application with GitLab CI and Kubernetes](https://about.gitlab.com/2016/12/14/continuous-delivery-of-a-spring-boot-application-with-gitlab-ci-and-kubernetes/)
  - [Setting up GitLab CI for iOS projects](https://about.gitlab.com/2016/03/10/setting-up-gitlab-ci-for-ios-projects/)
  - [Setting up GitLab CI for Android projects](https://about.gitlab.com/2016/11/30/setting-up-gitlab-ci-for-android-projects/)
  - [Building a new GitLab Docs site with Nanoc, GitLab CI, and GitLab Pages](https://about.gitlab.com/2016/12/07/building-a-new-gitlab-docs-site-with-nanoc-gitlab-ci-and-gitlab-pages/)
  - [CI/CD with GitLab in action](https://about.gitlab.com/2017/03/13/ci-cd-demo/)
  - [Building an Elixir Release into a Docker image using GitLab CI](https://about.gitlab.com/2016/08/11/building-an-elixir-release-into-docker-image-using-gitlab-ci-part-1/)
- 杂项
  - [Using `dpl` as deployment tool](https://docs.gitlab.com/ee/ci/examples/deployment/README.html)
  - [Repositories with examples for various languages](https://gitlab.com/groups/gitlab-examples)
  - [The .gitlab-ci.yml file for GitLab itself](https://gitlab.com/gitlab-org/gitlab-ce/blob/master/.gitlab-ci.yml)
  - [Example project that shows how to use Review Apps](https://gitlab.com/gitlab-examples/review-apps-nginx/)

## 集成

- 参考文章：
    - [Continuous Delivery with GitLab and Convox](https://about.gitlab.com/2016/06/09/continuous-delivery-with-gitlab-and-convox/)
    - [Getting Started with GitLab and Shippable Continuous Integration](https://about.gitlab.com/2016/05/05/getting-started-gitlab-and-shippable/)
    - [GitLab Partners with DigitalOcean to make Continuous Integration faster, safer, and more affordable](https://about.gitlab.com/2016/04/19/gitlab-partners-with-digitalocean-to-make-continuous-integration-faster-safer-and-more-affordable/)

## 为什么选择GitLab CI？

- 参考文章：
    - [Why We Chose GitLab CI for our CI/CD Solution](https://about.gitlab.com/2016/10/17/gitlab-ci-oohlala/)
    - [Building our web-app on GitLab CI: 5 reasons why Captain Train migrated from Jenkins to GitLab CI](https://about.gitlab.com/2016/07/22/building-our-web-app-on-gitlab-ci/)

## 正在发生的变化

- [为GitLab 9.0重命名CI变量](https://docs.gitlab.com/ee/ci/variables/README.html#9-0-renaming) 阅读一些已经不推荐的CI变量，以及如何使用GitLab 9.0+。
- [新的CI工作权限模型](https://docs.gitlab.com/ee/user/project/new_ci_build_permissions_model.html) 查看在GitLab 8.12中发生了什么变化，以及这会如何影响工作。有一种新的方法可以访问工作中的Git子模块和LFS对象。



[编辑此页面](https://gitlab.com/gitlab-org/gitlab-ee/blob/master/doc/ci/README.md)