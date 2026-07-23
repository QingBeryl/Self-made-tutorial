# Numpy基础

> 本文主要介绍Python使用Jupyter进行数据的基本知识，建议有Python基础的人浏览。

NumPy（Numerical Python）是 Python 中最底层、最核心的数值计算库。它提供了大量的数学和统计工具，满足科 学家、工程师和数据分析师在Python编程中高效处理数据的需求。

## 一、数据类型

| 类型           | 备注 | 说明       |
| -------------- | ---- | ---------- |
| bool_          | 8位  | 布尔类型   |
| int8           | 8位  | 整形       |
| int16          | 16位 | 整形       |
| int32          | 32位 | 整形       |
| int64/int_     | 64位 | 整形       |
| uint8          | 8位  | 无符号整型 |
| uint16         | 16位 | 无符号整型 |
| uint32         | 32位 | 无符号整型 |
| uint64         | 64位 | 无符号整型 |
| float16        | 16位 | 浮点型     |
| float32        | 32位 | 浮点型     |
| float64/float_ | 64位 | 浮点型     |
| str_           | -    | 字符串型   |
| datetime64     | -    | 日期时间型 |
| timedelta64    | -    | 时间差型   |

说明：一般情况下，以上类型不需要手动指定，NumPy 会自动推断

## 二、常量

1. `numpy.nan`：

   表示空值，不等于任何量，包括它自己；我们可以使用下面方法判断是否为空：

   ```python
   import numpy as np
   a = np.array([1, 2, 3, np.nan, 5])
   np.isnan(a)
   ```

   ```python
   输出结果应为：
   array([False, False, False,  True, False])
   ```

   

2. `numpy.inf`：

   表示正无穷大(负的无穷大：-np.inf)；可以使用如下方法来判断是不是正负无穷大：

   ```python
   import numpy as np
   a = np.inf
   np.isinf(np.inf)
   ```

   ```python
   # 输出结果应为：
   np.True_
   ```

   

3. `numpy.pi`：

   表示圆周率：3.141592653589793

4. `numpy.e`：

   表示自然常数：2.718281828459045

## 三、创建数组

### 1. numpy.array函数创建数组

```python
numpy.array(object, dtype=None, copy=True, order='K', subok=False, ndmin=0, like=None)
```

参数说明：

| 名称        | 描述                                                     |
| ----------- | -------------------------------------------------------- |
| object      | 必须参数，用来创建数组的输入数据。可以是任何可迭代数据。 |
| dtype=None  | 可选参数，指定数组元素的数据类型。                       |
| copy=True   | 略                                                       |
| order='K'   | 略                                                       |
| subok=False | 略                                                       |
| ndmin=0     | 略                                                       |
| like=None   | 略                                                       |

示例如下：

```python
import numpy as np
data = [[1, 2, 3, 4, 5], [6, 7, 8, 9, 10]]
arr = np.array(data)
print(arr, type(arr))
```

```python
# 输出结果应为：
[[ 1  2  3  4  5]
 [ 6  7  8  9 10]] <class 'numpy.ndarray'>
```

### 2. numpy.array函数创建数组

```python
numpy.arange(start, stop, step, dtype=None)
```

参数说明：

| 名称  | 描述                |
| ----- | ------------------- |
| start | 起始数字，默认为0。 |
| stop  | 结束数字。          |
| step  | 步长，默认为1。     |
| dtype | 指定数据类型。      |

示例如下：

```python
import numpy as np
arr = np.arange(5)
arr  
```

```python
# 输出结果应为：
array([0, 1, 2, 3, 4])
```

### 3. random创建随机数组

- 创建一个由[0,1)内的随机数组成的数组：

  ```python
  numpy.random.rand(d0,d1,…,dn)
  ```

  参数说明：

  | 名称        | 描述               |
  | ----------- | ------------------ |
  | d0,d1,...dn | 指定数组形状的整数 |

  示例如下：

  ```python
  import numpy as np
  arr1 = np.random.rand(5)           
  arr2 = np.random.rand(2, 3)
  arr1
  arr2
  ```

  ```python
  # 输出结果应为：
  array([0.09294466, 0.59863072, 0.58535122, 0.40607265, 0.13878048])
  array([[0.36256758, 0.88819762, 0.11922292],
  	  [0.32804837, 0.55153622, 0.74913818]])
  ```

- 生成具有给定形状的随机整数数组，随机整 数的范围区间为[low, high)：

  ```python
  numpy.random.randint(low, high=None, size=None, dtype=int)
  ```

  参数说明：

  | 名称  | 描述                                                         |
  | ----- | ------------------------------------------------------------ |
  | low   | 为最小值，如果没有指定  high 这个参数，则  low 为生成的元素值的最大值， [0, low) |
  | high  | 为最大值，如果提供了  high 参数，则范围是 [low, high)        |
  | size  | 可选参数，用于指定数组的形状，如果提供了  size 参数，则返回指定形状的数组；如果未提供  参数，则返回单个随机整数。 |
  | dtype | 指定返回数组的数据类型，默认的数据类型是np.int               |

  示例如下：

  ```python
  import numpy as np
  arr = np.random.randint(1, 12, size=(2, 3, 2))
  arr
  ```

  ```python
  # 输出结果应为：
  array([[[10,  2],
          [ 9, 10],
          [ 6,  8]],
  
         [[ 8, 10],
          [ 5,  6],
          [ 4, 10]]])
  ```

说明：指定数组形状的参数应该传入一个元组，从前往后代表数组从外往内的层数。

### 4. NumPy 创建特殊数组

- 全一数组：

  ```python
  numpy.ones(shape, dtype=None, order='C')
  ```

  示例如下：

  ```python
  import numpy as np
  arr = np.ones((1, 2, 3))
  arr
  ```

  ```python
  # 输出结果应为：
  array([[[1., 1., 1.],
          [1., 1., 1.]]])
  ```

- 全零数组：

  ```python
  numpy.zeros(shape, dtype=None, order='C')
  ```

  示例如下：

  ```python
  import numpy as np
  arr = np.zeros((1, 2, 3))
  arr
  ```

  ```python
  # 输出结果应为：
  array([[[0., 0., 0.],
          [0., 0., 0.]]])
  ```

- 单位数组：一个对角线上为1，其它地方为零的数组。

  ```python
  numpy.eye(N, M=None, k=0, dtype=float, order='C')
  ```

  参数说明：

  | 名称 | 描述                                                         |
  | ---- | ------------------------------------------------------------ |
  | N    | 返回数组的行数。                                             |
  | M    | 输出中的列数。如果没有，则默认为 N 。                        |
  | k    | 对角线的索引：0（默认）表示主对角线，正值表示上对角线，负值表示下对角线。 |

  示例如下：

  ```python
  import numpy as np
  arr = np.eye(3)
  arr
  ```

  ```python
  # 输出结果应为：
  array([[1., 0., 0.],        
  	   [0., 1., 0.],        
         [0., 0., 1.]])
  ```

- 常数数组：

  ```python
  numpy.full(shape, fill_value, dtype=None, order='C')
  ```

  参数说明：

  | 名称       | 描述   |
  | ---------- | ------ |
  | fill_value | 填充值 |

  示例如下：

  ```python
  import numpy as np
  arr = np.full([2,3], 4)
  arr
  ```

  ```python
  # 输出结果应为：
  array([[4, 4, 4],
  	   [4, 4, 4]])
  ```

- 均匀分布数组：一个指定大小，指定数据区间的均匀分布序列

  ```python
  numpy.linspace(start, stop, num=50, endpoint=True, retstep=False, dtype=None)
  ```

  参数说明：

  | 名称     | 描述                                                         |
  | -------- | ------------------------------------------------------------ |
  | start    | 起始数字。                                                   |
  | end      | 介绍数字。                                                   |
  | num      | 生成序列个数；其值默认为50。                                 |
  | endpoint | 取True时，序列包含最大值end；否则不包含；默认为True。        |
  | retstep  | 该值取True时，生成的序列中显示间距；否则不显示；默认为false。 |

  示例如下：

  ```python
  import numpy as np
  arr = np.linspace(1, 10, 5)
  arr 
  ```

  ```python
  # 输出结果应为：
  array([ 1.  ,  3.25,  5.5 ,  7.75, 10.  ])
  ```

## 四、数组的属性



