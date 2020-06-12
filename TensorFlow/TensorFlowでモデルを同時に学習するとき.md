- Use a GPU
https://www.tensorflow.org/guide/gpu#using_multiple_gpus

モデルを同時に学習するときのコード
TF1系では下記のようになるが、TF2系では、そもそもdefine by run方式なので、
このようにする必要がないのかもしれない

```python
with tf.device('/cpu:0'):
# with tf.device('/gpu:0'):
    model = Model()
with tf.device('/cpu:0'):
# with tf.device('/gpu:0'):
    model = Model()
```
