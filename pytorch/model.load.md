原模型训练时使用GPU，使用了torch.nn.DataParallel()保存，保存字典里的key有module.layer.xx， 而模型加载时需要key为layer.xxx

```python
state = torch.load(pretrain_path, map_location='cpu')

if len(self.gpu_ids):
    network.load_state_dict(state)            					#保存时为单个gpu或cpu
else:
    network.load_state_dict({k.replace('module.',''):v for k,v in state.items()}  #保存时为多个GPU
```



