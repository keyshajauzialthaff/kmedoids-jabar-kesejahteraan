# kmedoids-jabar-kesejahteraan

# Pengelompokan Tingkat Kesejahteraan Kabupaten/Kota di Jawa Barat Menggunakan Metode K-Medoids
Repositori ini berisi kode Python dan dokumentasi untuk pengelompokan (clustering) 27 Kabupaten/Kota di Provinsi Jawa Barat berdasarkan indikator kesejahteraan masyarakat menggunakan metode **K-Medoids**. Penelitian ini bertujuan untuk mengidentifikasi pola ketimpangan wilayah sebagai bahan pertimbangan dalam penyusunan kebijakan pembangunan daerah.

---

## Ringkasan Proyek

- **Objek Penelitian**: 27 Kabupaten/Kota di Provinsi Jawa Barat.
- **Sumber Data**: Badan Pusat Statistik (BPS) Provinsi Jawa Barat (Data Tahun 2024).
- **Variabel yang Digunakan**:
  1. **$X_1$ - Umur Harapan Hidup (UHH)** (Dimensi Kesehatan)
  2. **$X_2$ - Rata-rata Lama Sekolah (RLS)** (Dimensi Pendidikan)
  3. **$X_3$ - Persentase Penduduk Miskin** (Dimensi Ekonomi)
- **Metode**: Algoritma K-Medoids (*Euclidean Distance*).
- **Evaluasi Cluster**: *Silhouette Coefficient* & Pertimbangan Substantif Karakteristik Wilayah.

---

## Metodologi & Alur Analisis

1. **Analisis Statistik Deskriptif**: Memahami sebaran dan karakteristik awal data.
2. **Preprocessing Data**:
   - Pemeriksaan *missing value* dan data duplikat.
   - Pengecekan *outlier* menggunakan metode Boxplot.
   - Uji multikolinearitas menggunakan *Variance Inflation Factor* (VIF) untuk memastikan nilai $\text{VIF} < 10$.
3. **Standarisasi Data**: Menggunakan **Z-score Normalization** agar seluruh variabel berada pada skala yang sama ($N(0, 1)$).
4. **Penentuan Jumlah Cluster ($k$)**: Evaluasi menggunakan *Silhouette Score*. Meskipun $k=2$ memiliki skor tertinggi secara statistik ($0.5003$), ditetapkan **$k=4$** berdasarkan pertimbangan substantif interpretabilitas perbedaan antarwilayah.
5. **Clustering K-Medoids**: Proses iterasi hingga mencapai konvergensi posisi medoid akhir (berhenti pada iterasi ke-9).
6. **Profilisasi Cluster**: Analisis rata-rata variabel pada setiap klaster untuk klasifikasi tingkat kesejahteraan.

---

## Hasil Klasterisasi

Algoritma K-Medoids menghasilkan 4 kelompok (*cluster*) wilayah dengan karakteristik sebagai berikut:

| Cluster | Kategori Kesejahteraan | Jumlah Anggota | Anggota Kabupaten/Kota |
| :---: | :--- | :---: | :--- |
| **Cluster 1** | Menengah | 8 | Kab. Bogor, Kab. Sukabumi, Kab. Cianjur, Kab. Ciamis, Kab. Sumedang, Kab. Purwakarta, Kab. Karawang, Kab. Pangandaran |
| **Cluster 2** | Cukup Baik | 5 | Kab. Bandung, Kab. Bekasi, Kota Sukabumi, Kota Cirebon, Kota Banjar |
| **Cluster 3** | Rendah | 9 | Kab. Garut, Kab. Tasikmalaya, Kab. Kuningan, Kab. Cirebon, Kab. Majalengka, Kab. Indramayu, Kab. Subang, Kab. Bandung Barat, Kota Tasikmalaya |
| **Cluster 4** | Tinggi | 5 | Kota Bogor, Kota Bandung, Kota Bekasi, Kota Depok, Kota Cimahi |

### Ringkasan Rata-Rata Variabel per Cluster

| Cluster | UHH ($X_1$) | RLS ($X_2$) | Persentase Miskin ($X_3$) |
| :---: | :---: | :---: | :---: |
| **1** | 75.16 tahun | 8.02 tahun | 8.20% |
| **2** | 75.23 tahun | 9.73 tahun | 6.61% |
| **3** | 74.93 tahun | 7.91 tahun | 10.74% |
| **4** | **75.83 tahun** | **11.34 tahun** | **4.23%** |

---

## Teknologi & Library

Proyek ini dibuat menggunakan Python pada lingkungan Jupyter Notebook dengan library berikut:
- `pandas` — Manipulasi dan analisis data
- `numpy` — Operasi matriks dan numerik
- `matplotlib` & `seaborn` — Visualisasi data (Boxplot, Pairplot, Lineplot)
- `scikit-learn-extra` — Algoritma K-Medoids (`KMedoids`)
- `scikit-learn` — Standarisasi data (`StandardScaler`) & Evaluasi (`silhouette_score`)
- `statsmodels` — Pengecekan multikolinearitas (`variance_inflation_factor`)
