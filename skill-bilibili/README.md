# B站爆款内容分析器

搜索 **B站** 关键词下的高赞视频，自动提取 AI 字幕、抓取热门评论，生成 **爆款分析报告**。

## 核心特点

- 🔍 **多关键词搜索**：基于核心关键词自动拓展为 5 个相关搜索词，分别搜索后按标题去重，取点赞 Top N
- 📝 **AI 字幕提取**：通过 Player API 获取 AI 自动字幕（需 Cookie）
- 💬 **热门评论抓取**：支持多页抓取，按点赞排序（需 Cookie）
- 📊 **自动生成报告**：Markdown 格式爆款分析报告，含数据总览、Top 视频排行、评论分析、爆款公式
- 🔗 **URL 直接分析**：支持直接提供 B 站视频 URL 进行分析

## 快速开始

1. **获取 B 站 Cookie**：打开 bilibili.com → 登录 → F12 → Application → Cookies → 复制全部
2. **修改配置**：编辑 `scripts/run.py` 顶部配置区
3. **运行**：`cd scripts && python run.py`
4. **查看报告**：`output/report/bili_report_*.md`

## 文件结构

```
skill-bilibili/
├── SKILL.md                  # AI 指令
├── README.md                 # 说明文档
├── example_report.md         # 示例报告
├── scripts/
│   ├── run.py                # 主入口
│   ├── bilibili_api.py       # B 站 API 封装
│   ├── cookie_helper.py      # Cookie 管理
│   └── generate_report.py    # 报告生成
└── references/
    └── cookie-guide.md       # Cookie 获取指南
```

## 前置依赖

- Python 3.6+
- 仅使用 Python 标准库，无需安装第三方包

## 注意事项

- **Cookie 必需**：字幕和评论 API 都需要 B 站登录态 Cookie
- **Cookie 有效期**：通常较长，过期需重新获取
