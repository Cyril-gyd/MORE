# MORE: Learning Motion-Oriented Registers for Driving World Models and Planning

[[Paper](https://openreview.net/forum?id=WcveyOpJGj)] [[Code](https://github.com/Cyril-gyd/MORE)]

---

## 🚧 Code and Models

We are preparing the code, training configurations, pretrained models, and evaluation tools for public release. The repository will be updated progressively. Stay tuned!

## Overview

**MORE** is a V-JEPA framework that learns **M**otion-**O**riented **RE**gisters during video pretraining as a compact state interface for driving world models and planning. It addresses the *state-interface mismatch* between dense visual representations learned during pretraining and the motion-sensitive, predictive states required by downstream world models and planners.

During pretraining, MORE injects temporally aligned ego motion into a small set of register tokens. Masked patch representations are predicted exclusively through these registers, routing dense visual supervision through a compact state bottleneck. A complementary blockwise register-masking objective further encourages predictive structure in the learned state space. During downstream training, the same register space is reused for non-autoregressive future-state prediction, trajectory generation, and trajectory scoring.

<p align="center">
  <img src="assets/pipeline.png" alt="Overview of the MORE framework" width="100%">
</p>

<p align="center">
  <em>MORE learns motion-oriented registers during video pretraining and reuses the same compact state space for world modeling and trajectory planning.</em>
</p>

## Highlights

- **Motion-oriented register pretraining.** Temporally aligned ego motion is injected into compact register tokens to shape motion-sensitive driving states before downstream training.
- **Register-mediated masked prediction.** Dense patch-level targets are predicted solely from the registers, encouraging the compact state to retain sufficient visual information.
- **Predictive register structure.** Blockwise register masking explicitly trains the register space itself as a prediction target.
- **Shared state interface.** The same register representation is used by the future-state world model, trajectory generator, and trajectory scorer.
- **Strong accuracy-efficiency trade-off.** MORE reaches state-of-the-art planning performance while using only about one tenth of DriveLaW's inference latency.

## Main Results

| Benchmark | Metric | MORE |
|:--|:--|--:|
| NAVSIM-v2 | EPDMS | **92.5** |
| NAVSIM-v1 | PDMS | **93.2** |
| HUGSIM (zero-shot closed loop) | Route Completion | **51.6** |
| HUGSIM (zero-shot closed loop) | HD-Score | **39.4** |
| Efficiency (RTX 4090, batch size 1) | Inference latency | **110.0 ms** |

MORE improves the previous best NAVSIM-v2 EPDMS by **1.6 points** and achieves strong zero-shot closed-loop generalization on 436 HUGSIM scenarios without benchmark-specific training or fine-tuning.

## Citation

If you find MORE useful in your research, please consider citing our work:

```bibtex
@article{gu2026more,
  title   = {MORE: Learning Motion-Oriented Registers for Driving World Models and Planning},
  author  = {Gu, Yingdong and Wang, Haoyu and Yan, Shaocheng and Zhao, Zhenjun and Han, Hao and Shi, Pengcheng and Li, Xianfei and Tan, Qinghua and Liao, Wenlong and He, Tao and Li, Jiayuan and Peng, Pai},
  journal = {arXiv preprint},
  year    = {2026}
}
```

## Acknowledgements

This project builds upon the excellent open-source efforts of [V-JEPA 2](https://github.com/facebookresearch/vjepa2), [OpenScene](https://github.com/OpenDriveLab/OpenScene), [NAVSIM](https://github.com/autonomousvision/navsim), and [HUGSIM](https://github.com/hyzhou404/HUGSIM). We thank their contributors for making this research possible.
