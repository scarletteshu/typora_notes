# ```torchvision```

0.4.0及以前版本不支持PIL image以外的输入

### transforms

1. ```transforms.ToTensor()```

   输入为PIL image或者ndarray: (H x W x C)
   ​仅对uint8类型的图像转换到[0,1]

2.  ```transforms.Resize(size, interpolation)```

    输入为PIL image或Tensor：(BxCxHxW)， 或(CxHxW)

    - size: int or sequence. if int and H>W:（size *H/W, size）
    - interpolation: default```InterpolationMode.BILINEAR```

    

### Dataset

```python
class testDataset(Dataset):
    def __init__(self, data_path:str):
        self.transform = transforms.Compose([
            transforms.ToTensor(),
            transforms.Normalize(mean=[0.485, 0.456, 0.406],
                                 std=[0.229, 0.224, 0.225]),
        ])
        
        f = open(data_path, "rb")
        self.keys=[]   # img_names
        self.imgs =[]  # float32 img nparray (228, 200)
        while True:
            try:
                img_dict = pkl.load(f)
                
                key = list(img_dict.keys())[0]
                self.keys.append(key)
                
                img = img_dict[key].astype('float32')
                img = img/np.max(img)                             # to [0,1], if not convert to float32 fisrt, dtype will be float64
                img = np.expand_dims(img, 0).repeat(3, axis=0)   # (3, 228, 200)
                # print(img.shape)
                self.imgs.append(img)
            except:
                break
        f.close()
        self.imgs = np.array(self.imgs).transpose(0,2,3,1)                           # (batch, 3, 288, 200)
        # print(len(self.keys), self.imgs.shape, self.imgs.dtype)
        

    def __getitem__(self, index):
        #print(self.imgs.shape)
        img = self.transform(self.imgs[index])
        #print(img.shape)
        return img

    def __len__(self):
        return self.imgs.shape[0]
```

