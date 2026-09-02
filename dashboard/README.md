# 📈 2026 试运行 · 系统工作台（Dashboard）

A股周级价值投资系统的**2026 试运行工作台** —— 零构建静态站点（原生 HTML + Chart.js CDN）。
试运行起始 2026-01-01，初始资金 ¥1,000,000，逐周按生产冻结配置（v16-R）模拟运行，展示截止到最新决策周的仓位信息。**仅展示，不做任何交易决策。**

## 目录

```
dashboard/
├── index.html          # 工作台页面（单页，台头"2026 试运行"）
├── data/
│   ├── pilot_metrics.json     # 总览：净值/收益/回撤/Sharpe/成本/区间
│   ├── pilot_equity.json      # 每日净值 + 回撤 + 持仓数
│   ├── pilot_weekly.json      # 周决策：模式/目标池/买卖/持仓/周收益
│   ├── pilot_daily.json       # 日决策：六指数温度/大盘得分/模式/崩盘/当日动作
│   ├── pilot_four_dim.json    # 每周持仓股四维度评价（技术/预期/资金/价值）
│   └── observation.json       # 观察日志
└── README.md
```

## 数据更新（本地生成）

试运行回放（缓存扩展 → 回测 → 数据生成）：

```
.venv\Scripts\st-cli.exe backtest --precompute --start <新周起点> --end <截止> --full-market --cache-dir data\backtest\weekly_feature_cache_survivor_short
.venv\Scripts\st-cli.exe backtest --start 2026-01-01 --end <截止> --cached --initial-cash 1000000 --cache-dir data\backtest\weekly_feature_cache_survivor_short
.venv\Scripts\python.exe scripts\_ds_pilot_2026_data.py
```

（回测结果输出到 `data/backtest/results/backtest_2026-01-01_<截止>.json`）

## GitHub 部署

- 部署仓库：`Oliver102259/ST-html`（公开，Free 计划 Pages 要求公开仓库）
- push 到 `main` 触发 `.github/workflows/dashboard.yml` → GitHub Pages 自动部署
- 站点：https://oliver102259.github.io/ST-html/
- 每日 16:30 巡检（`_ds_daily_inspection.py` ⑦ 步）自动同步 `dashboard/` 并推送

## 说明

- 周决策/日决策/温度/四维度全部来自本地生产数据（`data/market`、`weekly_feature_cache_survivor_short` 缓存、试运行回测结果），口径 = v16-R 冻结配置（见 `reports/BASELINE_MANIFEST.md`）
- 观察日志来自 `reports/observation/*.md`
