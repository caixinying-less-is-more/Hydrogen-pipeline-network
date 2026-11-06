# Hydrogen-pipeline-network
h2 distribution and pipeline planning in 2060 in China

## 项目说明
本项目聚焦于 2060 年中国氢能（H₂）的输配与管网规划。详细的建模与调度代码已整合到 **`Pipeline-and-grid-dispatch/`** 子目录下（由原独立仓库合并而来，完整提交历史保留）。

## 代码架构
主仓库根目录包含管网模型相关的 `code/`、`data/`、`figure/`、`paper/`、`result/` 等；下面重点说明 `Pipeline-and-grid-dispatch/` 的目录结构。

### `Pipeline-and-grid-dispatch/`
氢气管道规划与氢能调度的核心代码。

**数据评估与预处理（Jupyter Notebook）**
- `analysis.ipynb` — 对规划结果进行分析
- `consumption potential.ipynb` — 评估各省氢能需求潜力
- `existing_pipelines.ipynb` — 现有管道的数据清洗与统计分析
- `geodata process.ipynb` — 地理数据处理
- `geodata_lambert.ipynb` — 将地理数据转换为 Lambert 投影，便于在 QGIS 中展示
- `loss_cable.ipynb` — 计算任意两省之间电网的输电损耗
- `production potential.ipynb` — 各省可再生发电潜力减去用电潜力，得到制氢潜力
- `renewable potential.ipynb` — 评估各省主流可再生能源发电潜力
- `cost_matrix.ipynb` — 建立管道建设成本因子矩阵

**优化与求解（Python）**
- `dispatch_cable.py` — 主数学规划代码（基于 Gurobi 的混合整数规划模型，统筹纯氢管道、掺氢/纯氢改造的天然气管网与电网代输）
- `optimal_path.py` — 调用改进 A* 算法求解任意两省间的最优管道路径
- `function.py` — 常用函数集合（数据导入 `import_data`、结果保存 `save_results` 等）

**空间算法模块**
- `mesh/mesh.py` — 以两省为对角，将中国内陆网格切割为矩形搜索区域
- `planner/Astar.py` — 改进的二维 A* 寻路算法

**工具与配置（`src/`）**
- `src/calculate_distance.py` — 基于 Haversine 公式，按经纬度计算两点球面距离
- `src/const.py` — 模型参数与省级行政区列表等常量
- `src/config.py` — 配置文件

> 数据可通过 Google Drive 获取：https://drive.google.com/drive/folders/1ROALcJucUvuub-WgnjqzpnBvDpQ61TZy?usp=sharing
> 详细方法请参阅对应论文。
