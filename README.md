# PYSKL

## Requirements
## My setup information

- A server with one Nvidia Tesla V100 GPU
- Operating system is Ubuntu 20
- Nvidia drivers version 455 installed with the Ubuntu package repositories "apt "
- Cuda version 11.10 installed with the Nvidia Cuda runfile installation method:
```https://developer.nvidia.com/cuda-11.1.0-download-archive?target_os=Linux&target_arch=x86_64&target_distro=Ubuntu&target_version=2004&target_type=debnetwork```
```Create Python 3.9 virtual env:
python3.9 -m venv PYSKL_venv
activate the virtual environment:
source PYSKL_venv/bin/activate
```
- Pytorch installation in this virtual environment
- Pytorch version 1.10 installed according to the Pytorch instructions for virtual env
```https://pytorch.org/get-started/previous-versions/#v1101```
The command used is: 
```pip install torch==1.10.0+cu111 torchvision==0.11.0+cu111 torchaudio==0.10.0 -f https://download.pytorch.org/whl/torch_stable.html```
- Install the Pythorn requirements from the new requirements.txt file in the root path of the repository.

## Below is the official ReadMe

[![PWC](https://img.shields.io/endpoint.svg?url=https://paperswithcode.com/badge/revisiting-skeleton-based-action-recognition/skeleton-based-action-recognition-on-ntu-rgbd)](https://paperswithcode.com/sota/skeleton-based-action-recognition-on-ntu-rgbd?p=revisiting-skeleton-based-action-recognition)
[![PWC](https://img.shields.io/endpoint.svg?url=https://paperswithcode.com/badge/dg-stgcn-dynamic-spatial-temporal-modeling/skeleton-based-action-recognition-on-ntu-rgbd-1)](https://paperswithcode.com/sota/skeleton-based-action-recognition-on-ntu-rgbd-1?p=dg-stgcn-dynamic-spatial-temporal-modeling)
[![PWC](https://img.shields.io/endpoint.svg?url=https://paperswithcode.com/badge/revisiting-skeleton-based-action-recognition/skeleton-based-action-recognition-on-kinetics)](https://paperswithcode.com/sota/skeleton-based-action-recognition-on-kinetics?p=revisiting-skeleton-based-action-recognition)
[[**Report**]](https://arxiv.org/abs/2205.09443)

PYSKL is a toolbox focusing on action recognition based on **SK**e**L**eton data with **PY**Torch. Various algorithms will be supported for skeleton-based action recognition. We build this project based on the OpenSource Project [MMAction2](https://github.com/open-mmlab/mmaction2).

This repo is the official implementation of [PoseConv3D](https://arxiv.org/abs/2104.13586) and [STGCN++](https://github.com/kennymckormick/pyskl/tree/main/configs/stgcn%2B%2B).

<div id="wrapper" align="center">
<figure>
  <img src="https://user-images.githubusercontent.com/34324155/123989146-2ecae680-d9fb-11eb-916b-b9db5563a9e5.gif" width="520px">&emsp;
  <img src="https://user-images.githubusercontent.com/34324155/218010909-ccfc89f0-9ed4-4b04-b38d-af7ffe49d2cd.gif" width="290px"><br>
  <p style="font-size:1.2vw;">Left: Skeleton-base Action Recognition Results on NTU-RGB+D-120; Right: CPU Realtime Skeleton-base Gesture Recognition Results</p>
</figure>
</div>

## Change Log

## Supported Algorithms

- [x] [DG-STGCN (Arxiv)](https://arxiv.org/abs/2210.05895) [[MODELZOO](/configs/dgstgcn/README.md)]
- [x] [ST-GCN (AAAI 2018)](https://arxiv.org/abs/1801.07455) [[MODELZOO](/configs/stgcn/README.md)]
- [x] [ST-GCN++ (ACMMM 2022)](https://arxiv.org/abs/2205.09443) [[MODELZOO](/configs/stgcn++/README.md)]
- [x] [PoseConv3D (CVPR 2022 Oral)](https://arxiv.org/abs/2104.13586) [[MODELZOO](/configs/posec3d/README.md)]
- [x] [AAGCN (TIP)](https://arxiv.org/abs/1912.06971) [[MODELZOO](/configs/aagcn/README.md)]
- [x] [MS-G3D (CVPR 2020 Oral)](https://arxiv.org/abs/2003.14111) [[MODELZOO](/configs/msg3d/README.md)]
- [x] [CTR-GCN (ICCV 2021)](https://arxiv.org/abs/2107.12213) [[MODELZOO](/configs/ctrgcn/README.md)]

## Supported Skeleton Datasets

- [x] [NTURGB+D (CVPR 2016)](https://arxiv.org/abs/1604.02808) and [NTURGB+D 120 (TPAMI 2019)](https://arxiv.org/abs/1905.04757)
- [x] [Kinetics 400 (CVPR 2017)](https://arxiv.org/abs/1705.06950)
- [x] [UCF101 (ArXiv 2012)](https://arxiv.org/pdf/1212.0402.pdf)
- [x] [HMDB51 (ICCV 2021)](https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=6126543)
- [x] [FineGYM (CVPR 2020)](https://arxiv.org/abs/2004.06704)
- [x] [Diving48 (ECCV 2018)](https://openaccess.thecvf.com/content_ECCV_2018/papers/Yingwei_Li_RESOUND_Towards_Action_ECCV_2018_paper.pdf)

## Installation
```shell
git clone https://github.com/kennymckormick/pyskl.git
cd pyskl
# This command runs well with conda 22.9.0, if you are running an early conda version and got some errors, try to update your conda first
conda env create -f pyskl.yaml
conda activate pyskl
pip install -e .
```

## Demo

Check [demo.md](/demo/demo.md).

## Data Preparation

We provide HRNet 2D skeletons for every dataset we supported and Kinect 3D skeletons for the NTURGB+D and NTURGB+D 120 dataset. To obtain the human skeleton annotations, you can:

1. Use our pre-processed skeleton annotations: we directly provide the processed skeleton data for all datasets as pickle files (which can be directly used for training and testing), check [Data Doc](/tools/data/README.md) for the download links and descriptions of the annotation format.
2. For NTURGB+D 3D skeletons, you can download the official annotations from https://github.com/shahroudy/NTURGB-D, and use our [provided script](/tools/data/ntu_preproc.py) to generate the processed pickle files. The generated files are the same with the provided `ntu60_3danno.pkl` and `ntu120_3danno.pkl`. For detailed instructions, follow the [Data Doc](/tools/data/README.md).
3. We also provide scripts to extract 2D HRNet skeletons from RGB videos, you can follow the [diving48_example](/examples/extract_diving48_skeleton/diving48_example.ipynb) to extract 2D skeletons from an arbitrary RGB video dataset.

You can use [vis_skeleton](/demo/vis_skeleton.ipynb) to visualize the provided skeleton data.

## Training & Testing

You can use following commands for training and testing. Basically, we support distributed training on a single server with multiple GPUs.
```shell
# Training
bash tools/dist_train.sh {config_name} {num_gpus} {other_options}
# Testing
bash tools/dist_test.sh {config_name} {checkpoint} {num_gpus} --out {output_file} --eval top_k_accuracy mean_class_accuracy
```
For specific examples, please go to the README for each specific algorithm we supported.

## Citation

If you use PYSKL in your research or wish to refer to the baseline results published in the Model Zoo, please use the following BibTeX entry and the BibTex entry corresponding to the specific algorithm you used.

```BibTeX
@inproceedings{duan2022pyskl,
  title={Pyskl: Towards good practices for skeleton action recognition},
  author={Duan, Haodong and Wang, Jiaqi and Chen, Kai and Lin, Dahua},
  booktitle={Proceedings of the 30th ACM International Conference on Multimedia},
  pages={7351--7354},
  year={2022}
}
```

## Contributing

PYSKL is an OpenSource Project under the Apache2 license. Any contribution from the community to improve PYSKL is appreciated. For **significant** contributions (like supporting a novel & important task), a corresponding part will be added to our updated tech report, while the contributor will also be added to the author list.

Any user can open a PR to contribute to PYSKL. The PR will be reviewed before being merged into the master branch. If you want to open a **large** PR in PYSKL, you are recommended to first reach me (via my email dhd.efz@gmail.com) to discuss the design, which helps to save large amounts of time in the reviewing stage.

## Contact

For any questions, feel free to contact: dhd.efz@gmail.com



