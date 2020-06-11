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

Trueになっていれば

```
$ python
>>> import torch
>>> torch.cuda.is_available()
True
```

