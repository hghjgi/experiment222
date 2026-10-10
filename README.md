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
-原图及灰度图如下：
<img width="460" height="196" alt="2f26b782119c3da511eb62977e91cee" src="https://github.com/user-attachments/assets/e18b0682-51df-4b86-a586-abc14f058429" />

### 3、添加噪声
-在原始图像的基础上添加噪声，引⼊了两个API⽅法，椒盐噪声和⾼斯噪声，通过对⽐可以发现，椒盐噪声和⾼斯噪声的本质不同，椒盐噪声表现为像素会随机替换为⽩⾊或者⿊⾊像素（灰度通道），在RGB通道表现为像素变成随机彩⾊点，⽽⾼斯噪声会在每个像素上添加随机偏差，服从⾼斯分布
-噪声对⽐图：
<img width="703" height="209" alt="c36c24b435f00301867613e4b15ad5a" src="https://github.com/user-attachments/assets/3ed0aa6b-48d8-40db-91c4-cd99362b722a" />

### 4、图像滤波
-
-图像滤波对⽐图：
<img width="813" height="200" alt="1c5d48a56c182242b0e1d0ab251d5ce" src="https://github.com/user-attachments/assets/6c690289-9279-46ea-a0f2-89f21f7f6859" />
<img width="802" height="198" alt="03ee6464fe91215f11bf74cdaff4f1a" src="https://github.com/user-attachments/assets/90769d8e-781b-42c8-a177-f11d0877789d" />

### 5、中值滤波
-
-⼿动构建中值滤波效果图：
<img width="740" height="385" alt="1a9c79f0549d2df72f88ef0cdb49349" src="https://github.com/user-attachments/assets/caab9e22-ec6c-4054-a381-de268be2cf83" />


## 三、实验结果与分析

## 四、实验小结
