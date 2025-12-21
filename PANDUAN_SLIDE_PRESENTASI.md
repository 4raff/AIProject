# PANDUAN SLIDE PRESENTASI (10 SLIDES)
## Prediksi Student Performance dengan Optimasi Algoritma Genetika

---

## SLIDE 1: COVER
**Judul:**
Prediksi Student Performance Index Menggunakan Linear Regression dengan Optimasi Algoritma Genetika untuk Feature Selection

**Anggota Kelompok:**
- Muhammad Azigha Azhar (103012300143)
- Ahmad Raffi Arasy (103012330207)
- Axel Davin Lazar Panenggak (103012330386)

**Mata Kuliah:** Kecerdasan Artifisial (CAK3DAR3)
**Semester Ganjil 2025/2026**

---

## SLIDE 2: PENDAHULUAN & RUMUSAN MASALAH
**Latar Belakang:**
- 🎓 Prediksi performa siswa penting untuk early intervention
- 📊 Dataset dengan banyak fitur → kompleksitas tinggi, risiko overfitting
- 🎯 Perlu identifikasi fitur kritis untuk model efisien

**Pertanyaan Penelitian:**
1. ❓ Bisakah akurasi tinggi dipertahankan sambil mengurangi fitur?
2. ❓ Fitur mana yang paling kritis untuk performa siswa?
3. ❓ Berapa trade-off antara kompleksitas dan akurasi?

**Motivasi:**
- Identifikasi dini siswa berisiko
- Model lebih interpretable untuk stakeholder
- Efisiensi pengumpulan data & inference

---

## SLIDE 3: DATASET & TUJUAN PENELITIAN
**Dataset: Student Performance (Kaggle)**
- **Jumlah:** 10.000 siswa
- **Fitur (5):** 
  - Hours Studied (jam belajar per minggu)
  - Previous Scores (nilai ujian sebelumnya)
  - Extracurricular Activities (Ya/Tidak)
  - Sleep Hours (jam tidur per hari)
  - Sample Question Papers Practiced (jumlah latihan soal)
- **Target:** Performance Index (skor 10-100, kontinyu)
- **Split:** 60% Train / 20% Validation / 20% Test

**Tujuan:**
1. Mengimplementasikan GA untuk automatic feature selection
2. Membandingkan baseline (5 fitur) vs GA-optimized (fitur terpilih)
3. Menganalisis trade-off kompleksitas vs akurasi
4. Mengidentifikasi fitur paling berpengaruh
5. Mengembangkan klasifikasi kategorikal untuk aplikasi praktis

---

## SLIDE 4: METODOLOGI - PREPROCESSING & BASELINE
**Pipeline Eksperimen:**
```
Data (10k) → Preprocessing → Baseline Model (5 fitur) → GA Feature Selection → GA-Optimized (3 fitur) → Evaluasi
```

**Preprocessing:**
- **Label Encoding:** Extracurricular Activities (Yes=1, No=0)
- **Data Split:** 6000 train / 2000 validation / 2000 test
- **Standardization:** z = (x - μ) / σ
  - Scaler fit HANYA pada training → mencegah data leakage
  - Mean = 0, Std = 1

**Baseline Model:**
- **Algoritma:** Linear Regression (Ordinary Least Squares)
- **Fitur:** SEMUA 5 fitur
- **Tujuan:** Benchmark performa maksimum

---

## SLIDE 5: GENETIC ALGORITHM - DESAIN
**Representasi Kromosom:**
- **Encoding:** Vektor biner [b₁, b₂, b₃, b₄, b₅], bᵢ ∈ {0, 1}
- **Interpretasi:** 1 = fitur dipilih, 0 = fitur dikecualikan
- **Contoh:** [1, 1, 0, 1, 0] = pilih fitur 1, 2, 4

**Fungsi Fitness:**
- **Metrik:** R² validation (coefficient of determination)
- **Evaluasi:** Train Linear Regression dengan subset fitur → hitung R² pada validation set
- **Kenapa validation?** Mencegah overfitting, memastikan generalisasi

**Operator Genetika:**
- **Seleksi:** Tournament selection (size=3) → 3 kandidat, pilih terbaik
- **Crossover:** Single-point crossover, rate=0.8 (80% kemungkinan)
- **Mutasi:** Bit-flip mutation, rate=0.08 (8% per bit)
- **Elitisme:** Pertahankan 3 kromosom terbaik setiap generasi

**Hyperparameter:**
- Population size: 50
- Generations: 50
- Total evaluasi: 50 × 50 = 2,500 kandidat

---

## SLIDE 6: HASIL GA - KONVERGENSI & FITUR TERPILIH
**Konvergensi GA:**
- **Initial best fitness (Gen 0):** R² = 0.9781
- **Final best fitness (Gen 50):** R² = 0.9884
- **Peningkatan:** +1.05% (0.0103 poin)
- **Stabilitas:** Konvergen stabil setelah generasi 35
- **Visualisasi:** Grafik konvergensi menunjukkan optimasi efektif

**Fitur Terpilih oleh GA:**
| Fitur | Status | Koefisien | Interpretasi |
|-------|--------|-----------|--------------|
| **Previous Scores** | ⭐ Terpilih | **17.5789** | Prediktor terkuat |
| **Hours Studied** | ⭐ Terpilih | **7.4126** | Dampak positif signifikan |
| **Sleep Hours** | ⭐ Terpilih | **0.8253** | Pengaruh moderat |
| Extracurricular Activities | ❌ Dikecualikan | - | Redundan/korelasi rendah |
| Sample Question Papers | ❌ Dikecualikan | - | Redundan/korelasi rendah |

**Insight:** GA berhasil reduksi 40% fitur (5→3) sambil mempertahankan akurasi tinggi!

---

## SLIDE 7: HASIL EKSPERIMEN - BASELINE MODEL
**Baseline: Linear Regression dengan SEMUA 5 Fitur**

**Performa Lengkap:**
| Metrik | Training | Validation | Testing |
|--------|----------|------------|---------|
| **R²** | 0.9885 | 0.9890 | **0.9890** |
| **RMSE** | 2.0526 | 2.0974 | **2.0218** |
| **MAE** | 1.6261 | 1.6690 | **1.6123** |
| **MAPE** | 3.45% | 3.59% | **3.50%** |

**Observasi Kunci:**
- ✅ **Akurasi Excellent:** R² > 98.9% → model menjelaskan 98.9% varian
- ✅ **Konsistensi Tinggi:** Train-Val-Test sangat dekat (gap < 0.1%)
- ✅ **Tidak Ada Overfitting:** Model generalisasi baik
- ✅ **Error Rendah:** MAPE 3.50% → prediksi rata-rata error 3.5%
- ❓ **Pertanyaan:** Apakah semua 5 fitur benar-benar diperlukan?

---

## SLIDE 8: HASIL EKSPERIMEN - GA-OPTIMIZED MODEL
**GA-Optimized: Linear Regression dengan 3 Fitur Terpilih**

**Performa Lengkap:**
| Metrik | Training | Validation | Testing |
|--------|----------|------------|---------|
| **R²** | 0.9874 | 0.9884 | **0.9877** |
| **RMSE** | 2.1495 | 2.0974 | **2.1321** |
| **MAE** | 1.7148 | 1.6690 | **1.7052** |
| **MAPE** | 3.64% | 3.59% | **3.70%** |

**Observasi Kunci:**
- ✅ **Akurasi Masih Excellent:** R² = 98.77% (hanya turun 0.13%)
- ✅ **Konsistensi Terjaga:** Train-Val-Test gap < 0.2%
- ✅ **Model Lebih Sederhana:** 40% lebih sedikit fitur
- ✅ **Trade-off Minimal:** MAPE 3.70% (hanya +0.20% dari baseline)

**Model Coefficients:**
- Performance Index = 17.5789 × Previous Scores + 7.4126 × Hours Studied + 0.8253 × Sleep Hours

---

## SLIDE 9: ANALISIS KOMPARATIF & TRADE-OFF
**Perbandingan Head-to-Head (Test Set):**

| Kriteria | Baseline (5 Fitur) | GA-Optimized (3 Fitur) | Perbedaan |
|----------|-------------------|----------------------|-----------|
| **Jumlah Fitur** | 5 | 3 | **-40%** ✅ |
| **R²** | 0.9890 | 0.9877 | -0.13% |
| **RMSE** | 2.0218 | 2.1321 | +5.46% |
| **MAE** | 1.6123 | 1.7052 | +5.76% |
| **MAPE** | 3.50% | 3.70% | +0.20% |

**Analisis Trade-off:**
- 🎯 **Reduksi Kompleksitas:** 40% (5 → 3 fitur)
- 📉 **Cost Akurasi:** Hanya 0.13% penurunan R²
- ⚡ **Return on Investment (ROI):** **307:1**
  - Formula: (40% reduksi) / (0.13% cost) = 307.7
  - Interpretasi: Setiap 1% penurunan akurasi menghemat 307% kompleksitas!
- 🏆 **Performa Relatif:** Model mencapai **99.87%** dari performa maksimum baseline

**Kesimpulan:** Trade-off SANGAT exceptional → model praktis untuk production!

---

## SLIDE 10: KATEGORISASI, APLIKASI & KESIMPULAN
**Klasifikasi Kategorikal (Berbasis Kuartil):**
| Kategori | Threshold | Interpretasi |
|----------|-----------|--------------|
| 🏆 **Excellent** | > 70 (Q₃) | Performa sangat tinggi |
| ✅ **Good** | 55-70 (Q₂-Q₃) | Performa di atas rata-rata |
| 📊 **Average** | 40-55 (Q₁-Q₂) | Performa rata-rata |
| ⚠️ **Poor** | < 40 (Q₁) | Perlu intervensi |

**Hasil (Model GA):** Akurasi Kategorikal = **92.05%** | Confusion Matrix diagonal kuat

**Aplikasi Praktis:**
1. **Early Warning System:** Identifikasi siswa Poor/Average untuk intervensi dini
2. **Rekomendasi Personal:** Optimasi Hours Studied & Sleep Hours berdasarkan Previous Scores
3. **Alokasi Sumber Daya:** Fokus tutoring pada kategori berisiko
4. **Monitoring Real-time:** Alert otomatis penurunan performa

**KESIMPULAN UTAMA:**
1. ✅ GA + Linear Regression berhasil reduksi **40% fitur** dengan ROI **307:1**
2. ✅ **3 Fitur kritis:** Previous Scores (17.58), Hours Studied (7.41), Sleep Hours (0.83)
3. ✅ Akurasi kategorisasi **92.05%** → aplikasi praktis feasible
4. ✅ **Tidak ada overfitting** (train-test gap < 0.2%)
5. ✅ Model **production-ready:** Score 9.93/10 vs baseline 7.14/10

**Riset Lanjutan:** Multi-objective GA | Algoritma advanced (RF, XGBoost) | Deployment real-world

**Terima Kasih! 🙋 Pertanyaan?**

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