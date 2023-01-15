## Git Flow
两种不同 git 工作流
- [GitHub flow - GitHub Docs](https://docs.github.com/en/get-started/quickstart/github-flow)






## 丢弃本地变更
```sh
git clean -di {{path}}
```
其中 `i` 是进入交互模式，git 会询问是否删除所有没有被跟踪的文件
[Git - git-clean Documentation (git-scm.com)](https://git-scm.com/docs/git-clean)

## 恢复工作树文件
如果想要丢弃已经被跟踪文件的变更，使用 
```sh
git restore {{path}}
```
[Git - git-restore Documentation (git-scm.com)](https://git-scm.com/docs/git-restore)