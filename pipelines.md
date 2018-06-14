# pipelines和jobs介绍

官方文档：https://docs.gitlab.com/ee/ci/pipelines.html

> 在GitLab 8.8中引入的。

> 注意：如果你的项目是从[GitLab中拉取的镜像仓库](https://docs.gitlab.com/ee/workflow/repository_mirroring.html#pulling-from-a-remote-repository)，需要在项目中开启触动开关
>
> **Settings > Repository > Pull from a remote repository > Trigger pipelines for mirror updates**.

## Pipelines

pipeline 是一组按[阶段](https://docs.gitlab.com/ee/ci/yaml/README.html#stages)（批处理）执行的[jobs](https://docs.gitlab.com/ee/ci/pipelines.html#jobs)。同一个阶段中的所有任务都是并行执行的（如果有足够的并发[Runners](https://docs.gitlab.com/ee/ci/runners/README.html)），如果它们全部成功，pipeline就进入下一个阶段。如果其中一个jobs失败，则下一个阶段不（通常）执行。您可以访问项目**Pipelines**选项卡中的pipeline页面。

在下面的图像中，您可以看到pipeline由4个阶段组成（`build(构建)`, `test(测试)`, `staging(分级)`, `production(生产)`），每个阶段都有一个或多个作业。

