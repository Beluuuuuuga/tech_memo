## フロー
1: CUDAのバージョンを確認

フォルダの場所: `C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v10.0`

https://medium.com/lsc-psd/%E6%A9%9F%E6%A2%B0%E5%AD%A6%E7%BF%92%E6%99%82%E3%81%ABgpu%E3%82%92%E8%AA%8D%E8%AD%98%E3%81%97%E3%81%A6%E3%81%8F%E3%82%8C%E3%81%AA%E3%81%8F%E3%81%A6-%E3%81%A8%E3%81%A3%E3%81%A6%E3%82%82%E5%9B%B0%E3%81%A3%E3%81%A6%E3%81%84%E3%82%8B%E4%BA%BA%E5%90%91%E3%81%91%E3%81%AE%E8%A8%98%E4%BA%8B-58586f1ffc0c

2: condaでの仮想環境構築

https://qiita.com/ozaki_physics/items/985188feb92570e5b82d

```
$ conda install ライブラリ名
```

3: バージョンを確認

自分の場合、1でCUDA10.0だと確認できたので、tensorflow-gpuの2.0.0をインストールする

https://www.tensorflow.org/install/source#gpu_support_2

4: 仮想環境でcondaインストール


```
$ conda activate ライブラリ名
$ python
>>> tensorflow.python.client import device_lib
>>> device_lib.list_local_devices（）
```

これで、GPUが表示されていればよい

```
[name: "/device:CPU:0"
device_type: "CPU"
memory_limit: 268435456
locality {
}
incarnation: 17328600630093263791
, name: "/device:GPU:0"
device_type: "GPU"
memory_limit: 9070530396
locality {
  bus_id: 1
  links {
  }
}
incarnation: 8056966349673554342
physical_device_desc: "device: 0, name: GeForce RTX 2080 Ti, pci bus id: 0000:01:00.0, compute capability: 7.5"
]
```


