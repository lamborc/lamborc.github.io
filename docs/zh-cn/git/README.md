# Git


## Github fork project sync origin

  - git remote -v : check [origin:本地, upstream:远程]
  - git remote add upstream <原项目url>
  - git fetch upstream 将远程取到本地
  - git checkout master 检查本地变更
  - git merge upstream/master 合并分支



## Git Message 规范

- upd：更新某功能（不是 feat, 不是 fix）
- feat：新功能（feature）
- fix：修补bug
- docs：文档（documentation）
- style： 格式（不影响代码运行的变动）
- refactor：重构（即不是新增功能，也不是修改bug的代码变动）
- test：增加测试
- chore：构建过程或辅助工具的变动