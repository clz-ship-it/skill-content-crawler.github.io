# 多平台爆款内容拆解器

同时分析 **小红书、抖音、B站** 三个平台的爆款内容，支持多关键词搜索、智能去重、内容提取和评论分析，生成跨平台对比分析报告。

## 核心特点

- 🔍 **多关键词搜索**：基于核心关键词自动拓展为 5 个相关搜索词，分别搜索后按标题去重，取点赞 Top N
- 📺 **三平台并行采集**：小红书（图文+视频）、抖音（视频）、B站（视频）
- 📝 **智能内容处理**：视频 → 字幕提取/Whisper 转录；图文 → 直接提取正文
- 💬 **评论深度分析**：抓取高赞评论，提取用户关注点和高频词
- 📊 **跨平台对比**：生成三平台数据对比和爆款公式总结
- 🔗 **URL 直接分析**：支持直接提供视频/笔记 URL 进行分析

## 包含的 Skill

本项目包含 4 个独立的 Claude Code Skill，可单独使用也可组合使用：

| Skill | 平台 | 说明 |
|-------|------|------|
| [skill-xiaohongshu](./skill-xiaohongshu/) | 小红书 | undetected-chromedriver + 点击卡片导航 + DOM 提取 |
| [skill-douyin](./skill-douyin/) | 抖音 | undetected-chromedriver + 四级内容提取 + 三级评论抓取 |
| [skill-bilibili](./skill-bilibili/) | B站 | 纯 API 调用 + AI 字幕提取 + 评论抓取 |
| [skill-multi-platform](./skill-multi-platform/) | 三平台 | 并行执行三平台采集 + 跨平台对比报告 |

## 环境要求

- **Python 3.8+**
- **Chrome 浏览器**（抖音和小红书需要）
- **ffmpeg**（音视频处理）

## 快速开始

### 1. 安装依赖

```bash
pip install selenium undetected-chromedriver openai-whisper moviepy yt-dlp requests
```

### 2. 获取 Cookie

| 平台 | Cookie 要求 | 获取方式 |
|------|-----------|---------|
| 小红书 | **必须** | xiaohongshu.com → F12 → Application → Cookies |
| 抖音 | **必须** | douyin.com → F12 → Application → Cookies |
| B站 | **必须** | bilibili.com → F12 → Application → Cookies |

### 3. 配置关键词

编辑对应 skill 的 `scripts/run.py` 配置区：

```python
# 关键词列表：基于核心关键词拓展为 5 个相关搜索词
KEYWORDS = ["openclaw", "openclaw教程", "openclaw测评", "openclaw怎么用", "openclaw开源"]
```

### 4. 运行

```bash
# 单平台运行
cd skill-bilibili/scripts && python run.py
cd skill-douyin/scripts && python run.py
cd skill-xiaohongshu/scripts && python run.py

# 三平台并行运行
cd skill-multi-platform/scripts && python run.py
```

## 项目结构

```
├── README.md                     # 全局说明（本文件）
├── skill-bilibili/               # B站爆款分析器
│   ├── SKILL.md
│   ├── README.md
│   ├── scripts/
│   └── references/
├── skill-douyin/                 # 抖音爆款分析器
│   ├── SKILL.md
│   ├── README.md
│   ├── scripts/
│   └── references/
├── skill-xiaohongshu/            # 小红书爆款拆解器
│   ├── SKILL.md
│   ├── README.md
│   ├── scripts/
│   └── references/
└── skill-multi-platform/         # 多平台并行分析器
    ├── SKILL.md
    ├── scripts/
    └── references/
```

## 报告输出

每个平台的报告包含以下板块：

| 板块 | 内容 |
|------|------|
| 📊 数据总览 | 视频/笔记数、总点赞、平均点赞、内容提取成功率 |
| 🏆 Top 排行 | 按点赞排序的内容列表，含摘要和热门评论 |
| 💬 评论分析 | 全网最热评论 Top 10、高频关键词 Top 20 |
| 📝 内容分析 | 内容高频主题词 Top 20 |
| 🎯 爆款特征 | 标题特征、互动数据、标题关键词 |
| 🔑 爆款公式 | 可复制的创作建议 |

## AI 模型

- **Demucs htdemucs** (~80MB)：Facebook Research 音源分离，提取纯人声
- **Whisper base** (~140MB)：OpenAI 语音识别，中文转录
- 首次运行自动下载，之后缓存在本地

## 注意事项

- **Cookie 有效期**：小红书 1-7 天，抖音约 24 小时，B站较长
- **反爬策略**：小红书和抖音使用 undetected-chromedriver 绕过检测
- **合规使用**：仅用于个人学习和研究，尊重内容创作者版权
