# baokuan-article-analysis

Fetch and analyze WeChat Official Account hot articles by sector or keywords.

The main skill instructions live in [`SKILL.md`](SKILL.md). The bundled script writes:

- `data.json`: raw structured article data
- `report.html`: visual analysis report with KPIs, charts, ranked articles, writing style patterns, hot reasons, and writing references

## Quick Start

```bash
python3 scripts/daily_sector_trends.py \
  --sector-config references/default-sectors.json \
  --days 7 \
  --output-dir ./output
```

Run custom sectors:

```bash
python3 scripts/daily_sector_trends.py \
  --sector 'AI Agent=AI Agent,智能体,Agent框架' \
  --sector 'Skill=skill,Skills,AI Skill' \
  --sector 'Claude Code=Claude Code,Codex,AI编程' \
  --output-dir ./output
```

## Contents

- `SKILL.md`: Codex skill instructions
- `agents/openai.yaml`: short skill metadata for OpenAI agent usage
- `references/default-sectors.json`: default sector keyword config
- `scripts/daily_sector_trends.py`: hot article fetch and report generator

