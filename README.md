Bài 1:
- Đọc ảnh gốc bằng PIL và chuyển thành mảng NumPy.
image = Image.open('bird.png')
arr = np.array(image)
- Tạo 3 ảnh khác màu nhau
red_image = arr.copy()
red_image[:, :, 1] = 0
red_image[:, :, 2] = 0

green_image = arr.copy()
green_image[:, :, 0] = 0
green_image[:, :, 2] = 0

blue_image = arr.copy()
blue_image[:, :, 0] = 0
blue_image[:, :, 1] = 0

- Hiển thị 3 ảnh màu bằng matplotlib.
plt.figure(figsize=(12, 4))
plt.subplot(1, 3, 1)
plt.imshow(red_image)
plt.subplot(1, 3, 2)
plt.imshow(green_image)
plt.subplot(1, 3, 3)
plt.imshow(blue_image)
plt.tight_layout()
plt.show()

Bài 2
- Đọc ảnh gốc bằng PIL và chuyển thành mảng NumPy.
image = Image.open('bird.png')
arr = np.array(image)
-Đảo thứ tự kênh màu từ RGB sang BGR
swapped = arr[..., [2, 1, 0]]
- Hiển thị ảnh đã đảo kênh màu
  plt.imshow(swapped)

Bài 3
Đọc ảnh và chuyển sang RGB
image = Image.open('bird.png').convert('RGB')
Duyệt từng pixel và chuyển từ RGB sang HSV
for i in range(arr.shape[0]):
    for j in range(arr.shape[1]):
        hsv[i, j] = colorsys.rgb_to_hsv(arr[i, j, 0], arr[i, j, 1], arr[i, j, 2])
Tách các kênh H, S, V và chuyển về dạng 8-bit để hiển thị ( H = sắc độ; S = độ bão hòa; V= độ sáng)
H = (hsv[:, :, 0] * 255).astype(np.uint8)   
S = (hsv[:, :, 1] * 255).astype(np.uint8)   
V = (hsv[:, :, 2] * 255).astype(np.uint8)   

Bài 4
Duyệt từng pixel, chuyển RGB sang HSV, chỉnh sửa, rồi chuyển ngược HSV sang RGB
for i in range(arr.shape[0]):
    for j in range(arr.shape[1]):
        h, s, v = colorsys.rgb_to_hsv(arr[i, j, 0], arr[i, j, 1], arr[i, j, 2])
        ( Giảm Hue xuống 1/3 (dịch tông màu về phía đỏ/vàng))
        h = h / 3             
        ( Giảm độ sáng xuống 75%)
        v = v * 0.75         
        hsv[i, j] = colorsys.hsv_to_rgb(h, s, v)   # Chuyển lại về RGB
Bài 5
Đọc 3 ảnh dưới dạng grayscale (ảnh xám), giá trị float
a = iio.imread('baby.jpeg', mode='F')
b = iio.imread('balloons_noisy.png', mode='F')
c = iio.imread('flower.jpeg', mode='F')
Áp dụng lọc trung bình cho từng ảnh và chuyển sang kiểu uint8 (0–255)
d = sn.convolve(a, k).astype(np.uint8)
e = sn.convolve(b, k).astype(np.uint8)
f = sn.convolve(c, k).astype(np.uint8)
Lưu các ảnh đã được lọc vào file mới
iio.imsave('baby_mean.jpeg', d)
iio.imsave('balloons_noisy_mean.png', e)
iio.imsave('flower_mean.jpeg', f)


