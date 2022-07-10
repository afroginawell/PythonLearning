## matplotlib 3D绘图代码详解

### 1.建立三维坐标系

方法一：

```python
# 三维坐标系建立——方法一
# -*- coding: UTF-8 -*- 
import matplotlib.pyplot as plt
# plt.axes() 绘制子图 projection参数默认是二维作图，3d表示是三维作图
ax = plt.axes(projection='3d')
# plt.show() 显示图像
plt.show()
```

方法二：

```python
# 三维坐标系建立——方法二
# -*- coding: UTF-8 -*- 
import matplotlib.pyplot as plt
# plt.figure() 绘制子图 figsize参数设置子图大小，dpi设置子图的清晰度，即像素
fig = plt.figure(figsize = (5,5), dpi = 300)
# fig.add_subplot() 添加画布，111表示是1个x轴，1个y轴，1个z轴，projection参数默认为二维，3d表示为三维
ax = fig.add_subplot(111, projection = '3d')
# plt.show() 显示图像
plt.show()
```

方法三：

```python
# 三维坐标系建立——方法一
# -*- coding: UTF-8 -*- 
import matplotlib.pyplot as plt
# Axes3D 可以用来建立三维子图
from mpl_toolkits.mplot3d import Axes3D 
# plt.figure() 创建一个画布
fig = plt.figure()
# Axes3D() 创建3D子图
ax = Axes3D(fig)
# plt.show() 显示图像
plt.show()
```

设置子图的大小和像素，可以在方法二或方法三，使用plt.figure()方法设置，参数为figsize=元祖（两个元素 宽和长），dpi=像素值

### 2.绘制三维散点图

```python
# 绘制三维散点图
import matplotlib.pyplot as plt
import numpy as np
# 建立三维坐标系 采用了之前写的方法二
fig = plt.figure(figsize = (5,5), dpi = 200)
ax = fig.add_subplot(111, projection = '3d')
# 准备三维散点图的数据，使用numpy库，散点的数据根据具体情况定义
# np.random.random(100), 生成取值范围在0~1的一百个随机数组成的数组
z = 20 * np.random.random(100)	
# np.sin(z), 以z数组作为参考，一一对应生成100个由z数组中的元素的sin值组成的数组
x = 5 * np.sin(z)
# np.cos(z), 以z数组作为参考，一一对应生成100个由z数组中的元素的cos值组成的数组
y = 5 * np.cos(z)
# ax.scatter3D() 绘制三维散点图, x,y,z是相同大小的数组，对应每个点的(x,y,z)坐标，color参数是设置散点的颜色,s是点的面积，edgecolors是点的边缘颜色，color是点的颜色
ax.scatter3D(x,y,z,color = 'red', s = 200, edgecolors = 'red', color = 'orange')
# plt.show() 显示图像
plt.show()
```

### 3. 绘制三维曲线图

```python
# 绘制三维曲线图
import matplotlib.pyplot as plt
import numpy as np
# 建立三维坐标系 采用了之前写的方法二
fig = plt.figure(figsize = (5,5), dpi = 200)
ax = fig.add_subplot(111, projection = '3d')
# 准备曲线的数据，使用numpy库
# np.linspace(x,y,n)，将x~y平均分为n份，形成一个数组
z = np.linspace(0,20,1000)
x = 5 * np.sin(z)
y = 5 * np.cos(z)
# 绘制三维曲线图
ax.plot3D(x,y,z,color = 'red')
# plt.show() 显示图像
plt.show()
```

### 4.绘制三维面图

```python
# 绘制三维面图
import matplotlib.pyplot as plt
import numpy as np
from mpl_toolkits.mplot3d import Axes3D 
# 创建画布
fig = plt.figure()
# 在画布上生成子图
# ax = Axes3D(fig), 使用Axes3D库方法生成子图对象
ax = fig.add_subplot(111,projection = '3d')
'''
球的参数方程
x = Rsin(a)cos(b)
y = Rsin(a)sin(b)
z = Rcos(a)
'''
# 0 ~ 2pi
a = np.linspace(0,np.pi*2,100)
# 0 ~ pi
b = np.linspace(0,np.pi,100)
# 将数据网格化，进行一一对应的关系
a,b = np.meshgrid(a,b)
# 通过a和b得到球的参数方程,半径默认为1
x = np.sin(a) * np.cos(b)
y = np.sin(a) * np.sin(b)
z = np.cos(a)
# plot_surface() 绘制球体表面, x,y,z是三维数据，rstride和cstride是每个方块点的长和宽，数值越小，图像越精确，数值越大，图像越粗糙，cmap(colormap)是色系，plt.get_cmap()参数可以从网上得到，rainbow是彩虹色系
ax.plot_surface(x,y,z,rstride = 1, cstride = 1,cmap=plt.get_cmap('rainbow'))
# plt.show() 显示图像
plt.show()
```

### 5.保存图像

```python
import matplotlib.pyplot as plt
# plt.savefig() 一般将文件保存在默认目录下（当前python程序所在的文件），dpi是像素值
# 一般用在plt.show()之前，用于在展示图之前，将图进行保存
plt.savefig('文件名.png',dpi = 200)
```

### 6.绘制物体等高线投影图

```python
# 绘制物体等高线投影图
# ax.contourf()用于生成投影图，x,y,z是三维数据，zdir='z'表示投影在z轴上，offset=-1表示投影在z=-1的平面上， 一般用在plt.show()之前 或 三维数据组织完之后，ax是3D子图对象
ax.contourf(x,y,z, zdir = 'z', offset = -1)
```

### 7.设置坐标轴

```python
# 设置坐标轴的范围
# ax是3D子图对象，set_zlim(-2,2)表示z轴的范围是-2~2，还有set_xlim(),set_ylim(),用在生成了3D子图对象之后
ax.set_zlim(-2,2)
```

### 8.Jupyter Notebook使用matplotlib.pyplot

​		以下%语句可以放在 导入库语句之后

```python
# 将用matplotlib生成的图嵌入当前页面，仅仅是图嵌入
%MATPLOTLIB INLINE
```

```python
# 将用matplotlib生成的图以及配套的图像工具嵌入当前页面
%matplotlib NOTEBOOK
```

```python
# 以下两个的功能一样，将用matplotlib生成的图以及配套的图像工具生成一个弹窗
%matplotlib QT 
%matplotlib QT5
```

