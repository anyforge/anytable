# AnyTable

<a href="https://huggingface.co/oriforge/anytable" target="_blank"><img src="https://img.shields.io/badge/%F0%9F%A4%97-HuggingFace-blue"></a>
<a href="https://www.modelscope.cn/models/oriforge/table" target="_blank"><img alt="Static Badge" src="https://img.shields.io/badge/%E9%AD%94%E6%90%AD-ModelScope-blue"></a>
<a href=""><img src="https://img.shields.io/badge/Python->=3.6-aff.svg"></a>
<a href=""><img src="https://img.shields.io/badge/OS-Linux%2C%20Win%2C%20Mac-pink.svg"></a>
<a href=""><img alt="Static Badge" src="https://img.shields.io/badge/engine-cpu_gpu_onnxruntime-blue"></a>

```
    ___               ______      __    __   
   /   |  ____  __  _/_  __/___ _/ /_  / /__ 
  / /| | / __ \/ / / // / / __ `/ __ \/ / _ \
 / ___ |/ / / / /_/ // / / /_/ / /_/ / /  __/
/_/  |_/_/ /_/\__, //_/  \__,_/_.___/_/\___/ 
             /____/                          

```

简体中文 | [English](./README_en.md)

<div align="left">
    <img src="./assets/sample1.jpg">
</div>


## 1. 简介

AnyTable是一个专注于从文档或者图片中表格解析的模型工具，主要分成两个部分：
- anytable-det：用于表格区域检测（已开放）
- anytable-rec：用于表格结构识别（未来开放）

项目地址：
- github地址：[AnyTable](https://github.com/oriforge/anytable)
- Hugging Face: [AnyTable](https://huggingface.co/oriforge/anytable)
- ModelScope: [AnyTable](https://www.modelscope.cn/models/oriforge/anytable)

## 2. 缘起

目前市面上表格数据非常多且混杂，很难有一个干净的完整数据和模型，为此我们收集并整理了很多表格数据，训练了我们的模型。

检测数据集分布：

- pubtables: 947642
- synthtabnet.marketing: 149999
- tablebank: 278582
- fintabnet.c: 97475
- pubtabnet: 519030
- synthtabnet.sparse: 150000
- synthtabnet.fintabnet: 149999
- docbank: 24517
- synthtabnet.pubtabnet: 150000
- cTDaRTRACKA: 1639
- SciTSR: 14971
- doclaynet.large: 21185
- IIITAR13K: 9905
- selfbuilt: 121157

数据集总计：大于`2.6M`(大约2633869张图片)。

### 扩展训练

- 训练集：`2.6M（大于10万的部分只抽样了42000， 没办法因为贫穷，卡有限。）`
- 测试集：`4k`
- python: 3.12
- pytorch: 2.6.0
- cuda: 12.3
- ultralytics: 8.3.128

### 模型介绍

表格检测模型位于det文件夹下：
- yolo系列：使用ultralytics训练yolo检测
- rt-detr：使用ultralytics训练rt-detr检测

注释：您可以直接模型预测，也可以作为预训练模型微调私有数据集

### 评估

自建评估集：`4K`

| model | imgsz | epochs | metrics/precision |
|---|---|---|---|
|rt-detr-l|960|10|0.97|
|yolo11s|960|10|0.97|
|yolo11m|960|10|0.964|
|yolo12s|960|10|0.978|


## 3. 使用方法

### 安装依赖

```bash
pip install ultralytics pillow
```

### 使用方法

```python
## simple
## 下载模型后直接使用ultralytics即可

from ultralytics import YOLO,RTDETR

# Load a model
model = YOLO("/path/to/download_model")  # pretrained YOLO11n model

# Run batched inference on a list of images
results = model(["/path/to/your_image"],imgsz = 960)  # return a list of Results objects

# Process results list
for result in results:
    boxes = result.boxes  # Boxes object for bounding box outputs
    masks = result.masks  # Masks object for segmentation masks outputs
    keypoints = result.keypoints  # Keypoints object for pose outputs
    probs = result.probs  # Probs object for classification outputs
    obb = result.obb  # Oriented boxes object for OBB outputs
    result.show()  # display to screen
    result.save(filename="result.jpg")  # save to disk

```

## Buy me a coffee

- 微信(WeChat)

<div align="left">
    <img src="./zanshan.jpg" width="30%" height="30%">
</div>

## 特别鸣谢
- ultralytics公开的训练模型和文档
- 各种数据集提供者

## Star History

[![Star History Chart](https://api.star-history.com/svg?repos=oriforge/anytable&type=Date)](https://www.star-history.com/#oriforge/anytable&Date)
