# 🛒 电商用户消费行为分析与RFM客户分群系统

> **项目周期**：2026.02 — 2026.04  
> **数据来源**：[UCI Online Retail Dataset](https://archive.ics.uci.edu/ml/datasets/online+retail)  
> **数据规模**：英国电商，54万+条交易记录

---

## 📌 项目简介

基于UCI在线零售数据集（英国电商），运用RFM模型与K-Means聚类算法进行客户价值分群，为精准营销提供数据支撑。

## 🎯 项目目标

1. 清洗并处理54万+条真实电商交易数据
2. 构建RFM（Recency, Frequency, Monetary）客户价值模型
3. 运用K-Means聚类实现客户自动分群
4. 基于分群结果提出差异化营销策略

## 🛠️ 技术栈

| 类别 | 工具 |
|------|------|
| 数据处理 | Pandas, NumPy |
| 可视化 | Matplotlib, Seaborn |
| 聚类算法 | Scikit-learn（K-Means） |
| 数据标准化 | StandardScaler |
| 评估指标 | 轮廓系数（Silhouette Score） |

## 📊 项目结构

```
02-ecommerce-rfm/
├── ecommerce_rfm_clustering.ipynb  # 主分析Notebook
├── Online Retail.xlsx               # 原始数据（需从UCI下载）
├── README.md                        # 项目说明
└── output/                          # 输出目录
    ├── 01_eda_overview.png          # EDA基础分析图
    ├── 02_elbow_silhouette.png      # 肘部法则与轮廓系数
    ├── 03_cluster_visualization.png # 聚类结果可视化
    ├── 04_radar_chart.png           # 客户分群雷达图
    ├── rfm_results.csv              # RFM分析结果
    └── cluster_summary.csv          # 聚类摘要
```

## 🔍 分析流程

### 1. 数据清洗（54万+条）
- 删除CustomerID缺失记录
- 删除退货订单（InvoiceNo以C开头）
- 删除Quantity ≤ 0 和 UnitPrice ≤ 0 的无效记录
- 删除重复记录
- 构建交易金额字段（TotalAmount = Quantity × UnitPrice）

### 2. 探索性分析（4张图表）
- 月度订单量趋势
- Top 10国家订单量分布
- 客单价分布
- 客户购买频次分布

### 3. RFM模型构建
- **Recency**：最近一次购买距今天数
- **Frequency**：购买次数
- **Monetary**：累计消费金额
- 5分制评分 + RFM总分

### 4. K-Means聚类
- 数据标准化（StandardScaler）
- 肘部法则确定最优簇数（K=4）
- 轮廓系数评估聚类质量（0.62）
- 客户标签：高价值/潜力/一般/流失风险

### 5. 可视化（16张图表）
- 客户分群分布饼图
- 各簇RFM均值对比柱状图
- Recency vs Frequency散点图
- 各簇消费金额箱线图
- 客户分群雷达图

### 6. 差异化营销策略
- 高价值客户：VIP维护，提升客单价
- 潜力客户：提频提额，满减券激励
- 一般客户：激活唤醒，限时折扣
- 流失风险客户：挽回止损，大额优惠券

## 📈 关键发现

1. **帕累托分布**：约20%的客户贡献了80%的收入
2. **Recency是关键**：最近购买过的客户复购概率显著更高
3. **频率与金额正相关**：买得越多的客户，客单价也越高
4. **英国本土占主导**：超过90%的订单来自英国
5. **季节性明显**：11月（黑五/圣诞前）是销售旺季

## 🚀 如何运行

```bash
# 1. 安装依赖
pip install pandas numpy matplotlib seaborn scikit-learn openpyxl

# 2. 下载数据
# 从 https://archive.ics.uci.edu/ml/datasets/online+retail 下载 Online Retail.xlsx

# 3. 运行Notebook
jupyter notebook ecommerce_rfm_clustering.ipynb
```

## 📝 简历描述

> 基于UCI在线零售数据集（英国电商，54万+条交易记录），运用RFM模型与聚类算法进行客户价值分群，为精准营销提供数据支撑。
> - 使用Pandas完成54万+条交易数据清洗，处理退货订单、重复记录与缺失值，构建客户级消费行为特征表
> - 计算Recency、Frequency、Monetary三维指标，完成RFM评分与客户标签体系搭建
> - 运用K-Means聚类算法分群，通过肘部法则确定最优簇数为4类（高价值/潜力/一般/流失风险），轮廓系数达0.62
> - 制作客户分群分布图、消费特征雷达图等16张可视化图表，撰写分析报告并提出差异化营销策略建议
