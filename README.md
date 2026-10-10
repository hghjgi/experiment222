# 实验二：图像增强
202410315019-彭艺琼-人工智能241

## 一、实验目的
学会OpenCV的基本使用方法，利用OpenCV等计算机视觉库对图像进行平滑、滤波等操作，实现图像增强。

## 二、实验内容
### 1、导入图像滤波相关依赖包
- OpenCV库：计算机视觉与图像处理<br>
- scikit-image库：图像增强与分析，random_noise 用于给图像添加噪声<br>
- NumPy库：科学计算的基础库<br>
- Matplotlib库：绘图与数据可视化<br>
```
# =====================导入依赖库=====================
import cv2
from skimage.util import random_noise
import numpy as np
from matplotlib import pyplot as plt
```

### 2、读取原始图像并进行色彩空间转换
- 读取计算机本地图像文件，获取并输入【100，100】处像素点的RBG参数并输出,通过下面的输出结果可以看到，【100,100】像素点的RGB为【82,86,241】，表现为偏蓝色，通过图像也可以看到这个像素点属于猫猫的衣服处的深蓝色部位。<br>
```
# ====================读取原始图像=====================
img = cv2.imread('p1.jpg')
# 获取图像中【100，100】这个像素的rbg三色
(b, g, r) = img[100, 100]
# 打印这个像素点的rbg参数
print(b, g, r)
# 输出原始图像
plt.imshow(img)
plt.title('Original Image')
plt.savefig('output_images/original_bgr.jpg', dpi=300)
plt.show()
```
```
- 输出：
        82 86 241
```

- cv2.COLOR_BGR2GRAY是将原始图像的RBG格式转换为灰度图，将三维的RGB通道映射为一维的灰度通道<br>
```
# 将原始图像的RBG格式转换为灰度图
gray_img = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
plt.imshow(gray_img, cmap='gray')
plt.title('Gray Image')
plt.savefig('output_images/gray_image.jpg', dpi=300)
plt.show()
```
原图及灰度图如下：<br>
<img width="460" height="196" alt="2f26b782119c3da511eb62977e91cee" src="https://github.com/user-attachments/assets/e18b0682-51df-4b86-a586-abc14f058429" />

### 3、添加噪声
- 这里在原始图像的基础上添加噪声，引入了两个API方法，椒盐噪声和高斯噪声，通过对比可以发现，椒盐噪声和高斯噪声的本质不同，椒盐噪声表现为像素会随机替换为白色或者黑色像素（灰度通道），在RGB通道表现为像素变成随机彩色点，而高斯噪声会在每个像素上添加随机偏差，服从高斯分布<br>
```
# ==========================添加噪声=========================
# mode='s&p'代表椒盐噪声，s代表白色，p代表黑色，amount=0.4代表会有40%的像素会随机替换为白色或者黑色像素（灰度通道），在RGB通道表现为像素变成随机彩色点，更“杂乱”一点
sp_noise_img = random_noise(rgb_img, mode='s&p', amount=0.4)
# mode='gaussian' 代表高斯噪声，会在每个像素上添加随机偏差，服从高斯分布（均值=0，方差默认=0.01），我这里调整了均值和方差值，使其噪声更明显一点
gus_noise_img = random_noise(rgb_img, mode='gaussian', mean=0.2, var=0.03)

# 原图
plt.subplot(1, 3, 1)
plt.imshow(rgb_img, cmap='gray')
plt.title('Original Image')

# 椒盐噪声
plt.subplot(1, 3, 2)
plt.imshow(sp_noise_img, cmap='gray')
plt.title('S&P Noise')

# 高斯噪声
plt.subplot(1, 3, 3)
plt.imshow(gus_noise_img, cmap='gray')
plt.title('Gus Noise')

plt.tight_layout()
plt.savefig('output_images/noise_comparison.jpg', dpi=300)
plt.show()
```
噪声对⽐图：<br>
<img width="703" height="209" alt="c36c24b435f00301867613e4b15ad5a" src="https://github.com/user-attachments/assets/3ed0aa6b-48d8-40db-91c4-cd99362b722a" />

### 4、图像滤波
- 将图像认为产生噪声后，用OpenCV的三个API滤波方式进行对比，分别对椒盐滤波和高斯滤波使用【均值滤波】，【中值滤波】，【高斯滤波】，对比每个最适合的滤波方式。<br>
```
# =========================图像滤波=============================
# 均值滤波
mean_sp = cv2.blur(sp_noise_img, (5, 5))
mean_gus = cv2.blur(gus_noise_img, (5, 5))

# 中值滤波（需要 uint8）
mid_sp = cv2.medianBlur((sp_noise_img*255).astype(np.uint8), 5)
mid_gus = cv2.medianBlur((gus_noise_img*255).astype(np.uint8), 5)

# 高斯滤波
gauss_sp = cv2.GaussianBlur((sp_noise_img*255).astype(np.uint8), (5, 5), 0)
gauss_gus = cv2.GaussianBlur((gus_noise_img*255).astype(np.uint8), (5, 5), 0)

# 图像显示
plt.figure(figsize=(13, 9))
# 第1行：椒盐噪声
plt.subplot(2, 3, 1)
plt.imshow(mean_sp)
plt.title("S&P noise with Mean Filter")

plt.subplot(2, 3, 2)
plt.imshow(mid_sp)
plt.title("S&P Noise with Median Filter")

plt.subplot(2, 3, 3)
plt.imshow(gauss_sp)
plt.title("S&P Noise with Gaussian Filter")

# 第2行：高斯噪声
plt.subplot(2, 3, 4)
plt.imshow(mean_gus)
plt.title("Gaussian noise with Mean Filter")

plt.subplot(2, 3, 5)
plt.imshow(mid_gus)
plt.title("Gaussian noise with Median Filter")

plt.subplot(2, 3, 6)
plt.imshow(gauss_gus)
plt.title("Gaussian noise with Gaussian Filter")

plt.tight_layout()
plt.savefig('result/filter_results_2x3.jpg', dpi=300)
plt.show()
```
图像滤波对⽐图：<br>
<img width="813" height="200" alt="1c5d48a56c182242b0e1d0ab251d5ce" src="https://github.com/user-attachments/assets/6c690289-9279-46ea-a0f2-89f21f7f6859" /><img width="802" height="198" alt="03ee6464fe91215f11bf74cdaff4f1a" src="https://github.com/user-attachments/assets/90769d8e-781b-42c8-a177-f11d0877789d" />

### 5、中值滤波
```
# ===========================手动实现中值滤波============================
def manual_median_filter_color(image, kernel_size=5):
    """
    手动实现彩色图像的中值滤波
    :param image: 输入彩色图像，numpy数组，shape=(H, W, 3)
    :param kernel_size: 滤波窗口大小
    :return: 中值滤波后的彩色图像
    """
    pad = kernel_size // 2
    # 对每个通道单独处理
    filtered_img = np.zeros_like(image)

    for c in range(3):  # 遍历通道 R,G,B
        channel = image[:, :, c]
        padded_channel = np.pad(channel, pad_width=pad, mode='edge')
        for i in range(channel.shape[0]):
            for j in range(channel.shape[1]):
                region = padded_channel[i:i + kernel_size, j:j + kernel_size]
                filtered_img[i, j, c] = np.median(region)

    return filtered_img


# 对之前添加椒盐噪声的图像进行手动中值滤波
manual_mid = manual_median_filter_color((sp_noise_img * 255).astype(np.uint8), kernel_size=5)

# 显示对比
plt.figure(figsize=(8, 4))

plt.subplot(1, 2, 1)
plt.imshow(sp_noise_img, cmap='gray')
plt.title("s&p noise img")

plt.subplot(1, 2, 2)
plt.imshow(manual_mid, cmap='gray')
plt.title("manual median filter")

plt.tight_layout()
plt.savefig('result/manual_median.jpg', dpi=300)
plt.show()
```
⼿动构建中值滤波效果图：<br>
<img width="740" height="385" alt="1a9c79f0549d2df72f88ef0cdb49349" src="https://github.com/user-attachments/assets/caab9e22-ec6c-4054-a381-de268be2cf83" />

## 三、实验结果与分析
- 实验完成图像色彩转换，添加了椒盐噪声与高斯噪声。椒盐噪声出现随机黑白噪点，高斯噪声使图像整体产生颗粒抖动。<br>
- 均值滤波对高斯噪声平滑效果较好，但去椒盐噪声效果差，容易模糊图像。中值滤波可以有效去除椒盐噪声、保留边缘，对高斯噪声效果一般。手动实现的中值滤波效果和库函数相近，不过运行速度较慢。<br>
- 实验说明不同噪声要选用合适滤波方法：高斯噪声适合均值滤波，椒盐噪声适合中值滤波，手动实现能帮助理解滤波原理。<br>

## 四、实验小结
- 本次实验学习了OpenCV图像读取、色彩空间转换的操作，给图像添加了椒盐噪声和高斯噪声，并使用多种滤波算法完成图像去噪。<br>
- 通过对比发现中值滤波适合去除椒盐噪声，均值滤波更适合处理高斯噪声。手动实现中值滤波，让我理解了滤波的底层逻辑。<br>
- 实验认识到没有通用的滤波算法，需要根据噪声类型选择合适的处理方式，为后续图像处理学习打下基础。<br>
