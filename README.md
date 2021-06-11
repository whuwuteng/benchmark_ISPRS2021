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

In order to know the origin data, the file name is named from the origin image, "pair1_pair2_index.png".  The image pair along the flight strip and across the fight strip are different, an example is shown here:


| <img src="/figures/10030062_10030063.png" width="500"  alt="disparity hist" /> | <img src="/figures/10030062_10040084.png" width="500"  alt="disparity hist" /> |
| :----------------------------------------------------------: | :----------------------------------------------------------: |
|             *dispairity histogram(along-strip)*              |             *dispairity histogram(across-strip)*             |

### Data download

Training data is on [GoogleDrive](https://drive.google.com/file/d/1tXQ8qB2bS7JZz4wKmEzu0Qb0apPjOAr-/view?usp=sharing). There are *585* stereo pairs for the training dataset (1.8 Go). The folder structure is introduced above.


Testing data is on [GoogleDrive](https://drive.google.com/file/d/15WFxVH9YJkP_ESqUW_QSm5uTc8MBHjwR/view?usp=sharing). There are *507* stereo pairs for the testing dataset (1.5 Go). For the testing data, the ground truth disparity is not provided. 

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

The disparity search range is an important parameter for stereo dense matching.
Some methods do not need this parameter, i.e., *MICMAC* and *DeepPruner*. In *SGM(GPU)*, the range is set to 128 and is dictated by the implementation. For other methods, it is set to 192.

For machine learning based methods, the training data and hyper-parameters impact significantly the results. For the Random Forest based method *CBMV*, 54 epipolar pairs are used for training. For deep learning based methods, all the training data is used. For the evaluation, all the testing data is used for all methods.

We decided to use the default batch size proposed in the implementation: 12 for *PSM net*, 28 for *HRS net* and 16 for *DeepPruner*. For the fine-tuning experiments on Vaihingen dataset,  the number of epochs is set as following: 20 for *DeepFeature*, 500 for *PSM net*, 700 for *HRS net* and 900 for *DeepPruner*.

### Training Model

#### CBMV

The [scikit-learn](https://scikit-learn.org/stable/install.html) version is important, the model is training on version 0.20.4, the model is on [GoogleDrive](https://drive.google.com/file/d/1sW3Ip22vYKvi0E03lNNFQc4ybtoUKfoj/view?usp=sharing). 

#### DeepFeature

DeepFeature method is based on Lua torch. The model is on [GoogleDrive](https://drive.google.com/file/d/1Pw_CyG5pmm8Vc0u55meyZ1REF9vSGNGJ/view?usp=sharing), the file should be unpacked.

#### PSM net

For PSM net, the code is base on Pytorch, the load method is same with the origin code. The model is on [GoogleDrive](https://drive.google.com/file/d/1RXYcpoBJimVUy7lxT1tNYWDh5IU_THPY/view?usp=sharing), the file can be directly loaded by the code.

#### HRS net

For HRS net, the code is base on Pytorch, the load method is same with the origin code. The model is on [GoogleDrive](https://drive.google.com/file/d/1_KG0_kWWdyL2vmYdgbiGc00mCjZbGaaV/view?usp=sharing),the file can be directly loaded by the code.

#### DeepPruner

For DeepPruner, the code is base on Pytorch, the load method is same with the origin code. The model is on [GoogleDrive](https://drive.google.com/file/d/1_KG0_kWWdyL2vmYdgbiGc00mCjZbGaaV/view?usp=sharing), the file can be directly loaded by the code.

### Evaluation result 

The 2,3 and 5 pixel error is used, the result is also list here:

|     Method      | 2-pixel error[%] | 3-pixel error[%] | 5-pixel error[%] |
| :-------------: | :--------------: | :--------------: | :--------------: |
|     MICMAC      |      67.169      |      74.283      |      81.429      |
|    SGM(GPU)     |      71.564      |      78.539      |      84.799      |
|    GraphCuts    |      71.704      |      76.404      |      80.951      |
|    CBMV(SGM)    |      74.941      |      80.540      |      85.342      |
| CBMV(GraphCuts) |      76.387      |      82.229      |      87.227      |
|   DeepFeature   |      78.265      |      83.982      |      88.878      |
|     PSM net     |    **84.065**    |    **88.324**    |    **92.395**    |
|     HRS net     |      79.135      |      85.243      |      91.238      |
|   DeepPruner    |      83.568      |      87.893      |      92.223      |

A figure shows from 0 to 10 pixel error:
| <img src="/figures/vaihingen_all.png" width="700" alt="Evaluation of pixel error on Vaihingen" /> |
| :----------------------------------------------------------: |
|           *Evaluation of pixel error on Vaihingen*           |

To do list:

- [x] Method introduction
- [x] Training Model
- [x] Evaluation result
- [ ] Evaluation method for other users(?)

## Acknowledge

### Dataset

The Vaihingen data set was provided by the German Society for Photogrammetry, Remote Sensing 
and Geoinformation (DGPF) 

### References

The methods in the experiment are listed here:

1. Pierrot-Deseilligny, M., & Paparoditis, N., 2006. A multiresolution and optimization-based image matching approach: An application to surface reconstruction from SPOT5-HRS stereo imagery. *Archives of Photogrammetry, Remote Sensing and Spatial Information Sciences*, *36*(1/W41), 1-5.
2. Hernandez-Juarez, D., Chacón, A., Espinosa, A., Vázquez, D., Moure, J. C., & López, A. M., 2016. Embedded real-time stereo estimation via semi-global matching on the GPU. Procedia Computer Science, 80, 143-153.
3. Taniai, T., Matsushita, Y., Sato, Y., Naemura, T., 2017. Continuous 3D label stereo matching using local expansion moves.IEEE transactions on pattern analysis and machine intelligence, 40(11), 2725–2739.
4. Batsos, K., Cai, C., Mordohai, P., 2018. Cbmv: A coalescedbidirectional matching volume for disparity estimation. Proceedings of the IEEE Conference on Computer Vision and Pattern Recognition, 2060–2069.
5. Luo, W., Schwing, A. G., Urtasun, R., 2016. Efficient deeplearning for stereo matching. Proceedings of the IEEE Conference on Computer Vision and Pattern Recognition, 5695–5703.
6. Chang, J.-R., Chen, Y.-S., 2018. Pyramid stereo matching network. Proceedings of the IEEE Conference on Computer Vision and Pattern Recognition, 5410–5418.
7. Yang, G., Manela, J., Happold, M., Ramanan, D., 2019. Hierarchical deep stereo matching on high-resolution images. Proceedings of the IEEE Conference on Computer Vision and Pattern Recognition, 5515–5524.
8. Duggal, S., Wang, S., Ma, W.-C., Hu, R., Urtasun, R., 2019. Deeppruner: Learning efficient stereo matching via differentiable patchmatch. Proceedings of the IEEE International Conference on Computer Vision, 4384–4393.

### Citation

The dataset is introduced in the ISPRS 2021 congress paper, if you use this dataset, please cite our paper.

If you think you have any problem, contact [Teng Wu]<whuwuteng@gmail.com>

