# AI-Assisted Grounded Theory Analysis: Legacy Code

## Project Overview

This project aims to use Large Language Models (LLMs) to assist with Grounded Theory analysis. The entire workflow uses "Open Source Cases" as the subject of study. Through several automated stages, it extracts causal relationships from the original case texts and progressively builds a theoretical model. The project's code is clearly divided into five core stages, from data extraction to the theory saturation test.

## Project Workflow

This project connects five core stages through `main.py`, with each stage calling the DeepSeek API to perform specific analysis tasks:

1.  **Stage 1: Information Extraction**
    * **Script**: `stages/stage1_information_extraction.py`
    * **Task**: Reads the text of AI model open-source cases from the input Excel file (`test.xlsx`) and extracts causal relationship pairs.
    * **Output**: Generates `step1.xlsx`, which includes the case number, causal pair number, original text of the cause, original text of the effect, and the source text snippet.

2.  **Stage 2: Open Coding**
    * **Script**: `stages/stage2_open_coding.py`
    * **Task**: Reads the causal pairs from `step1.xlsx` and performs open coding on the "cause" and "effect" to generate concepts and subcategories.
    * **Output**: Generates `step2.xlsx`, adding `cause_concept`, `effect_concept`, `cause_subcategory`, and `effect_subcategory` fields to the existing data.

3.  **Stage 3: Axial Coding**
    * **Script**: `stages/stage3_axial_coding.py`
    * **Task**: Extracts all subcategories from `step2.xlsx` and consolidates them into main categories through cluster analysis, providing explanations for each.
    * **Output**: Generates `step3.xlsx`, which contains the main categories, their explanations, and a list of subcategories under each main category.

4.  **Stage 4: Selective Coding**
    * **Script**: `stages/stage4_selective_coding.py`
    * **Task**: Identifies the core category from the main categories in `step3.xlsx` and elaborates on its relationship with other main categories.
    * **Output**: Generates `step4.xlsx`, containing the core category and its explanation.

5.  **Stage 5: Data Saturation Test**
    * **Script**: `stages/stage5_saturation_test.py`
    * **Task**: Uses data from `step2.xlsx` and `step3.xlsx` to test whether all subcategories can be covered by the existing main categories. If not, it proposes new main categories.
    * **Output**: Generates `step5.xlsx`, which shows the classification label for each subcategory or proposes new categories.

## Prompt Source

The prompts used for analysis in each stage of this project are from the following research:

Zhou, Y., Yuan, Y., Huang, K., & Hu, X. (2024). Can ChatGPT perform a grounded theory approach to do risk analysis? An empirical study. *Journal of Management Information Systems, 41*(4), 982-1015.

## Project Structure
```
/
|-- main.py                     # Main program entry point
|-- data/
|   |-- input_data/
|   |   `-- test.xlsx           # Raw input data
|   |-- output_data/            # Output results for all stages
|   |   |-- step1.xlsx
|   |   |-- step2.xlsx
|   |   |-- step3.xlsx
|   |   |-- step4.xlsx
|   |   `-- step5.xlsx
|   `-- data_processing.py      # Utility functions for data reading, writing, and processing
|-- stages/                     # Scripts for each analysis stage
|   |-- stage1_information_extraction.py
|   |-- stage2_open_coding.py
|   |-- stage3_axial_coding.py
|   |-- stage4_selective_coding.py
|   `-- stage5_saturation_test.py
|-- api/
|   `-- deepseek_client.py      # Client that encapsulates DeepSeek API calls
`-- README.md                   # This file
```

## How to Run

1.  **Configure Environment**:
    * Install the required Python libraries, mainly `pandas` and `openai`.
    * Configure your DeepSeek API key in the `api/deepseek_client.py` file.

2.  **Prepare Data**:
    * Organize your raw case data into the `data/input_data/test.xlsx` file. This file should contain at least two columns: `Number of Cases` and `Case text`.

3.  **Run Analysis**:
    * Run the main program `main.py`.
        ```bash
        python main.py
        ```
    * The program will execute all five stages in sequence and generate intermediate and final result files in the `data/output_data/` directory.

## Dependencies

* pandas
* openai

-----


# AI 辅助扎根理论分析 初版

## 项目概述

本项目旨在使用大型语言模型（LLM）辅助进行扎根理论（Grounded Theory, GT）分析。整个流程以“开源案例”作为研究对象，通过多个自动化阶段，从原始案例文本中提取因果关系，并逐步构建理论模型。项目代码清晰地划分了从数据提取到理论饱和度检验的五个核心阶段。

## 项目流程

本项目通过 `main.py` 串联起五个核心阶段，每个阶段都调用 DeepSeek API 来完成特定的分析任务：

1.  **阶段1：信息抽取 (Stage 1: Information Extraction)**
    * **脚本**: `stages/stage1_information_extraction.py`
    * **任务**: 从输入的 Excel 文件（`test.xlsx`）中读取AI模型开源案例的文本，提取因果关系对。
    * **输出**: 生成 `step1.xlsx`，包含案例编号、因果对编号、原因原文、结果原文以及来源文本片段。

2.  **阶段2：开放编码 (Stage 2: Open Coding)**
    * **脚本**: `stages/stage2_open_coding.py`
    * **任务**: 读取 `step1.xlsx` 中的因果对，对“原因”和“结果”进行开放编码，生成概念（Concept）和子范畴（Subcategory）。
    * **输出**: 生成 `step2.xlsx`，在原有数据基础上增加了 `cause_concept`, `effect_concept`, `cause_subcategory`, `effect_subcategory` 字段。

3.  **阶段3：主轴编码 (Stage 3: Axial Coding)**
    * **脚本**: `stages/stage3_axial_coding.py`
    * **任务**: 从 `step2.xlsx` 中提取所有子范畴，通过聚类分析将其归纳为主范畴（Main Category），并提供解释。
    * **输出**: 生成 `step3.xlsx`，包含主范畴、其解释以及该主范畴下的子范畴列表。

4.  **阶段4：选择性编码 (Stage 4: Selective Coding)**
    * **脚本**: `stages/stage4_selective_coding.py`
    * **任务**: 基于 `step3.xlsx` 中的主范畴，识别出核心范畴（Core Category），并阐述其与其他主范畴之间的关系。
    * **输出**: 生成 `step4.xlsx`，包含核心范畴及其解释。

5.  **阶段5：理论饱和度检验 (Stage 5: Data Saturation Test)**
    * **脚本**: `stages/stage5_saturation_test.py`
    * **任务**: 使用 `step2.xlsx` 和 `step3.xlsx` 的数据，检验所有子范畴是否能被已有的主范畴所覆盖。如果不能，则提出新的主范畴建议。
    * **输出**: 生成 `step5.xlsx`，展示每个子范畴的归属标签或新范畴提议。

## 提示词来源

本项目中用于各阶段分析的提示词（Prompts）主要来自以下研究：

Zhou, Y., Yuan, Y., Huang, K., & Hu, X. (2024). Can ChatGPT perform a grounded theory approach to do risk analysis? An empirical study. *Journal of Management Information Systems, 41*(4), 982-1015.

## 项目结构

```
/
|-- main.py                     # Main program entry point
|-- data/
|   |-- input_data/
|   |   `-- test.xlsx           # Raw input data
|   |-- output_data/            # Output results for all stages
|   |   |-- step1.xlsx
|   |   |-- step2.xlsx
|   |   |-- step3.xlsx
|   |   |-- step4.xlsx
|   |   `-- step5.xlsx
|   `-- data_processing.py      # Utility functions for data reading, writing, and processing
|-- stages/                     # Scripts for each analysis stage
|   |-- stage1_information_extraction.py
|   |-- stage2_open_coding.py
|   |-- stage3_axial_coding.py
|   |-- stage4_selective_coding.py
|   `-- stage5_saturation_test.py
|-- api/
|   `-- deepseek_client.py      # Client that encapsulates DeepSeek API calls
`-- README.md                   # This file
```

## 如何运行

1.  **配置环境**:
    * 安装所需的 Python 库，主要是 `pandas` 和 `openai`。
    * 在 `api/deepseek_client.py` 文件中配置您的 DeepSeek API密钥。

2.  **准备数据**:
    * 将您的原始案例数据整理成 `data/input_data/test.xlsx` 文件。该文件应包含至少两列：`Number of Cases`（案例编号）和 `Case text`（案例文本）。

3.  **执行分析**:
    * 运行主程序 `main.py`。
        ```bash
        python main.py
        ```
    * 程序将按顺序执行所有五个阶段，并依次生成中间和最终结果文件到 `data/output_data/` 目录下。

## 依赖

* pandas
* openai

---


