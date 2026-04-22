# Exploratory Data Analysis: Historical Memory Prices (1957–2026)

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.10+-blue?style=flat-square&logo=python" />
  <img src="https://img.shields.io/badge/Platform-Google%20Colab-orange?style=flat-square&logo=googlecolab" />
  <img src="https://img.shields.io/badge/Dataset-Kaggle-20BEFF?style=flat-square&logo=kaggle" />
  <img src="https://img.shields.io/badge/Status-Completed-success?style=flat-square" />
</p>

---

## Identitas

| Keterangan | Detail |
|---|---|
| **Nama** | Muhammad Fahriel |
| **NIM** | 2509116050 |
| **Mata Kuliah** | Analisis dan Visualisasi Data |
| **Tugas** | UTS - Exploratory Data Analysis |
| **Platform** | Google Colab |

---

## Daftar Isi

1. [Latar Belakang](#1-latar-belakang)
2. [Tujuan Analisis](#2-tujuan-analisis)
3. [Dataset](#3-dataset)
4. [Lingkungan dan Library](#4-lingkungan-dan-library)
5. [Tahapan Proses](#5-tahapan-proses)
   - [5.1 Import Library dan Load Data](#51-import-library-dan-load-data)
   - [5.2 Inspeksi Tipe Data](#52-inspeksi-tipe-data)
   - [5.3 Data Cleaning](#53-data-cleaning)
   - [5.4 Statistik Deskriptif](#54-statistik-deskriptif)
   - [5.5 Visualisasi Data](#55-visualisasi-data)
   - [5.6 Identifikasi Pola dan Insight](#56-identifikasi-pola-dan-insight)
6. [Hasil dan Temuan](#6-hasil-dan-temuan)
7. [Kesimpulan](#7-kesimpulan)
8. [Struktur Repository](#8-struktur-repository)

---

## 1. Latar Belakang

Teknologi memori komputer merupakan salah satu komponen yang mengalami perkembangan paling pesat dalam sejarah industri teknologi. Sejak era komputer pertama pada tahun 1950-an, harga memori per unit kapasitas telah mengalami penurunan yang sangat drastis seiring dengan berkembangnya metode manufaktur, peningkatan skalabilitas produksi, dan inovasi material semikonduktor.

Fenomena ini berkaitan erat dengan **Hukum Moore** (*Moore's Law*), yang menyatakan bahwa jumlah transistor dalam sebuah sirkuit terpadu akan berlipat ganda setiap dua tahun sekali dengan biaya yang relatif tetap. Implikasi dari hukum ini tidak hanya berlaku pada kapasitas pemrosesan, tetapi juga pada kapasitas penyimpanan dan memori, yang menjadi semakin murah dan semakin besar dari dekade ke dekade.

Dataset yang digunakan dalam analisis ini merekam perjalanan harga memori komputer selama hampir tujuh dekade, dari **tahun 1957 hingga 2026**, mencakup berbagai produsen, jenis teknologi memori, kapasitas dalam kilobyte, serta harga dalam satuan dolar Amerika Serikat (USD). Dengan melakukan analisis eksplorasi data (*Exploratory Data Analysis*/EDA) secara sistematis, diharapkan dapat ditemukan pola, tren, dan anomali yang memberikan gambaran komprehensif mengenai evolusi industri memori komputer.

---

## 2. Tujuan Analisis

Analisis ini memiliki empat tujuan utama, yaitu:

1. **Memahami tren penurunan harga memori** sepanjang dekade dari tahun 1957 hingga 2026 menggunakan pendekatan statistik dan visualisasi.
2. **Mengidentifikasi perusahaan dan jenis memori** yang mendominasi pasar pada berbagai periode waktu.
3. **Menganalisis hubungan antara kapasitas, kecepatan, dan harga** untuk memahami struktur penetapan harga dalam industri memori.
4. **Menemukan pola atau anomali** dalam data historis yang dapat memberikan insight tambahan mengenai dinamika pasar dan perkembangan teknologi.

---

## 3. Dataset

### Sumber Data

| Atribut | Keterangan |
|---|---|
| **Nama File** | `memory_prices_updated.csv` |
| **Sumber** | Kaggle / Data Publik |
| **Jumlah Baris** | 438 entri |
| **Jumlah Kolom** | 12 variabel |
| **Rentang Tahun** | 1957 – 2026 |

### Deskripsi Variabel

| Variabel | Tipe | Keterangan |
|---|---|---|
| `year` | Numerik | Tahun pencatatan data |
| `Company` | Kategorikal | Nama produsen/perusahaan memori |
| `Memory Type` | Kategorikal | Jenis/tipe teknologi memori |
| `Size in Kbyte` | Numerik | Kapasitas memori dalam kilobyte |
| `Cost in USD` | Numerik | Harga memori dalam dolar Amerika (USD) |
| `Speed in nanosec` | Numerik (objek) | Kecepatan akses memori dalam nanodetik |
| `day_month` | Kategorikal | Informasi waktu pencatatan |
| `Page` | Numerik | Referensi halaman sumber |
| `JDR Chip Prices - USD` | Numerik | Harga chip versi JDR dalam USD |
| `JDR Chip Prices - nanosec` | Numerik | Kecepatan chip JDR dalam nanodetik |
| `JDR Chip Prices - Size Kbit` | Numerik | Kapasitas chip JDR dalam kilobit |

### Kondisi Data Awal

Dataset memiliki sejumlah permasalahan yang perlu ditangani sebelum analisis dilakukan:

- Beberapa kolom memiliki **missing values** yang signifikan, seperti `JDR Chip Prices - nanosec` (71.46%) dan `Page` (57.53%).
- Kolom `Speed in nanosec` bertipe **objek** (bukan numerik), mengindikasikan kemungkinan adanya format data yang tidak konsisten.
- Terdapat kemungkinan nilai yang tidak valid (≤ 0) pada kolom harga dan kapasitas.

---

## 4. Lingkungan dan Library

### Platform

Analisis dilakukan menggunakan **Google Colaboratory (Colab)** dengan Python 3.10+.

### Library yang Digunakan

| Library | Fungsi |
|---|---|
| `pandas` | Manipulasi dan analisis data tabular |
| `numpy` | Operasi numerik dan array |
| `matplotlib` | Pembuatan visualisasi dasar |
| `seaborn` | Visualisasi statistik berbasis matplotlib |
| `scipy` | Analisis statistik lanjutan (regresi, z-score) |

> Semua library di atas telah tersedia secara default di Google Colab dan tidak memerlukan instalasi tambahan.

---

## 5. Tahapan Proses

### 5.1 Import Library dan Load Data

Tahap pertama adalah mengimpor seluruh library yang diperlukan dan memuat dataset dari Google Drive. Setelah data berhasil dimuat, dilakukan inspeksi awal untuk memahami ukuran dataset, rentang tahun, dan sepuluh baris pertama data.

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import matplotlib.ticker as mticker
import seaborn as sns
from scipy import stats
import warnings
from google.colab import drive

warnings.filterwarnings('ignore')
sns.set_theme(style='whitegrid', palette='muted')

drive.mount('/content/drive')
df = pd.read_csv('/content/drive/MyDrive/dataset/memory_prices_updated.csv')
```

**Hasil:** Dataset berhasil dimuat dengan **438 baris** dan **12 kolom**, mencakup data dari tahun 1957 hingga 2026.

---

### 5.2 Inspeksi Tipe Data

Dilakukan inspeksi menggunakan `df.info()` untuk memahami tipe data setiap kolom dan mengidentifikasi kolom yang memiliki nilai tidak lengkap.

**Temuan:**
- Dataset terdiri dari 438 entri dengan 12 variabel.
- Variabel numerik meliputi `year`, `Size in Kbyte`, dan `Cost in USD`.
- Variabel kategorikal seperti `Company`, `Memory Type`, dan `day_month` bertipe objek.
- Kolom `Speed in nanosec` bertipe objek meskipun seharusnya numerik -  mengindikasikan adanya inkonsistensi format data.
- Beberapa kolom memiliki jumlah nilai non-null yang jauh di bawah 438, menandakan adanya missing values yang perlu ditangani.

---

### 5.3 Data Cleaning

Proses pembersihan data dilakukan dalam tiga sub-tahap:

#### a. Pengecekan dan Penanganan Missing Values

Missing values dihitung per kolom dan divisualisasikan menggunakan bar chart horizontal untuk memudahkan interpretasi.

| Kolom | Missing (%) | Penanganan |
|---|---|---|
| `JDR Chip Prices - nanosec` | 71.46% | Dihapus dari analisis |
| `JDR Chip Prices - USD` | 71.00% | Dihapus dari analisis |
| `Page` | 57.53% | Dihapus dari analisis |
| `Speed in nanosec` | 42.47% | Dihapus dari analisis |
| `JDR Chip Prices - Size Kbit` | 24.43% | Dihapus dari analisis |
| `Company` | 3.20% | Diisi dengan `"Unknown"` |
| `Memory Type` | 3.42% | Diisi dengan `"Unknown"` |
| `day_month` | 1.30% | Dibiarkan (tidak digunakan) |

**Strategi:** Kolom dengan missing tinggi (>20%) dihapus karena tidak memberikan nilai informasi yang cukup. Kolom kategorikal dengan missing rendah (<5%) diisi dengan label `"Unknown"` untuk menjaga konsistensi data.

#### b. Seleksi Kolom dan Transformasi

Hanya kolom-kolom relevan yang dipertahankan untuk analisis. Selanjutnya dibuat beberapa **variabel turunan** untuk memperkaya analisis:

| Variabel Baru | Formula | Fungsi |
|---|---|---|
| `Cost_per_KB` | `Cost in USD / Size in Kbyte` | Efisiensi harga per kilobyte |
| `Size_in_MB` | `Size in Kbyte / 1024` | Konversi kapasitas ke megabyte |
| `Cost_per_MB` | `Cost in USD / Size_in_MB` | Efisiensi harga per megabyte |
| `Decade` | `(year // 10 * 10).astype(str) + 's'` | Pengelompokan per dekade |

#### c. Penghapusan Data Duplikat

Dilakukan pengecekan dan penghapusan baris duplikat menggunakan `duplicated().sum()` dan `drop_duplicates()` untuk mencegah bias dalam analisis statistik.

---

### 5.4 Statistik Deskriptif

Analisis statistik deskriptif dilakukan terhadap empat variabel numerik utama: `Cost in USD`, `Size in Kbyte`, `Cost_per_KB`, dan `Cost_per_MB`.

**Temuan utama:**

- **`Cost in USD`**: Rata-rata **$196.58**, maksimum **$4.680**, standar deviasi besar (339.14) -  distribusi sangat tersebar dan dipengaruhi outlier.
- **`Size in Kbyte`**: Rata-rata >10 juta KB (~10 GB), nilai maksimum 67 juta KB (64 GB) -  mencerminkan perkembangan dramatis kapasitas lintas generasi.
- **`Cost_per_KB` dan `Cost_per_MB`**: Distribusi sangat tidak merata dengan perbedaan ekstrem antara nilai minimum dan maksimum, mencerminkan data historis awal yang sangat mahal dibandingkan teknologi modern.

> **Catatan:** Distribusi variabel numerik bersifat tidak normal dan sangat dipengaruhi outlier, sehingga analisis lanjutan memerlukan transformasi data logaritmik.

---

### 5.5 Visualisasi Data

#### a. Distribusi Harga Memori -  Histogram + KDE

Distribusi harga divisualisasikan pada dua skala: skala asli dan skala logaritmik (log₁₀).

- Distribusi pada skala asli sangat *right-skewed*, dengan rata-rata ($196.58) jauh di atas median ($91.99).
- Transformasi log₁₀ menghasilkan distribusi yang lebih simetris dan mendekati normal.

---

#### b. Tren Harga Per KB Sepanjang Tahun -  Line Chart (Skala Log)

- Penurunan harga dari sekitar **$401.408/KB** (1957) menjadi mendekati nol di era modern.
- Tren eksponensial selaras dengan Hukum Moore.
- Memasuki 2020-an, laju penurunan mulai melambat dan cenderung stabil.

---

#### c. Jumlah Data per Dekade -  Bar Chart

- Data paling sedikit dari 1950-an dan 1960-an (2 entri masing-masing).
- Puncak data pada **1990-an (85 entri)**, diikuti 2010-an (83) dan 2000-an (76).
- Dataset lebih representatif untuk periode modern.

---

#### d. Top 10 Perusahaan -  Horizontal Bar Chart

- **NewEgg.com** mendominasi dengan **193 entri** (>44% dari total data).
- Kontributor lain jauh lebih kecil: *Crucial Technology* (23), *Unknown* (14).
- Ketimpangan sumber data ini berpotensi menimbulkan bias analisis.

---

#### e. Distribusi Harga per Dekade -  Box Plot

- Median harga menurun konsisten dari dekade ke dekade.
- Variasi terlebar pada 1970-an dan 1980-an, mencerminkan diversifikasi teknologi.
- Pada 2020-an, terjadi sedikit peningkatan median dan pelebaran distribusi.

---

#### f. Hubungan Ukuran vs Harga -  Scatter Plot (Skala Log)

- Korelasi Pearson (log-log): **r = -0.281** (p < 0.001).
- Korelasi negatif lemah: kapasitas lebih besar → harga per unit lebih rendah (*economies of scale*).
- Pewarnaan berdasarkan tahun menunjukkan pola temporal yang jelas.

---

#### g. Heatmap Korelasi Antar Variabel Numerik

| Pasangan Variabel | r | Interpretasi |
|---|---|---|
| `year` ↔ `Size in Kbyte` | **+0.714** | Kapasitas meningkat kuat seiring waktu |
| `year` ↔ `Cost in USD` | **-0.365** | Harga cenderung turun seiring waktu |
| `year` ↔ `Cost_per_KB` | **-0.197** | Efisiensi harga membaik seiring waktu |
| `Size in Kbyte` ↔ `Cost in USD` | **-0.111** | Korelasi lemah |
| `Cost in USD` ↔ `Cost_per_KB` | **+0.026** | Hampir tidak berkorelasi |

> **Kesimpulan:** `year` adalah faktor paling dominan dalam menjelaskan perubahan kapasitas dan harga memori.

---

#### h. Deteksi Outlier -  Z-Score (|Z| > 3)

- Sebagian besar outlier berasal dari **1960-an hingga 1970-an** dengan harga sangat ekstrem.
- Outlier ini memiliki makna historis penting dan tidak selalu perlu dihapus dalam konteks analisis longitudinal.

---

#### i. Tren dan Perubahan YoY Harga per KB

- Penurunan paling tajam terjadi pada **dekade 1960-an hingga 1980-an**.
- Setelah tahun 2000, laju penurunan melambat secara signifikan.
- Beberapa periode modern menunjukkan kenaikan harga, kemungkinan akibat lonjakan permintaan AI dan komputasi modern.

---

#### j. Distribusi Ukuran Memori per Dekade -  Violin Plot

- Distribusi bergeser ke nilai lebih tinggi secara konsisten dari dekade ke dekade.
- Era modern (2000-an ke atas): distribusi lebih rapat, mencerminkan standarisasi kapasitas produksi massal.

---

### 5.6 Identifikasi Pola dan Insight

Tiga insight utama dikuantifikasi secara eksplisit:

**Insight 1 -  Faktor penurunan harga:**
Harga per KB di tahun 1957 dibandingkan dengan harga di era 2020-an menghasilkan faktor penurunan yang mencapai **jutaan kali lipat**.

**Insight 2 -  Dekade dengan penurunan terbesar:**
Analisis *percentage change* median harga per KB antar dekade mengidentifikasi dekade dengan penurunan harga paling signifikan dalam sejarah industri memori.

**Insight 3 -  Produk termahal vs. termurah:**
Identifikasi produk dengan harga tertinggi dan terendah dalam dataset, beserta informasi tahun, perusahaan, kapasitas, dan tipe memori.

---

## 6. Hasil dan Temuan

| No | Temuan | Implikasi |
|---|---|---|
| 1 | **Penurunan harga eksponensial** -  Harga/KB turun jutaan kali lipat dari 1957 ke 2020-an | Mengkonfirmasi Hukum Moore dalam konteks harga memori |
| 2 | **Distribusi sangat right-skewed** -  Harga memiliki long tail yang signifikan | Transformasi log diperlukan untuk analisis statistik yang valid |
| 3 | **IBM mendominasi era awal (1950–1970)** -  Pasar mulai beragam pada 1980-an | Mencerminkan transisi dari monopoli ke pasar kompetitif |
| 4 | **Kapasitas meningkat drastis** -  Dari <1 KB di 1950-an menjadi ratusan GB di era modern | Konsisten dengan tren *semiconductor scaling* global |
| 5 | **Outlier terkonsentrasi di era 1957–1970** -  Harga sangat tinggi pada masa awal | Data historis awal memiliki karakteristik berbeda secara statistik |
| 6 | **Korelasi waktu–kapasitas sangat kuat (r = 0.714)** | Waktu adalah prediktor utama kapasitas memori |
| 7 | **NewEgg.com menyumbang >44% data** -  Potensi bias sumber data | Hasil analisis harus diinterpretasikan dengan mempertimbangkan ketidakseimbangan ini |

---

## 7. Kesimpulan

Analisis eksplorasi data terhadap dataset *Historical Memory Prices* berhasil mengungkap tren dan pola yang signifikan dalam evolusi industri memori komputer selama hampir tujuh dekade.

Secara keseluruhan, industri memori komputer menunjukkan salah satu **tren penurunan harga teknologi paling dramatis dalam sejarah**. Harga per kilobyte memori telah menurun jutaan kali lipat dari tahun 1957 hingga era 2020-an, memvalidasi konsep *deflationary trend* dalam teknologi semikonduktor secara empiris. Fenomena ini sejalan dengan prediksi Hukum Moore dan memberikan gambaran yang jelas tentang bagaimana inovasi teknologi dapat mendorong penurunan biaya secara eksponensial.

Namun demikian, data terbaru mengindikasikan adanya **perubahan pola menuju stabilisasi**, bahkan kenaikan harga jangka pendek, yang kemungkinan dipengaruhi oleh peningkatan permintaan untuk komputasi berbasis kecerdasan buatan, tekanan rantai pasok global, serta keterbatasan fisik dalam pengembangan teknologi semikonduktor.

Temuan-temuan ini memiliki relevansi penting tidak hanya dari perspektif historis, tetapi juga sebagai dasar untuk memahami arah perkembangan industri memori di masa mendatang.

---

## 8. Struktur Repository

```
uts-avd-fahriel/
│
├── UTS_AVD_Muhammad_Fahriel.ipynb 
├── README.md
└── memory_prices_updated.csv      
```

---

<p align="center">
  Dibuat untuk memenuhi tugas UTS Mata Kuliah Analisis dan Visualisasi Data<br>
  <strong>Muhammad Fahriel - NIM 2509116050</strong>
</p>
