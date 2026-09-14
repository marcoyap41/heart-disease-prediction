# heart-disease-prediction
---

## [Kelompok 5] Tugas Data Science KOM: Replikasi Metodologi Artikel Penerapan Sains Data
## Anggota

| Nama                    | NIM                |
| ----------------------- | ------------------ |
| Mikail Achmad           | 24/542370/PA/23026 |
| Marco Christian         | 24/539714/PA/22915 |
| Thufail Bahir Al Bariq  | 24/537843/PA/22801 |
| Erdizah Ghodi Al Haidar | 24/537670/PA/22787 |

---

Proyek data science untuk **mereplikasi dan menganalisis metodologi penelitian** pada artikel:

> **Heart Disease Prediction Using a Hybrid Feature Selection and Ensemble Learning Approach**

Proyek ini merupakan **proyek jangka panjang selama satu semester** yang akan dikembangkan secara bertahap menuju replikasi metodologi penelitian secara menyeluruh.

Repositori ini berisi kode dan laporan analisis data untuk mereplikasi dan mengaudit eksperimen *machine learning* dari jurnal **"Heart Disease Prediction Using a Hybrid Feature Selection and Ensemble Learning Approach"** (Gupta et al., 2025).

Proyek ini disusun untuk mendiagnosis penyakit jantung dengan memadukan algoritma *nature-inspired* (Genetic Algorithm & Cuckoo Search) untuk seleksi fitur, dan model *ensemble* (Random Forest & 1D-CNN) untuk klasifikasi, disertai dengan **koreksi metodologis** untuk mencegah *data leakage*.

---

## Referensi

* **Paper:** [IEEE Xplore](https://ieeexplore.ieee.org/document/11053763)
* **Dataset:** [UCI Heart Disease Dataset](https://www.kaggle.com/datasets/hamnawaseem112222222/uci-heart-disease-dataset)

---
## Project Scope

Proyek mencakup proses **pemahaman dataset, analisis metodologi, implementasi eksperimen, evaluasi, serta analisis hasil** untuk mereplikasi penelitian asli. Seiring berjalannya semester, cakupan proyek akan dikembangkan dan disesuaikan dengan tahapan penelitian dan tugas yang diberikan.

---

## Latar Belakang & Masalah
* **Klinis:** Diagnosis penyakit jantung konvensional memakan waktu, lambat beradaptasi dengan medis modern, dan memicu variabilitas diagnosis akibat subjektivitas keahlian dokter. 
* **Teknis:** Implementasi ML/DL pada data medis rentan terhadap komputasi yang berat, dimensi fitur berlebih (*high dimensionality*) yang memicu *overfitting*, serta rendahnya interpretabilitas klinis (masalah *black-box*).

**Tujuan Proyek:** Mengembangkan *pipeline* prediksi biner penyakit jantung yang mengungguli kelemahan tersebut dengan memadukan seleksi fitur hibrida yang mengoptimalkan eksplorasi (GA) dan eksploitasi (CSO), dengan kekuatan klasifikasi *ensemble* (RF + CNN).

---

## Deskripsi Dataset
Dataset yang digunakan bersumber dari **UCI Heart Disease Dataset (Cleveland)**.
* **Jumlah Data:** 303 observasi (pasien).
* **Fitur:** 13 variabel prediktor klinis (seperti usia, jenis kelamin, *chest pain type*, tekanan darah, kolesterol, dll).
* **Target:** 1 variabel biner (`0` = Tidak ada penyakit jantung, `1` = Ada penyakit jantung).
* **Distribusi Kelas:** Cukup seimbang, dengan 164 pasien (54.1%) sehat dan 139 pasien (45.9%) mengidap penyakit.

---

## Koreksi Pipeline Metodologi
Replikasi ini melakukan audit terhadap jurnal referensi. Beberapa koreksi yang kami terapkan untuk menjaga validitas model meliputi:
1. **Pencegahan Data Leakage (Penting):** Melakukan *Stratified Train-Test Split* (80:20) **sebelum** imputasi, pembersihan *outlier* (IQR), dan *Min-Max Scaling*. Penghitungan parameter hanya dilakukan pada data latih (*training set*).
2. **IQR Trimming Khusus:** Pembersihan *outlier* dibatasi hanya pada fitur numerik kontinu (`age`, `trestbps`, `chol`, `thalach`, `oldpeak`) agar tidak merusak distribusi fitur kategorikal/biner.
3. **Robust Fitness Evaluation:** Menggunakan `StratifiedKFold(n_splits=3)` pada fungsi *fitness* di algoritma GA+CSO untuk mencegah bias saat seleksi fitur.
4. **Reproducibility:** Seluruh alur stokastik diikat dengan `random_state = 42`.

---

## Model & Hasil Eksperimen

### 1. Hybrid Feature Selection (GA + CSO)
Algoritma hibrida GA+CSO berhasil membuktikan superioritasnya dengan menghindari *local optima* (konvergen di nilai objektif terendah **17.133**). Algoritma ini menyeleksi **5 fitur paling relevan** dari total 13 fitur, yaitu:
`['age', 'sex', 'exang', 'ca', 'thal']`

### 2. Performa Klasifikasi (Test Set)
Model *Ensemble Tuned (GA)* dioptimasi melalui *hyperparameter tuning* (RF: `n_estimators=204`, `max_depth=23`; CNN: `filters=55`, `kernel_size=3`, `lr≈0.0067`).
 
| Model | Accuracy | Precision | Recall (Sensitivity) | F1-Score | Specificity | ROC AUC |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: |
| Random Forest | 78.69% | 72.73% | 85.71% | 0.78 | 72.73% | 89.45% |
| 1D-CNN | 77.05% | 71.88% | 82.14% | 0.76 | 72.73% | 87.55% |
| **Ensemble Tuned (GA)** | **86.89%** | **83.33%** | **89.29%** | **0.86** | **84.85%** | **91.13%** |

**Kesimpulan:** 
Performa *Ensemble Tuned GA* (Akurasi 86.89%, *Recall* 89.29%) mengungguli model tunggal. Angka ini secara metodologis **lebih realistis** dibandingkan klaim akurasi 95% pada *paper* asli, karena metrik kami dihasilkan dari uji *test set* yang sudah dibersihkan dari *data leakage*.

---
