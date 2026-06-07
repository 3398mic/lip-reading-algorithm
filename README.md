# 唇语识别算法研究与软件设计

完整的唇语识别系统，包含模型、训练、推理等核心功能。

## 快速开始

```bash
# 1. 克隆项目
git clone https://github.com/3398mic/lip-reading-algorithm.git
cd lip-reading-algorithm

# 2. 创建虚拟环境
python -m venv venv
source venv/bin/activate  # Linux/Mac
# 或 venv\Scripts\activate  # Windows

# 3. 安装依赖
pip install -r requirements.txt

# 4. 运行演示
python scripts/demo.py

# 5. 训练模型
python experiments/train.py --config experiments/configs/default.yaml

# 6. 推理预测
python experiments/inference.py --video_path your_video.mp4 --model_path checkpoints/model.pth
```

## 项目结构

```
lip-reading-algorithm/
├── src/                 # 源代码
│   ├── models/         # 模型定义 (CNN + Transformer)
│   ├── data/           # 数据处理模块
│   ├── training/       # 训练模块
│   ├── inference/      # 推理模块
│   └── config.py       # 配置管理
├── experiments/        # 实验脚本
│   ├── train.py       # 训练脚本
│   ├── inference.py   # 推理脚本
│   └── configs/       # 配置文件
├── docs/              # 文档
├── tests/             # 单元测试
├── scripts/           # 工具脚本
├── requirements.txt   # 依赖列表
└── setup.py          # 安装脚本
```

## 核心特性

- 🎯 端到端唇语识别
- 🔄 Transformer 架构
- 📊 完整训练管道
- 🧪 单元测试覆盖
- 📚 详细文档说明

## 模型架构

```
视频输入 → CNN特征提取 → Transformer编码器 → Transformer解码器 → 文本输出
```

## 技术栈

- PyTorch 2.0+
- Transformer
- ResNet
- OpenCV
- YAML配置

## 许可证

MIT License
