# Domain Adaptation for Network Intrusion Detection

這個資料夾整理了論文實驗用的三份 notebook，目標是比較三個表格式入侵偵測資料集在 source/target domain shift 下的泛化能力。

## 實驗設計

- 資料集：NSL-KDD、CICIDS2017、UNSW-NB15。
- Backbone：CNN、RNN、Transformer，皆先使用 feature tokenization 將 tabular features 轉成 token sequence。
- 方法：Source-only baseline、DANN、MMD、Deep CORAL。
- 任務：二元入侵偵測，normal 為 0，attack/anomaly 為 1。
- 訓練：source labels 用於分類損失，target features 僅用於無監督領域適應。

## 目錄

```text
domain_adaptation_ids_github/
  notebooks/
    CNN_RNN_TRA_NSL_KDD_DANN_MMD_CORAL.ipynb
    CNN_RNN_TRA_CICIDS_2017_DANN_MMD_CORAL.ipynb
    CNN_RNN_TRA_UNSW_NB15_DANN_MMD_CORAL.ipynb
  docs/
    paper_alignment.md
  requirements.txt
  .gitignore
```

## 資料集放置位置

資料集檔案通常較大，已由 `.gitignore` 排除。請在 repo 根目錄建立 `data/`，並依下列結構放置原始資料：

```text
data/
  NSL_KDD/
    KDDTrain+.arff
    KDDTest+.arff
  CICIDS_2017/
    Monday-WorkingHours.pcap_ISCX.csv
    Tuesday-WorkingHours.pcap_ISCX.csv
    Wednesday-workingHours.pcap_ISCX.csv
    Thursday-WorkingHours-Morning-WebAttacks.pcap_ISCX.csv
    Thursday-WorkingHours-Afternoon-Infilteration.pcap_ISCX.csv
    Friday-WorkingHours-Morning.pcap_ISCX.csv
    Friday-WorkingHours-Afternoon-DDos.pcap_ISCX.csv
    Friday-WorkingHours-Afternoon-PortScan.pcap_ISCX.csv
  UNSW_NB15/
    UNSW_NB15_training-set.csv
    UNSW_NB15_testing-set.csv
```

## 使用方式

1. 建立 Python 環境。
2. 安裝套件：

```bash
pip install -r requirements.txt
```

3. 從 repo 根目錄啟動 Jupyter：

```bash
jupyter lab
```

4. 依序開啟 `notebooks/` 內的 notebook，先執行資料讀取與前處理，再依序執行 Source-only、DANN、MMD、CORAL 的訓練與評估 cells。

## 備註

- Notebook outputs 已清空，適合直接上傳 GitHub。
- 預設每個 epoch 最多訓練 200 batches，以對齊論文中的實驗設定並避免 CICIDS2017 訓練時間過長。
- `config.num_epochs` 預設為 30；若只是確認流程，可以先調小。
