# vfit-clothing
clothing experimentations 

## Getting Started
Python 3.6+, Pytorch 1.2, torchvision 0.4, cuda10.0, at least `3.8GB` GPU memory and other requirements.
All codes are tested on Linux Distributions (Ubutun 16.04 is recommended), and other platforms have not been tested yet.

### Environment installation
```
sudo apt-get update

sudo apt-get install python3.6
```
* please reference this [guide](https://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html) to install cuda

### Requirements
``` bash
git clone https://github.com/highend3d/vfit-clothing.git
cd vfit-clothing
pip install -r requirements.txt
```

### installation third party library
```bash
cd thirdparty/neural_renderer
python setup.py install
```

### Download resources.

Download `checkpoints` from [google dirve](https://drive.google.com/open?id=1orqAsSJjr2-AbwLJELp55E7-G91sXl5q) and move them to `outputs` directory.

### Running 
```
python run_swap.py --gpu_ids 0 --model imitator --output_dir ./outputs/results/  \
        --src_path      $SOURCE_IMAGE_PATH    \
        --tgt_path      TARGET_IMAGE_PATH    \
        --bg_ks 13  --ft_ks 3 \
        --has_detector  --post_tune  --front_warp --swap_part body

```

### Training Guide
```
chmod a+x scripts/train_iPER_Place2.sh
./scripts/train_iPER_Place2.sh
```
### Running Detail Guide
```

src_path="./assets/src_imgs/internet/men1_256.jpg"



gpu=0
name="imper_results"
checkpoints_dir="./outputs/checkpoints/"
output_dir="./outputs/results/"

## if use ImPer dataset trained model
#load_path="./outputs/checkpoints/lwb_imper/net_epoch_30_id_G.pth"

## if use ImPer and Place datasets trained model
#load_path="./outputs/checkpoints/lwb_imper_place/net_epoch_30_id_G.pth"

## if use ImPer, DeepFashion, and Place datasets trained model
load_path="./outputs/checkpoints/lwb_imper_fashion_place/net_epoch_30_id_G.pth"

## if use DeepFillv2 trained background inpainting network,
bg_model="./outputs/checkpoints/deepfillv2/net_epoch_50_id_G.pth"
## otherwise, it will use the BGNet in the original LiquidWarping GAN
#bg_model="ORIGINAL"

python run_swap.py --gpu_ids ${gpu} \
    --model imitator \
    --image_size 256 \
    --name ${name}  \
    --checkpoints_dir ${checkpoints_dir} \
    --bg_model ${bg_model}      \
    --load_path ${load_path}    \
    --output_dir ${output_dir}  \
    --src_path   ${src_path}    \
    --bg_ks 11 --ft_ks 3         \
    --has_detector  --post_tune  --front_warp --save_res  
```# vfit-clothing
