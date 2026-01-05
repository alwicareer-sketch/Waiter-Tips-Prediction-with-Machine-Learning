# 🍽️ Waiter Tips Prediction with Machine Learning

Proyek ini bertujuan untuk menganalisis faktor-faktor yang memengaruhi pemberian tip kepada pelayan dan membangun model prediksi menggunakan **Linear Regression**. [cite_start]Proyek ini mencakup alur kerja data science lengkap mulai dari EDA hingga uji asumsi klasik[cite: 23, 340].

## 📊 Informasi Dataset
Dataset diperoleh dari Kaggle: [Tips Dataset](https://www.kaggle.com/datasets/aminizahra/tips-dataset).

**Fitur Dataset:**
* `total_bill`: Total tagihan dalam dollar termasuk pajak.
* `tip`: Jumlah tip yang diberikan dalam dollar (**Target**).
* `sex`: Jenis kelamin pelanggan.
* `smoker`: Status merokok pelanggan.
* `day`: Hari kunjungan[cite: 10].
* [cite_start]`time`: Waktu makan (Lunch/Dinner)[cite: 11].
* [cite_start]`size`: Jumlah orang dalam satu meja[cite: 12].

---

## 🔍 Analisis Proyek

### 1. Masalah (Problem Statement)
Tantangan utama dalam industri layanan adalah memahami perilaku konsumen terkait pemberian tip. Masalah yang diangkat adalah: **"Bagaimana hubungan antara variabel transaksi (tagihan) dan demografi terhadap jumlah tip, serta seberapa akurat kita dapat memprediksinya?"**

### 2. Pendekatan (Methodology)
* [cite_start]**Exploratory Data Analysis (EDA):** Visualisasi korelasi menggunakan scatter plot dengan garis tren OLS [cite: 96, 114] [cite_start]dan distribusi proporsi tip menggunakan pie chart[cite: 154, 158].
* [cite_start]**Pra-pemrosesan Data:** * Normalisasi fitur numerik (`total_bill`, `size`) menggunakan `MinMaxScaler` ke rentang 0-1[cite: 187, 192].
  * [cite_start]Transformasi data kategorikal menjadi numerik menggunakan `LabelEncoder`[cite: 19, 199, 212].
* [cite_start]**Pemodelan:** Menggunakan algoritma **Linear Regression** untuk memodelkan hubungan linear antara fitur dan target[cite: 285, 288].

### 3. Tujuan (Objective)
* [cite_start]Membangun model regresi yang mampu memprediksi nilai tip dengan tingkat kesalahan (error) yang rendah[cite: 320].
* [cite_start]Melakukan uji validitas model melalui uji asumsi klasik untuk memastikan model tidak bias[cite: 340].

---

## 📈 Hasil dan Performa Model

### Evaluasi Metrik (Testing Set)
[cite_start]Berdasarkan pengujian pada 20% data uji, model menghasilkan[cite: 283, 335, 336, 337, 339]:
* [cite_start]**R-Squared ($R^2$):** 0.444 (44,4% variasi tip dijelaskan oleh model)[cite: 339].
* [cite_start]**Mean Absolute Error (MAE):** 0.670[cite: 336].
* [cite_start]**MAPE:** 27.85%[cite: 337].
* [cite_start]**RMSE:** 0.833[cite: 338].

### Uji Signifikansi (Analisis OLS)
[cite_start]Berdasarkan hasil ringkasan OLS[cite: 466, 486]:
* [cite_start]**Signifikansi Simultan (Uji F):** Model sangat signifikan dengan p-value $4.50 \times 10^{-30}$[cite: 482].
* [cite_start]**Signifikansi Parsial (Uji t):** * `total_bill` (p-value: 0.000) dan `size` (p-value: 0.043) adalah prediktor yang signifikan[cite: 486, 541].
  * [cite_start]Variabel lain seperti `sex`, `smoker`, `day`, dan `time` tidak memiliki pengaruh signifikan secara statistik (p-value > 0.05)[cite: 486].

### Uji Asumsi Klasik
* [cite_start]**Normalitas:** Residual berdistribusi normal (Shapiro-Wilk p-value: 0.445 > 0.05)[cite: 355, 356].
* [cite_start]**Multikolinearitas:** Tidak ditemukan multikolinearitas serius (VIF untuk semua variabel utama < 2)[cite: 389, 402].
* [cite_start]**Autokorelasi:** Nilai Durbin-Watson sebesar 1.93 (mendekati 2), menunjukkan tidak ada autokorelasi[cite: 457].

---

## 💡 Insight Bisnis
1. **Dominasi Total Tagihan:** Total tagihan adalah faktor terkuat. [cite_start]Setiap kenaikan tagihan akan diikuti oleh kenaikan tip secara konsisten[cite: 251, 486].
2. [cite_start]**Kapasitas Meja:** Ukuran rombongan (`size`) memberikan dampak positif; melayani meja besar secara teknis meningkatkan peluang mendapatkan tip lebih tinggi[cite: 486, 556].
3. **Kualitas Pelayanan:** Karena model hanya menjelaskan 44,4% variasi, sisanya dipengaruhi oleh faktor eksternal yang tidak ada dalam data, seperti kualitas keramahan pelayan atau rasa makanan.
4. [cite_start]**Fokus Operasional:** Karena hari (`day`) dan waktu (`time`) tidak signifikan secara statistik dalam mempengaruhi besaran tip, manajemen tidak perlu membedakan skema insentif pelayan berdasarkan shift kerja[cite: 486].

---
