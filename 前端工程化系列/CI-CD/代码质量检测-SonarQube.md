# 代码质量检测工具-SonarCube 安装与使用
## 简介
SonarQube 是一个代码质量检测工具，可以持续检查代码的质量和安全性

## 安装

SonarQube 有四个版本，其中社区版本是免费的，SonarQube 的整体架构如下
![[SonarQube.png]]

(1) 使用 docker 安装 SonarQube
创建匿名数据卷
```sh
docker volume create --name sonarqube_data
docker volume create --name sonarqube_logs
docker volume create --name sonarqube_extensions
```
安装
```sh
docker run -d --name sonarqube \
    -p 9000:9000 \
    -v sonarqube_data:/opt/sonarqube/data \
    -v sonarqube_extensions:/opt/sonarqube/extensions \
    -v sonarqube_logs:/opt/sonarqube/logs \
    sonarqube:8.9.10-community
    ```
（2）登录
默认账号密码是 admin/admin，第一次登录之后需要重新设置密码




## 问题
### 和 Vue 相关的问题
vue 的一些语法 SonarQube 暂时没法识别，可以自定义


### 不检测生产环境的代码
```
sonar.exclusions = "dist"
```

## 规则扩展

SonarQube 没有自定义规则的配置选项，前端项目可以通过配置 Eslint 来自定义规则 https://github.com/SonarSource/eslint-plugin-sonarjs