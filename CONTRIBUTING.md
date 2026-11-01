# CONTRIBUTING.md - 贡献指南

本文是客户支持领域仓的维护规范：工程纪律与提交流程。领域是什么、边界在哪见本文件 `AGENTS.md`。

## 提交规则

1. **每次 commit 以后自动 push**（本仓库与所有子仓库一视同仁）。
2. **分层提交**：子仓库内 commit + push → 回本仓库 `git add <子模块路径>` 更新指针 + commit + push → 根仓库（`repos/quanttide`）同法更新。三层都推完才算完成。
3. 提交信息用 Conventional Commits（`feat`/`fix`/`docs`/`chore`）。

## 子模块纪律

1. 子仓库操作前先 `git checkout main && git pull`——子模块常处于分离头指针。
2. **分离头提交陷阱**：若 commit 落在游离提交上，修复：`git checkout main && git merge --ff-only <sha> && git push`。
3. 信任 `.gitmodules`，不信任 README——README 的路径表可能滞后。
4. 验证以远端为准：推送后用 `gh api repos/quanttide/<repo>/branches/main --jq .commit.sha` 对账本地 HEAD。

## 人机协作

1. **最小干预**：仅在用户明确请求时操作。
2. **维护记录**：修改子模块内容后回本仓库同步更新指针；对用户可见的变更提醒同步 `CHANGELOG.md`。
3. **验证优先**：完成后运行构建/检查命令验证。
