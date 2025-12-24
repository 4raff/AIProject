# SPEAKER NOTES PRESENTASI
## Prediksi Student Performance Index dengan Linear Regression + Genetic Algorithm

---

### SLIDE 1: COVER
Selamat pagi/siang, perkenalkan kami dari kelompok ... akan mempresentasikan penelitian berjudul "Prediksi Student Performance Index Menggunakan Linear Regression dengan Optimasi Algoritma Genetika untuk Feature Selection". Penelitian ini bertujuan membuat model prediksi performa siswa yang efisien dan akurat.

---

### SLIDE 2: PENDAHULUAN & RUMUSAN MASALAH
Motivasi utama riset ini adalah kebutuhan identifikasi dini siswa berisiko agar intervensi bisa dilakukan lebih cepat. Permasalahan yang kami angkat: (1) Bisakah akurasi prediksi tetap tinggi meski jumlah fitur dikurangi? (2) Fitur mana yang paling kritis untuk performa siswa? (3) Seberapa besar trade-off antara kompleksitas dan akurasi? Dengan model yang lebih sederhana, proses implementasi dan pengambilan keputusan di sekolah akan lebih efisien.

---

### SLIDE 3: DATASET & TUJUAN PENELITIAN
Kami menggunakan dataset Student Performance dari Kaggle, berisi 10.000 siswa dengan 5 fitur utama: Hours Studied, Previous Scores, Extracurricular Activities, Sleep Hours, dan Sample Question Papers Practiced. Target prediksi adalah Performance Index (skor 10-100). Data dibagi 60% train, 20% validation, 20% test. Tujuan penelitian: mengimplementasikan GA untuk feature selection, membandingkan baseline (semua fitur) dengan model GA, menganalisis trade-off, dan mengembangkan klasifikasi kategorikal untuk aplikasi praktis.

---

### SLIDE 4: METODOLOGI - PREPROCESSING & BASELINE
Data diproses dengan label encoding untuk fitur kategorikal, lalu distandarisasi (mean=0, std=1) hanya pada data training untuk mencegah data leakage. Baseline model menggunakan Linear Regression dengan semua 5 fitur sebagai benchmark performa maksimum. Model ini akan dibandingkan dengan model hasil seleksi fitur oleh GA.

---

### SLIDE 5: GENETIC ALGORITHM - DESAIN
GA merepresentasikan fitur sebagai kromosom biner, di mana 1 berarti fitur dipilih. Fitness function menggunakan R² pada validation set agar model tidak overfitting. Operator utama: tournament selection (size=3), crossover (0.8), mutasi (0.08), dan elitisme (top 3). Hyperparameter: populasi 50, generasi 50. Proses evolusi dilakukan selama 50 generasi untuk mencari kombinasi fitur terbaik.

---

### SLIDE 6: HASIL GA - KONVERGENSI & FITUR TERPILIH
GA menunjukkan konvergensi stabil: best fitness naik dari 0.9781 ke 0.9884, stabil setelah generasi ke-35. Fitur terpilih: Previous Scores (koef. 17.5789), Hours Studied (7.4126), Sleep Hours (0.8253). Dua fitur lain dikecualikan karena kontribusinya rendah. Ini membuktikan model bisa lebih sederhana tanpa kehilangan banyak akurasi.

---

### SLIDE 7: HASIL EKSPERIMEN - BASELINE MODEL
Baseline model dengan 5 fitur menghasilkan R² test 0.9890, RMSE 2.0218, MAE 1.6123, MAPE 3.50%. Model sangat akurat, konsisten di semua set, dan tidak overfitting (train-test gap < 0.1%). Ini menjadi acuan performa maksimum.

---

### SLIDE 8: HASIL EKSPERIMEN - GA-OPTIMIZED MODEL
Model GA-optimized dengan 3 fitur: R² test 0.9877, RMSE 2.1321, MAE 1.7052, MAPE 3.70%. Akurasi hanya turun 0.13% dibanding baseline, namun model jauh lebih sederhana dan efisien. Koefisien tiap fitur: Previous Scores 17.5789, Hours Studied 7.4126, Sleep Hours 0.8253.

---

### SLIDE 9: ANALISIS KOMPARATIF & TRADE-OFF
Perbandingan head-to-head: GA mengurangi kompleksitas 40% (5→3 fitur) dengan cost akurasi hanya 0.13%. ROI 307:1, artinya setiap 1% penurunan akurasi menghemat 307% kompleksitas. Model GA tetap menjelaskan 99.87% performa baseline, sehingga sangat efisien untuk deployment.

---

### SLIDE 10: KATEGORISASI, APLIKASI & KESIMPULAN
Kami juga menguji klasifikasi kategorikal (Excellent/Good/Average/Poor) dengan akurasi 91.65%. Model siap untuk sistem early warning, rekomendasi personal, dan alokasi sumber daya. Kesimpulan: GA + Linear Regression efektif, model sederhana, akurat, dan siap diimplementasikan di institusi pendidikan. Riset lanjutan bisa menguji multi-objective GA, algoritma lain, dan deployment real-world.

---

### TIPS PENJELASAN MAIN.IPYNB (Jika ditanya detail kode)
- Jelaskan preprocessing: label encoding, split, standardisasi.
- Tunjukkan cell baseline model: training, evaluasi, hasil metrik.
- Tunjukkan cell GA: inisialisasi, evolusi, konvergensi, fitur terpilih.
- Tunjukkan cell evaluasi: perbandingan metrik, confusion matrix, categorical accuracy.
- Tekankan semua hasil di slide diambil langsung dari output notebook, sehingga data valid dan konsisten.
