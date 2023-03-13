# 代码质量检测工具-SonarCube 安装与使用
## 简介
SonarQube 是一个代码质量检测工具，通过分析代码来评估代码的质量，SonarQube 有四个版本，其中社区版本是免费的，SonarQube 的整体架构如下 
![[SonarQube.png]]
###   使用 docker 安装 SonarQube
安装数据库 (PostgreSql)
```zsh
docker pull PostgresSql
docker run -d \
	--name postgres \
	-e POSTGRES_PASSWORD=Forthink2019 \
	-e PGDATA=/var/lib/postgresql/data/pgdata \
	-v /custom/mount:/var/lib/postgresql/data \
	postgres
```
创建匿名数据卷
```sh
docker volume create --name sonarqube_data
docker volume create --name sonarqube_logs
docker volume create --name sonarqube_extensions
```
安装 SonarQube
```sh
sudo docker run --name sonarqube --link postgres  -e SONARQUBE_JDBC_URL=jdbc:postgresql://db:5432/sonar \
-e \
SONARQUBE_JDBC_USERNAME=sonar -e \
SONARQUBE_JDBC_PASSWORD=Forthink2019 \
-p 9000:9000 \
-v sonarqube_data:/opt/sonarqube/data \
-v sonarqube_extensions:/opt/sonarqube/extensions \
-v sonarqube_logs:/opt/sonarqube/logs \
-d sonarqube:9-community
```
如果为了方便而使用内置数据库，使用以下命令安装
```sh
docker run -d --restart=always --name sonarqube \
    -p 9000:9000 \
    -v sonarqube_data:/opt/sonarqube/data \
    -v sonarqube_extensions:/opt/sonarqube/extensions \
    -v sonarqube_logs:/opt/sonarqube/logs \
    sonarqube:9.9.0-community
```
（2）登录
登录 `http://localhost:9000`，默认账号密码是 admin/admin

 (3) 创建新项目
 ![[Pasted image 20230203102139.png]]
然后配置项目
![[Pasted image 20230203102204.png]]
然后添加一个 token
![[Pasted image 20230203102442.png]]
token 是为了验证 sonar-scanner 时使用的
![[Pasted image 20230203102539.png]]
选择对应的平台和语言，按照指示安装运行 Scanner
![[Pasted image 20230203102700.png]]
这里使用 docker 运行 scanner
```zsh
 docker run --network=host \
    --rm \
    -e SONAR_HOST_URL="http://localhost:9000" \
    -e SONAR_SCANNER_OPTS="-Dsonar.projectKey=fk" \
    -e SONAR_LOGIN="sqp_27e3815b25d8d14d24813342dbad958e25cb411e" \
    -v "/home/bjorn/dev/generalsystemfe:/usr/src" \
    sonarsource/sonar-scanner-cli
```
## 查看分析结果
扫描分析完成源代码之后，SonarQube 上可以看待扫描结果。SonarQube 会提供一些代码的建议供开发者来提高代码的质量。
![[Pasted image 20230203104125.png]]

### 衡量指标
除了提供编写代码的建议，还可以通过一些指标衡量代码的总体质量。

## 问题
### 分析源代码耗费时间长
每运行一次分析器大概需要 2~4 分钟
![[Pasted image 20230203105459.png]]
### 不支持某些 Vue 的特殊语法
Vue 的一些语法 SonarQube 暂时没法识别，比如**深度选择器**。不过可以通过配置一些规则的参数来避免。
1. SonarQube 内置的规则没法更改，需要新建一个规则
![[Pasted image 20230203095348.png]]
2. 然后在 Rules -> Quality Profile 选择刚才新建的规则
![[Pasted image 20230203095520.png]]
3. 搜索我们需要修改的规则
![[Pasted image 20230203095610.png]]

4. 点击 change 按钮
![[Pasted image 20230203095647.png]]
5. 然后传递规则参数
![[Pasted image 20230203095714.png]]
### 排除生产环境的代码
项目顶层目录下新建配置文件
```properties
# Define separate root directories for sources and tests
sonar.inclusions = packages/**/src/**/*
sonar.tests.inclusions = packages/**/tests/**/*
```

和 CI 集成
1. 在 GitLab 生成一个 oauth2 的 Application 应用，在 SonarQube 的 administration->authentication->GItlab 中设置好 Application ID，和Secret
2. 创建项目，然后从 gitlab 中获取 personal access token 填入 sonarqube 作为凭证。

## 规则扩展

SonarQube 本身不可以自定义规则，不过可以通过 Eslint 来实现  https://github.com/SonarSource/eslint-plugin-sonarjs


### 社区版本只能对主分支进行分析
SonarQube 的社区版本只能对主分支进行分析，不支持分析多分支


### 注意系统设置
SonarQube 本身使用 Elasticsearch 搜索引擎参考文档 [Prerequisites and overview (sonarqube.org)](https://docs.sonarqube.org/latest/requirements/prerequisites-and-overview/)