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

## SLIDE 2: INTRODUCTION & PROBLEM STATEMENT
**Research Questions:**
- ❓ Can we maintain high prediction accuracy while reducing features?
- ❓ Which features are most critical for student performance?

**Motivasi:**
- 🎓 Early identification of at-risk students
- 📊 Traditional approaches use all features → overfitting, complexity
- 🎯 Feature selection reduces dimensionality & improves interpretability

**Dataset: Student Performance (Kaggle)**
- **Samples:** 10,000 students
- **Input Features (5):** Hours Studied, Previous Scores, Extracurricular Activities, Sleep Hours, Sample Question Papers Practiced
- **Target:** Performance Index (continuous)

---

## SLIDE 3: RESEARCH OBJECTIVES & CONTRIBUTIONS
**Objectives:**
1. Implement GA for automatic feature selection
2. Compare baseline (all features) vs GA-optimized (selected features)
3. Analyze trade-off: complexity vs accuracy
4. Develop categorical classification for practical assessment
5. Identify most influential features

**Key Contributions:**
- ✅ Comprehensive GA + Linear Regression integration framework
- ✅ 40% feature reduction with only 0.13% accuracy trade-off (ROI: 307:1)
- ✅ Categorical analysis: 92.05% accuracy
- ✅ Identified 3 critical features
- ✅ Practical deployment guidelines for educational institutions

---

## SLIDE 4: PREPROCESSING DATA
**Langkah-langkah:**
- ✅ Dataset: 10,000 sampel
- ✅ Label EnMETHODOLOGY OVERVIEW
**Integrated Approach:**

**Pipeline:**
```
Data → Preprocessing → Baseline Model → GA Feature Selection → GA-Optimized Model → Evaluation
```

**1. Preprocessing:**
- Label Encoding (categorical → numerical)
- Data Split: 60% Train / 20% Val / 20% Test
- StandardScaler: z = (x - μ) / σ (mean=0, std=1)
- **Critical:** Fit scaler on trDESIGN
**Chromosome Representation:**
- Binary vector: [b₁, b₂, b₃, b₄, b₅] where bᵢ ∈ {0, 1}
- 1 = feature selected, 0 = feature excluded
- Example: [1, 1, 0, 1, 0] = select features 1, 2, 4

**Genetic Operators:**
- **Selection:** Tournament selection (size=3)
- **Crossover:** Single-point crossover (rate=0.8)
- **Mutation:** Bit-flip mutation (rate=0.08)
- **Elitism:** Preserve top 3 chromosomes

**Fitness Function:**
- fitness(c) = R²_validation with selected features
- Train Linear Regression with subset → Evaluate on validation
- **Why validation R²?** Prevents overfitting, ensures generalization

**Hyperparameters:** Population=50, Generations=50
- ⭐ **Elitism:** 3 kromosom terbaik

**Fitness Function:**
- Maximize R² Score pada validation set
- Evaluasi setiap kombinasi fitur

**Hasil GA:**
- ✅ Konvergen dengan baik
- ✅ Memilih **3 dari 5 fitur** terbaik
GA ALGORITHM WORKFLOW
**Main GA Loop (Algorithm 1):**
1. Initialize population: 50 random chromosomes
2. Evaluate fitness for all chromosomes
3. **For each generation (50 total):**
   - Sort population by fitness
   - **Elitism:** Keep top 3 chromosomes
   - **Selection:** Tournament selection (k=3)
   - **Crossover:** Single-point (80% probability)
   - **Mutation:** Bit-flip (8% per bit)
   - Evaluate new chromosomes
   - Track best fitness & chromosome
4. Return best feature subset

**Convergence:**
- Initial best fitness: 0.9781 (Gen 0)
- Final best fitness: 0.9884 (Gen 50)
- ImprovemenEXPERIMENTAL RESULTS - BASELINE
**Baseline Model: Linear Regression with ALL 5 Features**

**Performance Metrics:**
| Metric | Training | Validation | Testing |
|--------|----------|------------|---------|
| **R²** | 0.9891 | 0.9890 | **0.9890** |
| **RMSE** | 2.0086 | 2.0146 | **2.0218** |
| **MAE** | 1.6018 | 1.6069 | **1.6123** |
| **MAPE** | 3.48% | 3.49% | **3.50%** |

**Key Observations:**
- ✅ Excellent performance (R² > 98.9%)
- ✅ Highly consistent across all sets
- ✅ No overfitting detected (Train-Test gap < 0.1%)
- ❓ **Question:** Do we need all 5 features?
**Metrik Performa:**
| Set | R² | RMSE | MAE | MAPE |
|-----|-----|------|-----|------|
| **Training** | 0.9874 | 2.1494 | 1.7148 | 3.64% |
| **Validation** | 0.9884 | 2.0974 | 1.6690 | 3.59% |
| **Testing** | 0.9877 | 2.1321 | 1.7052 | 3.70% |

**Interpretasi:**
- ✅ PerformaEXPERIMENTAL RESULTS - GA-OPTIMIZED
**GA-Optimized Model: 3 Selected Features**

**Selected Features by GA:**
| Feature | Coefficient | Interpretation |
|---------|-------------|----------------|
| **Previous Scores** | 17.5789 | ⭐ Most influential |
| **Hours Studied** | 7.4126 | Strong positive impact |
| **Sleep Hours** | 0.8253 | Moderate influence |

**Excluded Features:** Extracurricular Activities, Sample Question Papers

**Performance Metrics:**
| Metric | Training | Validation | Testing |
|--------|----------|------------|---------|
| **R²** | 0.9874 | 0.9884 | **0.9877** |
| **RMSE** | 2.1494 | 2.0974 | **2.1321** |
| **MAE** | 1.7148 | 1.6690 | **1.7052** |
| **MAPE** | 3.64% | 3.59% | **3.70%** |

**Key:** Still excellent performance with 40% fewer features!

**Key Insight:**
- 🎯 **Reduksi Fitur:** 40% (5→3 fitur)
- 📉 **TradeCOMPARATIVE ANALYSIS
**Head-to-Head Comparison (Test Set):**

| Metric | Baseline (5) | GA-Opt (3) | Difference |
|--------|--------------|------------|------------|
| **Features** | 5 | 3 | **-40%** ✅ |
| **R²** | 0.9890 | 0.9877 | -0.13% |
| **RMSE** | 2.0218 | 2.1321 | +5.46% |
| **MAE** | 1.6123 | 1.7052 | +5.76% |
| **MAPE** | 3.50% | 3.70% | +0.20% |

**Trade-off Analysis:**
- 🎯 **Complexity Reduction:** 40% (5 → 3 features)
- 📉 **Accuracy Cost:** Only 0.13% R² decrease
- ⚡ **ROI (Return on Investment):** **307:1**
  - Formula: (40% / 0.13%) = 307.7

**Interpretation:** Exceptional trade-off! Model achieves **99.87%** of maximum performance with **60%** of features.** 100% (10/10 sampel)

**Aplikasi PrCATEGORICAL PERFORMANCE ANALYSIS
**Practical Classification System:**

**Quartile-based Categories:**
- 🏆 **Excellent:** > 75.73 (Q₃)
- ✅ **Good:** 60.63 - 75.73 (Q₂-Q₃)
- 📊 **Average:** 45.48 - 60.63 (Q₁-Q₂)
- ⚠️ **Poor:** < 45.48 (Q₁)

**Classification Results (GA Model):**
- **Categorical Accuracy:** 92.05%
- **Confusion Matrix:** Strong diagonal (accurate predictions)
- **Sample Match Rate:** 100% (10/10 samples correct)

**Practical Applications:**
1. **Early Warning System:** Identify at-risk students (Poor/Average)
2. **Resource Allocation:** Target interventions efficiently
3. **Personalized Recommendations:** Based on 3 key features
4. **Automated Monitoring:** Real-time alerts for performance drops
| Accuracy | 9.89 | 9.88 | Baseline |
| Simplicity | 5.0 | 10.0 | **GA** ✅ |
| Speed | 7.0 | 10.0 | **GA** ✅ |
| Interpretability | 7.0 | 10.0 | **GA** ✅ |
| **TOTAL** | 7.14/10 | **9.93/10** | **GA** 🏆 |

**Kesimpulan:** GA model mencapai **99.87%** performa maksimal dengan **60%** fitur

---

## SLIDE 11: KESIMPULAN & REKOMENDASI
**Kesimpulan DISCUSSION & MODEL SELECTION
**Why Choose GA-Optimized Model?**

**Multi-Criteria Evaluation:**
| Criterion | Baseline | GA-Optimized | Winner |
|-----------|----------|--------------|--------|
| Accuracy | 9.89/10 | 9.88/10 | Baseline |
| Simplicity | 5.0/10 | 10.0/10 | **GA** ✅ |
| Inference Speed | 7.0/10 | 10.0/10 | **GA** ✅ |
| Interpretability | 7.0/10 | 10.0/10 | **GA** ✅ |
| Data Collection | 6.0/10 | 9.5/10 | **GA** ✅ |
| **OVERALL** | **7.14/10** | **9.93/10** | **GA** 🏆 |

**Advantages of GA-Optimized:**
- ✅ Simpler model (easier to explain to stakeholders)
- ✅ Faster inference (production-ready)
- ✅ Lower data collection burden (only 3 features)
- ✅ Better generalization (reduced overfitting risk)
- ✅ Cost-effective (ROI 307:1)

**Limitations:** GA computation time higher, stochastic results
---

## SLIDE 12: CONCLUSION
**Key Findings:**
1. ✅ **Successful Integration:** GA + Linear Regression effectively reduces features
2. ✅ **Exceptional Trade-off:** 40% reduction for 0.13% accuracy cost (ROI: 307:1)
3. ✅ **Critical Features Identified:** Previous Scores (17.58), Hours Studied (7.41), Sleep Hours (0.83)
4. ✅ **High Categorical Accuracy:** 92.05% for practical classification
5. ✅ **No Overfitting:** Both models consistent across train/val/test
6. ✅ **Production-Ready:** GA-optimized scores 9.93/10 vs baseline's 7.14/10

**Future Work:**
- Multi-objective GA (accuracy + simplicity simultaneously)
- Test with advanced algorithms (Random Forest, XGBoost)
- Longitudinal studies across multiple academic terms
- Real-world deployment in educational institutions

**Impact:** Simpler, faster, interpretable model achieving 99.87% of maximum performance

**Thank You! Questions? 🙋**

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