# 🎓 Student Performance Prediction Project
## Linear Regression + Genetic Algorithm Optimization

**Tugas Besar Kecerdasan Artifisial**  
**Universitas Telkom - Semester Ganjil 2025/2026**

---

## 👥 Tim Pengembang

- **Muhammad Azigha Azhar** (103012300143)
- **Ahmad Raffi Arasy** (103012330207)
- **Axel Davin Lazar Panenggak** (103012330386)

**Mata Kuliah:** Kecerdasan Artifisial (CAK3DAR3)  
**Dosen:** [Nama Dosen]

---

## 📁 Struktur Project

```
AIProject/
├── main.ipynb                      # Notebook utama (COMPLETE ANALYSIS)
├── README.md                       # File ini (Project overview)
├── CHANGELOG_OPTIMIZATION.md       # Dokumentasi lengkap semua perubahan
├── SUMMARY_OPTIMIZATION.txt        # Quick reference optimasi
└── PERFORMANCE_COMPARISON.md       # Perbandingan Before/After
```

---

## 🎯 Tujuan Project

Memprediksi **Performance Index** siswa menggunakan:
- **Metode Learning:** Linear Regression (Supervised Learning)
- **Optimasi:** Genetic Algorithm untuk Feature Selection
- **Integrasi:** GA → Feature Selection → Linear Regression

---

## 📊 Dataset

**Source:** [Kaggle - Student Performance Dataset](https://www.kaggle.com/datasets/nikhil7280/student-performance-multiple-linear-regression)

**Fitur (5 Features):**
1. Hours Studied
2. Previous Scores
3. Extracurricular Activities (Yes/No)
4. Sleep Hours
5. Sample Question Papers Practiced

**Target:**
- Performance Index (10-100)

**Statistik:**
- Total Samples: 10,000
- Missing Values: None
- Categorical Features: 1 (Extracurricular Activities)

---

## 🔬 Metodologi

### **1. Data Quality Analysis** ✨ NEW!
- Outlier detection (Z-Score method)
- Distribution visualization (Histogram + Box Plot)
- Correlation matrix & heatmap
- Multicollinearity check (VIF)

### **2. Preprocessing**
- Label Encoding untuk categorical features
- StandardScaler normalization ✨ NEW!
- Train/Val/Test split (60%/20%/20%)

### **3. Feature Selection (Genetic Algorithm)**
- Population-based optimization
- Tournament selection
- Single-point crossover
- Bit-flip mutation
- Elitism strategy

**GA Hyperparameters (OPTIMIZED):** ✨ NEW!
```python
population_size = 50
generations     = 50  # ↑ dari 30
crossover_rate  = 0.8
mutation_rate   = 0.08  # ↓ dari 0.1
elitism         = 3  # ↑ dari 2
min_features    = 1  # Dinamis (tidak hardcoded 3)
```

### **4. Model Training**
- **Baseline:** Linear Regression (all features)
- **GA-Optimized:** Linear Regression (selected features)

### **5. Evaluation**
- Metrics: R², RMSE, MAE, MSE
- Comparison: Baseline vs GA-Optimized
- Visualization: Predictions, Residuals, Feature Importance

---

## 🚀 Cara Menjalankan

### **Prerequisites:**
```bash
Python 3.8+
Jupyter Notebook / VS Code
```

### **Install Dependencies:**
```bash
pip install kagglehub pandas numpy matplotlib seaborn scikit-learn scipy statsmodels
```

### **Run Notebook:**
1. Buka `main.ipynb` di Jupyter/VS Code
2. Run semua cells dari atas ke bawah
3. Tunggu hingga selesai (~3-5 menit)

⚠️ **PENTING:** Jalankan semua cells secara berurutan karena ada dependencies!

---

## 📈 Hasil (Expected)

### **Before Optimization:**
```
Baseline Model:
- Test R²:   98.90%
- Test RMSE: 2.022
- Features:  5

GA-Optimized Model:
- Test R²:   98.77%
- Test RMSE: 2.132
- Features:  3 (Hours Studied, Previous Scores, Sleep Hours)
```

### **After Optimization:** ✨ NEW!
```
[Akan diupdate setelah eksekusi]
- Expected: Sedikit improvement atau stable
- Benefit: Analisis jauh lebih lengkap & professional
```

Lihat `PERFORMANCE_COMPARISON.md` untuk detail lengkap.

---

## 📚 Dokumentasi

### **Main Files:**

#### **1. main.ipynb**
Notebook lengkap berisi:
- Section 1: Pendahuluan & Data
  - 1.1 Penjelasan Masalah
  - 1.2 Import Libraries
  - 1.3 Load Dataset
  - 1.4 Statistik Deskriptif
  - **1.5 Data Quality Analysis** ✨ NEW!
  - 1.6 Preprocessing
  - 1.7 Train/Val/Test Split
  - **1.8 Normalization** ✨ NEW!
- Section 2: Metode & Eksperimen
  - 2.1 Linear Regression Theory
  - 2.2 Evaluation Metrics
  - 2.3 Hyperparameters
  - 2.4 Genetic Algorithm
  - 2.5 GA Execution
  - 2.6 GA Convergence
  - 2.7 Model Comparison
- Section 3: Hasil & Analisis
  - 3.1 Best Model Analysis
  - 3.2 Performance Comparison
  - 3.3 Visualizations
- Section 4: Kesimpulan

#### **2. CHANGELOG_OPTIMIZATION.md**
Dokumentasi lengkap:
- Kondisi awal (before)
- Semua perubahan (what changed)
- Rationale (why changed)
- Expected results (impact)

**Gunakan untuk:**
- Understanding perubahan
- Presentasi (show improvements)
- Laporan akhir

#### **3. SUMMARY_OPTIMIZATION.txt**
Quick reference untuk:
- Main changes
- Expected results
- Important notes
- Presentation tips

#### **4. PERFORMANCE_COMPARISON.md**
Template untuk dokumentasi hasil:
- Before metrics (sudah diisi)
- After metrics (isi setelah eksekusi)
- Improvement calculation
- Insights & conclusions

---

## 🎯 Key Features

### **✨ What's NEW in Optimized Version:**

1. **Data Quality Analysis** 🆕
   - Comprehensive outlier detection
   - Beautiful visualizations
   - Correlation insights
   - VIF multicollinearity check

2. **Feature Normalization** 🆕
   - StandardScaler implementation
   - Better model stability
   - Improved interpretability

3. **Optimized GA** 🆕
   - More generations (30→50)
   - Better mutation rate (0.1→0.08)
   - Enhanced elitism (2→3)
   - Dynamic min features (not hardcoded)

4. **Professional Analysis** 🆕
   - Publication-quality plots
   - Comprehensive statistics
   - Best practices applied
   - Excellent for presentation

---

## 📊 Visualizations

Project ini menghasilkan visualisasi:

1. **Data Quality:**
   - Distribution histograms (6 features)
   - Box plots for outliers (6 features)
   - Correlation heatmap
   - VIF bar chart

2. **GA Convergence:**
   - Best vs Average Fitness
   - Feature selection results

3. **Model Performance:**
   - Predicted vs Actual (Train/Val/Test)
   - Residuals distribution
   - Feature importance (coefficients)
   - Model comparison

4. **Before/After Normalization:**
   - Statistics comparison
   - Scale transformation

---

## 🎓 Untuk Presentasi

### **Poin Kunci:**

1. **Problem Statement**
   - Prediksi performance siswa
   - Faktor-faktor yang berpengaruh
   - Aplikasi praktis

2. **Metodologi**
   - Linear Regression (simple & interpretable)
   - GA optimization (feature selection)
   - Data-driven approach

3. **Data Quality** ✨ HIGHLIGHT!
   - Comprehensive analysis
   - No missing values
   - Outliers handled
   - Multicollinearity checked

4. **Optimization** ✨ HIGHLIGHT!
   - Normalization applied
   - GA hyperparameters tuned
   - Professional workflow

5. **Results**
   - High R² (98.9%+)
   - Low RMSE (~2 points)
   - Simple model (3-5 features)
   - Interpretable coefficients

6. **Insights**
   - Hours Studied = most important
   - Previous Scores = second
   - Sleep Hours = moderate impact
   - Sample Papers = least impact

### **Demo Flow:**
1. Show dataset
2. Show data quality visualizations 🌟
3. Explain normalization 🌟
4. Run GA (show convergence)
5. Compare models
6. Show predictions
7. Interpret results

---

## 🔧 Troubleshooting

**Q: Notebook error "module not found"?**  
A: Install semua dependencies dengan pip install

**Q: GA terlalu lama?**  
A: Normal, generations naik dari 30→50 (~2-3 menit)

**Q: Results berbeda setiap run?**  
A: GA stochastic, tapi dengan random_state=42 should be reproducible

**Q: Performance turun setelah optimization?**  
A: Check PERFORMANCE_COMPARISON.md, trade-off simplicity vs accuracy acceptable

**Q: Cell error di tengah?**  
A: Restart kernel, run from beginning (ada dependencies)

---

## 📖 References

**Dataset:**
- Kaggle: Student Performance Dataset
- URL: https://www.kaggle.com/datasets/nikhil7280/student-performance-multiple-linear-regression

**Algorithms:**
- Scikit-learn: Linear Regression
- Custom implementation: Genetic Algorithm
- Scipy: Z-Score outlier detection
- Statsmodels: VIF calculation

**Literatur:**
- Linear Regression: Ordinary Least Squares
- Genetic Algorithms: Holland (1975)
- Feature Selection: Wrapper methods
- StandardScaler: Standardization techniques

---

## 💡 Tips

### **Untuk Development:**
- ✅ Selalu run cells berurutan
- ✅ Check visualizations untuk insights
- ✅ Compare before/after metrics
- ✅ Document findings di notebook

### **Untuk Presentation:**
- ✅ Prepare demo notebook
- ✅ Save key visualizations as images
- ✅ Practice explanation flow
- ✅ Prepare Q&A scenarios

### **Untuk Laporan:**
- ✅ Include semua visualizations
- ✅ Reference CHANGELOG for improvements
- ✅ Show metrics comparison
- ✅ Explain rationale for optimization

---

## 📞 Contact

Untuk pertanyaan atau diskusi:

- **Muhammad Azigha Azhar** - 103012300143
- **Ahmad Raffi Arasy** - 103012330207
- **Axel Davin Lazar Panenggak** - 103012330386

**Email:** [Email tim jika ada]  
**Repository:** [GitHub link jika ada]

---

## 📝 License

Project ini dibuat untuk keperluan akademik (Tugas Besar Kecerdasan Artifisial).

---

## ✅ Checklist Project

- [x] Dataset loaded
- [x] Data quality analysis
- [x] Preprocessing complete
- [x] Feature normalization
- [x] GA implementation
- [x] GA optimization
- [x] Model training
- [x] Model evaluation
- [x] Visualizations
- [x] Documentation
- [ ] Notebook execution
- [ ] Results analysis
- [ ] Presentation preparation
- [ ] Laporan final

---

**Last Updated:** 19 December 2025  
**Version:** 2.0 (Optimized)  
**Status:** ✅ Ready for Execution

---

**🚀 GOOD LUCK! 🎓**
