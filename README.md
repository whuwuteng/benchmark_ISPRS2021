# Aerial Stereo Dense Matching Benchmark

This is the Github repository for the stereo dense matching benchmark hosted at [AI4GEO project](http://ai4geo.eu/index.php). The dataset is also introduced in ISPRS 2021 congress paper "A new stereo dense matching benchmark dataset for deep learning".

## Introduction
For stereo dense matching, there are many famous benchmark dataset in Robust Vision, for example, [KITTI stereo](http://www.cvlibs.net/datasets/kitti/eval_scene_flow.php?benchmark=stereo) and [middlebury stereo](https://vision.middlebury.edu/stereo/).
With the development of machine learning, especially deep learning, these methods usually need a lot of training data(or ground truth). 
For photogrammetry community, as far as we know, it is not easy to find these training data. We will publish our data as ground truth. The data is produced from original image and LiDAR dataset. To be noticed, the image and LiDAR should be well-registered.


### Vaihingen dataset
This data set is from [ISPRS 3D reconstruction benchmark](https://www2.isprs.org/commissions/comm2/wg4/benchmark/).

|<img src="/figures/vaihingen_show.png" width="700" alt="Vaihingen dataset training and testing area" />|
|:--:|
| *Vaihingen dataset training and testing area* |

The training and evluation dataset is also provided, the structure of the folder is :

    .
    +
    ├── training                                # trainging 
    │   ├──10030060_10030061                    # pair 1
    │   │   ├─colored_0                         # left image folder
    │   │   │   ├─10030060_10030061_0000.png
    │   │   │   ├─10030060_10030061_0001.png
    │   │   │   └─ ... 
    │   │   ├─colored_1                         # right image folder
    │   │   │   ├─10030060_10030061_0000.png
    │   │   │   ├─10030060_10030061_0001.png
    │   │   │   └─ ...
    │   │   └─disp_occ                          # disparity image folder
    │   │       ├─10030060_10030061_0000.png
    │   │       ├─10030060_10030061_0001.png
    │   │       └─ ...
    │   ├──10030061_10030062                    # pair 2
    │   └── ...                                 # other folder
    └── testing                                 # testing 
        ├──10030062_10030063                    # pair 1
        │   ├─colored_0                         # left image folder
        │   │   ├─10030062_10030063_0000.png
        │   │   ├─10030062_10030063_0001.png
        │   │   └─ ...
        │   ├─colored_1                         # right image folder
        │   │   ├─10030062_10030063_0000.png
        │   │   ├─10030062_10030063_0001.png
        │   │   └─ ...
        │   └─disp_occ                          # disparity image folder
        │       ├─10030062_10030063_0000.png
        │       ├─10030062_10030063_0001.png
        │       └─ ...
        ├──10030062_10040084                    # pair 2
        └── ...                                 # other folder

For the training and testing dataset, the image data is **8bit RGB** image, and disparity is **16bit unsigned short** format. In disparity image, the value is scaled by **256**. The image size is **1024x1024**.

| <img src="/vaihingen/10030060_10030061_0007_left.png" width="250"  alt="left image" />  | <img src="/vaihingen/10030060_10030061_0007_right.png" width="250"  alt="right image" /> | <img src="/vaihingen/10030060_10030061_0007.png" width="250"  alt="disparity image" /> |
| :----------------------------------------------------------: | :----------------------------------------------------------: | :----------------------------------------------------------: |
|                         *left image*                         |                        *right image*                         |                      *disparity image*                       |

In order to know the origin data, the file name is named from the origin image, "pair1_pair2_index.png". 

### Data download

Training data is on [GoogleDrive](https://drive.google.com/file/d/1tXQ8qB2bS7JZz4wKmEzu0Qb0apPjOAr-/view?usp=sharing). There are *585* stereo pairs for the training dataset (1.8 Go). The folder structure is introduced above.


Testing data is on [GoogleDrive](https://drive.google.com/file/d/1tXQ8qB2bS7JZz4wKmEzu0Qb0apPjOAr-/view?usp=sharing). There are *507* stereo pairs for the testing dataset(1.5 Go). For the testing data, the ground truth disparity is not provided. 

For deep learning method, a training and valuation list file is also provide, the ratio of training image is ***80%***, and the ratio valuation image is ***20%*** of the training data. The relative directory is the current directory, and only the left image is listed, there are **468** in ***vaihingen_trainlist.txt***, and **117** in ***vaihingen_vallist.txt***, the order is after random, an example is shown:

```
10030060_10040082/colored_0/10030060_10040082_0005.png
10050103_10050104/colored_0/10050103_10050104_0037.png
10040081_10040082/colored_0/10040081_10040082_0021.png
10050105_10050106/colored_0/10050105_10050106_0032.png
10050104_10050105/colored_0/10050104_10050105_0033.png
10040082_10040083/colored_0/10040082_10040083_0000.png
...
```

In the training directory, the folder list ***train_folderlist.txt*** is also provided, it just let you know the stereo pair type of the image. For example, **10030060_10030061** is along flight strip, and **10030060_10040082** is across flight strip.

```
10030060_10030061
10030060_10040082
10030061_10030062
10030061_10040083
...
```

In the testing data folder, all the file is listed in ***vaihingen_test.txt***, The relative directory is the current directory, and only the left image is listed, the total number is **507**:

```
10030061_10030062/colored_0/10030061_10030062_0000.png
10030061_10030062/colored_0/10030061_10030062_0001.png
10030061_10030062/colored_0/10030061_10030062_0002.png
10030061_10030062/colored_0/10030061_10030062_0003.png
10030061_10030062/colored_0/10030061_10030062_0004.png
10030061_10030062/colored_0/10030061_10030062_0005.png
...
```
## Experiment

### Method

|   Method    |       Brief introduction        |                             Code                             |
| :---------: | :-----------------------------: | :----------------------------------------------------------: |
|   MICMAC    |       NCC based SGM(CPU)        | [(Pierrot-Deseilligny, Paparoditis, 2006)](https://github.com/micmacIGN/micmac) |
|  SGM (GPU)  |      census base SGM(GPU)       |             [(Hernandez-Juarez et al., 2016)]()              |
|  GraphCuts  | plane constraint base Graphcuts | [(Taniai et al., 2017)](https://github.com/t-taniai/LocalExpStereo) |
|    CBMV     |   random forest+SGM/Graphcuts   |   [(Batsos et al., 2018)](https://github.com/kbatsos/CBMV)   |
| DeepFeature |           2D CNN+SGM            | [(Luo et al., 2016)](https://bitbucket.org/saakuraa/cvpr16_stereo_public/src/master/) |
|   PSM net   |        end to end method        | [(Chang, Chen, 2018)](https://github.com/JiaRenChang/PSMNet) |
|   HRS net   |        end to end method        | [(Yang et al., 2019a)](https://github.com/gengshan-y/high-res-stereo) |
| DeepPruner  |        end to end method        | [(Duggal et al., 2019)](https://github.com/uber-research/DeepPruner) |

### Experiment setup

In the paper, because **HRS net** do not need valuation dataset, so all the training dataset is used for training in the experiment. 

### Training Model



To do list:

- [x] Method introduction
- [ ] Training Model
- [ ] Evaluation result table

## Acknowledge

### Citation

The dataset is introduced in the ISPRS 2021 congress paper, if you use this dataset, please cite our paper.

If you think you have any problem, contact [Teng Wu]<whuwuteng@gmail.com>

### Dataset

The Vaihingen data set was provided by the German Society for Photogrammetry, Remote Sensing 
and Geoinformation (DGPF) 

