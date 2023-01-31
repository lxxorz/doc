# CICD 入门
![[gitlab-持续集成.png]]
## 安装 GitLab
```sh
# 声明一个具名数据卷
export GITLAB_HOME=/srv/gitlab
 sudo docker run --detach \
  --hostname localhost \
  --publish 443:443 --publish 8889:8889 --publish 22:22 \
  --name gitlab \
  --restart always \
  --volume $GITLAB_HOME/config:/etc/gitlab:Z \
  --volume $GITLAB_HOME/logs:/var/log/gitlab:Z \
  --volume $GITLAB_HOME/data:/var/opt/gitlab:Z \
  --shm-size 256m \
  gitlab/gitlab-ce:latest
```
## 运行器 (runner)
1. 安装运行器
```sh
# 定义一个匿名数据卷 
docker volume create gitlab-runner-config
# 安装runner，注意`--net=host`这个配置
docker run -d --name gitlab-runner --restart always \
    -v /var/run/docker.sock:/var/run/docker.sock \
    -v gitlab-runner-config:/etc/gitlab-runner \
    --net=host gitlab/gitlab-runner:latest

```
## 注册一个运行器
```
# 给项目注册一个runner
docker run --net=host --rm -it -v gitlab-runner-config:/etc/gitlab-runner gitlab/gitlab-runner:latest register   
```

```ad-note
如果使用docker安装了runner，执行器再次选择使用docker，就会导致无法pull项目代码
```

## `gitlab-ci.yml ` 文件编写
## 问题
1. 执行器选择 docker 无法 pull 项目代码而且准备 executor 太慢
![[trouble-0.png]]