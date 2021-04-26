

# SiamMaskUpdated
An updated version of SiamMask (CVPR2019) with slight changes to demo functionality, allowing for multiple ROIs

## Problem Definition
Object Tracking: taking an initial bounding box, creating a unique ID for each of the initial targets, and then tracking each of them as they move around frames in a video, maintaining the ID assignment.

## Method
- Environment setup
- Training base model
- Training refine model
- Testing on DAVIS 2016
- Recycling video demo
## Environment setup
This code has been tested on MacOS

- Clone the repository 
```
git clone https://github.com/lifuzhang1108/SiamMaskUpdated.git && cd SiamMaskUpdated
export SiamMask=$PWD
```
- Create Virtual Environment
```
pip install virtualenv
virtualenv --python=python3.6 .venv
source .venv/bin/activate
pip install -r requirements.txt
pip install pathos
pip install imageai==2.0.2
pip install Keras==2.2.5
pip install tensorflow==1.15
bash make.sh
```
- Add the project to your PYTHONPATH
```
export PYTHONPATH=$PWD:$PYTHONPATH
```
- Add Pretrained Resnet
```
Download from https://github.com/OlafenwaMoses/ImageAI/releases/download/1.0/resnet50_coco_best_v2.0.1.h5
add under SiamMaskUpdated/experiments/siammask_sharp
```
## Training base model
- Download the [Youtube-VOS](https://youtube-vos.org/dataset/download/), 
[COCO](http://cocodataset.org/#download), 
[ImageNet-DET](http://image-net.org/challenges/LSVRC/2015/), 
and [ImageNet-VID](http://image-net.org/challenges/LSVRC/2015/).
- Preprocess each datasets according the [readme](data/coco/readme.md) files.
- Download the pre-trained resnet model (174 MB)
- we trained for 17 epoches on 4 GPUs for 10 hours

## Training Refine module
- In the experiment file, train with the best SiamMask base model checkpoint_16.pth
- we trained for 19 epoches on 4 GPUs for 12 hours

## Testing on Davis

## Recycling video demo

https://user-images.githubusercontent.com/36130616/116123990-b01b9b00-a691-11eb-9223-e92993bb2033.mov

- Run `new-demo.py`
```shell

cd $SiamMask/experiments/siammask_sharp
export PYTHONPATH=$PWD:$PYTHONPATH
python ../../tools/new-demo.py --resume SiamMask_DAVIS.pth --config config_davis.json
```

