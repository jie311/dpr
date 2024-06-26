# Patch-based Selection and Refinement for Early Object Detection ([WACV2024](https://arxiv.org/abs/2311.02274))

[![arXiv](https://img.shields.io/badge/arXiv-Paper-<COLOR>.svg)](https://arxiv.org/abs/2311.02274)

## Abstract
Early object detection (OD) is a crucial task for the safety of many dynamic systems. Current OD algorithms have limited success for small objects at a long distance. To improve the accuracy and efficiency of such a task, we propose a novel set of algorithms that divide the image into patches, select patches with objects at various scales, elaborate the details of a small object, and detect it as early as possible. Our approach is built upon a transformer-based network and integrates the diffusion model to improve the detection accuracy. As demonstrated on BDD100K, our algorithms enhance the mAP for small objects from 1.03 to 8.93, and reduce the data volume in computation by more than 77\%.

![image](https://github.com/destiny301/dpr/blob/main/flowchart.png)

## Updates
*03/01/2024*

1. Published version: [Open Access](https://openaccess.thecvf.com/content/WACV2024/html/Zhang_Patch-Based_Selection_and_Refinement_for_Early_Object_Detection_WACV_2024_paper.html)

*11/21/2023*

<img src="https://github.com/destiny301/dpr/blob/main/ps_module.png" width="400">
<!-- ![image](https://github.com/destiny301/dpr/blob/main/ps_module.png | width=100) -->

1. Patch-Selector module code is released.

2. For Patch-Refiner module, please refer to [SR3](https://github.com/Janspiry/Image-Super-Resolution-via-Iterative-Refinement).

## Simple Start
1. Prepare the data as the following structure:
```shell
root/
├──images/
│  ├── train/
│  │   ├── 000001.jpg
│  │   ├── 000002.jpg
│  │   ├── ......
│  ├── ......
├──masks/
│  ├── val/
│  │   ├── 000001.png
│  │   ├── 000002.png
│  │   ├── ......
```
For your own datasets, the selection masks (binary masks) can be generated with object detection (OD) labels or instance segmentation labels.
For OD, you need to stack all the bounding boxes together, and set the object pixels to 1, and the background pixels to 0.
For segmentation labels, you can simply set all non-zero values to 1.

2. Split the input images into patches, and select the object-containing patches with this repo. Note, you can adjust the threshold (i.e. args.th) to get a higher TPR, which make sure less information loss.

3. Leverage the diffusion models [SR3](https://github.com/Janspiry/Image-Super-Resolution-via-Iterative-Refinement) to scale selected patches up. For your own datasets, you need to download the pretrained model and finetune it as the repo illustrates.

4. For the downstream tasks (eg. OD), you can directly input the upscaled patches, or simply interpolate non-selected patches with bilinear interpolation and group all patches together as the original images, then input the re-grouped images.
Note, you also need to adjust the labels for the downstream tasks to match the input patches or re-grouped images.

## Citation
If you use DPR in your research or wish to refer to the results published here, please use the following BibTeX entry. Sincerely appreciate it!
```shell
@inproceedings{zhang2024patch,
  title={Patch-based Selection and Refinement for Early Object Detection},
  author={Zhang, Tianyi and Kasichainula, Kishore and Zhuo, Yaoxin and Li, Baoxin and Seo, Jae-Sun and Cao, Yu},
  booktitle={Proceedings of the IEEE/CVF Winter Conference on Applications of Computer Vision},
  pages={729--738},
  year={2024}
}
```
