# 📊 PERFORMANCE COMPARISON
## Before vs After Optimization

**Dokumentasi ini akan diupdate setelah notebook dijalankan dengan konfigurasi baru**

---

## 🔴 BEFORE OPTIMIZATION (Original)

### Configuration:
```python
# Data
- Normalization: None
- Features: Raw scale

# GA Hyperparameters
- Population Size: 50
- Generations: 30
- Crossover Rate: 0.8
- Mutation Rate: 0.1
- Elitism: 2
- Min Features: 3 (hardcoded)
```

### Results:

#### **Baseline Model (All 5 Features)**
```
Training Set:
├─ R² Score: 0.988478
├─ RMSE:     2.052552
└─ MAE:      1.626058

Validation Set:
├─ R² Score: 0.989296
├─ RMSE:     2.010813
└─ MAE:      1.599473

Testing Set:
├─ R² Score: 0.988969
├─ RMSE:     2.021842
└─ MAE:      1.612254
```

#### **GA-Optimized Model (3 Features)**
```
Selected Features:
- Hours Studied
- Previous Scores  
- Sleep Hours

Training Set:
├─ R² Score: 0.987367
├─ RMSE:     2.149172
└─ MAE:      ~1.65

Validation Set:
├─ R² Score: 0.988355
├─ RMSE:     2.097359
└─ MAE:      ~1.63

Testing Set:
├─ R² Score: 0.987733
├─ RMSE:     2.132090
└─ MAE:      ~1.65
```

#### **Comparison:**
```
Baseline vs GA-Optimized:
├─ Feature Reduction: 5 → 3 (40% reduction)
├─ R² Difference:     -0.12%
├─ RMSE Difference:   +5.45%
└─ Conclusion:        Baseline menang, tapi GA lebih simple
```

---

## 🟢 AFTER OPTIMIZATION (New Configuration)

### Configuration:
```python
# Data
- Normalization: StandardScaler (mean=0, std=1)
- Features: Normalized scale

# GA Hyperparameters
- Population Size: 50
- Generations: 50 ↑ (+66.7%)
- Crossover Rate: 0.8
- Mutation Rate: 0.08 ↓ (-20%)
- Elitism: 3 ↑ (+50%)
- Min Features: 1 (dynamic, not hardcoded)
```

### Results:

#### **Baseline Model (All 5 Features, Normalized)**
```
Training Set:
├─ R² Score: [AKAN DIISI SETELAH EKSEKUSI]
├─ RMSE:     [AKAN DIISI SETELAH EKSEKUSI]
└─ MAE:      [AKAN DIISI SETELAH EKSEKUSI]

Validation Set:
├─ R² Score: [AKAN DIISI SETELAH EKSEKUSI]
├─ RMSE:     [AKAN DIISI SETELAH EKSEKUSI]
└─ MAE:      [AKAN DIISI SETELAH EKSEKUSI]

Testing Set:
├─ R² Score: [AKAN DIISI SETELAH EKSEKUSI]
├─ RMSE:     [AKAN DIISI SETELAH EKSEKUSI]
└─ MAE:      [AKAN DIISI SETELAH EKSEKUSI]
```

#### **GA-Optimized Model (? Features, Normalized)**
```
Selected Features:
[AKAN DIISI SETELAH EKSEKUSI]

Training Set:
├─ R² Score: [AKAN DIISI SETELAH EKSEKUSI]
├─ RMSE:     [AKAN DIISI SETELAH EKSEKUSI]
└─ MAE:      [AKAN DIISI SETELAH EKSEKUSI]

Validation Set:
├─ R² Score: [AKAN DIISI SETELAH EKSEKUSI]
├─ RMSE:     [AKAN DIISI SETELAH EKSEKUSI]
└─ MAE:      [AKAN DIISI SETELAH EKSEKUSI]

Testing Set:
├─ R² Score: [AKAN DIISI SETELAH EKSEKUSI]
├─ RMSE:     [AKAN DIISI SETELAH EKSEKUSI]
└─ MAE:      [AKAN DIISI SETELAH EKSEKUSI]
```

#### **Comparison:**
```
Baseline vs GA-Optimized:
├─ Feature Reduction: [AKAN DIISI]
├─ R² Difference:     [AKAN DIISI]
├─ RMSE Difference:   [AKAN DIISI]
└─ Conclusion:        [AKAN DIISI]
```

---

## 📊 OVERALL IMPROVEMENT (Before → After)

### **Baseline Model:**
```
R² Score:
├─ Before: 0.988969
├─ After:  [AKAN DIISI]
└─ Change: [AKAN DIISI]

RMSE:
├─ Before: 2.021842
├─ After:  [AKAN DIISI]
└─ Change: [AKAN DIISI]
```

### **GA-Optimized Model:**
```
R² Score:
├─ Before: 0.987733
├─ After:  [AKAN DIISI]
└─ Change: [AKAN DIISI]

RMSE:
├─ Before: 2.132090
├─ After:  [AKAN DIISI]
└─ Change: [AKAN DIISI]

Features:
├─ Before: 3 features (hardcoded minimum)
├─ After:  [AKAN DIISI] features (dynamic selection)
└─ Change: [AKAN DIISI]
```

---

## 🎯 KEY INSIGHTS

### **Data Quality:**
```
Outliers Detected:
[AKAN DIISI SETELAH EKSEKUSI]

Multicollinearity (VIF):
[AKAN DIISI SETELAH EKSEKUSI]

Correlation with Target:
[AKAN DIISI SETELAH EKSEKUSI]
```

### **GA Convergence:**
```
Generations to Converge:
├─ Before: ~1-5 (stabil cepat)
├─ After:  [AKAN DIISI]
└─ Insight: [AKAN DIISI]

Best Fitness Evolution:
[AKAN DIISI SETELAH EKSEKUSI]
```

---

## 📝 NOTES

**Untuk mengisi data ini:**
1. Jalankan notebook dari awal
2. Catat semua metrics di cell output
3. Update file ini dengan angka aktual
4. Analyze improvement percentage
5. Write conclusion

**Expected Benefits:**
- ✅ Better or similar R² score
- ✅ Better or similar RMSE
- ✅ More flexible feature selection
- ✅ Better understanding of data quality
- ✅ More professional analysis

**Possible Outcomes:**

**Scenario 1: Performance Improvement**
- R² naik 0.1-0.3%
- RMSE turun 1-3%
- Fitur lebih sedikit atau sama
- 🎉 Best case!

**Scenario 2: Performance Stable**
- R² stabil (±0.05%)
- RMSE stabil (±1%)
- Fitur lebih sedikit
- ✅ Still good! (simpler model, same performance)

**Scenario 3: Slight Performance Drop**
- R² turun < 0.1%
- RMSE naik < 2%
- Fitur jauh lebih sedikit
- ⚖️ Trade-off: Simplicity vs Accuracy (acceptable)

**Tidak expected:**
- R² turun > 0.5%
- RMSE naik > 5%
- (Jika ini terjadi, perlu investigate)

---

**Status:** 🟡 Waiting for Execution  
**Last Updated:** 19 Dec 2025 (Initial)  
**Next Update:** After notebook execution
