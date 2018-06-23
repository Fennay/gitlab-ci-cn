# 管道和作业介绍

官方文档：https://docs.gitlab.com/ee/ci/pipelines.html

> 在GitLab 8.8中引入的。

> 注意：如果你的项目是从[GitLab中拉取的镜像仓库](https://docs.gitlab.com/ee/workflow/repository_mirroring.html#pulling-from-a-remote-repository)，需要在项目中开启触动开关
>
> **Settings > Repository > Pull from a remote repository > Trigger pipelines for mirror updates**.

## 管道

管道是一组[分阶段](https://docs.gitlab.com/ee/ci/yaml/README.html#stages)（批处理）执行的[工作](https://docs.gitlab.com/ee/ci/pipelines.html#jobs)。同一个阶段中的所有工作都是并行执行的（如果有足够的并发[Runners](https://docs.gitlab.com/ee/ci/runners/README.html)），如果它们全部成功，管道就进入下一个阶段。如果其中一个jobs失败，则下一个阶段不（通常）执行。您可以访问项目的**Pipeline**选项卡中的管道页面。

在下图中，您可以看到管道由4个阶段组成（`build(构建)`, `test(测试)`, `staging(分级)`, `production(生产)`），每个阶段都有一个或多个工作。

> 注意：在GitLab [pipeline图](https://docs.gitlab.com/ee/ci/pipelines.html#pipeline-graphs)上显示时，应当大写显示stats的名称。

![](https://docs.gitlab.com/ee/ci/img/pipelines.png)

### 管道类型

管道分三种，但是通常都使用单一的“管道”来代替所有。人们经常谈论他们，就好像每个都是“管道”一样，但实际上，他们只是综合管道的一部分。 

![](https://docs.gitlab.com/ee/ci/img/types-of-pipelines.svg)

1. **CI Pipeline：** 在`gitlab-ci.yml`中定义的构建和测试阶段。

2. **Deploy Pipeline：** 在`.gitlab-ci.yml`中定义的部署阶段，用来通过各种各样的方式将代码部署到服务器：

   例如，将代码发布到生成环境

3. **Project Pipeline**：[通过API触发](https://docs.gitlab.com/ee/ci/triggers/README.html#ci-job-token)跨项目CI依赖关系，尤其是针对微服务，但也适用于复杂的构建依赖关系：

   例如，api-> front-end，ce / ee-> omnibus。

## 开发工作流程

管道适应多种开发工作流程：

1. **Branch Flow**（例如，dev，qa，分期，生产等不同分支）
2. **Trunk-based Flow** （例如，功能分支、单一的主分支和可能带有标签的发布）
3. **基于分叉的流程**（例如，来自fork的合并请求）

连续交付流程示例：

![](https://docs.gitlab.com/ee/ci/img/pipelines-goal.svg)

### 工作

工作可以在[`.gitlab-ci.yml`](https://docs.gitlab.com/ee/ci/yaml/README.html#jobs)文件中定义。不要与`build`工作或`build` 阶段混淆。

## 定义管道 

在`.gitlab-ci.yml`中通过指定[阶段](https://docs.gitlab.com/ee/ci/yaml/README.html#stages)运行的[作业](https://docs.gitlab.com/ee/ci/pipelines.html#jobs)来定义管道。

有关[作业](https://docs.gitlab.com/ee/ci/yaml/README.html#jobs)，请参阅参考[文档](https://docs.gitlab.com/ee/ci/yaml/README.html#jobs)。

## 查看管道状态

您可以在项目的 **Pipeline**选项卡下找到当前和历史运行的管道 。点击管道将显示为该管道运行的作业。 

![](https://docs.gitlab.com/ee/ci/img/pipelines_index.png)

## 查看工作状态 

当您访问单个管道时，您可以看到该管道的相关作业。点击单个作业会显示该作业运行历史，并允许您取消作业，重试作业或清除作业运行日志。

[![管道示例](https://docs.gitlab.com/ee/ci/img/pipelines.png)](https://docs.gitlab.com/ee/ci/img/pipelines.png)

## 查看工作失败的原因 

> 在GitLab 10.7中[引入](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/17782)。 

当管道发生故障或允许失败时，有几个地方可以快速检查失败的原因：

- **在管道图中** 出现在管道图中。
- **在管道小部件中** 出现在合并请求和提交页面中。
- **在工作视图中 **出现在全局和详细的工作视图中。

无论任何方式中，你将鼠标悬停在失败的作业上，你可以看到失败的原因。

[![管道细节](https://docs.gitlab.com/ee/ci/img/job_failure_reason.png)](https://docs.gitlab.com/ee/ci/img/job_failure_reason.png)

从[GitLab 10.8中](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/17814)，您还可以在工作详情页面上看到失败的原因。

## 管道图 

> 在GitLab 8.11中[引入](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5742)。

管道可以是复杂的结构，具有许多顺序和平行的作业。为了让您更容易看到发生了什么，它可以查看单个管道及其状态。

管道图可以通过两种不同的方式显示，具体取决于您所处的页面。

------

当您在[单个管道页面](https://docs.gitlab.com/ee/ci/pipelines.html#seeing-pipeline-status)上时，可以找到显示每个阶段作业名称的常规管道图。

[![管道示例](https://docs.gitlab.com/ee/ci/img/pipelines.png)](https://docs.gitlab.com/ee/ci/img/pipelines.png)

其次，有管道迷你图，占用更少的空间，并且可以快速浏览所有作业是成果还是失败。管道迷你图可以在您访问以下页面时找到：

- 管道索引页面
- 提交页面
- 合并请求页面

通过这种方式，您可以看到所有相关的作业以及每个阶段的最终结果。这使您可以快速查看失败的工作并修复它。管道迷你图的阶段是可折叠的。将鼠标悬停在它们上面，然后单击以展开其他作业。

| **迷你图**                                                   | **迷你图展开**                                               |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [![管道迷你图](https://docs.gitlab.com/ee/ci/img/pipelines_mini_graph_simple.png)](https://docs.gitlab.com/ee/ci/img/pipelines_mini_graph_simple.png) | [![管道迷你图扩展](https://docs.gitlab.com/ee/ci/img/pipelines_mini_graph.png)](https://docs.gitlab.com/ee/ci/img/pipelines_mini_graph.png) |

### 将相似的工作分组 

> 在GitLab 8.12中[引入](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6242)。

如果你有许多类似的工作，你的管道图会变得很长，很难阅读。出于这个原因，类似的工作可以自动组合在一起。如果作业名称以某种格式命名，则它们将在常规管线图（非迷你图）中折叠为一个组。如果您没有看到重试或取消按钮，您就知道管道将作业已经合并分组了。将鼠标悬停在上面会显示分组作业的数量。可以点击展开它们。

[![分组管道](https://docs.gitlab.com/ee/ci/img/pipelines_grouped.png)](https://docs.gitlab.com/ee/ci/img/pipelines_grouped.png)

基本要求是需使用以下方式的一种将两个数字分隔开（可以互换使用）（查看下面的示例）：

- 空间
- 斜线（`/`）
- 冒号（`:`）

> **注意：** 更准确地说，[它使用](https://gitlab.com/gitlab-org/gitlab-ce/blob/2f3dc314f42dbd79813e6251792853bc231e69dd/app/models/commit_status.rb#L99)这个正则表达式：`\d+[\s:\/\\]+\d+\s*`。

这些工作将通过从左到右比较这两个数字来进行排序。通常第一个是索引，第二个是总数。

例如，以下作业将被分组在一个名为的作业下`test`：

- `test 0 3` => `test`
- `test 1 3` => `test`
- `test 2 3` => `test`

以下作业将被分组在下列作业中`test ruby`：

- `test 1:2 ruby` => `test ruby`
- `test 2:2 ruby` => `test ruby`

下列作业也将被归类在一个作业中`test ruby`：

- `1/3 test ruby` => `test ruby`
- `2/3 test ruby` => `test ruby`
- `3/3 test ruby` => `test ruby`

### 手动操作

> 在GitLab 8.15中[引入](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7931)。

[手动操作](https://docs.gitlab.com/ee/ci/yaml/README.html#manual)允许您在使用CI中的指定作业之前需要手动操作。整个管道可以自动运行，但实际[部署到生产](https://docs.gitlab.com/ee/ci/environments.html#manually-deploying-to-environments)需要点击。

您可以直接从管道图中做到这一点。只需点击播放按钮即可执行指定作业。例如，在下面的图片中，`production` 舞台上有一项手动操作。

[![管道示例](https://docs.gitlab.com/ee/ci/img/pipelines.png)](https://docs.gitlab.com/ee/ci/img/pipelines.png)

### 作业排序 

**常规管道图**

在单个管道页面中，作业按名称排序。

**迷你管道图**

> 在GitLab 9.0中[引入](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/9760)。

在管道迷你图中，作业首先按重要性排序，然后按名称排序。重要性的顺序是：

- 失败
- 警告
- 有待
- 赛跑
- 手册
- 取消
- 成功
- 跳过
- 创建

[![管道迷你图排序](https://docs.gitlab.com/ee/ci/img/pipelines_mini_graph_sorting.png)](https://docs.gitlab.com/ee/ci/img/pipelines_mini_graph_sorting.png)

### 多项目管道图

> 可在GitLab Premium 、GitLab Sliver或更高级版本中使用。

[多项目管道](https://docs.gitlab.com/ee/ci/multi_project_pipelines.html)，您可以访问跨项目管道。

## 如何计算管道持续时间 

管道的总运行时间将排除重试和待处理（排队）时间。我们可以将这个问题缩减为寻找周期的联合。

所以每个工作都会被表示为 `Period`，其中包括 `Period#first`工作开始`Period#last`时和工作完成时。一个简单的例子是：

- A（1,3）
- B（2,4）
- C（6,7）

这里A从1开始，到3结束。B从2开始，并到4结束。C从6开始，到7结束。视觉上它可以被看作：

```
0  1  2  3  4  5  6  7
   AAAAAAA
      BBBBBBB
                  CCCC
```

A，B和C的联合将是（1,4）和（6,7），因此总运行时间应该是：

```
(4 - 1) + (7 - 6) => 4
```

## 徽章 

管道状态和测试范围内报告徽章可用。您可以在[管道设置](https://docs.gitlab.com/ee/user/project/pipelines/settings.html)页面找到它们各自的链接。

## 受保护分行的安全 

管道在[受保护的分支](https://docs.gitlab.com/ee/user/project/protected_branches.html)上执行时，将执行严格的安全模型 。

只有在[允许](https://docs.gitlab.com/ee/user/project/protected_branches.html#using-the-allowed-to-merge-and-allowed-to-push-settings)用户[合并或推送](https://docs.gitlab.com/ee/user/project/protected_branches.html#using-the-allowed-to-merge-and-allowed-to-push-settings) 特定分支时，才允许在受保护的分支上执行以下操作 ：

- 运行**手动管道**（使用Web UI或Pipelines API）
- 运行**预定的管道**
- 使用**触发器**运行管道
- 在现有管线上触发**手动操作**
- **重试/取消**现有作业（使用Web UI或Pipelines API）

标记为**受保护的变量**仅适用于在受保护分支上运行的作业，从而避免不受信任的用户无意中访问敏感信息，如部署凭证和令牌。

标记为**受保护的Runners**只能保护分支机构运行的作业，避免不受信任的代码要在保护runner和保存部署键被意外地触发或其他凭证执行。为了确保打算在受保护的跑步者上执行的工作不会使用常规runner，必须对其进行相应标记。

[帮助改进此翻译](https://github.com/Fennay/gitlab-ci-cn/blob/master/pipelines.md)

