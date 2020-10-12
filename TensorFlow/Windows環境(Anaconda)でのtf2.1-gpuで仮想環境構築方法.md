## コマンド

```
# 仮想環境作成
conda create -n 仮想環境名

# TF: 2020/09/30の時点でバージョン2.1
conda install tensorflow-gpu

# Addon
conda install -c esri tensorflow-addons

# jupyter
conda install -c conda-forge notebook

# pandas
conda install -c anaconda pandas

# opencv
conda install -c conda-forge opencv

# sciklit learn
conda install -c conda-forge scikit-learn 

# matplotlib
conda install -c anaconda matplotlib
```

winでは公式でサポートされてないため

```
pip install tensorflow-gpu==2.3
pip install tensorflow-addons
```
