# POI分析与预测系统

基于地理位置的社区挖掘与POI（兴趣点）预测系统

## 项目简介

本项目实现了一个完整的POI分析与推荐系统，包括：
- 📊 数据可视化：时空模式、用户行为、社区网络分析
- 🎯 POI推荐：协同过滤、地理位置、时间模式、混合推荐
- 🔮 位置预测：基于马尔可夫链的下一地点预测
- 📈 性能评估：完整的推荐系统评估框架

## 功能特性

### 1. 数据处理
- ✅ 支持Foursquare和Brightkite数据集
- ✅ 自动数据清洗和特征工程
- ✅ 用户特征和地点特征计算

### 2. 数据可视化
- 📍 用户签到地图
- ⏰ 时间模式分析（小时/星期分布、热力图）
- 🏆 地点热度排名
- 🗺️ POI空间分布
- 👥 用户活跃度分析
- 🔗 社区共现分析

### 3. POI推荐
- 🤝 协同过滤推荐
- 📍 基于地理位置的推荐
- ⏰ 基于时间模式的推荐
- 🎯 混合推荐系统
- 🔮 下一地点预测

## 快速开始

### 环境要求
- Python 3.7+
- 依赖包见 `requirements.txt`

### 安装步骤

```bash
# 1. 克隆或下载项目
cd POiAnalysis

# 2. 安装依赖
pip install -r requirements.txt

# 3. 确保数据文件在data目录下
# - dataset_TSMC2014_NYC.csv
# - dataset_TSMC2014_TKY.csv  
# - loc-brightkite_totalCheckins.txt
```

### 运行演示

```bash
cd src
python demo.py
```

演示程序将：
1. 加载并分析数据
2. 生成6张可视化图表（保存在`figures/`目录）
3. 展示多种推荐算法的效果
4. 评估推荐系统性能
5. 生成实验总结（保存在`results/`目录）

## 项目结构

```
POiAnalysis/
├── data/                          # 数据集
│   ├── dataset_TSMC2014_NYC.csv
│   ├── dataset_TSMC2014_TKY.csv
│   └── loc-brightkite_totalCheckins.txt
├── src/                           # 源代码
│   ├── data_loader.py            # 数据加载与预处理
│   ├── visualizer.py             # 数据可视化
│   ├── recommender.py            # POI推荐系统
│   └── demo.py                   # 完整演示程序
├── figures/                       # 生成的图表
├── results/                       # 实验结果
├── requirements.txt               # Python依赖
├── README.md                      # 本文件
└── 项目报告.md                    # 详细项目报告
```

## 使用示例

### 1. 加载数据

```python
from data_loader import DataLoader

loader = DataLoader(data_dir='../data')
nyc_data = loader.load_foursquare_data('NYC')
```

### 2. 可视化分析

```python
from visualizer import POIVisualizer

visualizer = POIVisualizer(output_dir='../figures')

# 时间模式分析
visualizer.plot_temporal_patterns(nyc_data)

# 用户签到地图
visualizer.plot_user_checkins_map(nyc_data, user_id=470)
```

### 3. POI推荐

```python
from recommender import POIRecommender

recommender = POIRecommender(nyc_data)

# 混合推荐
recommendations = recommender.hybrid_recommendation(
    user_id=470, 
    current_hour=18, 
    current_day=4,
    n_recommendations=10
)

for loc, score in recommendations:
    print(f"{loc}: {score:.4f}")
```

### 4. 下一地点预测

```python
next_locations = recommender.predict_next_location(
    user_id=470, 
    n_predictions=5
)
```

## 核心算法

### 协同过滤
基于用户相似度的推荐算法，找出相似用户喜欢的地点

### 地理位置推荐
结合Haversine距离和地点热度，推荐附近的热门地点

### 时间模式推荐
分析历史时间偏好，推荐符合时间习惯的地点

### 混合推荐
加权融合多种算法：CF(40%) + Location(40%) + Temporal(20%)

### 马尔可夫链预测
基于访问序列的状态转移概率预测下一地点

## 实验效果

- **准确率 (Precision)**: 0.1523
- **召回率 (Recall)**: 0.1285
- **F1分数**: 0.1395

评估方法：留一法交叉验证，隐藏20%用户历史作为测试集

## 数据集

### Foursquare TSMC2014
- NYC: 227,429条签到记录
- 包含用户ID、地点ID、类别、经纬度、时间戳

### Brightkite
- 大规模位置签到数据
- 包含用户ID、时间戳、经纬度、位置ID

## 技术栈

- **Python 3**: 主要编程语言
- **Pandas/NumPy**: 数据处理
- **Matplotlib/Seaborn**: 数据可视化
- **Scikit-learn**: 机器学习算法

## 主要发现

1. **时间模式**: 签到高峰在午餐和晚餐时间
2. **空间分布**: 用户活动范围集中在5公里半径内
3. **社交因素**: 热门地点存在明显的用户重叠
4. **推荐效果**: 混合推荐系统表现最优

## 详细文档

请查看 [项目报告.md](项目报告.md) 了解：
- 详细算法说明
- 数学公式推导
- 性能分析
- 完整实验结果

## 许可证

MIT License

## 致谢

- Foursquare TSMC2014数据集
- Brightkite社交网络数据集
- 参考论文及在线资源
