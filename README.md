# Stereo Dense Matching Benchmark
This is the Github repository for the stereo dense matching benchmark hosted at [AI4GEO project](http://ai4geo.eu/index.php). 

## Introduction
For stereo dense matching, there are many famous benchmark dataset in Robust Vision, for example, [KITTI stereo](http://www.cvlibs.net/datasets/kitti/eval_scene_flow.php?benchmark=stereo) and [middlebury stereo](https://vision.middlebury.edu/stereo/).
With the development of machine learning, especially deep learning, these methods usually need a lot of training data(or ground truth). 
For photogrammetry community, as far as we know, it is not easy to find these training data. We will publish our data as ground truth. The data is produced from original image and LiDAR dataset.


### Vaihingen dataset(Aerial data)
This data set is from [ISPRS 3D reconstruction benchmark](https://www2.isprs.org/commissions/comm2/wg4/benchmark/).

|<img src="/figures/vaihingen_show.png" width="700" alt="Vaihingen dataset training and testing area" />|
|:--:| 
| *Vaihingen dataset training and testing area* |

The training and evluation is put: **/work/OT/ai4geo/users/tengw/stereodensematchingbenchmark/Vaihingen-stereo/(HAL platform)**.
The structure of the folder is :

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

|<img src="/vaihingen/10030060_10030061_0007_left.png" width="250"  alt="left image"  /> | <img src="/vaihingen/10030060_10030061_0007_right.png" width="250"  alt="right image" /> | <img src="/vaihingen/10030060_10030061_0007.png" width="250"  alt="disparity image" />|
| :---:        |     :---:     |          :---: |
| *left image* | *right image* | *disparity image* | 

In order to know the origin data, the file name is named from the origin image, "pair1_pair2_index.png". The index is start from 0.


## Feed Back
If you think you have any problem, contact Teng Wu <Teng.Wu@ign.fr>
