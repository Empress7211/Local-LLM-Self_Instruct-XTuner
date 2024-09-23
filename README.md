#一键自监督指令生成-微调

## 项目简介

本项目旨在通过本地LLM的自监督指令生成并利用该指令数据集微调其自身。项目包含了从指令生成到模型微调的完整流程，使用了self-instruct方法和XTuner工具。

## 环境要求

- Python 3.10+
- Conda
- CUDA支持的GPU（推荐）


## 安装步骤

1. 导入Conda环境：
   conda env create -f self_instruct.yaml
   conda env create -f xtuner0121.yaml


## 项目结构

- `full_pipeline.sh`: 主脚本，协调整个流程的执行。
- `self_instruct_pipeline.sh`: 负责自监督指令生成过程。
- `finetune_Qwen.sh`: 执行Qwen模型的微调过程。
- `configs/`: 包含模型配置文件。

## 使用方法

1. 配置环境变量：
   打开 `full_pipeline.sh`，根据您的环境修改以下变量：
   - `BASE_DIR`: 项目根目录
   - `WORK_DIR`: 工作目录
   - `BASE_MODEL_PATH`: 预训练模型路径
   - `INITIAL_CONFIG_FILE`: 初始配置文件路径


2. 运行完整流程：
   ```bash
   bash full_pipeline.sh
   ```
   这将依次执行指令生成和模型微调过程。

3. 单独运行指令生成：
   ```bash
   bash self_instruct_pipeline.sh
   ```

4. 单独运行模型微调：
   ```bash
   bash finetune_Qwen.sh
   ```

## 注意事项

- 确保 `BASE_MODEL_PATH` 指向正确的预训练模型目录。
- 首次运行时，脚本会自动创建必要的目录结构。
- 如遇到权限问题，请确保脚本具有执行权限：`chmod +x *.sh`

## 自定义配置

- 修改 `configs/qwen1_5_7b_chat_qlora_alpaca_e3_template.py` 以自定义模型训练参数。
- 在 `full_pipeline.sh` 中调整环境变量以更改数据路径和输出目录。

## 输出说明

- 生成的指令数据将保存在 `OUTPUT_DIR` 指定的目录中。
- 微调后的模型将保存在 `MERGED_DIR` 指定的目录中。

## 故障排除

- 如果遇到 "File not found" 错误，请检查 `full_pipeline.sh` 中的路径设置。
- 确保已正确安装并配置api-for-open-llm。
- 确保已正确安装并配置 XTuner。
- 检查 CUDA 和 GPU 驱动是否正确安装和配置。

