- 文件夹中文件的个数

  ```bash
  ll | grep ^- | wc -l
  ```

- 文件夹中文件夹的个数

  ```bash
  ll | grep ^d | wc -l
  ```

- 文件夹中查找文件

  ```bash
  find folder/ -name filename
  ```

- 当前文件夹下各一级文件占用大小

  ```bash
  du -h --max-depth=1
  ```

- 清空回收站

  ```bash
  sudo rm -rf ~/.local/share/Trash/
  ```

- 查看CPU信息（型号）

  ```shell
  cat /proc/cpuinfo | grep name | cut -f2 -d: | uniq -c
  ```

- 查看物理CPU个数

  ```shell
  cat /proc/cpuinfo| grep "physical id"| sort| uniq| wc -l
  ```

- 查看每个物理CPU中core的个数(即核数)

  ```shell
  cat /proc/cpuinfo| grep "cpu cores"| uniq
  ```

- 查看逻辑CPU的个数

  ```shell
  cat /proc/cpuinfo| grep "processor"| wc -l
  ```

  

