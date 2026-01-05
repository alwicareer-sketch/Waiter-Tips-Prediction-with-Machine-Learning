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

### 📊 Model Regresi Linear

Berdasarkan hasil pelatihan model menggunakan *Linear Regression*, diperoleh persamaan matematis sebagai berikut:

$$Y = 1.2014 + 4.4859(X_1) + 0.0327(X_2) - 0.1917(X_3) - 0.0054(X_4) + 0.0612(X_5) + 1.2015(X_6)$$

### 🧐 Interpretasi Model

Berikut adalah penjelasan mendalam mengenai pengaruh setiap variabel terhadap jumlah tip yang diterima:

1. **Konstanta (Intercept) = 1.2014**
   Secara teoritis, jika semua variabel independen bernilai nol, maka pelayan diprediksi tetap menerima tip sebesar **$1.20**. Ini menunjukkan adanya nilai dasar tip yang diberikan pelanggan sebagai etika layanan standar.

2. **Total Bill ($X_1$) = 4.4859 (Signifikan)**
   Variabel ini memiliki pengaruh **paling besar dan positif**. Setiap kenaikan satu satuan pada total tagihan (setelah dinormalisasi) akan meningkatkan tip sebesar **$4.48**. Hal ini membuktikan bahwa pelanggan cenderung memberikan tip secara persentase dari total belanja mereka.

3. **Size ($X_6$) = 1.2015 (Signifikan)**
   Jumlah orang dalam satu meja berpengaruh positif secara signifikan. Semakin banyak orang dalam satu rombongan, beban kerja pelayan meningkat, dan secara statistik hal ini mendorong pemberian tip yang lebih besar sebesar **$1.20** per kenaikan skala grup.

4. **Status Perokok ($X_3$) = -0.1917 (Tidak Signifikan)**
   Koefisien negatif menunjukkan bahwa pelanggan yang merokok cenderung memberikan tip sedikit lebih rendah (sekitar **$0.19$** lebih kecil) dibandingkan non-perokok, meskipun secara statistik pengaruh ini tidak terlalu kuat.

5. **Waktu Makan ($X_5$) = 0.0612 (Tidak Signifikan)**
   Ada kecenderungan tip pada waktu makan siang (*Lunch*) sedikit lebih tinggi dibandingkan makan malam (*Dinner*) sebesar **$0.06$**, namun perbedaannya sangat kecil sehingga dianggap tidak berpengaruh nyata.

6. **Jenis Kelamin ($X_2$) & Hari ($X_4$)**
   Kedua variabel ini memiliki koefisien yang sangat kecil (masing-masing **0.0327** dan **-0.0054**). Artinya, identitas gender pelanggan maupun hari kunjungan (apakah itu akhir pekan atau hari kerja) tidak memberikan dampak yang berarti terhadap besarnya tip yang diberikan.

---

### Evaluasi Metrik (Testing Set)
Berdasarkan pengujian pada 20% data uji, model menghasilkan:
* **R-Squared ($R^2$):** 0.444 (44,4% variasi tip dijelaskan oleh model).
* **Mean Absolute Error (MAE):** 0.670.
* **MAPE:** 27.85%.
* **RMSE:** 0.833.

### Uji Signifikansi 
Berdasarkan hasil ringkasan OLS:
* **Signifikansi Simultan (Uji F):** Model sangat signifikan dengan p-value $4.50 \times 10^{-30}$.
* **Signifikansi Parsial (Uji t):** * `total_bill` (p-value: 0.000) dan `size` (p-value: 0.043) adalah prediktor yang signifikan.
  * Variabel lain seperti `sex`, `smoker`, `day`, dan `time` tidak memiliki pengaruh signifikan secara statistik (p-value > 0.05).

### Uji Asumsi Klasik
* **Normalitas:** Residual berdistribusi normal (Shapiro-Wilk p-value: 0.445 > 0.05).
* **Multikolinearitas:** Tidak ditemukan multikolinearitas serius (VIF untuk semua variabel utama < 2).
* **Autokorelasi:** Nilai Durbin-Watson sebesar 1.93 (mendekati 2), menunjukkan tidak ada autokorelasi.

---

## 💡 Insight
1. **Dominasi Total Tagihan:** Total tagihan adalah faktor terkuat. Setiap kenaikan tagihan akan diikuti oleh kenaikan tip secara konsisten.
2. **Kapasitas Meja:** Ukuran rombongan (`size`) memberikan dampak positif; melayani meja besar secara teknis meningkatkan peluang mendapatkan tip lebih tinggi.
3. **Kualitas Pelayanan:** Karena model hanya menjelaskan 44,4% variasi, sisanya dipengaruhi oleh faktor eksternal yang tidak ada dalam data, seperti kualitas keramahan pelayan atau rasa makanan, dll.
4. **Fokus Operasional:** Karena hari (`day`) dan waktu (`time`) tidak signifikan secara statistik dalam mempengaruhi besaran tip, manajemen tidak perlu membedakan skema insentif pelayan berdasarkan shift kerja.

---

## 📩 Kontak & Kolaborasi
Saya sangat terbuka untuk mendiskusikan temuan dalam proyek ini lebih lanjut atau mengenai peluang kolaborasi di bidang Data Analysis dan Data Science.

* **Nama:** Alwi
* **Email:** alwi.career@gmail.com
* **LinkedIn:** https://www.linkedin.com/in/alwi-22a3a7293/
* **Minat:** Data Analyst, Data Science, Machine Learning

---
