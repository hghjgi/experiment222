# experiment222
#### 一、实验目的
学会 Opencv 的基本使用方法，利用 Opencv 等计算机视觉库对图像进行平滑、滤波等操作，实现图像增强。

#### 二、实验内容
##### 1、**导入相关依赖包**
- 导入 OpenCV、Numpy、Matplotlib、Skimage。

##### 2、读入图像及展示
1. 为了后续方便绘图，定义一个绘图函数`plot_bgr（BGR, Title）`，如下所示：

2. 读入 "pilot.jpg"，需要注意 OpenCV 默认读取的图像格式是 BGR（蓝-绿-红通道），而不是常见的 RGB（红-绿-蓝通道）。可以使用 OpenCV 的 `cv2.cvtColor` 颜色空间转换函数转换为 RGB 。
3. 但在实际绘图时，我更倾向于直接使用切片操作 `img[..., ::-1]`，更加简洁高效（`plot_bgr`）。
