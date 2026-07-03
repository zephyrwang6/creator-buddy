---
name: social-content-reach-tools
description: 多平台内容运营数据工具｜当提到小红书/B站/抖音关键词搜索、笔记/视频详情、评论、博主/UP主作品监控时使用。基于 Agent Reach / OpenCLI / bili-cli / 公开只读接口访问，不再要求第三方 API key。
license: MIT
metadata:
  type: command
  runtime: "nodejs@16.14.0+"
  version: "2.0.0"
  requires:
    bins:
      - "node"
      - "agent-reach"
  category:
    - "Data&APIs"
    - "内容创作"
  tags:
    - "小红书"
    - "B站"
    - "抖音"
    - "Agent Reach"
    - "内容搜索"
    - "评论分析"
    - "竞品监控"
    - "趋势洞察"
    - "KOL筛选"
  examples:
    - "搜索小红书'露营装备': node src/xiaohongshu/search-cli.js --platform xiaohongshu --keyword '露营装备' --limit 10"
    - "搜索B站'AI编程': node src/xiaohongshu/search-cli.js --platform bilibili --keyword 'AI编程' --limit 10"
    - "分析小红书笔记详情及评论: node src/xiaohongshu/detail-cli.js --platform xiaohongshu --url 'https://www.xiaohongshu.com/explore/xxx?xsec_token=yyy' --limit 100"
    - "监控小红书博主作品: node src/xiaohongshu/post-cli.js --platform xiaohongshu --url 'https://www.xiaohongshu.com/user/profile/xxx?xsec_token=yyy' --limit 20"
---

# 多平台内容洞察与竞品分析助手

> 一句话价值主张：用 Agent Reach 的本地平台后端替代专用 API key，把小红书、B站和可扩展的抖音内容抓取统一到一套内容运营 CLI。

## 1. 技能概述

这个 Skill 原本依赖 `GUAIKEI_API_TOKEN`，现在改为优先使用 Agent Reach 生态中的只读后端：

- 小红书：`opencli xiaohongshu`、`xiaohongshu-mcp` 或 `xhs-cli`
- B站：`bili-cli`、`opencli bilibili` 或 B站公开搜索/详情 API
- 抖音：Agent Reach 当前未内置 channel，预留 `DOUYIN_COMMAND` 自定义只读 CLI 适配

## 2. 核心能力

| 使用场景 | 具体价值 |
| --- | --- |
| 内容创作选题 | 输入关键词，跨平台搜索热门内容，快速找到选题方向 |
| 竞品监控 | 输入创作者主页链接，查看公开作品与内容方向 |
| 评论/详情分析 | 读取笔记或视频详情，必要时抓取评论 |
| 趋势洞察 | 用同一个命令比较小红书、B站、抖音的内容分布 |

## 3. 快速使用

### 3.1 小红书关键词搜索

```bash
node src/xiaohongshu/search-cli.js --platform xiaohongshu --keyword "夏季穿搭" --limit 10
```

### 3.2 小红书笔记详情及评论

```bash
node src/xiaohongshu/detail-cli.js \
  --platform xiaohongshu \
  --url "https://www.xiaohongshu.com/explore/xxx?xsec_token=yyy" \
  --limit 100
```

### 3.3 小红书博主作品

```bash
node src/xiaohongshu/post-cli.js \
  --platform xiaohongshu \
  --url "https://www.xiaohongshu.com/user/profile/xxx?xsec_token=yyy" \
  --limit 20
```

### 3.4 B站搜索与视频详情

```bash
node src/xiaohongshu/search-cli.js --platform bilibili --keyword "AI编程" --limit 10
node src/xiaohongshu/detail-cli.js --platform bilibili --url "BVxxxx"
```

### 3.5 抖音扩展入口

Agent Reach 当前版本没有抖音 channel。若你有本地只读 CLI，可以这样接入：

```bash
export DOUYIN_COMMAND="/path/to/douyin-readonly-cli"
node src/xiaohongshu/search-cli.js --platform douyin --keyword "AI工具"
```

该 CLI 需支持：

```bash
$DOUYIN_COMMAND search <keyword> --limit <n>
$DOUYIN_COMMAND detail <url-or-id>
$DOUYIN_COMMAND user <user-url-or-id> --limit <n>
```

## 4. 后端检查

使用前建议运行：

```bash
agent-reach doctor --json
```

如果小红书显示 `active_backend: null`，请安装 OpenCLI 渠道并在 Chrome 登录小红书，或配置 `xiaohongshu-mcp`。

## 5. 重要限制

- 本工具只读公开数据，不支持发帖、评论、点赞等写操作。
- 小红书受 `xsec_token` 机制限制，详情页建议使用搜索结果返回的完整 URL。
- B站公开 API 不保证所有详情字段稳定；安装 `bili-cli` 后能力更完整。
- 抖音当前是扩展位，不随仓库内置可用后端。
- 所有任务结果会自动保存到 `logs/`，该目录默认不提交。

更多选项见 [完整选项说明](references/options.md)。
