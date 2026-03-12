# 抖音爆款内容分析器

搜索 **抖音** 关键词下的高赞视频，自动提取字幕或转录视频内容、抓取热门评论，生成 **爆款分析报告**。

## 核心特点

- 🔍 **多关键词搜索**：基于核心关键词自动拓展为 5 个相关搜索词，分别搜索后按标题去重，取点赞 Top N
- 📝 **四级内容提取**：抖音字幕 → yt-dlp → 必剪 ASR → Whisper 转录
- 💬 **三级评论抓取**：API → 源码正则 → DOM 解析
- 📊 **自动生成报告**：Markdown 格式爆款分析报告
- 🔗 **URL 直接分析**：支持直接提供抖音视频 URL 进行分析

## 快速开始

1. **安装依赖**：`pip install undetected-chromedriver openai-whisper moviepy yt-dlp requests`
2. **获取抖音 Cookie**：打开 douyin.com → 登录 → F12 → Application → Cookies → 复制全部
3. **修改配置**：编辑 `scripts/run.py` 顶部配置区
4. **运行**：`cd scripts && python run.py`
5. **查看报告**：`output/<关键词>/douyin_report_*.md`

## 文件结构

```
skill-douyin/
├── SKILL.md                  # AI 指令
├── README.md                 # 说明文档
├── example_report.md         # 示例报告
├── scripts/
│   ├── run.py                # 主入口
│   ├── douyin_api.py         # 搜索 + 评论抓取
│   ├── subtitle_extractor.py # 字幕提取（三级降级）
│   ├── downloader.py         # 视频下载
│   ├── transcriber.py        # Whisper 转录
│   ├── bcut_asr.py           # 必剪云端 ASR
│   ├── generate_report.py    # 报告生成
│   ├── html_structure_detector.py # HTML 结构检测
│   ├── cookie_helper.py      # Cookie 管理
│   └── config.py             # 配置
└── references/
    └── cookie-guide.md       # Cookie 获取指南
```

## 前置依赖

- Python 3.8+
- Chrome 浏览器
- ffmpeg
- `pip install undetected-chromedriver openai-whisper moviepy yt-dlp requests`

## 注意事项

- **Cookie 必需**：抖音搜索和评论都需要登录态 Cookie
- **Cookie 有效期**：约 24 小时，过期需重新获取
- **禁止 headless 模式**：抖音检测 headless 极严，必须可见浏览器模式
