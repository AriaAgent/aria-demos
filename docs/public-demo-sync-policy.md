# Public Demo Sync Policy / 公开 Demo 策展式同步策略

> 目的：让 Karma 在外面也能看到 Aria 做出的正式网页资产，同时避免把半成品、内部日志、私密记忆、密钥、真实客户数据或误导性草稿无脑公开到 GitHub Pages。

## 核心原则

公开同步不是“把本地文件夹倒进 GitHub”，而是“策展式发布”。

每一个 HTML 页面进入 `aria-demos` 前，都要回答：

1. 这个页面是否对 Karma 或外部读者有明确价值？
2. 是否已经有清楚入口、标题、说明、上下文？
3. 是否符合公开安全边界？
4. 是否经过基本设计审美把关？
5. 是否能在移动端和桌面端正常阅读？
6. 是否验证过链接、HTML、部署？

## 四级分类

### 1. `publish`

可以同步到 GitHub Pages。

条件：

- 可公开安全展示。
- 不含私密记忆、API Key、内部日志、真实客户数据、未授权材料。
- 有明确页面目的和入口。
- 至少完成基本设计系统、标题层级、留白、移动端适配。
- 链接可验证。

### 2. `refine-first`

有价值，但必须整理/重做后再公开。

常见情况：

- 是旧版 preview、实验变体、局部样例。
- 信息有价值，但视觉、命名、上下文或入口混乱。
- 可能需要合并成一个更清楚的专题页面。

### 3. `archive-only`

留在本地 archive，不公开。

常见情况：

- 中间过程草稿。
- 自我评审页、内部测试页。
- 只对 Aria 自己回溯有用。
- 公开后会造成误解或稀释正式 demo 品质。

### 4. `reject`

不应继续使用。

常见情况：

- 过时、重复、质量太低。
- 有安全/隐私风险。
- 方向已经被更好的页面替代。

## 公开同步流程

1. 运行 HTML 盘点脚本：`python3 scripts/public_demo_sync_audit.py`
2. 查看生成清单：`state/public-demo-sync/html-inventory.json` 和 `state/public-demo-sync/html-inventory.md`
3. 人工选择本轮最多 1–2 个 `refine-first` 页面进行策展和重做。
4. 重做后放入 `github/aria-demos/docs/<topic>/`。
5. 更新 `docs/index.html` 或对应专题驾驶舱入口。
6. 验证：
   - HTML parser 通过。
   - 内部链接无缺失。
   - 本地 HTTP 返回 200。
   - Git commit + push。
   - GitHub Pages run 成功。
   - 公开 URL fetch 200。
7. 在 Earning Lab 简洁汇报公开 URL、commit、验证证据。

## 安全边界

默认禁止公开：

- `MEMORY.md`、`memory/`、聊天记录、内部日志。
- API key、token、账号信息、密钥路径内容。
- 真实客户、朋友、公司、个人数据。
- 未经授权的对外承诺、价格承诺、合作承诺。
- 会让外部读者误以为已经正式上线/招募/收费的页面。

## 设计发布最低标准

参考：`archive/design/html-design-improvement-principles-2026-05-13.md`

最低要求：

- 有明确设计系统，而不是随机颜色。
- 标题自适应：`clamp()` + 移动端处理 + 避免奇怪断句。
- 页面有留白和呼吸感。
- 不把所有内容堆成便利贴式卡片。
- CTA 少而明确。
- 中文优先，必要时补英文摘要。

## 当前建议优先级

1. Earning Lab 驾驶舱：从材料索引升级为高审美项目主页。
2. Public demo 首页：统一视觉系统和入口层级。
3. Readiness Scorecard：优化互动工具移动端体验。
4. Lead Intake Audit：重做成更强商业场景叙事。
5. Content Repurposing / Newsletter：从本地 archive 中挑出一条线，策展成公开专题。
