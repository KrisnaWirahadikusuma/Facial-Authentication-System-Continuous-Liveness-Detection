# Real-Time Facial Biometric Authentication and Anti-Spoofing System for Proctored Academic Examinations

[![Python](https://img.shields.io/badge/Python-3.x-blue.svg)](https://www.python.org/)
[![OpenCV](https://img.shields.io/badge/OpenCV-Computer%25Vision-green.svg)](https://opencv.org/)
[![MediaPipe](https://img.shields.io/badge/MediaPipe-Face%25Mesh-orange.svg)](https://developers.google.com/mediapipe)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

## Abstrak / Ringkasan Proyek
Sistem pengawasan ujian daring (*online proctoring*) rentan terhadap berbagai bentuk kecurangan, termasuk penggunaan media cetak statis atau layar sekunder (*presentation attack / spoofing*). Proyek ini mengembangkan sistem verifikasi biometrik wajah berbasis *Computer Vision* yang mengintegrasikan **Continuous Liveness Detection (Deteksi Keaktifan Berkelanjutan)** menggunakan algoritma *Mesh Tracking*. Sistem dirancang untuk beroperasi secara *real-time* dengan mendeteksi kedipan mata (*blink detection*) dan melacak kehadiran subjek secara dinamis guna menjamin integritas akademik selama evaluasi berlangsung.

---

## 🔬 Arsitektur dan Metodologi Sistem

Sistem ini dibangun dengan meminimalkan ketergantungan pada pustaka kompleks berlisensi C++ (seperti `dlib`), sehingga lebih ringan dan andal di berbagai lingkungan perangkat keras.

1. **Face Detection & Bounding Box**: 
   Menggunakan *MediaPipe Face Detection* untuk mendeteksi koordinat spasial wajah secara akurat pada setiap frame video.
2. **Facial Landmark & Mesh Tessellation**: 
   Memetakan 468 titik landmark wajah menggunakan *MediaPipe Face Mesh* untuk menghasilkan visualisasi *tesselation* yang memantau geometri wajah secara konstan.
3. **Active Liveness Protocol (Anti-Spoofing)**: 
   Menerapkan metrik jarak vertikal kelopak mata (*Eye Aspect Ratio* tidak langsung via indeks landmark $159$ dan $145$). Pengguna diwajibkan melakukan kedipan berkala dalam rentang waktu yang ditentukan (`VERIFY_DURATION`) untuk membuktikan keaslian subjek.
4. **State Machine & Auto-Reset**: 
   * Jika wajah terdeteksi keluar dari *frame*, sistem secara otomatis mencabut status verifikasi dan membunyikan peringatan akustik (`winsound`).
   * Jika wajah baru masuk kembali, sistem otomatis menginisialisasi ulang fase *scanning* (hitung mundur 4.5 detik) untuk menunggu konfirmasi kedipan berikutnya.

---

## 🛠️ Spesifikasi Perangkat Lunak (Tech Stack)
* **Bahasa Pemrograman**: Python 3.x
* **Pengolahan Citra Digital**: OpenCV (`cv2`)
* **Machine Learning / Ekstraksi Fitur**: Google MediaPipe Solutions
* **Utilitas & Sistem Tanggap**: `time`, `winsound`

---

## 📂 Struktur Direktori Repositori
```text
facial-liveness-proctoring/
│
├── main.py              # Script utama logika sistem & antarmuka OpenCV
├── requirements.txt     # Daftar dependensi modul pustaka
└── README.md            # Dokumentasi sistem (Dokumen Akademik)
