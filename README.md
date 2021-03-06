

# Object Tracking with SiamMask
This is the project repository for CS585 final project#3 object tracking

Group Member: Lifu Zhang, Hin Lui Shum, Anjana Srivastava, Trivikram Ranga 


## Problem Definition
Object Tracking: taking an initial bounding box, creating a unique ID for each of the initial targets, and then tracking each of them as they move around frames in a video, maintaining the ID assignment.

## Method
1. Environment setup
2. Training SiamMask base model
3. Training SiamMask refine model

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
- select the best model as the final model, in our case checkpoint_19.pth
- 
## Results
1. Testing on DAVIS dataset
2. Recycling video demo

## Testing on Davis dataset
![Screen Shot 2021-04-27 at 1 13 13 PM](https://user-images.githubusercontent.com/36130616/116283983-8da18480-a75a-11eb-9a59-eb0fb96ca7b1.png)

## Recycling video demo

https://user-images.githubusercontent.com/36130616/116123990-b01b9b00-a691-11eb-9223-e92993bb2033.mov

- Run `new-demo.py`
```shell

cd $SiamMask/experiments/siammask_sharp
export PYTHONPATH=$PWD:$PYTHONPATH
python ../../tools/new-demo.py --resume SiamMask_DAVIS.pth --config config_davis.json
```

## Discussion
- SiamMask is a robust and powerful MOT model with the ability to produce accurate results with fast speed.
- SiamMask generates accurate mask, and simultaneously produce minimal enclosing rectangle as the bounding box.
- With reasonable amount of training time, we can achieve results that is comparable to that of pretrained model released by author.
- Model fails sometimes when the object being tracked does not have very distinct boundary or intersect with other objects.
- As a side effort, we made slight changes to allow multiple initial tracking objects (ROI) in tools/new-demo.py
