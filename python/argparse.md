# argparse

### 1 简介

- 官方文档：https://docs.python.org/zh-cn/3/library/argparse.html#argumentparser-objects

- 编写用户友好的命令行接口、自动生成帮助和使用手册

- 使用

  ```python
  import argparse
  ```

### 2 基本步骤

- 创建一个解析器

  ```python
  parser = argparse.ArgumentParser(description='xxx.')
  # description 描述信息
  ```

- 添加参数

  ```python
  parser.add_argument('integers', metavar='N', type=int, nargs='+',
                      help='an integer for the accumulator')
  parser.add_argument('--sum', dest='accumulate', action='store_const',
                      const=sum, default=max,
                      help='sum the integers (default: find the max)')
  ```

- 解析参数

  ```python
  args = parser.parse_args()
  ```

### 3 详细信息

##### 3.1 ArgumentParser.add_argument()

```python
ArgumentParser.add_argument(name or flags...[, action][, nargs][, const][, default][, type][, choices][, required][, help][, metavar][, dest])
```

参数解释

- ```name or flags```：一个命名或者一个选项字符串的列表

  ```python
  parser.add_argument('-f', '--foo')
  # parse_args()以’-‘识别选项
  
  parser.add_argument('bar')
  # 其它假定为位置参数
  ```

- ```action```：参数在命令行中出现时使用的动作基本类型

  - ```'store'```：默认动作, 存储参数的值

  - ```’store_const'```：存储被 ```const``` 命名参数指定的值

    ```python
    parser.add_argument('--foo', action='store_const', const=42)
    parser.parse_args(['--foo'])
    >>>Namespace(foo=42)
    ```

  - ```'store_true'```和```'store_false'```：```’store_const'```分别存储True/False的特殊用例

    ```python
    parser.add_argument('--foo', action='store_true')
    parser.add_argument('--bar', action='store_false')
    parser.parse_args('--foo --bar'.split())
    >>> Namespace(foo=True, bar=False)
    ```

  - ```'append'```：存储一个列表，并且将每个参数值追加到列表中

    ```python
    parser.add_argument('--foo', action='append')
    parser.parse_args('--foo 1 --foo 2'.split())
    >>> Namespace(foo=['1', '2'])

  - ```'append_const'```：存储一个列表，并将```const```命名参数指定的值追加到列表中

    **在多个参数需要在同一列表中存储常数时会有用**

  - ```'count'```：计算一个关键字参数出现的数目或次数

    ```python
    parser.add_argument('--verbose', '-v', action='count', default=0)
    parser.parse_args(['-vvv'])
    >>> Namespace(verbose=3)
    # default 将为 None，除非显式地设为 0
    ```

  - ```'help'```：打印帮助信息然后退出

  - ```'version'```：打印版本信息并在调用后退出

    ```python
    parser = argparse.ArgumentParser(prog='PROG')
    parser.add_argument('--version', action='version', version='%(prog)s 2.0')
    parser.parse_args(['--version'])
    >>> PROG 2.0
    ```

  - ```'extend'```：存储一个列表，并将每个参数值加入到列表中

    ```python
    parser.add_argument("--foo", action="extend", nargs="+", type=str)
    parser.parse_args(["--foo", "f1", "--foo", "f2", "f3", "f4"])
    >>> Namespace(foo=['f1', 'f2', 'f3', 'f4'])
    ```

- ```nargs```：关联不同数目的命令行参数到单一动作

  - ```N```：命令行中的 `N` 个参数会被聚集到一个列表中

    ```python
    parser.add_argument('--foo', nargs=2)
    parser.add_argument('bar', nargs=1)
    parser.parse_args('c --foo a b'.split())
    >>> Namespace(bar=['c'], foo=['a', 'b'])
    ```

  - ```?```

  - ```+```：所有当前命令行参数被聚集到一个列表中，当前没有至少一个命令行参数时会产生一个错误信息

    ```python
    parser.add_argument('foo', nargs='+')
    parser.parse_args(['a', 'b'])
    >>> Namespace(foo=['a', 'b'])
    parser.parse_args([])
    >>> usage: PROG [-h] foo [foo ...]
    >>> PROG: error: the following arguments are required: foo
    ```

  - ```*```：当前命令行参数被聚集到一个列表中。通过 `nargs='*'` 来实现多个位置参数通常没有意义，但是多个选项是可能的

  > 不提供nargs，消耗参数数目由action决定

- ```const```：保存不从命令行中读取但被各种```Argumentparser```动作需求的常数值
- ```default```：默认值为 `None`，指定了在命令行参数未出现时应当使用的值
- ```type```：默认情况下，解析器会将命令行参数当作简单字符串读入，`type` 关键字允许执行任何必要的类型检查和类型转换
- ```metaver```：仅改变*显示的*名称

##### 3.2 parse_args()

```python
ArgumentParser.parse_args(args=None, namespace=None)
# args - 要解析的字符串列表。 默认值是从 sys.argv 获取。
# namespace - 用于获取属性的对象。 默认值是一个新的空 Namespace 对象。
```





