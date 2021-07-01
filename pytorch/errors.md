```bash
ret = torch.addmm(bias, input, weight.t()) RuntimeError: mat1 dim 1 must match mat2 dim 0
```

输入与模型定义不一样