# SiamMaskUpdated
An updated version of SiamMask (CVPR2019) with slight changes to demo functionality, allowing for multiple ROIs and writing video outputs on Mac environment.
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
## Demo
- [Setup](#environment-setup) your environment
- Download the SiamMask model
```shell
cd $SiamMask/experiments/siammask_sharp
wget http://www.robots.ox.ac.uk/~qwang/SiamMask_VOT.pth
wget http://www.robots.ox.ac.uk/~qwang/SiamMask_DAVIS.pth
```
- Run `new-demo.py`

```shell
cd $SiamMask/experiments/siammask_sharp
export PYTHONPATH=$PWD:$PYTHONPATH
python ../../tools/new-demo.py --resume SiamMask_DAVIS.pth --config config_davis.json
(edit input file path if needed)
```

