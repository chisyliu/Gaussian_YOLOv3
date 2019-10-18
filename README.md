# Gaussian YOLOv3: An Accurate and Fast Object Detector Using Localization Uncertainty for Autonomous Driving
This repository contains the code for our **ICCV 2019** [Paper](https://arxiv.org/abs/1904.04620)

<img src="https://user-images.githubusercontent.com/56669525/67031779-37a75600-f14d-11e9-812c-aa14fd646400.png" width="100%">

*The provided weight file ("[Gaussian_yolov3_BDD.weights](https://drive.google.com/open?id=1Eutnens-3z6o4LYe0PZXJ1VYNwcZ6-2Y)") is not the weight file used in the paper, but newly trained weight for release code validation. Because this weight file is more accurate than the weight used in the paper, we provide this file in the repository.*

Citation
--------
**We will present on October 29, 2019.**
```
@InProceedings{Choi_2019_ICCV,
author = {Choi, Jiwoong and Chun, Dayoung and Kim, Hyun and Lee, Hyuk-Jae},
title = {Gaussian YOLOv3: An Accurate and Fast Object Detector Using Localization Uncertainty for Autonomous Driving},
booktitle = {The IEEE International Conference on Computer Vision (ICCV)},
month = {Oct},
year = {2019}
}
```

Requirements
----------------------
The code was tested on 

`Ubuntu 16.04, NVIDIA GTX 1080 Ti with CUDA 8.0 and cuDNNv7, OpenCV 3.4.0`

`Ubuntu 16.04, NVIDIA Titan Xp with CUDA 9.0 and cuDNNv7, OpenCV 3.3.0`


Setup
------
Please see the YOLOv3 website instructions [setup](https://pjreddie.com/darknet/yolo/)


Dataset
-------
We tested our algorithm using Berkeley deep drive (BDD) dataset.

If you want to use BDD dataset, please see [BDD website](https://bdd-data.berkeley.edu/) and download the dataset.

Training
--------
For training, you must make image list file (*e.g.,* "train_bdd_list.txt") and ground-truth data. Please see these websites: [YOLOv3](https://pjreddie.com/darknet/yolo/), [How to train YOLO](https://timebutt.github.io/static/how-to-train-yolov2-to-detect-custom-objects/)

`List files ("train_bdd_list.txt", "val_bdd_list.txt", "test_bdd_list.txt") in the repository are an example. You must modify the directory of the file name in the list to match the path where the dataset is located on your computer.`

Download pre-trained weights [darknet53.conv.74](http://pjreddie.com/media/files/darknet53.conv.74)

Compile the code
```Swift
make
```

Start training by using the command line
```Swift
./darknet detector train cfg/BDD.data cfg/Gaussian_yolov3_BDD.cfg darknet53.conv.74
```
If you want to use multiple gpus,
```Swift
./darknet detector train cfg/BDD.data cfg/Gaussian_yolov3_BDD.cfg darknet53.conv.74 -gpus 0,1,2,3
```

Inference
---------
Download the Gaussian_YOLOv3 example weight file. [Gaussian_yolov3_BDD.weights](https://drive.google.com/open?id=1Eutnens-3z6o4LYe0PZXJ1VYNwcZ6-2Y)

Run the following commands.
1. `make`
2. `./darknet detector test cfg/BDD.data cfg/Gaussian_yolov3_BDD.cfg Gaussian_yolov3_BDD.weights data/example.jpg`

You can see the result:

<img src="https://user-images.githubusercontent.com/56669525/67030475-7091fb80-f14a-11e9-8eeb-e71a8f3b4ee2.jpg" width="80%">

Evaluation
----------
Download the Gaussian_YOLOv3 example weight file. [Gaussian_yolov3_BDD.weights](https://drive.google.com/open?id=1Eutnens-3z6o4LYe0PZXJ1VYNwcZ6-2Y)

Run the following commands. You can get a detection speed of more than 42 FPS.
1. `make`

2. `./darknet detector valid cfg/BDD.data cfg/Gaussian_yolov3_BDD.cfg Gaussian_yolov3_BDD.weights`

3. `cd bdd_evaluation/`

4. `python evaluate.py det gt_bdd_val.json ../results/bdd_results.json`

You will get:
```
AP : 9.45 (bike)
AP : 40.28 (bus)
AP : 40.56 (car)
AP : 8.66 (motor)
AP : 16.85 (person)
AP : 10.59 (rider)
AP : 7.91 (traffic light)
AP : 23.15 (traffic sign)
AP : 0.00 (train)
AP : 40.28 (truck)
[9.448295420802772, 40.28022967768842, 40.562338308273596, 8.658317480713093, 16.85103955706777, 10.588396343004272, 7.914563796458698, 23.147189144825003, 0.0, 40.27786994583501] 

9.45 40.28 40.56 8.66 16.85 10.59 7.91 23.15 0.00 40.28

mAP 19.77 (512 x 512 input resolution)
```

If you want to get the mAP for BDD test set, 
1. `make`
2. `Change the list file in cfg file ("val_bdd_list.txt" --> "test_bdd_list.txt" in "cfg/BDD.data")`
3. `./darknet detector valid cfg/BDD.data cfg/Gaussian_yolov3_BDD.cfg Gaussian_yolov3_BDD.weights`
4. `Upload result file ("results/bdd_results.json") on BDD evaluation server` [Link](https://bdd-data.berkeley.edu/portal.html)

On the BDD test set, we got 19.2 mAP (512 x 512 input resolution).


Contact
-------
For questions about our paper or code, please contact Jiwoong Choi. 

<jwchoi384@gmail.com>