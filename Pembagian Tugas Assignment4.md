# Pembagian Tugas Assignment #4 (4 Orang)

| Anggota | Bagian | Tugas Utama |
|---|---|---|
| **Anggota 1** | Baseline & Data-Quality Review (Instruksi 1, 2) | Menjalankan ulang pipeline terbaik Assignment #3 sebagai baseline. Melaporkan metrik (macro F1, dll.). Merangkum masalah data yang belum terselesaikan dari EDA #2 dan hasil #3. Menyiapkan kerangka notebook dan CV yang konsisten untuk semua anggota. |
| **Anggota 2** | Class Imbalance (Instruksi 3) | Menerapkan class weighting dan SMOTE (hanya pada data training, di dalam pipeline CV). Membandingkan keduanya dengan baseline memakai metrik untuk data imbalanced. Memilih treatment terbaik. |
| **Anggota 3** | Label Quality dengan Cleanlab (Instruksi 4, 5) | Menjalankan Cleanlab dengan prediksi out-of-fold. Mereview observasi mencurigakan dan mengisi tabel keputusan (Keep/Correct/Remove/Unresolved). Menjalankan eksperimen D0–D3 dan membandingkan mean ± std CV. |
| **Anggota 4** | Interpretasi Model (Instruksi 6, 7) | Menerapkan SHAP/LIME untuk interpretasi global dan lokal. Menganalisis kesesuaian dengan EDA, kemungkinan data leakage, dan prediksi yang salah. Menghubungkan temuan ke masalah kualitas data. |

## Tugas Bersama

| Tugas | Penanggung Jawab |
|---|---|
| Evaluasi akhir di test set: baseline vs dataset final (Instruksi 8) | Anggota 1 + 2 |
| Diskusi hasil, limitasi, dan risiko keputusan cleaning (Instruksi 9) | Semua, tiap anggota menulis bagian miliknya |
| Penyatuan notebook akhir dan instruksi reproduksi | Anggota 1 |
| Penyusunan laporan ringkas dan tabel perbandingan | Anggota 3 |
| Proofreading dan pengecekan kelengkapan submission | Anggota 4 |

## Catatan Alur Kerja
- Anggota 1 harus selesai lebih dulu (baseline dan pipeline CV) karena menjadi dasar bagi yang lain.
- Anggota 2 dan 3 bisa berjalan paralel setelah baseline siap. Eksperimen D3 membutuhkan hasil dari keduanya (koreksi label, lalu imbalance treatment).
- Anggota 4 bekerja pada model final setelah dataset final ditentukan.
- Test set tidak boleh diubah, dan label tidak boleh diubah tanpa bukti kuat.