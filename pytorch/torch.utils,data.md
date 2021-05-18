# ```import torch.utils.data```

### WeightedRandomSampler

```python
torch.utils.data.WeightedRandomSampler(weights, num_samples, replacement=True, generator=None)
```

- **weights** (*sequence*) – a sequence of weights, not necessary summing up to one(每一个类别在采样过程中得到权重大小, 重越大的样本被选中的概率越大)
- **num_samples** ([*int*](https://docs.python.org/3/library/functions.html#int)) – number of samples to draw(样本总数)
- **replacement** ([*bool*](https://docs.python.org/3/library/functions.html#bool)) – if `True`, samples are drawn with replacement. If not, they are drawn without replacement, which means that when a sample index is drawn for a row, it cannot be drawn again for that row.（是否在一个epoch中重复选取某个样本）
- **generator** ([*Generator*](https://pytorch.org/docs/stable/generated/torch.Generator.html#torch.Generator)) – Generator used in sampling.)

