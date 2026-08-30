# 📈 A股周级价值投资 · 系统工作台（部署仓库）

本仓库仅承载工作台静态站点（`dashboard/`），由本地巡检流程生成数据后推送，GitHub Actions 自动部署到 Pages。

- 站点入口：`dashboard/index.html`（零构建，Chart.js CDN）
- 数据：`dashboard/data/`（metrics / equity_curves / trades / decisions / observation）
- 部署：push 到 `main` 触发 `.github/workflows/dashboard.yml` → GitHub Pages
- 数据生成与更新见系统主仓库 `System-Trading` 的巡检脚本（`_ds_daily_inspection.py`）

**仅展示，不做任何交易决策。**
