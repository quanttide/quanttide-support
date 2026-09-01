# Agent Instructions

## 理解：这个领域是什么

**量潮客户支持领域。一等实体是「问题 → 解决方案」，不是工单。**

- 工单只是对话容器，关单即终点，知识死在关闭的工单里——这是传统形态，不是本域的形态。
- 核心循环：AI 用已积累资产应答 → 答不了升级人工 → 人的解决被蒸馏回资产库 → 资产变厚，同类问题下次直接被答掉。建的是这个循环，不是客服入口。
- 四类资产（按优先级）：解决方案库（核心）→ 蒸馏规则（诊断树/路由/升级判据/支持智能体）→ 需求与缺陷信号（喂给需求地图）→ 原始交互档案（永不丢弃）。
- 平台风格对齐：决议之于 delib = 解决方案之于 support；蒸馏隐式经验的范式来自 agent 云，这里是用在客户边界上。
- 好坏标准不看关单数，看**无需人参与的比例**和**复用率**。

### 领域边界

- 客户档案（客户知识本身）归 `quanttide-customer` 域，本域是写入者之一，不另起炉灶。
- 给客户的知识（FAQ/教程/案例）落本域 `docs/`（tutorial/gallery/handbook）。
- 不清楚内容归属时，先问"这是支持过程沉淀的资产，还是客户的事实档案"。

### 结构

- 本仓库：领域骨架（1 主 + 20 子），`apps/qtcloud-support` 是可部署应用，`data/`×11 与 `docs/`×6 是资产位。
- 应用侧的开发原则见 `apps/qtcloud-support/docs/dev-guide/`，用户视角见 `docs/user-guide/`。

## 工程纪律

### 提交规则

1. **每次 commit 以后自动 push**（本仓库与所有子仓库一视同仁）。
2. **分层提交**：子仓库内 commit + push → 回本仓库 `git add <子模块路径>` 更新指针 + commit + push → 根仓库（`repos/quanttide`）同法更新。三层都推完才算完成。
3. 提交信息用 Conventional Commits（`feat`/`fix`/`docs`/`chore`）。

### 子模块纪律

1. 子仓库操作前先 `git checkout main && git pull`——子模块常处于分离头指针。
2. **分离头提交陷阱**：若 commit 落在游离提交上，修复：`git checkout main && git merge --ff-only <sha> && git push`。
3. 信任 `.gitmodules`，不信任 README——README 的路径表可能滞后。
4. 验证以远端为准：推送后用 `gh api repos/quanttide/<repo>/branches/main --jq .commit.sha` 对账本地 HEAD。

### 越界禁令

1. 不在子仓库里做本仓库的事（如改本 AGENTS.md、改 README 子模块表），反之亦然。
2. 不动其他域的仓库；跨域内容移动先提方案，用户拍板后执行。
3. 占位是声明：`apps/`、`src/` 等预留目录不因"看起来空"而删除。
