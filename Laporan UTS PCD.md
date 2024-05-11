# PROJECT UTS PENGOLAHAN CITRA 2024

_Nama_  
Bagas Imanuel Pasaribu  
_NIM_  
202231101  
_Pengolahan Citra Digital D_

## Project No 1

__1. Import Library:__
```
import cv2
import matplotlib.pyplot as plt
```
Di sini, dua library diimpor: OpenCV (cv2) untuk pengolahan gambar dan Matplotlib (`matplotlib.pyplot`) untuk visualisasi data.

__2. Membaca Gambar:__  
```
gambar = cv2.imread('citraBagas.jpg')
```
Gambar dengan nama 'citraBagas.jpg' dibaca menggunakan OpenCV dan disimpan dalam variabel `gambar`.

__3. Konversi Gambar ke Ruang Warna BGR dan RGB:__ 
```
gambar_RGB = cv2.cvtColor(gambar, cv2.COLOR_BGR2RGB)
```
Gambar diubah ke ruang warna RGB menggunakan OpenCV. Konversi ini diperlukan karena OpenCV menggunakan skema warna BGR secara default, sedangkan Matplotlib menggunakan skema warna RGB.  

__4. Memisahkan Kanal Warna:__ 
```
kanal_merah = gambar_RGB[:,:,0]
kanal_hijau = gambar_RGB[:,:,1]
kanal_biru = gambar_RGB[:,:,2]
```
Kanal warna (merah, hijau, biru) dipisahkan dari gambar RGB untuk analisis lebih lanjut..  

__5. Menampilkan Gambar Kanal Warna dalam Skala Abu-abu:__ 
```
plt.figure(figsize=(15, 4))

# Gambar Asli
plt.subplot(1, 4, 1)
plt.imshow(cv2.cvtColor(gambar_RGB, cv2.COLOR_RGB2BGR))
plt.title('Gambar Asli')
plt.axis('off')

# Gambar Kanal Merah
plt.subplot(1, 4, 2)
plt.imshow(kanal_merah, cmap='gray')
plt.title('Kanal Merah')
plt.axis('off')

# Gambar Kanal Hijau
plt.subplot(1, 4, 3)
plt.imshow(kanal_hijau, cmap='gray')
plt.title('Kanal Hijau')
plt.axis('off')

# Gambar Kanal Biru
plt.subplot(1, 4, 4)
plt.imshow(kanal_biru, cmap='gray')
plt.title('Kanal Biru')
plt.axis('off')

plt.tight_layout()
plt.show()
```
Gambar kanal warna (merah, hijau, biru) ditampilkan dalam subplot dengan skala abu-abu menggunakan Matplotlib.  

__6. Menghitung Histogram untuk Setiap Kanal Warna:__ 
```
hist_merah = cv2.calcHist([kanal_merah], [0], None, [256], [0,256])
hist_hijau = cv2.calcHist([kanal_hijau], [0], None, [256], [0,256])
hist_biru = cv2.calcHist([kanal_biru], [0], None, [256], [0,256])
```
Histogram dihitung untuk setiap kanal warna menggunakan fungsi `cv2.calcHist`. Ini memberikan informasi tentang distribusi intensitas piksel dalam setiap kanal warna.  

__7. Menampilkan Histogram:__ 
```
plt.plot(hist_merah, color='r')
plt.plot(hist_hijau, color='g')
plt.plot(hist_biru, color='b')
plt.title('Histogram Warna Merah, Hijau, dan Biru')
plt.xlabel('Nilai Intensitas')
plt.ylabel('Frekuensi')
plt.show()
```
Histogram untuk setiap kanal warna (merah, hijau, biru) ditampilkan menggunakan Matplotlib dengan warna yang sesuai. Ini membantu dalam analisis distribusi intensitas piksel dalam gambar.

## Project No 2

__1. Import Library:__
```
import cv2
import numpy as np
import matplotlib.pyplot as plt
```
Pada langkah ini, library yang diperlukan diimpor. `cv2` untuk pengolahan gambar dan visi komputer, `numpy` untuk manipulasi array, dan `matplotlib.pyplot` untuk visualisasi data.

__2. Membaca Gambar:__  
```
gambar = cv2.imread('citraBagas.jpg')
```
Gambar dengan nama 'citraBagas.jpg' dibaca menggunakan OpenCV `(cv2.imread)` dan disimpan dalam variabel `gambar`.

__3. KKonversi Gambar ke Ruang Warna HSV:__ 
```
hsv = cv2.cvtColor(gambar, cv2.COLOR_BGR2HSV)
```
Gambar yang telah dibaca dikonversi ke ruang warna HSV (Hue, Saturation, Value) menggunakan OpenCV.

__4. Definisi Ambang Batas (Rentang) Warna untuk Biru, Merah, dan Hijau:__ 
```
biru_bawah = np.array([100, 43, 46])
biru_atas = np.array([130, 255, 255])
merah_bawah = np.array([160, 43, 46])
merah_atas = np.array([180, 255, 255])
hijau_bawah = np.array([36, 43, 46])
hijau_atas = np.array([70, 255, 255])
```
Rentang warna untuk biru, merah, dan hijau didefinisikan dalam format HSV. Nilai-nilai ini menentukan rentang warna yang akan dideteksi.

__5. Membuat Masker untuk Setiap Warna:__ 
```
biru_mask = cv2.inRange(hsv, biru_bawah, biru_atas)
merah_mask = cv2.inRange(hsv, merah_bawah, merah_atas)
hijau_mask = cv2.inRange(hsv, hijau_bawah, hijau_atas)
```
Masker (binary image) dibuat untuk setiap warna berdasarkan rentang warna yang telah ditentukan.  

__6. Temukan Piksel yang Cocok dengan Setiap Warna:__ 
```
biru_piksel = cv2.bitwise_and(gambar, gambar, mask=biru_mask)
merah_piksel = cv2.bitwise_and(gambar, gambar, mask=merah_mask)
hijau_piksel = cv2.bitwise_and(gambar, gambar, mask=hijau_mask)
```
Piksel yang cocok dengan setiap warna ditentukan dengan menggunakan operasi bitwise AND antara gambar asli dan masker warna.  

__7. Menampilkan Gambar Asli dan Hasil Deteksi Warna:__ 
```
plt.figure(figsize=(10, 5))
plt.subplot(2, 2, 1)
plt.imshow(cv2.cvtColor(gambar, cv2.COLOR_BGR2RGB))
plt.title('Gambar Asli')
plt.axis('off')

plt.subplot(2, 2, 2)
plt.imshow(cv2.cvtColor(biru_piksel, cv2.COLOR_BGR2RGB))
plt.title('Biru')
plt.axis('off')

plt.subplot(2, 2, 3)
plt.imshow(cv2.cvtColor(merah_piksel, cv2.COLOR_BGR2RGB))
plt.title('Merah')
plt.axis('off')

plt.subplot(2, 2, 4)
plt.imshow(cv2.cvtColor(hijau_piksel, cv2.COLOR_BGR2RGB))
plt.title('Hijau')
plt.axis('off')

plt.tight_layout()
plt.show()
```
Gambar asli dan gambar yang telah dideteksi untuk setiap warna (biru, merah, hijau) ditampilkan dalam subplot menggunakan Matplotlib. Gambar disertai dengan judul dan sumbu x dan y dinonaktifkan untuk memperbaiki tampilan.
## Teori Yang Mendukung  
Berikut adalah teori yang mendukung proyek ini:

1. OpenCV (Open Source Computer Vision Library):

- OpenCV adalah pustaka sumber terbuka yang berfokus pada pengolahan gambar dan visi komputer.
- Ini menyediakan berbagai algoritma untuk pengolahan gambar, seperti deteksi objek, pengenalan wajah, transformasi geometris, segmentasi gambar, dll.
- Dalam proyek ini, Anda menggunakan OpenCV untuk membaca gambar, konversi warna, dan menghitung histogram.

2. Konversi Warna:
- Gambar dalam komputer disimpan dalam bentuk matriks di mana setiap elemen mewakili nilai piksel.
- OpenCV menggunakan skema warna BGR (Blue-Green-Red) sebagai defaultnya, sementara matplotlib menggunakan RGB (Red-Green-Blue).
- Oleh karena itu, Anda perlu mengonversi gambar dari BGR ke RGB saat menggunakan matplotlib untuk memastikan warna ditampilkan dengan benar.

3. Histogram:
- Histogram adalah grafik yang menunjukkan distribusi intensitas piksel dalam gambar.
- Histogram digunakan untuk menganalisis kontras, kecerahan, dan distribusi warna dalam gambar.
- Dalam proyek ini, Anda menggunakan `cv2.calcHist` untuk menghitung histogram untuk setiap kanal warna (merah, hijau, biru).

4. Matplotlib:

- Matplotlib adalah pustaka visualisasi data yang kuat di Python.
- Ini menyediakan fungsi untuk membuat plot, grafik, dan gambar.
- Dalam proyek ini, Anda menggunakan Matplotlib untuk membuat plot histogram dan menampilkan gambar kanal warna dalam subplot.
