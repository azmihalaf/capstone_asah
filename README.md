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

- **VIP Customers**  
  Pelanggan paling bernilai, sering dan baru bertransaksi.  
  Fokus: program loyalitas dan penawaran eksklusif.

- **Loyal Customers**  
  Pelanggan setia dengan potensi menjadi VIP.  
  Fokus: reward program dan upselling.

- **At-Risk Customers**  
  Pelanggan bernilai tinggi yang mulai jarang bertransaksi.  
  Fokus: re-engagement campaign.

- **Lost Customers**  
  Pelanggan lama yang sudah tidak aktif.  
  Fokus: promosi agresif dengan prioritas rendah.

- **Low-Value Customers**  
  Pelanggan dengan transaksi dan nilai rendah.  
  Fokus: edukasi produk dan akuisisi ringan.

---

## 🔁 How to Replicate

### 1. Environment Setup
Pastikan Python telah terinstal. Disarankan menggunakan virtual environment.

### 2. Install Dependencies
```bash
pip install pandas numpy scikit-learn matplotlib seaborn plotly joblib
