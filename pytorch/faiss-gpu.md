# faiss-gpu

- conda 安装

```bash
conda install faiss-gpu cudatoolkit=10.0 -c pytorch
```

此前用conda安装了pytorch系列。此时若使用cudatoolkit 10.2， 会报错```no such file libcudart.so.10.0, libcublas.so.10.0```

而cuda 10.0配对的torchvision版本为0.4.0， 其transforms只支持PIL image不支持tensor

- pip安装步骤

```bash
pip --no-cache-dir install torch==1.8.1+cu102 torchvision==0.9.1+cu102 torchaudio===0.8.1 -f https://download.pytorch.org/whl/torch_stable.html
```

若不加```--no-cache-dir```可能报错```no space left```

```bash
pip install faiss-gpu
```

