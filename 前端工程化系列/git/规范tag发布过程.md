# 规范 tag 发布过程

## 目的
- 规范 tag 的版本，避免人为 tag 出错
- 关联系统的版本，每次发布一个新的版本的时候，自动更新所有 ` package.json ` 的 version


## 如何使用
1. `pnpm run release`，构建文件
2. `pnpm run tag`，自动将构建出来的文件生成一个 commit，和版本 tag，最后推送到远端仓库
![[tag-version.png]]
如果是特殊版本，则选择自定义，如果输入输入的版本不符合规范比如 `eh_v4.12.xy` 则会报错

3. 确认发布
![[tag-confirm.png]]

确认发布之后
![[tag-all.png]]
![[tag-update-version 1.png]]
![[tag-file.png]]
- 会自动更新所有 `package.json` 中的版本号，以及根据 commit 生成对应的 changelog
- 生成对应版本的 tag
![[media/tag/tag-update-version.png]]
- `git add -A` 跟踪所有变更 (changes)
- 推送 tag 到远程分支
- 提交一个"release"的commit推送所有变更到远程分支


## 使用限制
- 因为该脚本依赖一些外部包，所有需要 `pnpm install`  之后使用，因此如果服务器没法 ` pnpm install` 则无法使用，如果有需要在服务器上打 tag，只能手动 tag
