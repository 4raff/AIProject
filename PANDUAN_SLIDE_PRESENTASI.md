# PANDUAN SLIDE PRESENTASI (RINGKAS - 7 SLIDES)
## Prediksi Student Performance dengan Optimasi Algoritma Genetika

---

## SLIDE 1: COVER
**Judul:**
Prediksi Student Performance Index Menggunakan Linear Regression dengan Optimasi Algoritma Genetika untuk Feature Selection

**Anggota Kelompok:**
- Muhammad Azigha Azhar (103012300143)
- Ahmad Raffi Arasy (103012330207)
- Axel Davin Lazar Panenggak (103012330386)

**Mata Kuliah:** Kecerdasan Artifisial (CAK3DAR3) | **Semester Ganjil 2025/2026**

---

## SLIDE 2: PENDAHULUAN & KONTRIBUSI
**Pertanyaan Penelitian:**
- ❓ Bisakah akurasi tinggi dipertahankan sambil mengurangi fitur?
- ❓ Fitur mana yang paling kritis untuk performa siswa?

**Dataset: Student Performance (Kaggle)**
- **10.000 siswa** | **5 Fitur:** Hours Studied, Previous Scores, Extracurricular Activities, Sleep Hours, Sample Question Papers | **Target:** Performance Index

**Kontribusi Utama:**
- ✅ Reduksi fitur **40%** dengan trade-off akurasi hanya **0.13%** → **ROI 307:1**
- ✅ Identifikasi **3 fitur kritis**: Previous Scores, Hours Studied, Sleep Hours
- ✅ Akurasi kategorisasi **92.05%** untuk sistem early warning
- ✅ Model **production-ready** tanpa overfitting

---

## SLIDE 3: METODOLOGI & GENETIC ALGORITHM
**Pipeline:**
```
Data (10k) → Preprocessing (60/20/20) → Baseline (5 fitur) → GA Feature Selection → GA-Optimized (3 fitur)
```

**Genetic Algorithm:**
- **Kromosom:** Vektor biner [b₁,b₂,b₃,b₄,b₅], bᵢ ∈ {0,1} (1=pilih fitur)
- **Fitness:** R²_validation (mencegah overfitting)
- **Operator:** Tournament selection (size=3), Crossover (0.8), Mutation (0.08), Elitism (top 3)
- **Hyperparameter:** Population=50, Generations=50

**Konvergensi:**
- Initial: 0.9781 → Final: 0.9884 (+1.05%) | Stabil generasi 35

---

## SLIDE 4: HASIL - PERBANDINGAN MODEL
**Performa Comprehensive (Test Set):**

| Metrik | Baseline (5 Fitur) | GA-Optimized (3 Fitur) | Δ |
|--------|-------------------|----------------------|---|
| **R²** | 0.9890 | 0.9877 | -0.13% |
| **RMSE** | 2.0218 | 2.1321 | +5.46% |
| **MAE** | 1.6123 | 1.7052 | +5.76% |
| **MAPE** | 3.50% | 3.70% | +0.20% |

**Fitur Terpilih oleh GA:**
| Fitur | Koefisien | Status |
|-------|-----------|--------|
| Previous Scores | 17.5789 | ⭐ Terpilih |
| Hours Studied | 7.4126 | ⭐ Terpilih |
| Sleep Hours | 0.8253 | ⭐ Terpilih |
| Extracurricular | - | ❌ Dikecualikan |
| Sample Papers | - | ❌ Dikecualikan |

**Trade-off Ratio:** **307:1** (40% reduksi / 0.13% cost) → Model mencapai **99.87%** performa maksimum!

---

## SLIDE 5: ANALISIS KATEGORISASI & APLIKASI
**Kategorisasi Performa (Berbasis Kuartil):**
- 🏆 **Excellent:** > 70 | ✅ **Good:** 55-70 | 📊 **Average:** 40-55 | ⚠️ **Poor:** < 40

**Hasil Klasifikasi:**
- **Akurasi Kategorikal:** 92.05% | **Confusion Matrix:** Diagonal kuat

**Aplikasi Praktis:**
1. **Sistem Early Warning:** Identifikasi siswa berisiko (Poor/Average) secara real-time
2. **Rekomendasi Personal:** Optimasi Hours Studied & Sleep Hours berdasarkan Previous Scores
3. **Alokasi Sumber Daya:** Fokus tutoring pada kategori "Poor" dan "Average"

**Keunggulan GA-Optimized:**
- ✅ Model lebih sederhana & interpretable
- ✅ Inferensi lebih cepat (production-ready)
- ✅ Beban data collection 40% lebih rendah
- ✅ Multi-criteria score: **9.93/10** vs baseline **7.14/10**

---

## SLIDE 6: DISKUSI
**Mengapa GA-Optimized Unggul?**

**Trade-off Analysis:**
- **Interpretabilitas:** 3 fitur vs 5 fitur → mudah dijelaskan ke stakeholder
- **Efisiensi:** Training & inference 40% lebih cepat
- **Cost-Effective:** Hanya perlu monitor 3 metrik (Previous Scores, Hours Studied, Sleep Hours)

**Insight Feature Selection:**
- **Previous Scores** (koef. 17.58): Prediktor terkuat → achievement historis = indikator terbaik
- **Hours Studied** (koef. 7.41): Usaha belajar & time management krusial
- **Sleep Hours** (koef. 0.83): Kesejahteraan fisik penting untuk kognitif optimal
- **Eksklusi Extracurricular & Sample Papers**: Redundan atau korelasi rendah

**Limitasi:** Waktu komputasi GA tinggi (one-time cost), hasil stokastik, asumsi linear

---

## SLIDE 7: KESIMPULAN
**Temuan Utama:**
1. ✅ **GA + Linear Regression** mereduksi **40% fitur** dengan **ROI 307:1**
2. ✅ **3 Fitur kritis** teridentifikasi: Previous Scores (17.58), Hours Studied (7.41), Sleep Hours (0.83)
3. ✅ **Akurasi kategorisasi 92.05%** → sistem early warning praktis
4. ✅ **Tidak ada overfitting** (train-test gap < 0.1%)
5. ✅ Model **production-ready** (score 9.93/10) ideal untuk institusi resource-constrained

**Dampak:** Model lebih simple, cepat, interpretable mencapai **99.87%** performa maksimum

**Riset Lanjutan:**
- Multi-objective GA | Algoritma advanced (RF, XGBoost) | Studi longitudinal | Deployment real-world

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