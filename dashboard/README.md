# 📈 系统工作台（Dashboard）

A股周级价值投资系统的工作台 —— 零构建静态站点（原生 HTML + Chart.js CDN），展示回测基线、交易台账、周度决策与观察日志。**仅展示，不做任何交易决策。**

## 目录

```
dashboard/
├── index.html          # 工作台页面（5 个标签页）
├── data/               # 生成的数据 JSON（入库，Pages 直接读取）
│   ├── metrics.json        # 三时代基线指标
│   ├── equity_curves.json  # 超长净值（抽稀）
│   ├── trades.json         # v16-R 短窗交易台账（最近 500 笔）
│   ├── decisions.json      # 最近 4 周决策
│   └── observation.json    # 观察日志
└── README.md
```

## 数据更新（本地，任何人可跑）

```
.venv\Scripts\python.exe scripts\generate_dashboard_data.py
git add dashboard/data && git commit -m "docs: dashboard 数据刷新"
```

## GitHub 部署（GitHub Pages）

1. 推送本仓库到 GitHub（含 `dashboard/`）
2. 仓库 Settings → Pages → Source: **GitHub Actions**（或分支 Pages，根目录选 `dashboard`）
3. 已附 `dashboard.yml` 工作流：**push 到 main 时自动部署 Pages**（仅部署，数据由本地生成后入库）

### 可选：定时自动刷新（需要仓库 Secrets 或自托管 runner）
数据源（回测存档/缓存）不在仓库内，Actions 无法自行重建。如需全自动：
- 方案 A（推荐）：本地定时任务（计划任务）跑 `generate_dashboard_data.py` → `git push`（需要写权限 token）
- 方案 B：自托管 runner 挂载数据盘，Actions 内跑生成脚本再提交

## 说明

- 净值抽稀至 240 点，交易台账取最近 500 笔（控制 JSON 体积）
- 观察日志来自 `reports/observation/*.md`（周度巡检产出）
- 所有数字口径 = v16-R 基线（见 `reports/BASELINE_MANIFEST.md` 三时代图谱）
