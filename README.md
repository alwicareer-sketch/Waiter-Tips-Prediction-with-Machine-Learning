# 🍽️ Waiter Tips Prediction with Machine Learning

Proyek ini bertujuan untuk menganalisis faktor-faktor yang memengaruhi pemberian tip kepada pelayan dan membangun model prediksi menggunakan **Linear Regression**. Proyek ini mencakup alur kerja data science lengkap mulai dari EDA hingga uji asumsi klasik.

## 📊 Informasi Dataset
Dataset diperoleh dari Kaggle: [Tips Dataset](https://www.kaggle.com/datasets/aminizahra/tips-dataset).

**Fitur Dataset:**
* `total_bill`: Total tagihan dalam dollar termasuk pajak.
* `tip`: Jumlah tip yang diberikan dalam dollar (**Target**).
* `sex`: Jenis kelamin pelanggan.
* `smoker`: Status merokok pelanggan.
* `day`: Hari kunjungan.
* `time`: Waktu makan (Lunch/Dinner).
* `size`: Jumlah orang dalam satu meja.

---

## 🔍 Analisis Proyek

### 1. Masalah (Problem Statement)
Tantangan utama dalam industri layanan adalah memahami perilaku konsumen terkait pemberian tip. Masalah yang diangkat adalah: **"Bagaimana hubungan antara variabel transaksi (tagihan) dan demografi terhadap jumlah tip, serta seberapa akurat kita dapat memprediksinya?"**

### 2. Pendekatan (Methodology)
* **Exploratory Data Analysis (EDA):** Visualisasi korelasi menggunakan scatter plot dengan garis tren OLS dan distribusi proporsi tip menggunakan pie chart.
* **Pra-pemrosesan Data:** * Normalisasi fitur numerik (`total_bill`, `size`) menggunakan `MinMaxScaler` ke rentang 0-1.
  * Transformasi data kategorikal menjadi numerik menggunakan `LabelEncoder`.
* **Pemodelan:** Menggunakan algoritma **Linear Regression** untuk memodelkan hubungan linear antara fitur dan target.

### 3. Tujuan (Objective)
* Membangun model regresi yang mampu memprediksi nilai tip dengan tingkat kesalahan (error) yang rendah.
* Melakukan uji validitas model melalui uji asumsi klasik untuk memastikan model tidak bias.

---

## 📈 Hasil dan Performa Model

### Evaluasi Metrik (Testing Set)
Berdasarkan pengujian pada 20% data uji, model menghasilkan:
* **R-Squared ($R^2$):** 0.444 (44,4% variasi tip dijelaskan oleh model).
* **Mean Absolute Error (MAE):** 0.670.
* **MAPE:** 27.85%.
* **RMSE:** 0.833.

### Uji Signifikansi (Analisis OLS)
Berdasarkan hasil ringkasan OLS:
* **Signifikansi Simultan (Uji F):** Model sangat signifikan dengan p-value $4.50 \times 10^{-30}$.
* **Signifikansi Parsial (Uji t):** * `total_bill` (p-value: 0.000) dan `size` (p-value: 0.043) adalah prediktor yang signifikan.
  * Variabel lain seperti `sex`, `smoker`, `day`, dan `time` tidak memiliki pengaruh signifikan secara statistik (p-value > 0.05).

### Uji Asumsi Klasik
* **Normalitas:** Residual berdistribusi normal (Shapiro-Wilk p-value: 0.445 > 0.05).
* **Multikolinearitas:** Tidak ditemukan multikolinearitas serius (VIF untuk semua variabel utama < 2).
* [cite_start**Autokorelasi:** Nilai Durbin-Watson sebesar 1.93 (mendekati 2), menunjukkan tidak ada autokorelasi.

---

## 💡 Insight Bisnis
1. **Dominasi Total Tagihan:** Total tagihan adalah faktor terkuat. [cite_start]Setiap kenaikan tagihan akan diikuti oleh kenaikan tip secara konsisten.
2. **Kapasitas Meja:** Ukuran rombongan (`size`) memberikan dampak positif; melayani meja besar secara teknis meningkatkan peluang mendapatkan tip lebih tinggi.
3. **Kualitas Pelayanan:** Karena model hanya menjelaskan 44,4% variasi, sisanya dipengaruhi oleh faktor eksternal yang tidak ada dalam data, seperti kualitas keramahan pelayan atau rasa makanan.
4. **Fokus Operasional:** Karena hari (`day`) dan waktu (`time`) tidak signifikan secara statistik dalam mempengaruhi besaran tip, manajemen tidak perlu membedakan skema insentif pelayan berdasarkan shift kerja.

---
