# SPICE: Semantic Pseudo-labeling for Image Clustering

### 1 摘要

### 2 方法

预训练无监督表征学习模型，其卷积网络提取的嵌入式特征用于生成伪标签训练分类模型(SPICE-Self, SPICE-Semi), 最后分类网络实现预测簇的类别

##### 2.1 SPICE-self

设计一个基于伪标签算法的相似性度量。该算法在训练过程中可以动态预测batch-wise的为标签

在每个训练iteration中包含三步：

- 在一个大batch数据上计算嵌入式特征（embedding feature）， 及其对应的语义预测

  和该数据弱变换的特征和预测

- 置信度最高的样本来估计每个簇的原型，其索引作为其最近邻的伪标签

- 固定CNN参数，用标签数据更新CLSHead， 数据先被强转换。选出最小损失$$ L_{DSCE}$$的最佳head

##### 2.2 SPICE-semi

已知聚类结果和嵌入式特征，利用半监督学习范式对分类模型进行再训练，进一步提高聚类性能

- 选择一组可靠的标签数据，减轻局部语义不一致性

### 3 实现

- Pretrain representation learning model

  ```shell
  python tools/train_moco.py
  ```

  需要修改的文件有：

  `tools/train_moco.py`,

  `spice/model/feature_modules/cluster_resnet.py`,

  `moco/builder.py`

  `moco/aurora.py`

  - train_moco.py

    `--data_type`, `--data`, `--img_size`, `--save_folder`, `--resume`

    `elif args.data_type`,

    `os.enviorn['CUDA_VISIBLE_DEVICES']`

    关于moco文件参数相关参见：https://github.com/facebookresearch/moco

  - cluster_resnet.py

    `in_size`, `avg_pool_sz `, `self.conv1`

  - builder.py

    `input_size`

  - aurora.py

    Dataset class, return [img, target]

- Precompute embedding features

  ```shell
  python tools/pre_compute_ebmedding.py
  ```

  需要查看的文件有：

  `spice.model.build_model_sim.py`， 

  

