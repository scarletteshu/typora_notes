# Jupyter

### jupyter connect server

1. install jupyter on server

```bash
conda install pyzmq tornado jinja2 jsonschema jupyterlab
```

2. config file

```bash
jupyter lab --generate-config
```

![image-20210519160252233](jupyter.assets/image-20210519160252233.png)

3. generate psswd

```python
python
from IPython.lib import passwd
passwd()

'sha1:91a33afc946f:20526579c365095ddb27475c6bb409a64650ee7a'
```

4. change config

```bash
vi /home/zhanglingshu/.jupyter/jupyter_lab_config.py
```

​	文末添加：

```
'sha1:91a33afc946f:20526579c365095ddb27475c6bb409a64650ee7a'
c.NotebookApp.ip='*'
c.NotebookApp.password=u'sha1:91a33afc946f:20526579c365095ddb27475c6bb409a64650ee7a'
c.NotebookApp.open_browser = False
c.NotebookApp.port = 9001
c.InteractiveShellApp.matplotlib ='inline'
```

5. Xshell 配置

   文件->属性->SSH->隧道

   添加侦听端口：9001

   目标主机：服务器IP

   目标端口：9001

6. run 

```bash
jupyter lab
```

​	浏览器：```localhost:9001```

### jupyter multi envs

1. 在需要的虚拟环境中安装ipykernel

   ```bash
   conda install ipykernel
   ```

2. 安装menus

   ```bash
   python -m ipykernel install --user --name keras --display-name "Python (keras)"
   ```

3. 刷新jupyterlab
