# 自监督检测预训练的目标定位

## 环境要求
- PyTorch 1.6+
- Python 3.6+
- CUDA 10.1+
- GCC 4.9+
- NVCC 2+
- mmcv 0.6.1

## 预训练
sh tools/install.sh

## 训练
```
./tools/dist_train.sh ${CONFIG_FILE} ${GPU_NUM} --no-validate [optional arguments]
```
optional arguments:
- `--work_dir`: 输出文件路径
- `--resume_from`: 先前的checkpoint file

**Important**: 默认为4GPUs，bacth为32

使用8卡训练的示例为：
```
./tools/dist_train.sh configs/FPN/insloc_fpn_200ep.py 4 \
    --no-validate \
    --work-dir ckpt/insloc_fpn_200ep \
    --seed 0
```

## 预训练模型下载
| Arch | Pretrain Epoch | Link |
| :---: | :------: | :--------: |
| C4    | 200      | [link](https://drive.google.com/file/d/1bgrMLZjfRYaUeOptIw6WfrOnXjYm-ccg/view?usp=sharing) |
| C4    | 400      | [link](https://drive.google.com/file/d/1WDg-xAs1L3LcgXuzcY2uw4cbKtnXFl6q/view?usp=sharing) |
| FPN    | 200     | [link](https://drive.google.com/file/d/1MRfM6aZ-WSQANVOq8T-6IrukPQfZG5uP/view?usp=sharing) |
| FPN    | 400     | [link](https://drive.google.com/file/d/1XTfIWk_S0NyPubBMt4e5Ha5YU789w6bL/view?usp=sharing) |

## 实验结果

以下我们列出了R50-C4和R50-FPN检测模型在MSCOCO上的实验结果。

Mask R-CNN **R50-C4 1x**: 
| Methods | Epoch | Box AP | Mask AP |  
| :---: | :------: | :--------: | :------: | 
| MoCo-v2 | 200 | 38.9 | 34.1 | 
| MoCo-v2 | 800 | 39.3 | 34.3 | 
| InsLoc  | 200 | 39.5 | 34.5 | 
| InsLoc  | 400 | 39.8 | 34.7 | 

Mask R-CNN **R50-C4 2x**: 
| Methods | Epoch | Box AP | Mask AP | 
| :---: | :------: | :--------: | :------: | 
| MoCo-v2 | 200 | 40.7 | 35.6 | 
| MoCo-v2 | 800 | 41.2 | 35.8 | 
| InsLoc  | 200 | 41.4 | 35.9 | 
| InsLoc  | 400 | 41.8 | 36.3 | 

Mask R-CNN **R50-FPN 1x**: 
| Methods | Epoch | Box AP | Mask AP |  
| :---: | :------: | :--------: | :------: | 
| MoCo-v2 | 200 | 39.8 | 36.1 | 
| MoCo-v2 | 800 | 40.4 | 36.4 | 
| InsLoc  | 200 | 41.4 | 37.1 | 
| InsLoc  | 400 | 42.0 | 37.6 | 

Mask R-CNN **R50-FPN 2x**: 
| Methods | Epoch | Box AP | Mask AP |  
| :---: | :------: | :--------: | :------: |  
| MoCo-v2 | 200 | 41.7 | 37.6 | 
| MoCo-v2 | 800 | 42.5 | 38.2 | 
| InsLoc  | 200 | 43.2 | 38.7 | 
| InsLoc  | 400 | 43.3 | 38.8 | 

