# 实验二：图像增强
202410315019-彭艺琼-人工智能241

## 一、实验目的
学会OpenCV的基本使用方法，利用OpenCV等计算机视觉库对图像进行平滑、滤波等操作，实现图像增强。

## 二、实验内容
### 1、导入图像滤波相关依赖包
- 导入.OpenCV库、NumPy库、Matplotlib库、scikit-image库。

### 2、读取原始图像并进行色彩空间转换
1. 为了后续方便绘图，定义一个绘图函数`plot_bgr（BGR, Title）`，如下所示：

2. 读入 "pilot.jpg"，需要注意 OpenCV 默认读取的图像格式是 BGR（蓝-绿-红通道），而不是常见的 RGB（红-绿-蓝通道）。可以使用 OpenCV 的 `cv2.cvtColor` 颜色空间转换函数转换为 RGB 。
3. 但在实际绘图时，我更倾向于直接使用切片操作 `img[..., ::-1]`，更加简洁高效（`plot_bgr`）。
原图及灰度图如下：<img width="460" height="196" alt="2f26b782119c3da511eb62977e91cee" src="https://github.com/user-attachments/assets/e18b0682-51df-4b86-a586-abc14f058429" />

### 3、添加噪声

### 4、图像滤波

### 5、中值滤波

## 三、实验结果与分析

## 四、实验小结
