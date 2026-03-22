# turtlePlus

| [English](./README.md) | 简体中文 |
| ---------------------- | -------- |







## 功能介绍



### 1. 向前移动

与turtle一样，fd函数用于以制定的方式移动光标并绘图。完全兼容turtle，并加入了大量新功能。

- 在turtle中，线型的控制纯靠手工控制penup和pendown。tutlePlus将其打包为常用的LineModes.none、LI neMode.solid和LineMode.dotted，分别是不画线（抬笔）、实线、虚线。当然，你仍然可以使用原有的penup等方式来精确控制。
- 对于GUI简单演示中，常常需要在点附近标注名称等。turtle原生支持对停顿点进行打点、标记文字。



函数需要的参数和对应的含义如下：

```python
fd(length,
	line_width=DEFAULT.LINE_WIDTH,
	line_color=Colors.black, 
  line_mode=LineModes.solid,
   
	write_name="", name_align=Align.LEFT,
	name_vertical_align=VerticalAlign.TOP,

  if_dot_at_end=True,
  dot_color=Colors.black, 
  dot_diameter=DEFAULT.DOT_DIAMETER,
	dotted_line_length=DEFAULT.DOTTED_LINE_LENGTH,
	dotted_gap=DEFAULT.DOTTED_GAP
)
```

`length`【必须】：前进的距离。

`line_width`: 前进时对路径进行画线的线宽。

`line_color`：画线的颜色,

`line_mode`：画线的线型，软件内置了直线、虚线两种基础线型以及none表示不画线。

`write_name`：是否把终点当作一个端点标注名称。默认不标注。

`name_align`：名称标注的水平对齐方向。默认为靠左对齐。

`name_vertical_align`：名称标注的垂直对齐方向。默认为靠顶部对齐。

`if_dot_at_end`：是否在终点处画一个端点。默认为真。

`dot_color`：绘制端点的颜色。

`dot_diameter`：绘制端点的半径。

`dotted_line_length`：虚线的连续长度。

`dotted_gap`：虚线的线段间间隔。



### 2. 前往某⼀坐标

可使用软件的goto函数来移动光标到文件中的某坐标并绘图。

与fd一样支持大量新特性。



```python
goto(target_point,
		line_mode，
		line_width,
		line_color,
     
		write_name,name_height=DEFAULT.FONT_HEIGHT,
		name_align=Align.LEFT, name_vertical_align=VerticalAlign.TOP,
		name_color=DEFAULT.FONT_COLOR,
     
		if_dot_at_end=True, dot_color=Colors.black,
		dot_diameter=DEFAULT.DOT_DIAMETER,
		dotted_line_length=DEFAULT.DOTTED_LINE_LENGTH
		dotted_gap=DEFAULT.DOTTED_GAP
)
```

`target_point`：目标坐标，一个[x, y]形式的列表。

`line_width`: 前进时对路径进行画线的线宽。

`line_color`：画线的颜色,

`line_mode`：画线的线型，软件内置了直线、虚线两种基础线型以及none表示不画线。

`write_name`：给端点标注名称。默认不标注。

`name_height`：标注的字体高度。

`name_align`：名称标注的水平对齐方向。默认为靠左对齐。

`name_vertical_align`：名称标注的垂直对齐方向。默认为靠顶部对齐。

`name_color`：标注的字体颜色。

`if_dot_at_end`：是否在终点处点一个端点。默认为真。

`dot_color`：绘制端点的颜色。

`dot_diameter`：绘制端点的半径。

`dotted_line_length`：虚线的连续长度。

`dotted_gap`：虚线的线段间间隔。



### 3. 绘制⽂字

write函数用于在图像中绘制文字，例如用于创建这样的图示。

<img src="./assets/image-20260323022253130.png" alt="image-20260323022253130" style="zoom: 25%;" />

函数需要的参数和对应的含义如下：

```python
write(string,
		pos=None,
		align=Align.LEFT,
		vertical_align=DEFAULT.FONT_VERTICAL_ALIGN,
		font_height=DEFAULT.FONT_HEIGHT,
		font_color=DEFAULT.FONT_COLOR,
		font_family=DEFAULT.FONT_FAMILY,
		font_weight=DEFAULT.FONT_WEIGHT)
```

`string`：要绘制的文本。

`pos`：绘制的坐标。

`align`：绘制的文字的水平对齐方式，

`vertical_align`：绘制的文字的垂直对齐方式。

`font_height`：绘制的文字高度。

`font_color`：绘制的文字颜色。

`font_family`：绘制的字体。

`font_weight`：字体的粗细。



### 4. 缩放视⼝

由于图案的大小与屏幕的分辨率并不一定相近，在turtle绘图中经常会出现绘制的图案太大超出

屏幕而无法查看，或者图案太小导致无法看清。turtlePlus 引入了视口缩放机制，解决了这一问题。

使用set_scale()函数即可对视口进行缩放。

函数需要的参数和对应的含义如下：

```python
set_scale(scale_value)
```

`scale_value`：缩放比例，一个大于0的数。



### 5. ⾃动缩放

turtlePlus 提供了自动缩放功能，把图形的所有点传入，即可根据位置进行自动缩放，使图案可

以在屏幕上正常显示，无需手动计算缩放比例。

函数需要的参数和对应的含义如下：

```
auto_scaling(points_pos)
```

`points_pos`：图案所有点的坐标。

以下左图为不开启缩放的效果，右图为开启缩放的效果。

<img src="./assets/image-20260323024230638.png" alt="image-20260323024230638" style="zoom:25%;" />  <img src="./assets/image-20260323024249044.png" alt="image-20260323024249044" style="zoom:25%;" />



### 6. 计算距离

勾股定理计算坐标距离。

⚠️ 并不是多此一举，函数兼容特殊格式的坐标以及考虑了视口缩放。

函数需要的参数和对应的含义如下：

```
distance(point_1, point_2)
```

`point_1`、`point_2`：传入的两个坐标。



### 7. ⾃动偏移视⼝

有时候，绘制的图形会因为形状问题，并不在窗口正中央，观感不好。为了解决这一问题，turtlePlus 引入了视口偏移机制，解决了这一问题。使用auto_offset 函数即可对视口进行移动

函数需要的参数和对应的含义如下：

```
auto_offset(points_pos, offset_mode):
```

`points_pos`：图形的所有点。

`offset_mode`：图形的偏移模式，Offset.at_start 为以起点为视口中心，Offset.center 为以图形几何中心为视口中心，Offset.none为不使用偏移。

例如，使用`auto_offset(points, Offset.center)`即可达到这样的效果，使图形居中：

<img src="./assets/image-20260323025337038.png" alt="image-20260323025337038" style="zoom:25%;" />       <img src="./assets/image-20260323025346619.png" alt="image-20260323025346619" style="zoom:25%;" />



### 8. ⾃动确保显示效果

全自动完成对视口的偏移、缩放，达到最佳显示效果。

函数需要的参数和对应的含义如下：

```python
ensure_appearance(points_pos, offset_mode=OffsetMode.none)
```

`points_pos`：点的参数

`offset_mode`：视口偏移模式。

使用此功能，就可以自动完成`auto_scaling`和`auto_offset`，实现最佳显示效果。



<img src="./assets/image-20260323025421851.png" alt="image-20260323025421851" style="zoom:25%;" />