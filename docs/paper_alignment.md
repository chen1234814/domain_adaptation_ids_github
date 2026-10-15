# Paper Alignment Notes

本資料夾的 notebook 依照定稿 PDF 的方法章整理，重點如下。

## Source / Target 設定

- NSL-KDD：`KDDTrain+.arff` 作為 source domain，`KDDTest+.arff` 作為 target domain。
- CICIDS2017：Friday 的 Morning、Afternoon DDos、Afternoon PortScan 作為 target domain，其餘 CSV 作為 source domain。
- UNSW-NB15：官方 training set 作為 source domain，official testing set 作為 target domain。

## 方法

- Source-only：只使用 source labels 訓練分類器，直接在 target domain 評估。
- DANN：使用 gradient reversal layer 與 domain classifier 做對抗式 feature alignment。
- MMD：使用 multi-kernel RBF MMD loss 對齊 source/target feature distributions。
- Deep CORAL：使用 covariance alignment loss 對齊 source/target feature covariance。

## 統一設定

- Backbone：CNN、RNN、Transformer。
- 特徵處理：feature tokenization。
- Classification loss：`BCEWithLogitsLoss`。
- Optimizer：AdamW。
- Learning rate：`1e-3`。
- Weight decay：`1e-4`。
- Batch size：`256`。
- Epochs：`30`。
- Max train batches per epoch：`200`。
- Source sampler：使用 source label 的 class-balanced sampling。
- Attack/anomaly class loss weight：`2.0`。


