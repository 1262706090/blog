# Python-Documentation


## Python Tutorial

[Python Tutorial](https://docs.python.org/zh-cn/3.11/tutorial/index.html#tutorial-index)

### 2.1. 唤出解释器

在主提示符中，输入文件结束符（Unix：Control-D，Windows：Control-Z）（即需要三个键 Control+Z+enter），就会退出解释器。或者输入命令：`quit()` 或 `exit()` 。

如果想在执行脚本后保持交互模式，可以使用-i 选项：

```bash
python -i my_script.py
```

#### 2.1.1. 传入参数

解释器读取命令行参数，将脚本名与其他参数转化为字符串列表存到 `sys` 模块的 `argv` 变量里，`sys.argv[0]`表示脚本名称或相关信息（例如 `-c` 或模块名称）。未给定输入参数时，`sys.argv[0]` 是空字符串（存疑）。

例如，以下文件 example.py 代码：

```python
import sys

print("脚本名称：", sys.argv[0])
print("参数列表：", sys.argv[1:])

```

-   正常情况

```
PS C:\Users\Python> python example.py
脚本名称： example.py
参数列表： []
```

-   运行脚本带参数

```
PS C:\Users\Python> python example.py arg1 arg2
脚本名称： example.py
参数列表： ['arg1', 'arg2']
```

-   使用 `-c` 选项

```
PS C:\Users\Python> python -c "import sys; print(sys.argv[0],sys.argv[1:])" arg1 arg2
-c ['arg1', 'arg2']
```

-   使用 `-m` 选项

```
PS C:\Users\Python> python -m example arg1 arg2
脚本名称： C:\Users\Python\example.py
参数列表： ['arg1', 'arg2']
```

#### 3.1.1 数字

交互模式下，上次输出的表达式会赋值给`_`，最好把该变量当做只读类型，否则会创建一个同名独立局部变量，使`_`变为一个普通变量名，失去原有效果。

### 4.3. range() 函数

`range()`函数接受一个、两个或三个函数

1. 一个参数 `stop`

    ```
    range(stop)
    ```

    - 生成从 `0` 到 `stop-1` 的整数序列，步长为 `1`。

    - 例如，`range(5)`生成`[0,1,2,3,4]`。

2. 两个参数 `start` 和 `stop`

    ```
    range(start,stop)
    ```

    - 生成从 `start` 到 `stop-1` 的整数序列，步长为 `1`。

    - 例如，`range(2,5)`生成`[2,3,4]`。

3. 三个参数 `start`、`stop` 和 `step`

    ```
    range(start,stop,step)
    ```

    - 生成从 `start` 到 `stop-1` 的整数序列，步长为 `step`。

    - 例如，`range(1,10,2)`生成`[1,3,5,7,9]`。

### 4.6. match 语句

`__match_args__`：

-   使用`__match_args__`，当使用位置参数匹配类的属性时，必须定义`__match_args__`，以使用 Point(x,y)形式
-   不使用`__match_args__`，对于简单的类实例，可以不定义`__match_args__`，只通过类名和关键字来匹配。

#### 4.8.1. 默认值参数

**默认值参数最好使用不可变对象**。

调用函数时，函数参数本质上是对参数空间的引用，当未给是可变对象的默认值传参时，会重复使用这个空间，里面的值会不断改变。

[为什么 Python 默认参数必须用不可变对象？](https://blog.csdn.net/qq_43580193/article/details/107702997)

