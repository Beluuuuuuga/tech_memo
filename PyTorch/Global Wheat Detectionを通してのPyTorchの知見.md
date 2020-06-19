## 提出記録
1回目：2020/06/18 0.5484 
2回目：2020/06/19 0.5484 


## PyTorchの知見
### 資料[TORCHVISION.MODELS](https://pytorch.org/docs/stable/torchvision/models.html)
- 物体検出では、Faster R-CNN ResNet-50 FPNとMask R-CNN ResNet-50 FPNが存在

- input画像は、[C, H, W]の順番で、例えば、画像4枚、3チャネル, 縦が600, 横が1200の場合、次元数は(4, 3, 600, 1200)

- 学習の際のtargetはboxとlabelが必要で、targetの例では、画像4枚で1枚当たりboxの数が11の場合、次元数は(4, 11, 4)になる。<br>
最後の4は[x1, y1, x2, y2]で小数(FloatTensor)である必要がある。<br>
また、targetは整数(Int64Tensor)である必要がある

実装例
```python
import torch
import torchvision

model = torchvision.models.detection.fasterrcnn_resnet50_fpn(pretrained=True)
# For training
images, boxes = torch.rand(4, 3, 600, 1200), torch.rand(4, 11, 4)
labels = torch.randint(1, 91, (4, 11)) # 1~91までの数値を生成
images = list(image for image in images)
targets = []
for i in range(len(images)):
    d = {}
    d['boxes'] = boxes[i]
    d['labels'] = labels[i]
    targets.append(d) # dictionary形式でtargetを作成
output = model(images, targets) 
# For inference
model.eval()
x = [torch.rand(3, 300, 400), torch.rand(3, 500, 400)]
predictions = model(x)

# optionally, if you want to export the model to ONNX:
torch.onnx.export(model, x, "faster_rcnn.onnx", opset_version = 11)
```

### [Pytorch Faster-R-CNN with ResNet152 backbone](https://www.kaggle.com/maherdeebcv/pytorch-faster-r-cnn-with-resnet152-backbone)のコード(その[推論バージョン]())
- KaggleではFasterRCNNを使用

- 実装でわからない部分
- In[4]の@dataclass
  - これはクラスを作成する際に、__init__などを自動生成してくれるもの(dunder(double underscoreの略))
  - 資料：[PEP557 dataclassの仕組みを解説する](https://qiita.com/yukinarit/items/0dbd81d3533a2b818f20)
  
```py
@dataclass
class DatasetArguments:
    data_dir: Path
    images_lists_dict: dict
    labels_csv_file_name: str

@dataclass
class DataLoaderArguments:
    batch_size: int
    num_workers: int
    dataset_arguments: DatasetArguments
```


クラスをインスタンス化して使用する場合の例

```hoge.py
@dataclass
class Hoge:
    i: int

hoge = Hoge(10)
hoge.i
```
    
- In[10]のtransforms
  - `bbox_params=BboxParams(`のBboxParamsでは、bounding boxが画像からはみ出さないようになっている
  - 詳しくは公式[Source code for albumentations.core.composition](https://albumentations.readthedocs.io/en/latest/_modules/albumentations/core/composition.html)
  - albumentationsのComposeのOneOfはランダムでaubmentation手法のどれかを適用する
  - 資料：[Albumentations: Fast and Flexible Image Augmentations](https://www.mdpi.com/2078-2489/11/2/125/htm)
  - Composeのp=1.0ではCompose内リスト全てを適用する確率でデフォルトでは1.0
  - 資料：[Core API (albumentations.core)
Composition](https://albumentations.readthedocs.io/en/latest/api/core.html)

## 備考
- tensorflowでも学習済みモデルがある<br>
https://note.nkmk.me/python-tensorflow-keras-applications-pretrained-models/
- APの説明<br>
https://qiita.com/tmtakashi_dist/items/863e1781b5252e453b47
- boxのアンサンブル＠kaggle<br>
https://www.kaggle.com/c/open-images-2019-object-detection/discussion/115086
- boxのアンサンブル2＠kaggle<br>
https://www.kaggle.com/shonenkov/wbf-approach-for-ensemble
- kaggle参考記事<br>
https://naotaka1128.hatenadiary.jp/entry/kaggle-challenge-story
- アンサンブルについて<br>
https://mlwave.com/kaggle-ensembling-guide/
- ロシアのすごい人＠kaggle<br>
https://www.kaggle.com/shonenkov/notebooks<br>
https://www.kaggle.com/shonenkov/bayesian-optimization-wbf-efficientdet<br>
https://www.kaggle.com/shonenkov/training-efficientdet


