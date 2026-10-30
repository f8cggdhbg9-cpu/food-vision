# 食鉴 AI：食品图片分类 Demo

## 功能

- 上传一张 JPG/JPEG/PNG 图片；
- 或使用摄像头拍摄一张图片；
- 调用公开预训练的 FoodVision Big 模型；
- 展示 Top-1、Top-5、模型分数、推理耗时和 CPU/CUDA 设备。

模型仅覆盖 Food-101 的 101 类菜品。它不是通用包装食品识别器；输入范围之外的图片也可能被分到某个类别。

## 环境要求

建议 Python 3.10 或 3.11。需要能正常导入 PyTorch 和 TorchVision。CPU 即可运行，不要求 GPU；若有兼容 CUDA 环境则可使用 CUDA。

## 安装

在项目目录打开终端。

1. 检查现有 PyTorch/TorchVision：

```bash
python -c "import torch, torchvision; print(torch.__version__, torchvision.__version__, torch.cuda.is_available())"
```

2. 如果上述命令成功，先保留现有版本，不要为了本项目随意重装。然后安装其余依赖：

```bash
pip install -r requirements.txt
```

3. 如果检查命令失败，或运行时出现明确的 torch/torchvision 版本不兼容错误，请按官方安装选择器安装匹配版本：https://pytorch.org/get-started/locally/

## 启动

```bash
streamlit run app.py
```

按终端显示的本地地址打开网页。选择上传图片或摄像头拍照，预览图片后点击"识别食品"。

## 首次运行说明

模型文件已保存在 `foodvision_big/` 目录中，首次运行无需联网下载。摄像头输入需要浏览器授权。

## 代码文件

- `app.py`：Streamlit 页面和输入/输出交互；
- `model_service.py`：统一入口，根据 torchvision 版本自动选择后端；
- `model_service_torchvision_new.py`：后端（torchvision >= 0.13）；
- `model_service_torchvision_old.py`：后端（torchvision < 0.13，内置兼容层）；
- `foodvision_big/`：模型文件（model.py、model.safetensors、config.json）；
- `test_images/`：测试用图片；
- `test_model_service.py`：模型服务自测脚本；
- `requirements.txt`：依赖；
- `README.md`：运行说明。

## 模型来源与许可证

- 模型仓库：https://huggingface.co/shalev396/foodvision-big
- 仓库声明许可证：MIT。
- 本项目复用该仓库提供的模型结构、权重、预处理和类别配置；不包含训练过程。

## 注意事项

- 模型输出的分数不是经校准的真实概率。
- 模型作者在其模型卡中报告的指标不是本组实测结果。
- 若下载、加载或推理失败，应记录实际报错并据此排查，不要用固定示例结果替代真实预测。
