# 红楼梦维基知识库 实施计划

> **For agentic workers:** REQUIRED: Use superpowers:executing-plans to implement this plan. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** 将红学研究知识库改造为 LLM Wiki 模式，建立三层架构的知识维基系统

**Architecture:** 在 `memory/` 下创建独立的 `hongloumeng-wiki/` 目录，包含 raw/（原始文献）、页面子目录（人物/主题/章节/概念）、WIKI_SCHEMA.md（规范）、index.md（目录）、log.md（日志）

**Tech Stack:** Markdown 文件、文件系统和 Git

---

## 文件结构

```
memory/hongloumeng-wiki/           # 新建维基根目录
  raw/                             # 原始文献（不可修改）
  WIKI_SCHEMA.md                   # Schema 规范文档
  index.md                         # Wiki 目录
  log.md                           # 操作日志
  人物/                             # 人物页面
  主题/                             # 主题页面
  章节/                             # 章节页面
  概念/                             # 概念页面
```

---

## 阶段一：目录结构

- [ ] **Step 1: 创建维基根目录**

```bash
mkdir -p memory/hongloumeng-wiki/{人物,主题,章节,概念,raw}
```

验证: `ls -la memory/hongloumeng-wiki/`

- [ ] **Step 2: 创建 WIKI_SCHEMA.md**

文件: `memory/hongloumeng-wiki/WIKI_SCHEMA.md`

内容：包含三类页面格式（人物/主题/章节/概念）、Ingest 流程、Lint 检查规则（见设计文档第四章）

- [ ] **Step 3: 创建空的 index.md 和 log.md**

index.md: 包含目录结构框架（人物/主题/章节/概念四个分类）
log.md: 包含日志格式说明

- [ ] **Step 4: Git 提交目录结构**

```bash
git add memory/hongloumeng-wiki/
git commit -m "feat: initialize hongloumeng-wiki directory structure"
```

---

## 阶段二：迁移现有研究文件

- [ ] **Step 5: 迁移 semantic 文件到 raw/**

```bash
cp memory/semantic/*.md memory/hongloumeng-wiki/raw/
# 重命名文件，加日期前缀
mv memory/hongloumeng-wiki/raw/hongloumeng.md memory/hongloumeng-wiki/raw/2026-03-24-红楼梦核心伏笔汇总.md
# ... 其他文件类似处理
```

- [ ] **Step 6: 分析现有文件，识别页面结构**

根据迁移文件内容，识别应创建的页面：
- 人物：林黛玉、薛宝钗、贾宝玉、贾元春、贾探春、史湘云、妙玉、贾迎春、贾惜春、王熙凤、贾巧姐、李纨、秦可卿
- 主题：木石前盟、金玉良缘、太虚幻境、脂批研究
- 章节：第五回（太虚幻境）
- 概念：伏笔系统、诗词谶语、判词系统

- [ ] **Step 7: 创建人物页面**

为每个金陵十二钗正册人物创建独立页面，使用 WIKI_SCHEMA.md 规定格式
文件: `memory/hongloumeng-wiki/人物/林黛玉.md` 等

- [ ] **Step 8: 创建主题页面**

文件: `memory/hongloumeng-wiki/主题/木石前盟.md` 等

- [ ] **Step 9: 创建章节页面**

文件: `memory/hongloumeng-wiki/章节/第五回-太虚幻境.md`

- [ ] **Step 10: 创建概念页面**

文件: `memory/hongloumeng-wiki/概念/伏笔系统.md` 等

- [ ] **Step 11: Git 提交初始维基内容**

```bash
git add memory/hongloumeng-wiki/
git commit -m "feat: populate hongloumeng-wiki with initial pages"
```

---

## 阶段三：Wiki 工作流建立

- [ ] **Step 12: 完善 index.md**

扫描所有创建的页面，更新 index.md 目录

- [ ] **Step 13: 初始化 log.md**

添加第一条日志: `## [2026-04-13] init | 红楼梦维基初始化完成`

- [ ] **Step 14: Git 提交维基工作流**

```bash
git add memory/hongloumeng-wiki/
git commit -m "feat: establish hongloumeng-wiki workflow (index, log)"
```

---

## 验证步骤

1. `ls -la memory/hongloumeng-wiki/` — 目录结构完整
2. `ls memory/hongloumeng-wiki/人物/` — 人物页面已创建
3. `cat memory/hongloumeng-wiki/index.md` — 目录包含所有页面
4. `cat memory/hongloumeng-wiki/log.md` — 日志已初始化

---

## 后续使用

**Ingest 新文献时：**
1. 保存到 `raw/`，文件名加日期前缀
2. 更新相关人物/主题/章节页面
3. 追加 `log.md` 日志
4. 更新 `index.md`

**Lint 检查时：**
1. 检查矛盾点（标注「争议」）
2. 检查孤儿页面
3. 检查缺失链接
4. 更新相关页面
