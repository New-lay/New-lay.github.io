---
layout: post
title: Paddle OCR Project
date: 2023-11-10 16:28 +0800
last_modified_at: 2023-11-10 16:28 +0800
tags: [OCR, Paddle]
toc:  true
---

PaddleOCR(飞桨OCR) github 开源
https://github.com/PaddlePaddle/PaddleOCR/blob/release/2.3/ppstructure/README_ch.md

PP-Structure是一个可用于复杂文档结构分析和处理的OCR工具包.

Install：

1: 安装PaddlePaddle：
pip3 install --upgrade pip
# GPU安装
python3 -m pip install paddlepaddle-gpu==2.1.1 -i https://mirror.baidu.com/pypi/simple
# CPU安装
 python3 -m pipinstall paddlepaddle==2.1.1 -i https://mirror.baidu.com/pypi/simple

更多GPU版本https://www.paddlepaddle.org.cn/install/quick

2: 安装Layout-Parser

pip3 install -U https://paddleocr.bj.bcebos.com/whl/layoutparser-0.0.0-py3-none-any.whl

依赖安装完成
安装PaddleOCR（PP-OCR， PP-Structure）

1: PIP快速安装PaddleOCRwhl包(仅预测)

pip install "paddleocr>=2.2" # 推荐使用2.2+版本

2: 完整克隆PaddleOCR源码(预测+训练)
gitclone https://github.com/PaddlePaddle/PaddleOCR


使用：
命令行使用：paddleocr--image_dir=../doc/table/1.png --type=structure

Python脚本使用：


离线模式clone整个github源码：
下载中文模型：
cd PaddleOCR/ppstructure

# 下载模型
mkdir inference && cd inference
# 下载PP-OCRv3文本检测模型并解压
wget https://paddleocr.bj.bcebos.com/PP-OCRv3/chinese/ch_PP-OCRv3_det_infer.tar && tar xf ch_PP-OCRv3_det_infer.tar
# 下载PP-OCRv3文本识别模型并解压
wget https://paddleocr.bj.bcebos.com/PP-OCRv3/chinese/ch_PP-OCRv3_rec_infer.tar && tar xf ch_PP-OCRv3_rec_infer.tar
# 下载PP-StructureV2中文表格识别模型并解压
wget https://paddleocr.bj.bcebos.com/ppstructure/models/slanet/ch_ppstructure_mobile_v2.0_SLANet_infer.tar && tar xf ch_ppstructure_mobile_v2.0_SLANet_infer.tar
cd ..




cd PaddleOCR/ppstructure

python3 table/predict_table.py --det_model_dir=path/to/det_model_dir--rec_model_dir=path/to/rec_model_dir --table_model_dir=path/to/table_model_dir--image_dir=../doc/table/1.png--rec_char_dict_path=../ppocr/utils/dict/table_dict.txt--table_char_dict_path=../ppocr/utils/dict/table_structure_dict.txt--rec_char_type=EN --det_limit_side_len=736 --det_limit_type=min --output../output/table


python table/predict_table.py \
   --det_model_dir=inference/ch_PP-OCRv3_det_infer \
   --rec_model_dir=inference/ch_PP-OCRv3_rec_infer  \
   --table_model_dir=inference/ch_ppstructure_mobile_v2.0_SLANet_infer \
   --rec_char_dict_path=../ppocr/utils/ppocr_keys_v1.txt \
   --table_char_dict_path=../ppocr/utils/dict/table_structure_dict_ch.txt \
   --image_dir=../doc/table/table.jpg \
   --output=../output/table



表格识别主要包含三个模型:
1.单行文本检测-DB
2.单行文本识别-CRNN
3.表格结构和cell坐标预测-SLANet
本地部署运行链接解释：
https://github.com/PaddlePaddle/PaddleOCR/blob/release/2.7/ppstructure/table/README_ch.md





-----
