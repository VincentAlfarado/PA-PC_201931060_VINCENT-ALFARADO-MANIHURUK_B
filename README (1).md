
# UAS PENGCID

cv2 adalah modul OpenCV yang digunakan untuk pemrosesan gambar.
numpy adalah pustaka untuk operasi numerik yang digunakan untuk membuat dan mengelola matriks.
matplotlib.pyplot adalah pustaka untuk menampilkan gambar.

cv.imread('Foto Diri.jpg') membaca gambar dari file bernama Foto Diri.jpg.
Jika gambar tidak ditemukan (misalnya, path salah), program akan memunculkan error FileNotFoundError.

img.shape[:2] mengembalikan ukuran gambar dalam bentuk (tinggi, lebar).

img_asli = img.copy()
Menyimpan salinan dari gambar asli untuk ditampilkan nanti.

height, width = img.shape[:2]
resized = cv.resize(img, (width // 2, height), interpolation=cv.INTER_CUBIC)
Mengubah ukuran gambar dengan memperkecil lebar menjadi setengah menggunakan interpolasi bicubic.

M_translate = np.float32([[1, 0, 100], [0, 1, 100]])
translated = cv.warpAffine(img, M_translate, (cols + 100, rows + 100))
Membuat matriks translasi untuk menggeser gambar 100 piksel ke kanan dan 100 piksel ke bawah.
Menerapkan matriks translasi pada gambar.

(tinggi, lebar) = img.shape[:2]
pusat = (lebar // 2, tinggi // 2)
M_rotate = cv.getRotationMatrix2D(pusat, 45, 1.0)
rotated = cv.warpAffine(img, M_rotate, (lebar, tinggi))
Menentukan pusat rotasi di tengah gambar.
Membuat matriks rotasi untuk memutar gambar sebesar 45 derajat.
Menerapkan matriks rotasi pada gambar.

cropped = img[50:300, 50:300]
Memotong bagian gambar dari koordinat (50,50) sampai (300,300).

flipped = cv.flip(img, 1)
Membalik gambar secara horizontal.

fig, axs = plt.subplots(2, 3, figsize=(15, 10))

axs[0, 0].imshow(cv.cvtColor(img_asli, cv.COLOR_BGR2RGB))
axs[0, 0].set_title('Citra Asli')
axs[0, 0].axis('off')

axs[0, 1].imshow(cv.cvtColor(rotated, cv.COLOR_BGR2RGB))
axs[0, 1].set_title('After Rotated')
axs[0, 1].axis('off')

axs[0, 2].imshow(cv.cvtColor(resized, cv.COLOR_BGR2RGB))
axs[0, 2].set_title('After Resized')
axs[0, 2].axis('off')

axs[1, 0].imshow(cv.cvtColor(cropped, cv.COLOR_BGR2RGB))
axs[1, 0].set_title('After Cropped')
axs[1, 0].axis('off')

axs[1, 1].imshow(cv.cvtColor(flipped, cv.COLOR_BGR2RGB))
axs[1, 1].set_title('After Flipped')
axs[1, 1].axis('off')

axs[1, 2].imshow(cv.cvtColor(translated, cv.COLOR_BGR2RGB))
axs[1, 2].set_title('After Translated')
axs[1, 2].axis('off')

plt.show()

Membuat layout 2x3 menggunakan Matplotlib untuk menampilkan gambar asli dan hasil transformasi.
Menggunakan imshow untuk menampilkan gambar dalam format RGB (karena OpenCV menggunakan BGR secara default).
Menambahkan judul untuk setiap gambar.
Menonaktifkan sumbu pada setiap gambar menggunakan axis('off').
Menampilkan semua gambar menggunakan plt.show().
