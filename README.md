# FinEco-hw

中山大学岭南学院 LN429《金融计量经济学》HW02 复现材料。

- 学生：魏致衡
- 公开仓库身份标识：LN429（完整学号仅保留在课程提交版）
- [HW02-1：股票收益与组合风险分析](./hw02-1/)
- [HW02-2：房地产上市公司财务特征分析](./hw02-2/)
- 教师作业页面：https://lianxhcn.github.io/FinEco/exercises/hw-02.html

## 复现说明

两题 Notebook 均已在提交前从头运行并保存输出。公开仓库不包含 CSMAR 受限原始数据；复现者需具有合法 CSMAR 访问权限，并按照各题 `data/README.md` 的表名、时间范围、字段和本地路径重新取得本次分析使用的数据快照。

运行顺序：

1. 进入对应题目目录。
2. `pip install -r requirements.txt`
3. 按 `data/README.md` 将原始 CSMAR ZIP 放到 `data/raw/`。
4. 打开对应 `hw02-*.ipynb`，Restart Kernel 后 Run All。
5. 核对 Notebook 中的 QA 表、图形和结论。

## 数据权限

CSMAR 数据受学校与数据库授权范围约束，因此原始 ZIP/CSV 不上传公开 GitHub，也不通过公开网盘转发。仓库仅提供完整分析代码、数据字段与下载条件、处理规则、QA 以及已保存的分析结果。

## 目录

```text
FinEco-hw/
├── README.md
├── .gitignore
├── hw02-1/
│   ├── hw02-1.ipynb
│   ├── README.md
│   ├── requirements.txt
│   └── data/
│       └── README.md
└── hw02-2/
    ├── hw02-2.ipynb
    ├── README.md
    ├── requirements.txt
    └── data/
        └── README.md
```

GitHub Pages、AI 对话链接及 SHA256 属于本次作业可选扩展，本仓库未将其作为必做复现条件。
