# GitLab CI/CD
## 概述

CI/CD 是一种通过[自动化](https://www.redhat.com/zh/topics/cloud-native-apps/why-choose-red-hat-cloud-native?cicd=32h281b)来频繁向客户交付[应用](https://www.redhat.com/zh/topics/cloud-native-apps?percmp=7013a0000034e7YAAQ&cicd=32h281b)的方法。CI/CD 的核心概念是**持续集成、[持续交付](https://www.redhat.com/zh/topics/devops/what-is-continuous-delivery?cicd=32h281b)和持续部署**。作为一种面向开发和运维团队的解决方案，CI/CD 主要针对在[集成](https://www.redhat.com/zh/topics/integration?cicd=32h281b)新代码时所引发的问题。 ^1


%%具体而言，CI/CD 可让持续自动化和持续监控贯穿于[应用的整个生命周期](https://www.redhat.com/zh/topics/devops/what-is-application-lifecycle-management-alm?cicd=32h281b)（从集成和测试阶段，到交付和[部署](https://www.redhat.com/zh/topics/automation/what-is-deployment-automation?cicd=32h281b)）。这些关联的事务通常被统称为“[CI/CD 管道](https://www.redhat.com/zh/topics/devops/what-cicd-pipeline?cicd=32h281b)”，由开发和运维团队以敏捷方式协同支持，采用的方法不是 [DevOps](https://www.redhat.com/zh/topics/devops?cicd=32h281b) 就是[站点可靠性工程（SRE）](https://www.redhat.com/zh/topics/devops/what-is-sre?cicd=32h281b)。%%

## 持续集成
持续继承也就是我们常说的 CI，可以帮助开发人员更加频繁地（有时甚至每天）将代码更改合并到共享分支或“主干”中。一旦开发人员对应用所做的更改被合并，系统就会通过自动构建应用并运行不同级别的自动化测试（通常是单元测试和集成测试）来验证这些更改，确保这些更改没有对应用造成破坏 ^1
![[持续交付典型过程.png]]
上图是一个持续交付的典型过程，开发者提交代码变更，然后服务器执行**构建、测试、通知开发者结果**

对于目前我们的系统而言，CI 至少可以保证规范的构建项目，节省手动构建的步骤。所谓的规范就是我们不能省略某些验证代码的步骤，比如在项目中存在 `lint` 这个步骤，但是实际情况是，很少会在构建代码之前执行 lint。然后修复 lint 错误。



## GitLab CI/CD 的目的


![[gitlab-cicd-structure.png]]



## 参考
* \[1\] [什么是 CI/CD？ (redhat.com)](https://www.redhat.com/zh/topics/devops/what-is-ci-cd)
* \[2\] [持续改善-自动化软件测试](https://pepgotesting.com/)
