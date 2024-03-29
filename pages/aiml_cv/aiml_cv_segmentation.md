# Segmentation

## 概要

- [歴史が記載された図](https://twitter.com/ZFPhalanx/status/1266391941589024768)

## 論文

- [2014/12/22] Semantic Image Segmentation with Deep Convolutional Nets and Fully Connected CRFs
  - https://arxiv.org/abs/1412.7062

- [2015/11/23] Multi-Scale Context Aggregation by Dilated Convolutions
  - https://arxiv.org/abs/1511.07122

- [2015/05/18] U-Net: Convolutional Networks for Biomedical Image Segmentation
  - https://arxiv.org/abs/1505.04597
  - U-Net構造といわれる階層的なskip-connectionにより高解像データを失わない工夫をしたモデル。

- [2018/07/18] UNet++: A Nested U-Net Architecture for Medical Image Segmentation
  - [https://arxiv.org/abs/1807.10165](https://arxiv.org/abs/1807.10165)

- [2022/03/24] Sparse Instance Activation for Real-Time Instance Segmentation
  - https://arxiv.org/abs/2203.12827

- [[2212.01579] Box2Mask: Box-supervised Instance Segmentation via Level-set Evolution](https://arxiv.org/abs/2212.01579)
  - [https://twitter.com/_akhaliq/status/1612034778236129280](https://twitter.com/_akhaliq/status/1612034778236129280)
  - 古典的なlevel-set evolutionをNNに結合し、バウンディングボックスの教師のみで、セグメンテーションのマスクを予測するBox2Maskを提案。
  - アプローチ自体はベースのモデル構造によらずに適用でき、CNNとTransformerベース双方で検証している。
  - Swin-Transformerを用いたBox2Maskは、COCOにおいて42.4%のマスク適用率を達成し、最近開発された完全マスク教師付き手法に匹敵する性能。
