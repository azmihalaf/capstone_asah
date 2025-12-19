# 📊 RFM Customer Segmentation using K-Means

## 📌 Overview
Proyek ini bertujuan untuk melakukan **Customer Segmentation** menggunakan metode  
**RFM (Recency, Frequency, Monetary)** yang dikombinasikan dengan algoritma  
**K-Means Clustering**.

Hasil segmentasi pelanggan ini dapat digunakan untuk menyusun **strategi pemasaran
yang lebih tepat sasaran**, meningkatkan **retensi pelanggan**, dan
**memaksimalkan nilai bisnis**.

---

## 📂 Dataset
Dataset yang digunakan adalah **`preprocessed_retail_data.csv`**, berisi data
transaksi ritel dengan kolom utama berikut:

| Kolom | Deskripsi |
|------|----------|
| `InvoiceNo` | Nomor invoice |
| `StockCode` | Kode produk |
| `Description` | Deskripsi produk |
| `Quantity` | Jumlah produk yang dibeli |
| `InvoiceDate` | Tanggal dan waktu transaksi |
| `UnitPrice` | Harga satuan produk |
| `CustomerID` | ID unik pelanggan |
| `Country` | Negara transaksi |
| `TotalPrice` | Total harga (Quantity × UnitPrice) |

---

## 🧠 Methodology
Tahapan analisis yang dilakukan dalam proyek ini adalah sebagai berikut:

### 1. Data Loading & Preprocessing
- Dataset dimuat menggunakan **Pandas**
- Kolom `InvoiceDate` dikonversi ke format `datetime`
- Kolom `TotalPrice` dihitung dari `Quantity × UnitPrice`

### 2. RFM Calculation
Perhitungan RFM dilakukan untuk setiap `CustomerID`:
- **Recency**: Selisih hari sejak transaksi terakhir
- **Frequency**: Jumlah transaksi unik
- **Monetary**: Total nilai transaksi pelanggan

### 3. Feature Scaling
- Data RFM distandarisasi menggunakan **StandardScaler**
- Tujuan: memastikan semua fitur memiliki kontribusi yang seimbang dalam proses clustering

### 4. Menentukan Jumlah Cluster Optimal
- **Elbow Method (SSE)** digunakan untuk melihat titik siku
- **Silhouette Score** digunakan untuk mengevaluasi kualitas cluster
- Jumlah cluster optimal diperoleh pada **k = 4**

### 5. K-Means Clustering
- Algoritma **K-Means** diterapkan pada data RFM yang telah diskalakan
- Pelanggan dikelompokkan ke dalam **4 cluster**

### 6. Interpretasi Cluster
- Analisis nilai rata-rata RFM pada setiap cluster
- Visualisasi dilakukan menggunakan:
  - Scatter Plot
  - Heatmap RFM

### 7. Customer Segmentation
Cluster kemudian diberi label segmen berdasarkan karakteristik bisnis:

| Segment | Karakteristik |
|-------|--------------|
| **VIP** | Recency rendah, Frequency & Monetary tinggi |
| **Loyal** | Frequency baik, Monetary menengah, Recency baik |
| **At-Risk** | Frequency & Monetary tinggi, namun Recency mulai tinggi |
| **Lost** | Recency sangat tinggi, Frequency & Monetary rendah |
| **Low-Value** | Frequency & Monetary rendah, Recency bervariasi |

### 8. Model Saving
- Model K-Means disimpan sebagai **`kmeans_model.pkl`**
- Penyimpanan dilakukan menggunakan library `joblib`
- Model dapat digunakan kembali untuk segmentasi pelanggan baru

---

## 📈 Results & Insights
Analisis menghasilkan **4 cluster utama** yang diinterpretasikan menjadi
**5 segmen pelanggan**:

1. Segmen VIP - Segmen ini berisi pelanggan dengan frekuensi pembelian tinggi, nilai transaksi besar, dan baru saja melakukan transaksi.
Ciri-ciri :
  - Recency rendah (baru belanja)
  - Frequency tinggi
  - Monetary sangat tinggi <br>
<br>**Interpretasi:** Pelanggan ini merupakan kontributor pendapatan terbesar dan memiliki nilai strategis yang tinggi. Perusahaan harus memprioritaskan program eksklusif seperti loyalty premium, early access, atau personalisasi penawaran.

2. Segmen Loyal - Segmen ini terdiri dari pelanggan yang membeli cukup sering dan memiliki nilai transaksi stabil.
Ciri-ciri:
  - Frequency di atas rata-rata
  - Monetary menengah
  - Recency cukup baik<br>
<br>**Interpretasi:** Pelanggan ini sudah memiliki engagement yang kuat dan berpotensi menjadi VIP jika diberikan insentif tambahan. Program cocok: poin reward, diskon rutin, membership.

3. Segmen At-Risk - Segmen ini menunjukkan pelanggan yang sebelumnya aktif tetapi belakangan mulai jarang berbelanja.
Ciri-ciri:

  - Recency tinggi
  - Frequency masih cukup tinggi
  - Monetary pernah besar <br>
<br>**Interpretasi:** Pelanggan ini berisiko pindah ke kompetitor. Perlu strategi retensi seperti email reminder, voucher comeback, atau campaign re-engagement.

4. Segmen Lost - Pelanggan yang sudah sangat lama tidak melakukan transaksi.
Ciri-ciri:
  - Recency sangat tinggi
  - Frequency rendah
  - Monetary rendah <br>
<br>**Interpretasi:** Segmen ini memiliki potensi rendah untuk kembali. Bisa diberi promosi agresif, tetapi tidak menjadi prioritas utama.

5. Segmen Low-Value - Pelanggan dengan aktivitas dan nilai pembelian rendah.
Ciri-ciri:
  - Frequency rendah
  - Monetary kecil
  - Recency bervariasi <br>
<br>**Interpretasi:** Pelanggan ini biasanya baru pertama kali belanja atau hanya pembeli insidental. Perlu edukasi produk dan campaign akuisisi ringan.

---

## 🔁 How to Replicate

### 1. Environment Setup
Pastikan Python telah terinstal. Disarankan menggunakan virtual environment.

### 2. Install Dependencies
```bash
pip install pandas numpy scikit-learn matplotlib seaborn plotly joblib
```

### 3. Dataset
Letakkan file `preprocessed_retail_data.csv` pada direktori yang sesuai. Contoh Google Colab:
```bash
/content/drive/MyDrive/Dataset/
```

### 4. Run Notebook
Jalankan notebook secara berurutan untuk:
- Perhitungan RFM
- Clustering
- Visualisasi
- Segmentasi Pelanggan

---

## 📦 Dependencies
- pandas
- numpy
- scikit-learn
- matplotlib
- seaborn
- plotly
- joblib
