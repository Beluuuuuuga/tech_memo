## フロー
1: CUDAのバージョンを確認する

フォルダの場所: C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v10.0

2: condaで仮想環境構築

pytorch-gpuは仮想環境名
pythonのバージョンはCUDAのバージョンで決定される適宜変更する

```
$ conda create -n pytorch-gpu python=3.7
```

3: 仮想環境内でgpu版pytorchをインストールする

基本下のサイトでCUDAのバージョンでインストールを変更するが、

https://pytorch.org/

当てはまらない場合は、

https://pytorch.org/get-started/previous-versions/

から選択する

```
$ conda install pytorch==1.0.0 torchvision==0.2.1 cuda100 -c pytorch
```

4: GPUがきちんと認識されているか確認する

TrueになっていればOK

https://www.it-swarm.dev/ja/python/pytorch%E3%81%8Cgpu%E3%82%92%E4%BD%BF%E7%94%A8%E3%81%97%E3%81%A6%E3%81%84%E3%82%8B%E3%81%8B%E3%81%A9%E3%81%86%E3%81%8B%E3%82%92%E8%AA%BF%E3%81%B9%E3%82%8B%E6%96%B9%E6%B3%95%E3%81%AF%EF%BC%9F/836403850/

```
$ python
>>> import torch
>>> torch.cuda.is_available()
True
```

