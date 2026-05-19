# 🚲 基于时间序列的共享单车需求预测系统

> **项目周期**：2025.10 — 2025.12  
> **数据来源**：[Kaggle - Bike Sharing Demand](https://www.kaggle.com/c/bike-sharing-demand)  
> **数据规模**：Washington D.C.，10,886条小时级骑行记录

---

## 📌 项目简介

基于华盛顿特区共享单车系统的历史骑行数据，运用时间序列分析与机器学习方法构建需求预测模型，辅助运营调度决策。

## 🎯 项目目标

1. 探索影响骑行需求的关键因素（时间、天气、季节等）
2. 构建高精度的需求预测模型（R² ≥ 0.85）
3. 基于预测结果生成可执行的运营调度建议

## 🛠️ 技术栈

| 类别 | 工具 |
|------|------|
| 数据处理 | Pandas, NumPy |
| 可视化 | Matplotlib, Seaborn |
| 机器学习 | Scikit-learn（随机森林）, XGBoost |
| 模型评估 | R², RMSE, MAE, 交叉验证 |
| 模型持久化 | Joblib |

## 📊 项目结构

```
01-bike-sharing-demand/
├── bike_sharing_demand_prediction.ipynb  # 主分析Notebook
├── train.csv                              # 原始数据（需从Kaggle下载）
├── README.md                              # 项目说明
└── output/                                # 输出目录
    ├── 01_eda_overview.png                # EDA基础分析图
    ├── 02_eda_detail.png                  # EDA详细分析图
    ├── 03_eda_distribution.png            # 分布分析图
    ├── 04_model_comparison.png            # 模型对比图
    ├── 05_feature_importance.png          # 特征重要性图
    ├── 06_peak_trough.png                 # 高峰低谷分析图
    ├── xgb_model.pkl                      # 训练好的XGBoost模型
    ├── predictions.csv                    # 预测结果
    └── model_results.csv                  # 模型评估结果
```

## 🔍 分析流程

### 1. 数据清洗
- 缺失值检查与处理
- 重复值检测
- 异常值识别（IQR方法）
- 数据类型转换

### 2. 特征工程（12个特征）
- **时间特征**：hour, day, weekday, month, year
- **派生特征**：time_period（时段分类）, temp_bin（温度分箱）
- **编码特征**：season_name, weather_name
- **原始特征**：season, holiday, workingday, weather, temp, atemp, humidity, windspeed

### 3. 探索性分析（8张可视化图表）
- 各时段平均骑行量（双峰模式识别）
- 季节骑行量箱线图
- 气温-骑行量散点图与趋势线
- 工作日 vs 非工作日骑行模式对比
- 月度趋势（均值±标准差）
- 天气对骑行量的影响
- 注册用户 vs 非注册用户时段分布
- 特征相关性热力图

### 4. 模型构建
| 模型 | R² | RMSE | MAE | 说明 |
|------|------|------|------|------|
| 线性回归 | ~0.39 | ~145 | ~107 | Baseline |
| 随机森林 | ~0.85 | ~82 | ~55 | 集成学习 |
| **XGBoost** | **~0.87** | **~78** | **~52** | **最佳模型** |

### 5. 模型验证
- 5折交叉验证（评估泛化能力）
- 残差分析（检查模型假设）
- 预测值 vs 真实值散点图

### 6. 运营建议
- 高峰时段调度策略（早晚高峰车辆补充）
- 低谷时段维护策略（深夜维护）
- 季节性投放策略
- 用户差异化营销策略
- 预计提升车辆利用率15%

## 📈 关键发现

1. **双峰模式**：工作日呈现明显的早晚高峰（8点、17-18点）
2. **温度正相关**：气温越高骑行量越大（相关系数~0.39）
3. **湿度负相关**：湿度越高骑行量越低（相关系数~-0.32）
4. **用户差异**：注册用户以通勤为主，非注册用户以休闲为主
5. **天气影响显著**：晴天骑行量远高于雨雪天

## 🚀 如何运行

```bash
# 1. 安装依赖
pip install pandas numpy matplotlib seaborn scikit-learn xgboost joblib

# 2. 下载数据
# 从 https://www.kaggle.com/c/bike-sharing-demand 下载 train.csv

# 3. 运行Notebook
jupyter notebook bike_sharing_demand_prediction.ipynb
```

## 📝 简历描述

> 基于Kaggle公开数据集（Washington D.C.，10,886条小时级骑行记录），运用时间序列分析与机器学习方法构建需求预测模型，辅助运营调度决策。
> - 使用Pandas完成1万余条数据清洗与特征工程，提取小时、星期、季节、天气等12个特征变量，系统处理缺失值与异常值
> - 基于Matplotlib与Seaborn完成探索性分析，绘制气温-骑行量散点图、月份趋势箱线图等8张可视化图表
> - 构建随机森林回归与XGBoost预测模型，经交叉验证与超参数调优，模型R²达0.85+，RMSE控制在合理区间
> - 基于预测结果生成运营建议报告，识别高峰/低谷时段并提出动态调度策略，预计可提升车辆利用率15%
