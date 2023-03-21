# Variables

官方文档：https://docs.gitlab.com/ce/ci/variables/README.html

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

| Variable                       | GitLab | Runner | Description                              |
| :----------------------------- | ------ | ------ | ---------------------------------------- |
| **CI**                         | all    | 0.4    | 标识该job是在CI环境中执行                          |
| **CI_COMMIT_REF_NAME**         | 9.0    | all    | 用于构建项目的分支或tag名称                          |
| **CI_COMMIT_REF_SLUG**         | 9.0    | all    | 先将`$CI_COMMIT_REF_NAME`的值转换成小写，最大不能超过63个字节，然后把除了`0-9`和`a-z`的其他字符转换成`-`。在URLs和域名名称中使用。 |
| **CI_COMMIT_SHA**              | 9.0    | all    | commit的版本号                               |
| **CI_COMMIT_TAG**              | 9.0    | 0.5    | commit的tag名称。只有创建了tags才会出现。              |
| **CI_DEBUG_TRACE**             | 9.0    | 1.7    | [debug tracing](https://docs.gitlab.com/ce/ci/variables/README.html#debug-tracing)开启时才生效 |
| **CI_ENVIRONMENT_NAME**        | 8.15   | all    | job的环境名称                                 |
| **CI_ENVIRONMENT_SLUG**        | 8.15   | all    | 环境名称的简化版本，适用于DNS，URLs，Kubernetes labels等 |
| **CI_JOB_ID**                  | 9.0    | all    | GItLab CI内部调用job的一个唯一ID                  |
| **CI_JOB_MANUAL**              | 8.12   | all    | 表示job启用的标识                               |
| **CI_JOB_NAME**                | 9.0    | 0.5    | `.gitlab-ci.yml`中定义的job的名称               |
| **CI_JOB_STAGE**               | 9.0    | 0.5    | `.gitlab-ci.yml`中定义的stage的名称             |
| **CI_JOB_TOKEN**               | 9.0    | 1.2    | 用于同GitLab容器仓库验证的token                    |
| **CI_REPOSITORY_URL**          | 9.0    | all    | git仓库地址，用于克隆                             |
| **CI_RUNNER_DESCRIPTION**      | 8.10   | 0.5    | GitLab中存储的Runner描述                       |
| **CI_RUNNER_ID**               | 8.10   | 0.5    | Runner所使用的唯一ID                           |
| **CI_RUNNER_TAGS**             | 8.10   | 0.5    | Runner定义的tags                            |
| **CI_PIPELINE_ID**             | 8.10   | 0.5    | GitLab CI 在内部使用的当前pipeline的唯一ID          |
| **CI_PIPELINE_TRIGGERED**      | all    | all    | 用于指示该job被触发的标识                           |
| **CI_PROJECT_DIR**             | all    | all    | 仓库克隆的完整地址和job允许的完整地址                     |
| **CI_PROJECT_ID**              | all    | all    | GitLab CI在内部使用的当前项目的唯一ID                 |
| **CI_PROJECT_NAME**            | 8.10   | 0.5    | 当前正在构建的项目名称（事实上是项目文件夹名称）                 |
| **CI_PROJECT_NAMESPACE**       | 8.10   | 0.5    | 当前正在构建的项目命名空间（用户名或者是组名称）                 |
| **CI_PROJECT_PATH**            | 8.10   | 0.5    | 命名空间加项目名称                                |
| **CI_PROJECT_PATH_SLUG**       | 9.3    | all    | `$CI_PROJECT_PATH`小写字母、除了`0-9`和`a-z`的其他字母都替换成`-`。用于地址和域名名称。 |
| **CI_PROJECT_URL**             | 8.10   | 0.5    | 项目的访问地址（http形式）                          |
| **CI_REGISTRY**                | 8.10   | 0.5    | 如果启用了Container Registry，则返回GitLab的Container Registry的地址 |
| **CI_REGISTRY_IMAGE**          | 8.10   | 0.5    | 如果为项目启用了Container Registry，它将返回与特定项目相关联的注册表的地址 |
| **CI_REGISTRY_PASSWORD**       | 9.0    | all    | 用于push containers到GitLab的Container Registry的密码 |
| **CI_REGISTRY_USER**           | 9.0    | all    | 用于push containers到GItLab的Container Registry的用户名 |
| **CI_SERVER**                  | all    | all    | 标记该job是在CI环境中执行                          |
| **CI_SERVER_NAME**             | all    | all    | 用于协调job的CI服务器名称                          |
| **CI_SERVER_REVISION**         | all    | all    | 用于调度job的GitLab修订版                        |
| **CI_SERVER_VERSION**          | all    | all    | 用于调度job的GItLab版本                         |
| **ARTIFACT_DOWNLOAD_ATTEMPTS** | 8.15   | 1.9    | 尝试运行下载artifacts的job的次数                   |
| **GET_SOURCES_ATTEMPTS**       | 8.15   | 1.9    | 尝试运行获取源的job次数                            |
| **GITLAB_CI**                  | all    | all    | 用于指示该job是在GItLab CI环境中运行                 |
| **GITLAB_USER_ID**             | 8.12   | all    | 开启该job的用户ID                              |
| **GITLAB_USER_EMAIL**          | 8.12   | all    | 开启该job的用户邮箱                              |
| **RESTORE_CACHE_ATTEMPTS**     | 8.15   | 1.9    | 尝试运行存储缓存的job的次数                          |

## 9.0 Renaming

根据GitLab的命名规则，在9.0以后将从`build`术语转到`job`CI变量中，并且已经被重命名。

| 8.x name             | 9.0+ name               |
| -------------------- | ----------------------- |
| `CI_BUILD_ID`        | `CI_JOB_ID`             |
| `CI_BUILD_REF`       | `CI_COMMIT_SHA`         |
| `CI_BUILD_TAG`       | `CI_COMMIT_TAG`         |
| `CI_BUILD_REF_NAME`  | `CI_COMMIT_REF_NAME`    |
| `CI_BUILD_REF_SLUG`  | `CI_COMMIT_REF_SLUG`    |
| `CI_BUILD_NAME`      | `CI_JOB_NAME`           |
| `CI_BUILD_STAGE`     | `CI_JOB_STAGE`          |
| `CI_BUILD_REPO`      | `CI_REPOSITORY_URL`     |
| `CI_BUILD_TRIGGERED` | `CI_PIPELINE_TRIGGERED` |
| `CI_BUILD_MANUAL`    | `CI_JOB_MANUAL`         |
| `CI_BUILD_TOKEN`     | `CI_JOB_TOKEN`          |

## `.gitlab-ci.yaml` defined variables

> 注意：此功能要求GitLab Runner 0.5或者更高版本，并且GitLab CI 7.14或者更高版本

GitLab CI允许你向`.gitlab-ci.yml`中添加变量，这个变量在构建环境中设置。因此，变量将保存在存储中，他们用于存储非敏感的项目配置，例如：`RAILS_ENV`或者`DATABASE_URL`。

举个例子，如果将变量设置为全局以下（不是在一个作业中），则它将用于所有执行的命令脚本中：

```yaml
variables:
  DATABASE_URL: "postgres://postgres@postgres/my_database"
```

YAML中定义的变量也将应用到所有创建的服务容器中，因此可以对它进行微调。

变量可以定义为全局，同时也可以定义为job级别。若要关闭作业中的全局定义变量，请定义一个空hash：

```yaml
job_name:
  variables: {}
```

您可以在变量定义中使用其他变量（或使用$$将其转义）：

```yaml
variables:
  LS_CMD: 'ls $FLAGS $$TMP_DIR'
  FLAGS: '-al'
script:
  - 'eval $LS_CMD'  # will execute 'ls -al $TMP_DIR'
```

## Secret variables

> 注意：
>
> - 这个功能需要GitLab Runner 0.4.0或者更高版本。
> - 请注意，私有变量不会隐藏，如果明确要这么做，他们的值可以显示在job日志中。如果您的项目是公共的或内部的，你可以在项目的pipeline中设置pipeline为私有的。关于私有变量的讨论在issue [#13784](https://gitlab.com/gitlab-org/gitlab-ce/issues/13784)。

GitLab CI允许你在构建环境过程中设置项目的私有变量。私有变量存储在仓库(.gitlab-ci.yml)中，并被安全的传递给GitLab Runner，使其在构建环境中可用。建议使用该方法存储诸如密码、秘钥和凭据之类的东西。

可用通过**Settings ➔ Pipelines**来增加私有变量，通过**Settings ➔ Pipelines**找到的模块称之为私有变量。

一次设置，所有的后续pipeline是都可以使用它们。

## Protected secret variables

> 注意：此功能要求GitLab 9.3或者更高。

私有变量可以被保护。每当一个私有变量被保护时，它只会安全的传递到在[受保护的分支](https://docs.gitlab.com/ce/user/project/protected_branches.html)或[受保护的标签](https://docs.gitlab.com/ce/user/project/protected_tags.html)上运行的pipeline。其他的pipeline将不会得到受保护的变量。

可用通过**Settings ➔ Pipelines**来增加私有变量，通过**Settings ➔ Pipelines**找到的模块称之为私有变量，然后点击*Protected*。

一次设置，所有的后续pipeline是都可以使用它们。

## Deploment variables

> 注意：此功能要求GitLab CI 8.15或者更高版本。

负责部署配置的[项目服务](https://docs.gitlab.com/ce/user/project/integrations/project_services.html)可以定义在构建环境中设置自己的变量。这些变量只定义用于[部署job](https://docs.gitlab.com/ce/ci/environments.html)。请参考您正在使用的项目服务的文档，以了解他们定义的变量。

一个定义有部署变量的项目服务示例[Kubernetes Service](https://docs.gitlab.com/ce/user/project/integrations/kubernetes.html)。

## Debug tracing

> GitLab Runner 1.7开始引入。
>
> **警告**：启用调试跟踪可能会严重的安全隐患。输出内容将包含所有的私有变量和其他的隐私！输出的内容将被上传到GitLab服务器并且将会在job记录中明显体现。

默认情况下，GitLab Runner会隐藏了处理job时正在做的大部分细节。这种行为使job跟踪很短，并且防止秘密泄露到跟踪中，除非您的脚本将他们输出到屏幕中。

如果job没有按照预期的运行，这也会让问题查找变得更加困难；在这种情况下，你可以在`.gitlab-ci.yml`中开启调试记录。它需要GitLab Runner v1.7版本以上，此功能可启用shell的执行记录，从而产生详细的job记录，列出所有执行的命令，设置变量等。

在启用此功能之前，您应该确保job只对[团队成](https://docs.gitlab.com/ce/user/permissions.html#project-features)员可见。您也应该https://docs.gitlab.com/ce/ci/pipelines.html#seeing-build-status所有生成的job记录，然后使其可见。

设置`CI_DEBUG_TRACE`变量的值为`true`来开启调试记录。

```yaml
job_name:
  variables:
    CI_DEBUG_TRACE: "true"
```

调试记录设置为TRUE的截断输出示例：

```shell
...

export CI_SERVER_TLS_CA_FILE="/builds/gitlab-examples/ci-debug-trace.tmp/CI_SERVER_TLS_CA_FILE"
if [[ -d "/builds/gitlab-examples/ci-debug-trace/.git" ]]; then
  echo $'\''\x1b[32;1mFetching changes...\x1b[0;m'\''
  $'\''cd'\'' "/builds/gitlab-examples/ci-debug-trace"
  $'\''git'\'' "config" "fetch.recurseSubmodules" "false"
  $'\''rm'\'' "-f" ".git/index.lock"
  $'\''git'\'' "clean" "-ffdx"
  $'\''git'\'' "reset" "--hard"
  $'\''git'\'' "remote" "set-url" "origin" "https://gitlab-ci-token:xxxxxxxxxxxxxxxxxxxx@example.com/gitlab-examples/ci-debug-trace.git"
  $'\''git'\'' "fetch" "origin" "--prune" "+refs/heads/*:refs/remotes/origin/*" "+refs/tags/*:refs/tags/*"
else
  $'\''mkdir'\'' "-p" "/builds/gitlab-examples/ci-debug-trace.tmp/git-template"
  $'\''rm'\'' "-r" "-f" "/builds/gitlab-examples/ci-debug-trace"
  $'\''git'\'' "config" "-f" "/builds/gitlab-examples/ci-debug-trace.tmp/git-template/config" "fetch.recurseSubmodules" "false"
  echo $'\''\x1b[32;1mCloning repository...\x1b[0;m'\''
  $'\''git'\'' "clone" "--no-checkout" "https://gitlab-ci-token:xxxxxxxxxxxxxxxxxxxx@example.com/gitlab-examples/ci-debug-trace.git" "/builds/gitlab-examples/ci-debug-trace" "--template" "/builds/gitlab-examples/ci-debug-trace.tmp/git-template"
  $'\''cd'\'' "/builds/gitlab-examples/ci-debug-trace"
fi
echo $'\''\x1b[32;1mChecking out dd648b2e as master...\x1b[0;m'\''
$'\''git'\'' "checkout" "-f" "-q" "dd648b2e48ce6518303b0bb580b2ee32fadaf045"
'
+++ hostname
++ echo 'Running on runner-8a2f473d-project-1796893-concurrent-0 via runner-8a2f473d-machine-1480971377-317a7d0f-digital-ocean-4gb...'
Running on runner-8a2f473d-project-1796893-concurrent-0 via runner-8a2f473d-machine-1480971377-317a7d0f-digital-ocean-4gb...
++ export CI=true
++ CI=true
++ export CI_DEBUG_TRACE=false
++ CI_DEBUG_TRACE=false
++ export CI_COMMIT_SHA=dd648b2e48ce6518303b0bb580b2ee32fadaf045
++ CI_COMMIT_SHA=dd648b2e48ce6518303b0bb580b2ee32fadaf045
++ export CI_COMMIT_BEFORE_SHA=dd648b2e48ce6518303b0bb580b2ee32fadaf045
++ CI_COMMIT_BEFORE_SHA=dd648b2e48ce6518303b0bb580b2ee32fadaf045
++ export CI_COMMIT_REF_NAME=master
++ CI_COMMIT_REF_NAME=master
++ export CI_JOB_ID=7046507
++ CI_JOB_ID=7046507
++ export CI_REPOSITORY_URL=https://gitlab-ci-token:xxxxxxxxxxxxxxxxxxxx@example.com/gitlab-examples/ci-debug-trace.git
++ CI_REPOSITORY_URL=https://gitlab-ci-token:xxxxxxxxxxxxxxxxxxxx@example.com/gitlab-examples/ci-debug-trace.git
++ export CI_JOB_TOKEN=xxxxxxxxxxxxxxxxxxxx
++ CI_JOB_TOKEN=xxxxxxxxxxxxxxxxxxxx
++ export CI_PROJECT_ID=1796893
++ CI_PROJECT_ID=1796893
++ export CI_PROJECT_DIR=/builds/gitlab-examples/ci-debug-trace
++ CI_PROJECT_DIR=/builds/gitlab-examples/ci-debug-trace
++ export CI_SERVER=yes
++ CI_SERVER=yes
++ export 'CI_SERVER_NAME=GitLab CI'
++ CI_SERVER_NAME='GitLab CI'
++ export CI_SERVER_VERSION=
++ CI_SERVER_VERSION=
++ export CI_SERVER_REVISION=
++ CI_SERVER_REVISION=
++ export GITLAB_CI=true
++ GITLAB_CI=true
++ export CI=true
++ CI=true
++ export GITLAB_CI=true
++ GITLAB_CI=true
++ export CI_JOB_ID=7046507
++ CI_JOB_ID=7046507
++ export CI_JOB_TOKEN=xxxxxxxxxxxxxxxxxxxx
++ CI_JOB_TOKEN=xxxxxxxxxxxxxxxxxxxx
++ export CI_COMMIT_REF=dd648b2e48ce6518303b0bb580b2ee32fadaf045
++ CI_COMMIT_REF=dd648b2e48ce6518303b0bb580b2ee32fadaf045
++ export CI_COMMIT_BEFORE_SHA=dd648b2e48ce6518303b0bb580b2ee32fadaf045
++ CI_COMMIT_BEFORE_SHA=dd648b2e48ce6518303b0bb580b2ee32fadaf045
++ export CI_COMMIT_REF_NAME=master
++ CI_COMMIT_REF_NAME=master
++ export CI_COMMIT_NAME=debug_trace
++ CI_JOB_NAME=debug_trace
++ export CI_JOB_STAGE=test
++ CI_JOB_STAGE=test
++ export CI_SERVER_NAME=GitLab
++ CI_SERVER_NAME=GitLab
++ export CI_SERVER_VERSION=8.14.3-ee
++ CI_SERVER_VERSION=8.14.3-ee
++ export CI_SERVER_REVISION=82823
++ CI_SERVER_REVISION=82823
++ export CI_PROJECT_ID=17893
++ CI_PROJECT_ID=17893
++ export CI_PROJECT_NAME=ci-debug-trace
++ CI_PROJECT_NAME=ci-debug-trace
++ export CI_PROJECT_PATH=gitlab-examples/ci-debug-trace
++ CI_PROJECT_PATH=gitlab-examples/ci-debug-trace
++ export CI_PROJECT_NAMESPACE=gitlab-examples
++ CI_PROJECT_NAMESPACE=gitlab-examples
++ export CI_PROJECT_URL=https://example.com/gitlab-examples/ci-debug-trace
++ CI_PROJECT_URL=https://example.com/gitlab-examples/ci-debug-trace
++ export CI_PIPELINE_ID=52666
++ CI_PIPELINE_ID=52666
++ export CI_RUNNER_ID=1337
++ CI_RUNNER_ID=1337
++ export CI_RUNNER_DESCRIPTION=shared-runners-manager-1.example.com
++ CI_RUNNER_DESCRIPTION=shared-runners-manager-1.example.com
++ export 'CI_RUNNER_TAGS=shared, docker, linux, ruby, mysql, postgres, mongo'
++ CI_RUNNER_TAGS='shared, docker, linux, ruby, mysql, postgres, mongo'
++ export CI_REGISTRY=registry.example.com
++ CI_REGISTRY=registry.example.com
++ export CI_DEBUG_TRACE=true
++ CI_DEBUG_TRACE=true
++ export GITLAB_USER_ID=42
++ GITLAB_USER_ID=42
++ export GITLAB_USER_EMAIL=user@example.com
++ GITLAB_USER_EMAIL=user@example.com
++ export VERY_SECURE_VARIABLE=imaverysecurevariable
++ VERY_SECURE_VARIABLE=imaverysecurevariable
++ mkdir -p /builds/gitlab-examples/ci-debug-trace.tmp
++ echo -n '-----BEGIN CERTIFICATE-----
MIIFQzCCBCugAwIBAgIRAL/ElDjuf15xwja1ZnCocWAwDQYJKoZIhvcNAQELBQAw'
...
```

## Using the CI variables in your job scripts

在构建环境变量时，所有的变量都被设置为环境变量，他们可以使用普通方法访问这些变量。在大多数情况下，用于执行job脚本都是通过bash或者是sh。

想要访问环境变量，请示使用一下Runner对应的语法：

| Shell         | 用法              |
| ------------- | --------------- |
| bash/sh       | `$variable`     |
| windows batch | `%variable%`    |
| PowerShell    | `$env:variable` |

在bash中访问环境变量，需要给变量名称加上前缀(`$`)：

```yaml
job_name:
  script:
    - echo $CI_JOB_ID
```

在Windows系统的PowerShell中访问环境变量，需要给变量名称加上前缀(`$env:`)：

```yaml
job_name:
  script:
    - echo $env:CI_JOB_ID	
```

您可以使用`export`命令来列出所有的环境变量。在使用此命令时要注意，此命令也会在job记录中列出所有私有变量的值：

```yaml
job_name:
  script:
    - export
```

实例的值：

```shell
export CI_JOB_ID="50"
export CI_COMMIT_SHA="1ecfd275763eff1d6b4844ea3168962458c9f27a"
export CI_COMMIT_REF_NAME="master"
export CI_REPOSITORY_URL="https://gitlab-ci-token:abcde-1234ABCD5678ef@example.com/gitlab-org/gitlab-ce.git"
export CI_COMMIT_TAG="1.0.0"
export CI_JOB_NAME="spec:other"
export CI_JOB_STAGE="test"
export CI_JOB_MANUAL="true"
export CI_JOB_TRIGGERED="true"
export CI_JOB_TOKEN="abcde-1234ABCD5678ef"
export CI_PIPELINE_ID="1000"
export CI_PROJECT_ID="34"
export CI_PROJECT_DIR="/builds/gitlab-org/gitlab-ce"
export CI_PROJECT_NAME="gitlab-ce"
export CI_PROJECT_NAMESPACE="gitlab-org"
export CI_PROJECT_PATH="gitlab-org/gitlab-ce"
export CI_PROJECT_URL="https://example.com/gitlab-org/gitlab-ce"
export CI_REGISTRY="registry.example.com"
export CI_REGISTRY_IMAGE="registry.example.com/gitlab-org/gitlab-ce"
export CI_RUNNER_ID="10"
export CI_RUNNER_DESCRIPTION="my runner"
export CI_RUNNER_TAGS="docker, linux"
export CI_SERVER="yes"
export CI_SERVER_NAME="GitLab"
export CI_SERVER_REVISION="70606bf"
export CI_SERVER_VERSION="8.9.0"
export GITLAB_USER_ID="42"
export GITLAB_USER_EMAIL="user@example.com"
export CI_REGISTRY_USER="gitlab-ci-token"
export CI_REGISTRY_PASSWORD="longalfanumstring"
```