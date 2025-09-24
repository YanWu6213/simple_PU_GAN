# simple_PU_GAN
Point cloud Upsampling GAN

此為自學應用GAN實作點雲上採樣

PU-GAN (Point cloud Upsampling GAN)
<br>
目的為開發一套基於生成對抗網路的點雲上採樣模型，用以解決原始3D點雲在解析度不足、形狀資訊遺失等問題，可提升下游任務如形狀辨識、3D 重建的準確性與表現。
<br>

<h1>1.資料集：ShapeNetCore.v2</h1>
<br>
ShapeNetCore.v2是ShapeNet資料集的子集，具有單一乾淨的3D模型。
<br>
共有55種類別，各筆點雲資料包含15,000個點，每個點有3維座標
<br>

![image](https://github.com/YanWu6213/simple_PU_GAN/blob/main/imgs/1.png)


<h1>2.模型與實驗設計</h1>
  <br>
Generator：<br>
輸入：[B, N, 3] 低解析度點雲 <br>
輸出：[B, N * r, 3] 上採樣後的點雲<br>

Discriminator：<br>
輸入：[B, N, 3] 的點雲（可能來自真實或Generator） <br>
輸出：將所有點經過 MLP 後平均，得到該點雲的真實性預測<br>

Epoch=20<br>
Batch size=8<br>

實作基本上採樣至1024pts<br>
實作PU-GAN上採樣至1024pts<br>
實作基本上採樣至2048pts<br>
實作PU-GAN上採樣至2048pts<br>

<h1>3.推論與可視化採用f-score </h1><br>
評估點雲之間的匹配程度，類似二分類的評估指標，綜合考慮： <br>
Precision：生成點中，有多少點與真實點相距小於閾值 <br>
Recall：真實點中，有多少點與生成點相距小於閾值 <br>

<h1>4.實驗成果</h1>
左：Ground Truth　　右：基本上採樣 512 points <br>

![image](https://github.com/YanWu6213/simple_PU_GAN/blob/main/imgs/GT.gif)![image](https://github.com/YanWu6213/simple_PU_GAN/blob/main/imgs/512.gif)








