This repo contains the **2nd solutions** on **BoostCamp AI_Tech** (2nd term) object detection competetion.  

## Contents
```
.
└── _base_
    ├── datasets
    ├── models
    │   └── Swin
    │       ├── swinB_cascade.py
    │       └── swinS_cascade_for_smallObjs.py
    └── schedules
```
`swinB_cascade.py`  
: It trains model on default dataset
- mAP50 0.677 (single model)
- mAP50 0.703 (k-fold CV ensembled)
- trains on a default dataset
- uses multi-scaled images [512 ~ 1024]
- default anchor ratios
- and default settings  

`swinS_cascade_for_smallObjs.py`  
: Focused on the small and medium objects.
- trains on a small & medium biased dataset
- uses expanded multi scales [800 ~ 1408]
- Anchor_ratios and anchor_scales focused on small and medium objects  

**Anchors**  
default anchors  
<img width="512" alt="image" src="https://user-images.githubusercontent.com/30382262/137625929-d0c31000-d794-4f34-b5e6-ec69692242fc.jpg">  
- the default anchor ratios are [0.5, 1.0, 2.0]  

customized anchors  
<img width="512" alt="image" src="https://user-images.githubusercontent.com/30382262/137625776-677e576f-6e52-45cb-af6a-c9a86ad79dc0.jpg">  
- the customized anchor ratios are [0.40, 0.70, 1.23, 2.00]  
  


## Requirements
**Libraries**
- Ubuntu 18.04 LTS
- Python 3.7.5
- PyTorch 1.7.1 <=
- mmdet 2.17.0  

**Hardware**
- GPU: 1 x NVIDIA Tesla V100 32G

## Train Models (GPU needed)
On a single GPU
```
python tools/train.py [path to swin*_cascade*.py]
```

On multiple GPUs
```
tools/dist_train.sh [path to swin*_cascade*.py] [number of GPUs]  
```  
## Datasets
**Default datatset**  
<img width="512" alt="image" src="https://user-images.githubusercontent.com/30382262/137625618-39656c65-ed13-42f0-8659-a3d7cd45f60c.jpg">  
[네이버 커넥트재단 - 재활용 쓰레기 데이터셋 / CC BY 2.0]
  
  
  
**[Custom] Pseudo Backgrounds**  
<img width="512" alt="image" src="https://user-images.githubusercontent.com/30382262/142757738-4bd35704-3590-455d-8fcc-f7932e22591f.png">
- 1. Execute **getBGpatches.py** to get Background patches(BG_patches) which will be used for make Pseudo Backgrounds.
- 2. Execute **makePseudoBG.py** to get Pseudo Backgrounds that comprised with BG_patches.
  
  

**[Custom]small & medium biased dataset**  
<img width="512" alt="image" src="https://user-images.githubusercontent.com/30382262/137625208-37fd84a5-fccb-42cb-9947-1660082fcd9e.png">  
[네이버 커넥트재단 - 재활용 쓰레기 데이터셋 / CC BY 2.0]  
- The criteria for small and medium of mmdetection are 0\~32 and 32\~96px, respectively.
  
  
## Performance in Customized model & dataset
<img width="512" alt="image" src="https://user-images.githubusercontent.com/30382262/137626551-32ef2425-62b1-4604-af3a-ca763f270a91.png">  
- Noticeable performance improvement was found in mAP_small.
<img width="512" alt="image" src="https://user-images.githubusercontent.com/30382262/142757063-33ec2cb9-2977-448d-aeca-3fbfaef50b89.jpg">  
- The performance of Cascade RCNN with SwinTransform is 0.704 on mAP50 metric.  

