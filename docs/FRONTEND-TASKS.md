# Human3.0 前端开发任务清单

## 1. 文档信息

- 文档名称：Human3.0 前端开发任务清单
- 对应文档：
  - `docs/PRD.md`
  - `docs/IA-WIREFRAMES.md`
- 技术栈：Next.js + TypeScript
- 文档日期：2026-03-11

## 2. 目标

将页面原型与信息架构拆分为可执行的前端开发任务，覆盖：

1. 项目初始化
2. 路由与布局
3. 页面开发
4. 组件抽离
5. 状态管理与数据请求
6. 与 FastAPI 的联调准备

## 3. 开发原则

1. 先搭结构，再填数据，再做细节交互。
2. `Daily Brief` 是主入口，优先完成。
3. 列表页和详情页共用组件，避免重复实现。
4. 先完成 P0 页面静态版，再接 API。
5. 页面必须先具备空状态、加载状态、错误状态。

## 4. 目录建议

```text
src/
├── app/
│   ├── dashboard/page.tsx
│   ├── brief/
│   │   ├── today/page.tsx
│   │   ├── history/page.tsx
│   │   └── [id]/page.tsx
│   ├── content/
│   │   ├── page.tsx
│   │   └── [id]/page.tsx
│   ├── knowledge/
│   │   ├── page.tsx
│   │   └── [id]/page.tsx
│   ├── sources/page.tsx
│   ├── tasks/page.tsx
│   ├── settings/page.tsx
│   ├── layout.tsx
│   └── page.tsx
├── components/
│   ├── layout/
│   ├── brief/
│   ├── content/
│   ├── knowledge/
│   ├── sources/
│   ├── tasks/
│   └── shared/
├── lib/
│   ├── api/
│   ├── schemas/
│   ├── constants/
│   └── utils/
├── hooks/
└── types/
```

## 5. 任务分阶段

### 阶段 A：项目基础设施

#### A1. 初始化 Next.js 项目

任务：

1. 创建 `Next.js App Router` 项目
2. 配置 `TypeScript`
3. 配置 `eslint`
4. 配置基础样式方案
5. 配置路径别名

完成标准：

1. 项目可本地启动
2. 页面路由可访问
3. lint 可通过

#### A2. 统一基础样式与设计变量

任务：

1. 定义颜色变量
2. 定义间距、圆角、阴影、字体级别
3. 定义页面容器宽度
4. 定义卡片、表格、标签、按钮基础样式

完成标准：

1. 具备统一视觉 token
2. 后续页面开发不再重复写基础样式

#### A3. 全局应用壳

任务：

1. 实现根布局 `app/layout.tsx`
2. 实现侧边导航
3. 实现顶部栏
4. 实现移动端底部导航或抽屉导航
5. 实现全局页面容器

完成标准：

1. 所有页面复用同一套布局
2. 桌面端与移动端导航可切换

### 阶段 B：核心共享能力

#### B1. 路由骨架

任务：

1. 创建全部页面路由占位
2. 为每个页面补标题与基础头部
3. 首页重定向到 `/dashboard` 或 `/brief/today`

完成标准：

1. PRD/IA 中所有主路由已存在
2. 页面切换链路完整

#### B2. 全局搜索与筛选框架

任务：

1. 实现顶栏全局搜索输入框
2. 抽象筛选栏组件 `FilterBar`
3. 支持标签、日期、评分、来源筛选 UI
4. 支持 URL 查询参数同步

完成标准：

1. 内容流、知识库等列表页可复用同一筛选框架
2. 刷新页面后筛选状态可保留

#### B3. 通用状态组件

任务：

1. 实现空状态组件
2. 实现骨架屏组件
3. 实现错误提示组件
4. 实现 toast 或 action feedback 组件

完成标准：

1. 所有核心页面均可复用

#### B4. API 客户端基础

任务：

1. 抽象 `fetcher`
2. 定义 API 路径常量
3. 定义通用响应类型
4. 封装错误处理

完成标准：

1. 能支持后续接入 `SWR` 或 `React Query`
2. API 层不直接散落在页面组件中

### 阶段 C：P0 页面开发

#### C1. 仪表盘 `/dashboard`

任务：

1. 开发指标卡区域
2. 开发今日重点预览卡片
3. 开发任务状态卡片
4. 开发最近知识条目卡片
5. 开发信息源健康度区块

依赖：

1. 全局布局
2. 指标卡组件
3. 内容预览卡组件

完成标准：

1. 页面结构与 `IA-WIREFRAMES` 一致
2. 支持空状态与加载状态

#### C2. 今日 Brief `/brief/today`

任务：

1. 开发日报头部区域
2. 开发 `BriefSection` 组件
3. 开发“今日最重要”卡片
4. 开发“值得关注”简版列表
5. 开发“工具更新”模块
6. 开发“一个启发”模块
7. 开发导出和重新生成按钮 UI

依赖：

1. `ScoreBadge`
2. `TopicTag`
3. `InsightCard`
4. 内容卡片组件

完成标准：

1. 页面可完整承载日报结构
2. 条目动作按钮有明确交互反馈

#### C3. 内容流 `/content`

任务：

1. 开发搜索栏
2. 开发多条件筛选栏
3. 开发排序切换
4. 开发内容列表卡片
5. 开发右侧统计区
6. 开发分页或无限加载占位

依赖：

1. `FilterBar`
2. `ContentCard`
3. URL 参数同步

完成标准：

1. 可通过筛选查看不同内容集合
2. 卡片支持详情、原文、加入知识库、重新分析

#### C4. 内容详情 `/content/[id]`

任务：

1. 开发标题与元数据头部
2. 开发 AI 摘要区块
3. 开发评分拆解展示
4. 开发正文预览区块
5. 开发相关内容推荐
6. 开发操作区按钮

依赖：

1. 详情页通用头部
2. `ScoreBadge`
3. `TopicTag`
4. 右侧抽屉或弹窗

完成标准：

1. 单篇内容的分析与动作完整可见
2. 支持加入知识库与查看原文

#### C5. 知识库 `/knowledge`

任务：

1. 开发分类侧栏
2. 开发知识条目列表
3. 开发知识条目详情抽屉
4. 开发搜索与筛选 UI
5. 开发备注编辑入口

依赖：

1. `FilterBar`
2. 抽屉组件
3. 内容卡片变体或知识条目卡

完成标准：

1. 支持按分类回顾内容
2. 支持查看 AI 摘要与用户备注

#### C6. 信息源管理 `/sources`

任务：

1. 开发信息源统计卡
2. 开发信息源表格
3. 开发新建信息源抽屉
4. 开发编辑信息源抽屉
5. 开发错误日志查看入口
6. 开发单源抓取按钮

依赖：

1. 表格组件
2. 表单组件
3. 抽屉组件

完成标准：

1. 信息源的新增、查看、编辑入口齐全
2. 状态和错误信息清晰可见

#### C7. 任务中心 `/tasks`

任务：

1. 开发任务状态统计卡
2. 开发任务列表表格
3. 开发筛选条件
4. 开发日志详情抽屉
5. 开发手动执行按钮

依赖：

1. 表格组件
2. 状态徽标组件
3. 抽屉组件

完成标准：

1. 能清楚查看任务运行与失败原因
2. 具备明显的重试入口

### 阶段 D：P1 页面开发

#### D1. Brief 历史 `/brief/history`

任务：

1. 开发日期筛选
2. 开发历史日报列表
3. 开发状态标签
4. 开发打开与重试操作

完成标准：

1. 可按日期回看日报
2. 可识别生成失败的日报

#### D2. Brief 详情 `/brief/[id]`

任务：

1. 复用今日 Brief 页面结构
2. 根据指定 `id` 获取历史日报内容
3. 保留导出和阅读能力

完成标准：

1. 结构与今日 Brief 一致
2. 仅数据源不同

#### D3. 设置 `/settings`

任务：

1. 开发模型设置区块
2. 开发评分权重设置区块
3. 开发主题体系设置区块
4. 开发日报模板设置区块
5. 开发权限设置占位

完成标准：

1. 系统级配置有清晰分区
2. 配置表单结构完整

### 阶段 E：组件抽离与复用

#### E1. 共享展示组件

任务：

1. `ScoreBadge`
2. `TopicTag`
3. `SourceChip`
4. `InsightCard`
5. `EmptyState`
6. `LoadingSkeleton`
7. `ErrorState`

完成标准：

1. 所有页面不重复造轮子

#### E2. 业务组件

任务：

1. `BriefSection`
2. `ContentCard`
3. `KnowledgeEntryDrawer`
4. `TaskStatusCard`
5. `SourceHealthTable`
6. `GlobalSearch`
7. `FilterBar`

完成标准：

1. 核心页面使用统一业务组件

### 阶段 F：数据联调准备

#### F1. 类型定义

任务：

1. 定义 `Source`
2. 定义 `ContentItem`
3. 定义 `ContentAnalysis`
4. 定义 `DailyBrief`
5. 定义 `KnowledgeEntry`
6. 定义 `TaskLog`

完成标准：

1. 前端类型与后端 API 字段保持一致

#### F2. Mock 数据层

任务：

1. 为仪表盘准备 mock 数据
2. 为日报准备 mock 数据
3. 为内容流准备 mock 数据
4. 为知识库准备 mock 数据
5. 为任务中心准备 mock 数据

完成标准：

1. 在后端未完成前可独立开发页面

#### F3. API Hook

任务：

1. `useDashboard`
2. `useTodayBrief`
3. `useBriefHistory`
4. `useContentList`
5. `useContentDetail`
6. `useKnowledgeList`
7. `useSources`
8. `useTasks`

完成标准：

1. 页面不直接写网络请求逻辑

## 6. 推荐开发顺序

1. 项目初始化与全局布局
2. 共享状态组件与样式 token
3. 今日 Brief
4. 内容流
5. 内容详情
6. 仪表盘
7. 信息源管理
8. 任务中心
9. 知识库
10. Brief 历史
11. 设置
12. API Hook 与联调

## 7. 页面级验收标准

### 7.1 仪表盘

1. 用户一眼能看到今日系统状态与高价值内容入口。
2. 所有卡片在无数据时有合理空状态。

### 7.2 今日 Brief

1. 日报四大区块结构清晰。
2. 条目支持查看原文和加入知识库。

### 7.3 内容流

1. 可通过标签、评分、来源、日期完成筛选。
2. 列表项动作一致且明确。

### 7.4 内容详情

1. AI 分析结果、评分拆解和动作区完整。
2. 可以进入原文和加入知识库。

### 7.5 知识库

1. 可按主题分类查看。
2. 可查看用户备注和原内容摘要。

### 7.6 信息源

1. 支持新增、编辑、启停。
2. 可看到错误状态和重试入口。

### 7.7 任务中心

1. 可按状态筛选任务。
2. 对失败任务有清晰重试动作。

## 8. 联调接口映射

### 页面到 API

1. 仪表盘：
   - `GET /api/briefs/today`
   - `GET /api/content`
   - `GET /api/tasks/logs`
   - `GET /api/sources`
2. 今日 Brief：
   - `GET /api/briefs/today`
   - `POST /api/briefs/generate`
3. Brief 历史：
   - `GET /api/briefs`
   - `GET /api/briefs/{id}`
4. 内容流：
   - `GET /api/content`
5. 内容详情：
   - `GET /api/content/{id}`
   - `POST /api/content/{id}/reanalyze`
6. 知识库：
   - `GET /api/knowledge`
   - `POST /api/knowledge`
   - `PATCH /api/knowledge/{id}`
   - `DELETE /api/knowledge/{id}`
7. 信息源：
   - `GET /api/sources`
   - `POST /api/sources`
   - `PATCH /api/sources/{id}`
   - `DELETE /api/sources/{id}`
8. 任务中心：
   - `GET /api/tasks/logs`
   - `POST /api/tasks/fetch`
   - `POST /api/tasks/analyze`

## 9. 风险点

1. 如果前端过早耦合最终 API 结构，后续联调成本会上升。
2. 信息源、任务中心、知识库都偏表格型页面，组件抽象不当会导致重复实现。
3. 今日 Brief 和 Brief 详情如果各做一套页面，会产生维护成本，应复用同一渲染结构。
4. 过滤条件较多，URL 状态管理若设计不好，后续会影响搜索和分享能力。

## 10. 最终交付物

1. 可运行的 Next.js 前端项目骨架
2. 完整的 P0 页面静态实现
3. 共享组件库基础版
4. Mock 数据驱动的页面联调前版本
5. API Hook 与类型定义
