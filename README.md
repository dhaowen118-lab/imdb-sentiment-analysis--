# 基于机器学习的电影评论情感分析

## IMDB Movie Reviews Sentiment Analysis

> 《人工智能基础》课程期末大作业 · Final Project of *Introduction to Artificial Intelligence*

---

## 项目简介

本项目以 **IMDB 电影评论数据集**为研究对象，通过自然语言处理（NLP）技术对电影评论进行情感分类（正面/负面）。项目实现了从数据预处理、特征提取、模型训练到结果可视化的完整流水线，并对比了 **3 种分类算法 × 2 种特征表示 = 6 组实验方案** 的分类性能。

### 核心结果

| 排名 | 模型 | 特征方法 | 准确率 |
|:----:|------|----------|:------:|
| 1 | **逻辑回归 (LR)** | **TF-IDF** | **89.3%** |
| 2 | 逻辑回归 (LR) | BoW | 88.6% |
| 3 | 线性 SVM | TF-IDF | 88.1% |
| 4 | 线性 SVM | BoW | 87.2% |
| 5 | 多项式朴素贝叶斯 (MNB) | BoW | 85.7% |
| 6 | 多项式朴素贝叶斯 (MNB) | TF-IDF | 84.3% |

🏆 **最优方案：逻辑回归 + TF-IDF，准确率 89.3%**

---

## 项目结构

```
├── README.md                              # 项目说明（本文件）
├── requirements.txt                       # Python 依赖列表
├── 电影评论情感分析_实验代码.ipynb           # 主实验 Notebook（完整代码 + 可视化）
├── 电影评论情感分析_期末设计报告.docx         # 期末设计报告（Word 格式）
├── generate_report.py                     # 报告自动生成脚本
├── generate_figures.py                    # 报告插图生成脚本
├── figures/                               # 报告插图（8 张，与章节对应）
│   ├── fig_3-1_data_distribution.png      # 3.2节 数据分布
│   ├── fig_3-2_positive_wordcloud.png     # 3.2节 正面评论词云
│   ├── fig_3-3_negative_wordcloud.png     # 3.2节 负面评论词云
│   ├── fig_4-1_system_flowchart.png       # 4.1节 系统流程图
│   ├── fig_5-1_confusion_matrix.png       # 5.4节 混淆矩阵
│   ├── fig_5-2_accuracy_comparison.png    # 5.4节 准确率对比
│   ├── fig_5-3_positive_wordcloud.png     # 5.4节 正面词云
│   └── fig_5-4_negative_wordcloud.png     # 5.4节 负面词云
└── IMDB Dataset.csv                       # 数据集（需自行下载，见下方说明）
```

> ⚠️ `IMDB Dataset.csv` 文件约 66MB，已通过 `.gitignore` 排除，请自行下载。

---

## 技术栈

| 类别 | 技术/工具 |
|------|-----------|
| 编程语言 | Python 3.10+ |
| NLP 工具 | NLTK, BeautifulSoup4 |
| 机器学习 | scikit-learn |
| 数据处理 | pandas, NumPy |
| 可视化 | matplotlib, seaborn, WordCloud |
| 交互环境 | Jupyter Notebook |

---

## 快速开始

### 1. 环境准备

```bash
# 克隆仓库
git clone https://github.com/<你的用户名>/<仓库名>.git
cd <仓库名>

# 创建虚拟环境（推荐）
python -m venv venv
source venv/bin/activate        # macOS/Linux
# venv\Scripts\activate         # Windows

# 安装依赖
pip install -r requirements.txt
```

### 2. 下载数据集

从 Kaggle 下载 IMDB 数据集：

> 📥 [IMDB Dataset of 50K Movie Reviews](https://www.kaggle.com/datasets/lakshmi25npathi/imdb-dataset-of-50k-movie-reviews)

将 `IMDB Dataset.csv` 放在项目根目录下。

### 3. 运行实验

```bash
jupyter notebook 电影评论情感分析_实验代码.ipynb
```

按顺序运行所有 Cell 即可。首次运行需下载 NLTK 停用词资源（自动完成）。

> 💡 预处理 50,000 条评论约需 2~5 分钟，请耐心等待。

### 4. 生成报告插图（可选）

如需重新生成报告插图：

```bash
python generate_figures.py
```

---

## 实验流程

```
原始数据 (50,000条评论)
    │
    ▼
┌──────────────┐
│  数据预处理    │  去除HTML → 去特殊字符 → Porter词干提取 → 去停用词
└──────┬───────┘
       │
       ▼
┌──────────────┐
│  数据划分      │  训练集 40,000 条 / 测试集 10,000 条 (8:2)
└──────┬───────┘
       │
       ▼
┌──────────────┐
│  特征提取      │  ┌─ BoW (词袋模型, 1-3gram)
│              │  └─ TF-IDF (词频-逆文档频率, 1-3gram)
└──────┬───────┘
       │
       ▼
┌──────────────┐
│  模型训练      │  ┌─ 逻辑回归 (Logistic Regression, L2正则)
│              │  ├─ 线性SVM (SGDClassifier, hinge loss)
│              │  └─ 多项式朴素贝叶斯 (MultinomialNB)
└──────┬───────┘
       │
       ▼
┌──────────────┐
│  评估与可视化   │  准确率 / 混淆矩阵 / 词云 / 热力图
└──────────────┘
```

---

## 实验结果

### 准确率对比

![准确率对比](figures/fig_5-2_accuracy_comparison.png)

### 混淆矩阵（最优模型 LR + TF-IDF）

![混淆矩阵](figures/fig_5-1_confusion_matrix.png)

### 词云对比

| 正面评论 | 负面评论 |
|:--------:|:--------:|
| ![正面词云](figures/fig_3-2_positive_wordcloud.png) | ![负面词云](figures/fig_3-3_negative_wordcloud.png) |

---

## 主要结论

1. **逻辑回归** 在两种特征表示下均表现最优，适合高维稀疏文本特征
2. **TF-IDF** 整体优于 BoW（朴素贝叶斯除外），加权方案更能突出关键词
3. **朴素贝叶斯** 在 TF-IDF 下反而不如 BoW，与其基于词频的概率模型假设有关
4. 最优方案（LR + TF-IDF）达到 **89.3%** 准确率，达到传统机器学习方法在该任务上的较优水平

### 未来改进方向

- 引入 Word2Vec / GloVe 词向量替代 TF-IDF
- 使用 BERT 等预训练语言模型（预计可提升至 93%+）
- 增加否定词处理与情感词典融合策略
- 探索深度学习模型（LSTM、CNN）

---

## 参考文献

1. Pang B, Lee L, Vaithyanathan S. *Thumbs up? Sentiment classification using machine learning techniques*. EMNLP, 2002.
2. Maas A L, Daly R E, Pham P T, et al. *Learning word vectors for sentiment analysis*. ACL, 2011.
3. Devlin J, Chang M W, Lee K, et al. *BERT: Pre-training of deep bidirectional transformers for language understanding*. NAACL, 2019.
4. Manning C D, Raghavan P, Schütze H. *Introduction to Information Retrieval*. Cambridge University Press, 2008.
5. Bird S, Klein E, Loper E. *Natural Language Processing with Python*. O'Reilly Media, 2009.
6. Pedregosa F, et al. *Scikit-learn: Machine learning in Python*. JMLR, 2011.
7. 刘知远, 孙茂松, 林衍凯, 等. 知识表示学习研究进展. 计算机研究与发展, 2016.
8. 赵妍妍, 秦兵, 刘挺. 文本情感分析. 软件学报, 2010.

---

## License

本项目仅用于学术教育目的，遵循 MIT License。
