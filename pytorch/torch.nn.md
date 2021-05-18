# ```import torch.nn```

### cross entropy loss

```python
torch.nn.CrossEntropyLoss(weight=None, size_average=None, ignore_index=-100, reduce=None, reduction='mean')
```

==combines [`LogSoftmax`] and [`NLLLoss`] in one single class==

- weight: 不同类别的加权，tensor类别

  ```python
  c_w = torch.FloatTensor([0.13859937, 0.5821059, 0.63871904, 2.30220396, 7.1588294, 0]).cuda()
  criterion = nn.CrossEntropyLoss(weight=c_w)
  ```

- reduction

  - `'none'`: no reduction 
  - `'mean'`: the weighted mean of the output(default)
  - `'sum'`: the output will be summed

