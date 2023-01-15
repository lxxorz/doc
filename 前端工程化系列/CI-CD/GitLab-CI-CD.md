# GitLab CI/CD
GitLab CI/CD 是一个使用持续方法论进行软件开发的工具
-  持续集成 [Continuous Integration (CI)](https://docs.gitlab.com/ee/ci/introduction/index.html#continuous-integration)
-  持续交付 [Continuous Delivery (CD)](https://docs.gitlab.com/ee/ci/introduction/index.html#continuous-delivery)
-  持续开发 [Continuous Deployment (CD)](https://docs.gitlab.com/ee/ci/introduction/index.html#continuous-deployment)

## GitLab CI/CD 的目的
为了在开发的早期捕获到项目的 bug 和错误，确保所有部署到生产环境的代码都使用**我们制定的代码标准**

![[gitlab-cicd-structure.png]]


## 创建第一个 pipeline

先决条件
1. 安装 GitLab
2. 安装 GitLab Runner 服务
3. 在 GitLab Runner 中注册 Runner
GitLab Runner 是运行 CICD 的代理，通过 Runner 来运行 CICD 的任务
```ad-note
推荐使用 docker 安装

如果使用wsl2，注意在注册runner时，使用`--net=host`选项使用宿主机的网络
```


