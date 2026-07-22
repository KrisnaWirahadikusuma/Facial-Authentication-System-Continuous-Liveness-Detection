# Facial-Authentication-System-Continuous-Liveness-Detection

Sistem keamanan biometrik berbasis Python yang dirancang untuk pengawasan ujian online dan verifikasi identitas secara real-time. Dilengkapi dengan mekanisme Anti-Spoofing (Continuous Liveness Check) untuk menolak manipulasi berbasis foto atau layar perangkat.

Fitur Utama
Real-Time Face Mesh Tracking: Memetakan titik koordinat wajah secara presisi menggunakan MediaPipe Face Mesh dengan visualisasi jaring-jaring (tesselation) futuristik berwarna kuning.

Active Liveness & Anti-Spoofing: Mencegah spoofing attack (bypass menggunakan foto/video statis) melalui sistem verifikasi kedipan berkelanjutan. Sistem otomatis mencabut status verifikasi jika pengguna diam kaku atau tidak berkedip dalam batas waktu tertentu.

Auto-Reset Session: Mendeteksi saat wajah keluar dari frame dan secara otomatis mengulang durasi pemindaian (scanning phase) begitu wajah kembali terdeteksi.

Audio & Visual Feedback: Terintegrasi dengan winsound untuk memberikan peringatan suara instan ketika wajah tidak terdeteksi atau terindikasi anomali/spoofing, dipadu dengan antarmuka UI dinamis berbasis warna (Hijau, Oranye, Merah).

Lightweight Architecture: Dibangun murni menggunakan OpenCV dan MediaPipe tanpa ketergantungan pada library berat berlisensi C++ seperti dlib atau face_recognition, sehingga bebas dari error saat instalasi.

🛠️ Tech Stack
Language: Python 3.x

Computer Vision: OpenCV (cv2)

Machine Learning / Facial Landmark: MediaPipe (mp.solutions.face_mesh, mp.solutions.face_detection)

Utility & Audio: time, winsound
