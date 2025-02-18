# Pix2Pix: Image-to-Image Translation with Conditional Adversarial Networks

## Introduction

<!-- [ALGORITHM] -->

<details>
<summary align="right"><a href="https://openaccess.thecvf.com/content_cvpr_2017/html/Isola_Image-To-Image_Translation_With_CVPR_2017_paper.html">Pix2Pix (CVPR'2017)</a></summary>

```bibtex
@inproceedings{isola2017image,
  title={Image-to-image translation with conditional adversarial networks},
  author={Isola, Phillip and Zhu, Jun-Yan and Zhou, Tinghui and Efros, Alexei A},
  booktitle={Proceedings of the IEEE conference on computer vision and pattern recognition},
  pages={1125--1134},
  year={2017},
  url={https://openaccess.thecvf.com/content_cvpr_2017/html/Isola_Image-To-Image_Translation_With_CVPR_2017_paper.html},
}
```
</details>

## Results and Models
<div align="center">
  <b> Results from Pix2Pix trained by MMGeneration</b>
  <br/>
  <img src="https://user-images.githubusercontent.com/22982797/114269080-4ff0ec00-9a37-11eb-92c4-1525864e0307.PNG" width="800"/>
</div>
We use `FID` and `IS` metrics to evaluate the generation performance of pix2pix.<sup>1</sup>

| Models |   Dataset   |   FID    |  IS   |                                                                     Config                                                                      |                                                                                                                     Download                                                                                                                     |
| :----: | :---------: | :------: | :---: | :---------------------------------------------------------------------------------------------------------------------------------------------: | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
|  Ours  |   facades   | 124.9773 | 1.620 |           [config](https://github.com/open-mmlab/mmgeneration/tree/master/configs/pix2pix/pix2pix_vanilla_unet_bn_facades_b1x1_80k.py)           |                [model](https://download.openmmlab.com/mmgen/pix2pix/refactor/pix2pix_vanilla_unet_bn_1x1_80k_facades_20210902_170442-c0958d50.pth?versionId=CAEQMhiBgICb8fTj3RciIGU2NmViM2QyYzJkODQ0MDBhYTFhMGE2YzNmMTA0ODk3)   \| [log](https://download.openmmlab.com/mmgen/pix2pix/pix2pix_vanilla_unet_bn_1x1_80k_facades_20210317_172625.log.json)<sup>2</sup>
|  Ours  | aerial2maps | 122.5856 | 3.137 |        [config](https://github.com/open-mmlab/mmgeneration/tree/master/configs/pix2pix/pix2pix_vanilla_unet_bn_aerial2maps_b1x1_220k.py)         |          [model](https://download.openmmlab.com/mmgen/pix2pix/refactor/pix2pix_vanilla_unet_bn_a2b_1x1_219200_maps_convert-bgr_20210902_170729-59a31517.pth?versionId=CAEQMhiBgICH9vTj3RciIDdiNGRmYTNlZjhlMjQ0ODc4OTJiOGEzMjY0YTJlZmQ5)          |
|  Ours  | maps2aerial | 88.4635  | 3.310 |        [config](https://github.com/open-mmlab/mmgeneration/tree/master/configs/pix2pix/pix2pix_vanilla_unet_bn_maps2aerial_b1x1_220k.py)         |          [model](https://download.openmmlab.com/mmgen/pix2pix/refactor/pix2pix_vanilla_unet_bn_b2a_1x1_219200_maps_convert-bgr_20210902_170814-6d2eac4a.pth?versionId=CAEQMhiBgMC08PTj3RciIGE4ODVkZWU0MTYyMTQ0MWJhZjE0YThmY2M2NDJmZjNi)          |
|  Ours  | edges2shoes | 84.3750  | 2.815 | [config](https://github.com/open-mmlab/mmgeneration/tree/master/configs/pix2pix/pix2pix_vanilla_unet_bn_wo_jitter_flip_edges2shoes_b1x4_190k.py) | [model](https://download.openmmlab.com/mmgen/pix2pix/refactor/pix2pix_vanilla_unet_bn_wo_jitter_flip_1x4_186840_edges2shoes_convert-bgr_20210902_170902-0c828552.pth?versionId=CAEQMhiBgIC57vTj3RciIGZlNmQ4ZDJhN2E1MDQ5ZmJiOWJmYTY5MDg1ZTc0N2Vi) |


`FID` comparison with official:

| Dataset  |   facades   | aerial2maps  | maps2aerial | edges2shoes |   average    |
| :------: | :---------: | :----------: | :---------: | :---------: | :----------: |
| official | **119.135** |   149.731    |   102.072   | **75.774**  |   111.678    |
|   ours   |  124.9773   | **122.5856** | **88.4635** |   84.3750   | **105.1003** |

`IS` comparison with official:

| Dataset  |  facades  | aerial2maps | maps2aerial | edges2shoes |  average   |
| :------: | :-------: | :---------: | :---------: | :---------: | :--------: |
| official | **1.650** |    2.529    |  **3.552**  |    2.766    |   2.624    |
|   ours   |   1.620   |  **3.137**  |    3.310    |  **2.815**  | **2.7205** |

Note:
1. we strictly follow the [paper](http://openaccess.thecvf.com/content_cvpr_2017/papers/Isola_Image-To-Image_Translation_With_CVPR_2017_paper.pdf) setting in Section 3.3: "*At inference time, we run the generator net in exactly
the same manner as during the training phase. This differs
from the usual protocol in that we apply dropout at test time,
and we apply batch normalization using the statistics of
the test batch, rather than aggregated statistics of the training batch.*" (i.e., use model.train() mode), thus may lead to slightly different inference results every time.
2. This is the training log before refactoring. Updated logs will be released soon.
