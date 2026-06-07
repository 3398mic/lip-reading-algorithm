# 使用指南

## 环境配置

### 1. 克隆仓库

```bash
git clone https://github.com/3398mic/lip-reading-algorithm.git
cd lip-reading-algorithm
```

### 2. 创建虚拟环境

#### 使用 Python venv

**Windows:**
```bash
python -m venv venv
venv\Scripts\activate
```

**Linux/macOS:**
```bash
python3 -m venv venv
source venv/bin/activate
```

#### 使用 Anaconda（推荐）

如果你使用 Anaconda（就像你的电脑上一样）：

```bash
# 创建 conda 环境（Python 3.10）
conda create -n lip-reading python=3.10

# 激活环境
conda activate lip-reading

# 如果有 CUDA（更快）
conda install pytorch torchvision torchaudio pytorch-cuda=11.8 -c pytorch -c nvidia

# 如果没有 CUDA（仅 CPU）
conda install pytorch torchvision torchaudio cpuonly -c pytorch
```

### 3. 安装依赖

```bash
pip install -r requirements.txt
```

如果下载太慢，使用国内镜像：
```bash
pip install -r requirements.txt -i https://pypi.tsinghua.edu.cn/simple
```

### 4. 验证安装

```bash
python scripts/demo.py
```

应该看到 PyTorch 版本和 GPU 状态。

## 快速开始

### 1. 运行演示

```bash
python scripts/demo.py
```

输出示例：
```
============================================================
  唇语识别算法 - Lip Reading Algorithm Demo
============================================================

系统信息 (System Information):
  PyTorch 版本: 2.0.1
  GPU 可用: True
  GPU 数量: 1
  当前 GPU: NVIDIA GeForce RTX 3080

项目模块 (Project Modules):
  ✓ 数据处理模块 (Data Processing)
  ✓ 模型定义模块 (Model Definition)
  ✓ 训练模块 (Training)
  ✓ 推理模块 (Inference)
...
```

### 2. 训练模型

```bash
python experiments/train.py --config experiments/configs/default.yaml
```

输出示例：
```
✓ Model created with 50,123,456 parameters
✓ Config: exp_001
✓ Output directory: checkpoints/exp_001
```

### 3. 推理预测

```bash
python experiments/inference.py \
  --video_path your_video.mp4 \
  --model_path checkpoints/best_model.pth \
  --device cuda
```

## 配置文件详解

编辑 `experiments/configs/default.yaml` 修改超参数：

```yaml
# 数据配置
data:
  batch_size: 32          # 批次大小
  frame_size: 96          # 帧大小（96x96）
  num_workers: 4          # 数据加载工作线程

# 模型配置
model:
  hidden_dim: 512         # 隐藏维度
  num_layers: 4           # Transformer 层数
  num_heads: 8            # 多头注意力头数
  vocab_size: 1000        # 词汇表大小

# 训练配置
training:
  num_epochs: 100         # 训练轮数
  learning_rate: 0.001    # 学习率
  device: cuda            # 设备（cuda 或 cpu）
```

## 常见问题

### Q: 运行 `pip install -r requirements.txt` 找不到文件怎么办？

**A:** 确保你在项目根目录。使用 `ls requirements.txt`（Linux/Mac）或 `dir requirements.txt`（Windows）检查。

### Q: 如何使用 CPU 而不是 GPU？

**A:** 在 `experiments/configs/default.yaml` 中改为：
```yaml
training:
  device: cpu
```

### Q: PyTorch 安装失败怎么办？

**A:** 用 conda 安装（比 pip 更稳定）：
```bash
conda install pytorch torchvision torchaudio -c pytorch
```

### Q: 如何加载预训练模型？

**A:**
```python
from src.models import LipReaderModel
import torch

model = LipReaderModel()
checkpoint = torch.load('checkpoints/best_model.pth', map_location='cpu')
model.load_state_dict(checkpoint)
model.eval()
```

### Q: 训练太慢怎么办？

**A:**
- 增加 `batch_size`
- 增加 `num_workers`
- 确保使用 GPU（检查 `device: cuda`）
- 减少 `num_layers` 或 `hidden_dim`

### Q: 怎样运行单元测试？

**A:**
```bash
pytest tests/
```

## 数据准备

将你的唇语视频放在 `data/` 目录中：

```
data/
├── train/
│   ├── video1.mp4
│   ├── video2.mp4
│   └── ...
├── val/
│   └── ...
└── test/
    └── ...
```

## 项目结构

```
lip-reading-algorithm/
├── src/                      # 源代码
│   ├── __init__.py
│   ├── config.py            # 配置管理
│   ├── models/              # 模型定义
│   ├── data/                # 数据处理
│   ├── training/            # 训练逻辑
│   └── inference/           # 推理逻辑
├── experiments/             # 实验脚本
│   ├── train.py            # 训练脚本
│   ├── inference.py        # 推理脚本
│   └── configs/
│       └── default.yaml    # 默认配置
├── tests/                   # 单元测试
│   ├── __init__.py
│   └── test_models.py
├── docs/                    # 文档
│   ├── architecture.md     # 架构说明
│   └── usage_guide.md      # 本文件
├── scripts/                 # 工具脚本
│   └── demo.py             # 演示脚本
├── requirements.txt         # 依赖列表
├── setup.py                 # 安装脚本
└── README.md               # 项目说明
```

## 下一步

- 查看 README.md 了解项目概览
- 查看 docs/architecture.md 了解系统设计
- 查看代码注释了解 API 细节
- 修改 `experiments/configs/default.yaml` 进行实验

## 需要帮助？

- 检查代码注释和文档字符串
- 运行 `pytest tests/` 测试功能
- 查看示例脚本如何使用 API
