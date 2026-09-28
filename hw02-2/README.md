# HW02-2：房地产上市公司财务特征分析

## 数据与样本

- 数据库：CSMAR
- 下载日期：2026-09-28
- 正式样本期：2005—2015
- 资产负债表额外包含 2004-12-31，用于 2005 年 ROA/ROE 平均分母
- 频率与口径：年度、合并报表
- 最终分析面板：172 家公司、1,193 条 firm-year

本次使用的主要 CSMAR 表：

| 表 | 文件 | 主要用途 |
|---|---|---|
| 上市公司基本信息年度表 | `STK_LISTEDCOINFOANL.csv` | 历史行业、上市日期 |
| 上市公司上市状态变更表 | `STK_ITEMCHANGE.csv` | 年末上市状态 |
| 中国上市公司股权性质文件 | `EN_EquityNatureAll.csv` | 年度产权属性 |
| 资产负债表 | `FS_Combas.csv` | 资产、负债、权益、货币资金、短/长期借款 |
| 利润表 | `FS_Comins.csv` | 合并净利润 |

正式分析使用包含短期借款和长期借款字段的新版资产负债表。

## 本地文件位置

公开仓库不包含受限 CSMAR 原始数据。复现时按 [data/README.md](./data/README.md) 的目录结构放到：

```text
hw02-2/
└── data/
    └── raw/
        ├── 01-company-basic-annual/
        ├── 02-listing-status/
        ├── 03-ownership/
        ├── 04-balance-sheet/
        └── 05-income-statement/
```

## 环境与运行

```bash
pip install -r requirements.txt
```

打开 `hw02-2.ipynb`，Restart Kernel → Run All。Notebook 使用相对路径；原始数据只读，不覆盖或删除。

## 指标与主要输出

- `leverage = total_liabilities / total_assets`
- `bankloan = (short_term_loan + long_term_loan) / total_liabilities`
- `short_debt_ratio = current_liabilities / total_liabilities`
- `ROA = consolidated_net_income / average_total_assets`
- `ROE = consolidated_net_income / average_total_equity`
- `Cash_TA = monetary_funds / total_assets`

Notebook 输出年度公司数量与产权结构、六项指标均值/中位数、SOE vs Private 均值/中位数、有效样本量，以及主键、合并、缺失、分母和离群值 QA。

## AI 使用声明与核验

使用 ChatGPT / Codex 辅助提取 rubric、解析复杂 CSV、设计变量字典和 merge QA、生成/调试 Python、绘图与中文说明。原始 CSMAR 数据由本人通过学校授权账户下载。

关键提示词示例：

> HW02-2 必须按 2005—2015 年历史行业、年末上市状态和年度产权构造非平衡面板；2005 年 ROA/ROE 必须使用 2004 年末资产/权益；每次 merge 前检查 code-year 唯一性，禁止静默 many-to-many；短期/长期借款缺失不能自动填 0，离群值必须检查但不得为了图好看自动缩尾。

本人重点核验：历史 `IndustryCodeC=K70` 口径、首次上市日期、年度产权分类、`Typrep=A` 合并年报、2004 年滞后分母、短/长期借款字段、上市状态变更及各比率分母。

实际修正过的问题：`STK_ITEMCHANGE.csv` 的 Comments 长文本导致普通 CSV 解析失败，最终没有使用 `skip_bad_lines` 静默丢记录；补齐 2004 年资产/权益；重新下载含短期/长期借款的资产负债表；保留借款缺失而非填 0；修正 Matplotlib 中文字体设置。

## 仓库

https://github.com/lh3536/FinEco-hw
