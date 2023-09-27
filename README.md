## Geometric Contrastive Learning
This repository contains the source code accompanying the paper "Geometric Contrastive Learning" ([paper](https://openreview.net/forum?id=cE4BY5XrzR)). This work was accepted for oral presentation to 4th Visual Inductive Priors for Data-Efficient Deep Learning Workshop at ICCV'23 ([VIPriors](https://vipriors.github.io/)).



---
## Abstract 
Contrastive learning has been a long-standing research
area due to its versatility and importance in learning representations.
Recent works have shown improved results if
the learned representations are constrained to be on a hypersphere.
However, this prior geometric constraint is not
fully utilized during training. In this work, we propose making
use of geodesic distances on the hypersphere to learn
contrasts between representations. Through empirical results,
we show that this contrastive learning approach improves
downstream tasks across different contrastive learning
frameworks. We show that having geometric inductive
priors perform even better in contrastive learning if used
along with other correct geometric information.

---

## Training

For pretraining the backbone, follow one of the many bash files in `scripts/pretrain/`.
We are now using [Hydra](https://github.com/facebookresearch/hydra) to handle the config files, so the common syntax is something like:
```bash
python -u main_pretrain.py \
    # path to training script folder
    --config-path scripts/pretrain/cifar \
    # training config name
    --config-name simclr.yaml \
    # 'True' for training with geometric contrastive loss
    method_kwargs.geometric_loss=True \
```

After that, for offline linear evaluation, follow the examples in `scripts/linear` or run this command
```bash
python -u main_linear.py \
    --config-path scripts/linear/cifar/ \
    --config-name simclr.yaml \
    pretrained_feature_extractor=path/to/pretrained/feature/extractor.ckpt
```

For k-NN evaluation check the scripts in `scripts/knn` or run:
```bash
python3 main_knn.py \
    --dataset cifar100 \
    --train_data_path ./datasets \
    --val_data_path ./datasets \
    --pretrained_checkpoint_dir 'pretrained/checkpoint/dir' \
    --k 1 10 \
    --temperature 0.2 \
    --feature_type backbone \
    --distance_function cosine \

```


## Citation
To cite our article, please cite:
```bibtex
@inproceedings{
  koishekenov2023geometric,
  title={Geometric Contrastive Learning},
  author={Yeskendir Koishekenov and Sharvaree Vadgama and Riccardo Valperga and Erik J Bekkers},
  booktitle={4th Visual Inductive Priors for Data-Efficient Deep Learning Workshop},
  year={2023},
  url={https://openreview.net/forum?id=cE4BY5XrzR}
}
```


To cite solo-learn, please cite their [paper](https://jmlr.org/papers/v23/21-1155.html):
```bibtex
@article{JMLR:v23:21-1155,
  author  = {Victor Guilherme Turrisi da Costa and Enrico Fini and Moin Nabi and Nicu Sebe and Elisa Ricci},
  title   = {solo-learn: A Library of Self-supervised Methods for Visual Representation Learning},
  journal = {Journal of Machine Learning Research},
  year    = {2022},
  volume  = {23},
  number  = {56},
  pages   = {1-6},
  url     = {http://jmlr.org/papers/v23/21-1155.html}
}
```
