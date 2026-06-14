---
title: "Bento Grid"
date: "2026-06-13"
tags: ["X-Art"]
issue: 1
summary: "从便当盒到 Apple 发布会——一种严格的几何网格如何成为 AI 创业公司的默认视觉语言,以及如何用 AI 把它做出来。"
---

2024–2026 年间,Webflow 和 Framer 上 Bento 风格作品集模板的增长幅度达到 240%。

Bento Grid 带来的体验提升数据:停留时长增加 47%;点击转化提高 38%。

## 起源:从便当盒到 iPhone 发布会

Bento Grid 的名字来自日本便当——一个托盘,多个格子,各装各的,互不干扰,一眼扫完。这个类比准确得令人意外。

- **2010**:微软 Metro Design Language 首次将瓷砖化 UI 带入大众视野(Windows Phone 7 → Xbox → Office)
- **2022**:Apple 开始在产品页和 Keynote 里大规模使用 Bento 卡片展示硬件规格,竞争对手 Google 随后跟进
- **2023**:Linear、Vercel、Loom 等 SaaS 产品将 Bento 引入落地页,成为 AI startup 的标准视觉语言
- **2025+**:Active Grid 时代——格子开始动起来,支持交互、实时数据与 AI 自动排布

![Bento Grid 案例](/images/week-01-bento-grid/week-01-bento-grid-1.png)

## 设计特征

Bento Grid 与普通的 masonry grid(如 Pinterest 的瀑布流)有本质区别:

- 严格的、几何的、有层级的:每个内容单元住在自己的格子里;
- 重要功能用大块 2×2 占位,次要信息用小块 1×1;
- 间距统一,圆角贯穿始终(通常 12–20px,传递亲和感)

## 使用场景

- 产品落地页:功能矩阵
- 数据仪表盘:KPI 卡、图表、状态并排
- 创作者作品集:跨媒介展示,无需线性导航
- 个人简介页:例如 Linktree
- 博客 / 媒体封面:专栏并列,层级清晰

## 经典案例

Apple 产品页、Linear、Notion、Perplexity、ElevenLabs、Datadog

![Bento Grid 经典案例](/images/week-01-bento-grid/week-01-bento-grid-2.png)

## 设计创新方向

- **Active Grid**:让格子动起来。悬停展开、视频填充、数据实时刷新。格子不仅是容器,而是界面的呼吸。
- **破格叙事**:打破矩形边界。部分元素溢出格子边界、图片跨格,制造视觉张力而不失秩序。
- **情绪色温系统**:不同格子承载不同情绪,用色彩温度而非仅靠尺寸传递内容权重。
- **用户可重排 Grid**:像 iPhone 主屏(widget)一样,让用户拖拽定制。
- **Soft Brutalism 混入**:在 Bento 的秩序里加入粗粝笔触、不完美排版,打破"太精致"带来的距离感。

## 用 AI 更好地呈现这种风格

Figma 官方的提示词框架:**TC-EBC** 场景。

- **Task 任务**:我要生成什么——"一个功能展示落地页的 Bento Grid 区块"
- **Context 背景**:产品是什么、目标用户是什么、用在哪个场景
- **Elements 要素**:几个格子、每格放什么内容、哪格是主角
- **Behavior 交互**:hover 效果、动画、是否响应式
- **Constraints 约束**:技术栈、颜色 token、字体、圆角值

常见错误:

- 模糊:"设计一个高级感的 Bento" → "参考 Linear.app 暗色风格的 Bento Grid,主色 #0F0F0F,卡片边框 #1F1F1F"
- 无层级:"放 6 个功能介绍" → "主功能格 grid-column: span 2,其余 5 个功能各 span 1"
- 无约束:"用 CSS 实现" → "grid-template-columns: repeat(4,1fr),gap: 12px,border-radius: 16px"
- 无情绪:"现代感" → "冷静、克制、留白大、没有装饰性元素,像 Notion 的官网"
- 一次全要:"帮我做完整个页面" → 先生成主题色板,再生成 Grid 骨架,最后填内容——三轮走

## 设计 token

- 列数:`repeat(4, 1fr)`
- 间距:`gap: 10–16px`
- 圆角:`12–20px`,全局统一
- 主角格:`span 2 / span 2`
- 横向宽格:`span 2 / span 1`
- 标准格:`span 1 / span 1`
- 内边距:`20–28px`
- 字体层级:主标 18px / 正文 13px

## 可直接使用的提示词模板

```
# 目标
用 Bento Grid 设计 [产品名] 的功能展示区块。

# 布局
- 4 列 CSS Grid,gap: 12px
- 主功能"[主功能名]"占 span 2 × span 2
- 其余 [N] 个功能各占 1×1 或 2×1
- border-radius: 16px,全局统一

# 视觉风格
- 参考 [Linear.app / Apple 产品页 / Notion 官网]
- 背景色 [#HEX],卡片色 [#HEX],强调色 [#HEX]
- 字体:[SF Pro / Inter / system-ui]
- 无装饰性元素,留白要大

# 约束
- 只用 HTML + CSS,无依赖
- 响应式:移动端单列堆叠
- hover 时格子轻微上浮(translateY -2px)
```
