[TOC]

# Variables

当GitLab CI 中接受到一个job后，[Runner](https://docs.gitlab.com/runner/)就开始准备构建环境。开始设置预定义的变量(环境变量)和用户自定义的变量。

## variables 的执行顺序

变量可以被重写，并且是按照下面的顺序进行执行：

1. [Trigger variables](https://docs.gitlab.com/ce/ci/triggers/README.html#pass-job-variables-to-a-trigger)(优先级最高)
2. [Secret variables](https://docs.gitlab.com/ce/ci/variables/README.html#secret-variables)
3. YAML-defined [job-level variables](https://docs.gitlab.com/ce/ci/yaml/README.html#job-variables)
4. YAML-defined [global variables](https://docs.gitlab.com/ce/ci/yaml/README.html#variables)
5. [Deployment variables](https://docs.gitlab.com/ce/ci/variables/README.html#deployment-variables)
6. [Predefined variables](https://docs.gitlab.com/ce/ci/variables/README.html#predefined-variables-environment-variables) (优先级最低)

举个例子，如果你定义了私有变量`API_TOKEN=secure`，并且在`.gitlab-ci.yml`中定义了 `  API_TOKEN=yaml`，那么私有变量`API_TOKEN`的值将是`secure`，因为secret variables的优先级较高。

## Predefined  variables(Environment variables)

有部分预定义的环境变量仅仅只能在最小版本的[GitLab Runner](https://docs.gitlab.com/runner/)中使用。请参考下表查看对应的Runner版本要求。

> **注意**：从GitLab 9.0 开始，部分变量已经不提倡使用。请查看[9.0 Renaming](https://docs.gitlab.com/ce/ci/variables/README.html#9-0-renaming)部分来查找他们的替代变量。强烈建议使用新的变量，我们也会在将来的GitLab版本中将他们移除。

| Variable                | GitLab | Runner | Description                              |
| :---------------------- | ------ | ------ | ---------------------------------------- |
| **CI**                  | all    | 0.4    | 标识该job是在CI环境中执行                          |
| **CI_COMMIT_REF_NAME**  | 9.0    | all    | 用于构建项目的分支或tag名称                          |
| **CI_COMMIT_REF_SLUG**  | 9.0    | all    | 先将`$CI_COMMIT_REF_NAME`的值转换成小写，最大不能超过63个字节，然后把除了`0-9`和`a-z`的其他字符转换成`-`。在URLs和域名名称中使用。 |
| **CI_COMMIT_SHA**       | 9.0    | all    | commit的版本号                               |
| **CI_COMMIT_TAG**       | 9.0    | 0.5    | commit的tag名称。只有创建了tags才会出现。              |
| **CI_DEBUG_TRACE**      | 9.0    | 1.7    | [debug tracing](https://docs.gitlab.com/ce/ci/variables/README.html#debug-tracing)开启时才生效 |
| **CI_ENVIRONMENT_NAME** | 8.15   | all    | job的环境名称                                 |
| **CI_ENVIRONMENT_SLUG** | 8.15   | all    | 环境名称的简化版本，适用于DNS，URLs，Kubernetes labels等 |
| **CI_JOB_ID**           | 9.0    | all    | GItLab CI内部调用job的一个唯一ID                  |
| **CI_JOB_MANUAL**       | 8.12   | all    | 表示job启用的标识                               |
| **CI_JOB_NAME**         |        |        |                                          |
|                         |        |        |                                          |









## 9.0 Renaming

## `.gitlab-ci.yaml` defined variables

## Secret variables

## Deploment variables

## Debug tracing

## Using the CI variables in your job scripts



