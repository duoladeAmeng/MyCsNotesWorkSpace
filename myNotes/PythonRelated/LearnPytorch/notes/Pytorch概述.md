# 什么是Pytorch

官网：[PyTorch官网](https://pytorch.org/)

PyTorch 是一个开源的深度学习框架，由 Facebook 的人工智能研究团队（FAIR）开发。

它以 **动态计算图**（Dynamic Computation Graph）为核心特性，广泛用于科研、教育和工业界。

PyTorch 是一个开源的深度学习框架，旨在为研究提供灵活性和模块化，同时具备生产部署所需的稳定性和支持。

PyTorch 是一个开源的机器学习框架，它加速了从研究原型到生产部署的路径。

其设计旨在提供最大的灵活性和速度，支持动态计算图，使研究人员和开发者能够快速直观地进行迭代。

其 Python 风格的设计以及与原生 Python 工具的深度集成，使其成为一个易于使用且强大的平台，用于大规模构建和训练深度学习模型。

PyTorch 在学术界和工业界广泛采用，已成为前沿研究和商业人工智能应用的首选框架。它支持广泛的应用场景——从自然语言处理和计算机视觉到强化学习和生成式人工智能——通过其强大的库、工具和集成生态系统。

PyTorch 还针对 CPU、GPU 和定制硬件加速器进行了性能优化，包括对分布式训练和云平台及移动设备部署的支持。

# Pytorch的组成

PyTorch 由多个核心模块组成，各模块分工明确，协同工作，构成了完整的深度学习生态系统。

---

## 🧱 PyTorch 的主要组成部分

### 1. Torch
这是 PyTorch 的基础库，提供了张量（Tensor）操作、数学运算、自动求导等底层功能。

- `torch.Tensor`：多维数组，类似于 NumPy 的 ndarray，但支持 GPU 加速。
- `torch.cuda`：提供 GPU 张量的支持，加速深度学习训练。
- `torch.nn`：神经网络模块，包含各种层（如线性层、卷积层）、损失函数、激活函数等。
- `torch.optim`：优化器模块，如 SGD、Adam 等。
- `torch.autograd`：自动微分引擎，实现反向传播。
- `torch.utils`：工具类模块，例如数据加载器 `DataLoader` 和数据集封装 `Dataset`。

---

### 2. TorchVision
是 PyTorch 的计算机视觉扩展库，专注于图像相关的任务。

- 提供常用的数据集（如 CIFAR、MNIST、ImageNet）
- 预定义模型（如 ResNet、VGG、YOLO 等）
- 图像变换（`transforms`）：对图像进行标准化、裁剪、旋转等预处理
- 目标检测、语义分割相关工具

```bash
pip install torchvision
```

---

### 3. TorchText
专为自然语言处理（NLP）设计的扩展库。

- 提供常见 NLP 数据集（如 IMDB、AG News、WikiText）
- 文本处理工具（如 Tokenizer、Vocab、Field）

> ⚠️ 注意：从 PyTorch 1.8 开始，TorchText 正在逐步被整合到 HuggingFace 或其他生态中，但仍可使用。

---

### 4. TorchAudio
音频处理扩展库，适用于语音识别、音频分类等任务。

- 支持音频文件读写（WAV, MP3 等）
- 提供音频模型（如 Wav2Vec2）
- 音频信号处理函数（滤波、特征提取等）

---

### 5. TorchScript（torch.jit）
用于将 PyTorch 模型转换为序列化的脚本格式，便于在非 Python 环境中运行（如 C++、移动端）。

- 支持 JIT 编译
- 提供 `script()` 和 `trace()` 两种方式将模型转为 TorchScript 格式

---

### 6. Distributed（torch.distributed）
支持分布式训练，包括多 GPU 和多节点训练。

- 提供通信原语（如 all_reduce、broadcast）
- 支持多种后端（如 NCCL、Gloo、MPI）
- 可配合 DDP（DistributedDataParallel）实现高效并行训练

---

### 7. Profiler（torch.profiler）
性能分析工具，帮助开发者分析模型运行时的资源消耗情况。

- 查看每个操作的耗时、内存占用
- 支持 TensorBoard 可视化

---

### 8. ONNX（torch.onnx）
PyTorch 支持将模型导出为 ONNX 格式，便于跨平台迁移（如导入到 TensorFlow、Caffe、TensorRT 中）。

```python
torch.onnx.export(model, dummy_input, "model.onnx")
```

---

## ✅ 总结表格

| 组件          | 功能                                     |
| ------------- | ---------------------------------------- |
| `torch`       | 核心库，提供张量、自动求导、神经网络模块 |
| `torchvision` | 计算机视觉相关，图像数据集和模型         |
| `torchtext`   | 自然语言处理相关                         |
| `torchaudio`  | 音频处理相关                             |
| `torchscript` | 模型序列化与跨平台部署                   |
| `distributed` | 分布式训练支持                           |
| `profiler`    | 性能分析工具                             |
| `onnx`        | 模型导出为通用格式                       |

# 安装

## 步骤 1: 确认环境

需要明确以下几点：

1. 操作系统 (OS)：Windows, macOS, 还是 Linux?

2. 包管理器 (Package Manager)：习惯使用`pip`还是`conda`？

3. - **Conda**：强烈推荐。Conda 不仅能管理 Python 包，还能管理 Python 解释器本身和复杂的非 Python 依赖（如 CUDA 工具包），可以创建隔离的环境，避免版本冲突。
   - **Pip**：Python 官方的包管理器，如果你不打算使用 GPU 或能自行管理好 CUDA 环境，Pip 也是一个不错的选择。

4. 硬件 (Compute Platform)：打算只使用 CPU 还是利用 NVIDIA GPU 进行加速？

5. - **CPU**：所有电脑都支持。
   - **GPU (CUDA)**：如果有 NVIDIA 显卡，并且想利用它来加速训练，就需要安装支持 CUDA 的 PyTorch 版本。需要先确认显卡驱动和 CUDA Toolkit 版本。可以在终端（或 Windows 的 cmd/PowerShell）中输入 `nvidia-smi` 命令来查看。

## 步骤 2: 执行安装命令

**强烈建议**在一个新的虚拟环境中安装 PyTorch，以避免与系统中其他 Python 包冲突。

```
# 1. 创建一个新的 conda 环境 (例如，名为 'pytorch_env')，并指定 Python 版本
conda create -n pytorch_env python=3.9

# 2. 激活这个新环境
conda activate pytorch_env
```

### 有GPU

```shell
conda install pytorch torchvision torchaudio pytorch-cuda=11.8 -c pytorch -c nvidia
```

`pytorch-cuda`的值(即NVIDIA 驱动支持的 CUDA 版本)在终端（或 Windows 的 cmd/PowerShell）中输入 `nvidia-smi` 命令来查看：

1. 打开终端（Linux/macOS）或命令提示符（Windows）

2. 运行以下命令：

   ```shell
   nvidia-smi
   ```

   输出示例：

   ```shell
   +-----------------------------------------------------------------------------+
   | NVIDIA-SMI 515.65.01    Driver Version: 515.65.01    CUDA Version: 11.7     |
   |-------------------------------+----------------------+----------------------+
   | GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
   | Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
   |                               |                      |               MIG M. |
   |===============================+======================+======================|
   |   0  NVIDIA GeForce ...  On   | 00000000:01:00.0  On |                  N/A |
   | 30%   45C    P8    10W / 250W |    123MiB / 12288MiB |      0%      Default |
   |                               |                      |                  N/A |
   +-------------------------------+----------------------+----------------------+
   ```

   - **`CUDA Version: 11.7`** 表示的 **驱动支持的最高 CUDA 版本**。

### 无GPU

```shell
conda install pytorch torchvision torchaudio cpuonly -c pytorch
```

## 步骤 3: 验证安装

安装完成后，在你的终端（确保虚拟环境已激活）中启动 Python 解释器，然后输入以下代码：

```
import torch

# 1. 打印 PyTorch 版本
print(f"PyTorch Version: {torch.__version__}")

# 2. 检查一个张量是否可以被创建
x = torch.rand(5, 3)
print(x)

# 3. (关键) 检查 CUDA 是否可用
is_cuda_available = torch.cuda.is_available()
print(f"CUDA Available: {is_cuda_available}")

if is_cuda_available:
    # 4. 打印 CUDA 版本
    print(f"CUDA Version: {torch.version.cuda}")
    # 5. 打印 GPU 数量
    print(f"GPU Count: {torch.cuda.device_count()}")
    # 6. 打印当前 GPU 名称
    print(f"GPU Name: {torch.cuda.get_device_name(0)}")
```

如果以上代码都能顺利运行，并且 `CUDA Available` 的状态符合预期，那么PyTorch 已经成功安装！