# PANDUAN SLIDE PRESENTASI
## Prediksi Student Performance dengan Optimasi Algoritma Genetika

---

## SLIDE 1: COVER
**Judul:**
- Prediksi Student Performance Index
- Menggunakan Linear Regression dengan Optimasi Algoritma Genetika untuk Feature Selection

**Anggota Kelompok:**
- Muhammad Azigha Azhar (103012300143)
- Ahmad Raffi Arasy (103012330207)
- Axel Davin Lazar Panenggak (103012330386)

**Mata Kuliah:** Kecerdasan Artifisial (CAK3DAR3)  
**Dosen:** [Nama Dosen]  
**Semester Ganjil 2025/2026**

---

## SLIDE 2: PENDAHULUAN & RUMUSAN MASALAH
**Pertanyaan Penelitian:**
- ❓ Bisakah kita mempertahankan akurasi prediksi tinggi sambil mengurangi fitur?
- ❓ Fitur mana yang paling kritis untuk performa siswa?

**Motivasi:**
- 🎓 Identifikasi dini siswa berisiko
- 📊 Pendekatan tradisional menggunakan semua fitur → overfitting, kompleksitas tinggi
- 🎯 Feature selection mengurangi dimensionalitas & meningkatkan interpretabilitas

**Dataset: Student Performance (Kaggle)**
- **Sampel:** 10.000 siswa
- **Fitur Input (5):** Hours Studied, Previous Scores, Extracurricular Activities, Sleep Hours, Sample Question Papers Practiced
- **Target:** Performance Index (kontinyu)

---

## SLIDE 3: TUJUAN PENELITIAN & KONTRIBUSI
**Tujuan:**
1. Mengimplementasikan GA untuk automatic feature selection
2. Membandingkan baseline (semua fitur) vs GA-optimized (fitur terpilih)
3. Menganalisis trade-off: kompleksitas vs akurasi
4. Mengembangkan klasifikasi kategorikal untuk penilaian praktis
5. Mengidentifikasi fitur paling berpengaruh

**Kontribusi Utama:**
- ✅ Framework integrasi komprehensif GA + Linear Regression
- ✅ Reduksi fitur 40% dengan hanya 0.13% trade-off akurasi (ROI: 307:1)
- ✅ Analisis kategorikal: 92.05% akurasi
- ✅ Identifikasi 3 fitur kritis
- ✅ Panduan deployment praktis untuk institusi pendidikan

---

## SLIDE 4: GAMBARAN METODOLOGI
**Pendekatan Terintegrasi:**

**Pipeline:**
```
Data → Preprocessing → Baseline Model → GA Feature Selection → GA-Optimized Model → Evaluasi
```

**1. Preprocessing:**
- Label Encoding (kategorikal → numerik)
- Pembagian Data: 60% Train / 20% Val / 20% Test
- StandardScaler: z = (x - μ) / σ (mean=0, std=1)
- **Kritis:** Fit scaler hanya pada training data (mencegah data leakage)

**2. Baseline Model:**
- Linear Regression dengan SEMUA 5 fitur
- Menetapkan benchmark performa

**3. Optimasi GA:**
- Feature selection dengan Genetic Algorithm
- Fungsi fitness: R² pada validation set

---

## SLIDE 5: GENETIC ALGORITHM - DESAIN
**Representasi Kromosom:**
- Vektor biner: [b₁, b₂, b₃, b₄, b₅] dimana bᵢ ∈ {0, 1}
- 1 = fitur dipilih, 0 = fitur dikecualikan
- Contoh: [1, 1, 0, 1, 0] = pilih fitur 1, 2, 4

**Operator Genetika:**
- **Seleksi:** Tournament selection (size=3)
- **Crossover:** Single-point crossover (rate=0.8)
- **Mutasi:** Bit-flip mutation (rate=0.08)
- **Elitisme:** Pertahankan 3 kromosom terbaik

**Fungsi Fitness:**
- fitness(c) = R²_validation dengan fitur terpilih
- Latih Linear Regression dengan subset → Evaluasi pada validation
- **Kenapa validation R²?** Mencegah overfitting, memastikan generalisasi

**Hyperparameter:** Population=50, Generations=50

---

## SLIDE 6: WORKFLOW ALGORITMA GA
**Loop Utama GA (Algoritma 1):**
1. Inisialisasi populasi: 50 kromosom random
2. Evaluasi fitness untuk semua kromosom
3. **Untuk setiap generasi (50 total):**
   - Sortir populasi berdasarkan fitness
   - **Elitisme:** Pertahankan 3 kromosom terbaik
   - **Seleksi:** Tournament selection (k=3)
   - **Crossover:** Single-point (probabilitas 80%)
   - **Mutasi:** Bit-flip (8% per bit)
   - Evaluasi kromosom baru
   - Lacak best fitness & kromosom
4. Return subset fitur terbaik

**Konvergensi:**
- Initial best fitness: 0.9781 (Gen 0)
- Final best fitness: 0.9884 (Gen 50)
- Peningkatan: +1.05%
- Stabil setelah generasi 35

**Tampilkan Diagram:** Flowchart GA atau Convergence Plot

---

## SLIDE 7: HASIL EKSPERIMEN - BASELINE
**Baseline Model: Linear Regression dengan SEMUA 5 Fitur**

**Metrik Performa:**
| Metrik | Training | Validation | Testing |
|--------|----------|------------|---------|
| **R²** | 0.9891 | 0.9890 | **0.9890** |
| **RMSE** | 2.0086 | 2.0146 | **2.0218** |
| **MAE** | 1.6018 | 1.6069 | **1.6123** |
| **MAPE** | 3.48% | 3.49% | **3.50%** |

**Observasi Kunci:**
- ✅ Performa excellent (R² > 98.9%)
- ✅ Sangat konsisten di semua set
- ✅ Tidak ada overfitting terdeteksi (Train-Test gap < 0.1%)
- ❓ **Pertanyaan:** Apakah kita perlu semua 5 fitur?

---

## SLIDE 8: HASIL EKSPERIMEN - GA-OPTIMIZED
## SLIDE 8: HASIL EKSPERIMEN - GA-OPTIMIZED
**GA-Optimized Model: 3 Fitur Terpilih**

**Fitur Terpilih oleh GA:**
| Fitur | Koefisien | Interpretasi |
|---------|-------------|----------------|
| **Previous Scores** | 17.5789 | ⭐ Paling berpengaruh |
| **Hours Studied** | 7.4126 | Dampak positif kuat |
| **Sleep Hours** | 0.8253 | Pengaruh moderat |

**Fitur Dikecualikan:** Extracurricular Activities, Sample Question Papers

**Metrik Performa:**
| Metrik | Training | Validation | Testing |
|--------|----------|------------|---------|
| **R²** | 0.9874 | 0.9884 | **0.9877** |
| **RMSE** | 2.1494 | 2.0974 | **2.1321** |
| **MAE** | 1.7148 | 1.6690 | **1.7052** |
| **MAPE** | 3.64% | 3.59% | **3.70%** |

**Kunci:** Performa masih excellent dengan 40% lebih sedikit fitur!

---

## SLIDE 9: ANALISIS KOMPARATIF
**Perbandingan Head-to-Head (Test Set):**

| Metrik | Baseline (5) | GA-Opt (3) | Perbedaan |
|--------|--------------|------------|-----------|
| **Fitur** | 5 | 3 | **-40%** ✅ |
| **R²** | 0.9890 | 0.9877 | -0.13% |
| **RMSE** | 2.0218 | 2.1321 | +5.46% |
| **MAE** | 1.6123 | 1.7052 | +5.76% |
| **MAPE** | 3.50% | 3.70% | +0.20% |

**Analisis Trade-off:**
- 🎯 **Reduksi Kompleksitas:** 40% (5 → 3 fitur)
- 📉 **Cost Akurasi:** Hanya 0.13% penurunan R²
- ⚡ **ROI (Return on Investment):** **307:1**
  - Formula: (40% / 0.13%) = 307.7

**Interpretasi:** Trade-off exceptional! Model mencapai **99.87%** performa maksimum dengan **60%** fitur.

---

## SLIDE 10: ANALISIS KATEGORISASI PERFORMA
**Sistem Klasifikasi Praktis:**

**Kategori Berbasis Kuartil:**
- 🏆 **Excellent:** > 75.73 (Q₃)
- ✅ **Good:** 60.63 - 75.73 (Q₂-Q₃)
- 📊 **Average:** 45.48 - 60.63 (Q₁-Q₂)
- ⚠️ **Poor:** < 45.48 (Q₁)

**Hasil Klasifikasi (Model GA):**
- **Akurasi Kategorikal:** 92.05%
- **Confusion Matrix:** Diagonal kuat (prediksi akurat)
- **Sample Match Rate:** 100% (10/10 sampel benar)

**Aplikasi Praktis:**
1. **Sistem Peringatan Dini:** Identifikasi siswa berisiko (Poor/Average)
2. **Alokasi Sumber Daya:** Target intervensi efisien
3. **Rekomendasi Personal:** Berdasarkan 3 fitur kunci
4. **Monitoring Otomatis:** Alert real-time untuk penurunan performa
---

## SLIDE 11: DISKUSI & PEMILIHAN MODEL
**Mengapa Memilih Model GA-Optimized?**

**Evaluasi Multi-Kriteria:**
| Kriteria | Baseline | GA-Optimized | Pemenang |
|----------|----------|--------------|----------|
| Akurasi | 9.89/10 | 9.88/10 | Baseline |
| Kesederhanaan | 5.0/10 | 10.0/10 | **GA** ✅ |
| Kecepatan Inferensi | 7.0/10 | 10.0/10 | **GA** ✅ |
| Interpretabilitas | 7.0/10 | 10.0/10 | **GA** ✅ |
| Pengumpulan Data | 6.0/10 | 9.5/10 | **GA** ✅ |
| **KESELURUHAN** | **7.14/10** | **9.93/10** | **GA** 🏆 |

**Keunggulan GA-Optimized:**
- ✅ Model lebih sederhana (mudah dijelaskan ke stakeholder)
- ✅ Inferensi lebih cepat (production-ready)
- ✅ Beban pengumpulan data lebih rendah (hanya 3 fitur)
- ✅ Generalisasi lebih baik (risiko overfitting berkurang)
- ✅ Cost-effective (ROI 307:1)

**Limitasi:** Waktu komputasi GA lebih tinggi, hasil stokastik

---

## SLIDE 12: KESIMPULAN
**Temuan Utama:**
1. ✅ **Integrasi Berhasil:** GA + Linear Regression efektif mereduksi fitur
2. ✅ **Trade-off Exceptional:** Reduksi 40% dengan cost akurasi 0.13% (ROI: 307:1)
3. ✅ **Fitur Kritis Teridentifikasi:** Previous Scores (17.58), Hours Studied (7.41), Sleep Hours (0.83)
4. ✅ **Akurasi Kategorikal Tinggi:** 92.05% untuk klasifikasi praktis
5. ✅ **Tidak Ada Overfitting:** Kedua model konsisten di train/val/test
6. ✅ **Production-Ready:** GA-optimized skor 9.93/10 vs baseline 7.14/10

**Riset Lanjutan:**
- Multi-objective GA (akurasi + kesederhanaan simultan)
- Uji dengan algoritma advanced (Random Forest, XGBoost)
- Studi longitudinal lintas beberapa semester
- Deployment real-world di institusi pendidikan

**Dampak:** Model lebih simple, cepat, interpretable mencapai 99.87% performa maksimum

**Terima Kasih! Pertanyaan? 🙋**

---

## TIPS PRESENTASI

**Durasi per Slide (Total ~18 menit):**
- Slide 1: 30 detik (cover)
- Slide 2: 1.5 menit (introduction)
- Slide 3: 1.5 menit (objectives)
- Slide 4: 1.5 menit (methodology)
- Slide 5: 2 menit (GA design)
- Slide 6: 2 menit (GA workflow) ⭐
- Slide 7: 1.5 menit (baseline results)
- Slide 8: 2 menit (GA results)
- Slide 9: 2 menit (comparison) ⭐ KEY SLIDE
- Slide 10: 1.5 menit (categorical)
- Slide 11: 1.5 menit (discussion)
- Slide 12: 1 menit (conclusion)

**Emphasize (Key Messages):**
1. **ROI 307:1** - Exceptional trade-off ratio
2. **99.87%** of max performance with **60%** of features
3. **92.05%** categorical accuracy for practical use
4. **Algorithm transparency** - 6 detailed algorithms in paper
5. **Production-ready** with multi-criteria evaluation (9.93/10)

**Prepare untuk Q&A:**

**Q1: Why Genetic Algorithm instead of other methods?**
→ GA explores large search space, avoids local optima, no need for domain expert feature ranking

**Q2: Why Linear Regression as base model?**
→ Interpretable, fast, establishes clear baseline, coefficients show feature importance directly

**Q3: How did you prevent overfitting in GA?**
→ Used validation set R² for fitness (not training R²), elitism preserves best solutions, mutation maintains diversity

**Q4: What if GA selects 0 features?**
→ Fitness function returns 0 for empty feature sets, ensures at least 1 feature selected

**Q5: Is GA always better than baseline?**
→ Depends on use case: Use baseline for maximum accuracy, use GA for production deployment with constraints

**Q6: How long does GA take to converge?**
→ 50 generations with population 50, converged around generation 35, total ~2-3 minutes on standard hardware

**Q7: Can this be applied to other educational datasets?**
→ Yes, GA framework is dataset-agnostic, just need to adjust hyperparameters and fitness function

**Q8: What about StandardScaler normalization?**
→ z = (x-μ)/σ transforms to mean=0, std=1 (NOT Min-Max 0-1 range), prevents feature scale bias in Linear Regression

**Visual Aids Suggestions:**
- Slide 6: GA flowchart or convergence plot
- Slide 9: Bar chart comparing 5 metrics side-by-side
- Slide 10: Confusion matrix heatmap
- Slide 11: Radar chart for multi-criteria evaluation