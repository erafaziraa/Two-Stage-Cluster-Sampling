# Estimasi Tingkat Distraksi Digital dalam Aktivitas Pembelajaran Mahasiswa Program Studi Statistika Universitas Mataram Menggunakan Two-Stage Cluster Sampling
## Latar Belakang

Perkembangan teknologi digital telah memberikan kemudahan bagi mahasiswa dalam mengakses informasi dan mendukung proses pembelajaran. Namun, penggunaan perangkat digital yang tidak terkontrol juga dapat menimbulkan distraksi digital, yaitu gangguan perhatian akibat aktivitas seperti penggunaan media sosial, aplikasi pesan instan, maupun hiburan digital selama kegiatan belajar. Distraksi digital berpotensi menurunkan konsentrasi, efektivitas belajar, serta hasil akademik mahasiswa.

Mahasiswa Program Studi Statistika Universitas Mataram sebagai pengguna aktif teknologi digital juga tidak terlepas dari potensi terjadinya distraksi digital. Oleh karena itu, diperlukan informasi mengenai tingkat distraksi digital yang dialami mahasiswa sebagai dasar untuk memahami kondisi yang ada dan mendukung penyusunan strategi pembelajaran yang lebih efektif.

Penelitian ini bertujuan untuk mengestimasi tingkat distraksi digital dalam aktivitas pembelajaran mahasiswa Program Studi Statistika Universitas Mataram menggunakan metode *Two-Stage Cluster Sampling*. Metode tersebut dipilih karena populasi mahasiswa secara alami terbagi dalam kelompok-kelompok, seperti angkatan atau kelas, sehingga proses pengambilan sampel menjadi lebih efisien tanpa mengurangi kualitas estimasi yang dihasilkan.

## Tujuan

Tujuan penelitian ini adalah sebagai berikut:

1. Menjelaskan konsep distraksi digital dalam aktivitas pembelajaran mahasiswa.
2. Menjelaskan teknik *Two-Stage Cluster Sampling* yang digunakan dalam pengambilan sampel.
3. Menjelaskan metode estimasi yang digunakan untuk mengestimasi tingkat distraksi digital mahasiswa.
4. Menjelaskan metode analisis data yang digunakan dalam penelitian.
5. Mengestimasi tingkat distraksi digital dalam aktivitas pembelajaran mahasiswa Program Studi Statistika Universitas Mataram berdasarkan data hasil kuesioner.

## Metode Penelitian

Penelitian ini merupakan penelitian kuantitatif dengan metode survei. Data yang digunakan adalah data primer yang diperoleh melalui penyebaran kuesioner kepada mahasiswa Program Studi Statistika Universitas Mataram. Populasi penelitian adalah seluruh mahasiswa aktif Program Studi Statistika Universitas Mataram.

Teknik pengambilan sampel yang digunakan adalah *Two-Stage Cluster Sampling*. Pada tahap pertama, dipilih klaster dari populasi, yaitu berdasarkan angkatan mahasiswa. Selanjutnya, pada tahap kedua dipilih sejumlah mahasiswa dari klaster terpilih menggunakan *Simple Random Sampling*. Data yang telah diperoleh kemudian diuji validitas dan reliabilitas instrumennya sebelum dilakukan analisis.

Estimasi tingkat distraksi digital dilakukan berdasarkan data hasil kuesioner menggunakan penduga pada *Two-Stage Cluster Sampling*. Selanjutnya, data dianalisis secara deskriptif untuk menggambarkan tingkat distraksi digital mahasiswa, meliputi ukuran pemusatan, ukuran penyebaran, serta penyajian data dalam bentuk tabel dan grafik.

## Teknik Pengambilan Sampel

Penelitian ini menerapkan metode Two-Stage Cluster Sampling, yaitu teknik pengambilan sampel yang dilakukan dalam dua tahapan.
 ### Tahap 1. Pemilihan Cluster
 
 Pada tahap pertama, populasi dikelompokkan ke dalam enam cluster berdasarkan kelas, yaitu:
 - 2023 A
 - 2023 B
 - 2024 A
 - 2024 B
 - 2025 A
 - 2025 B

Selanjutnya, setiap cluster diberikan bilangan acak menggunakan fungsi RAND() pada Microsoft Excel. Hasil pengacakan digunakan untuk menentukan cluster yang akan dijadikan sampel penelitian. Berdasarkan proses tersebut, diperoleh dua cluster terpilih, yaitu:
- 2023 A
- 2024 A

### Tahap 2. Pemilihan Responden

Setelah cluster terpilih, dilakukan pemilihan responden dari masing-masing cluster menggunakan metode Simple Random Sampling. Setiap mahasiswa pada cluster 2023 A dan 2024 A diberikan bilangan acak menggunakan fungsi RAND(), kemudian dipilih sesuai dengan jumlah sampel yang telah ditentukan. Jumlah responden yang diambil dari setiap cluster disesuaikan secara proporsional berdasarkan banyaknya mahasiswa pada masing-masing cluster.

| Cluster | Jumlah Mahasiswa | Jumlah Sampel |
|---|---|---|
| 2023 A | 18 | 11 |
| 2024 A | 26 | 19 |
| Total | 44 | 30 |

Berdasarkan hasil pemilihan sampel, diperoleh 30 responden yang digunakan sebagai sampel penelitian.

## Tahap Analisis Data

### 1. Import Data Kuesioner

Data hasil kuesioner diimpor ke dalam R sebagai tahap awal sebelum dilakukan pengolahan dan analisis data.
```
library(readxl)

data <- read_excel("C:/Users/ACER/Downloads/Estimasi Tingkat Distraksi Digital dalam Aktivitas Pembelajaran Mahasiswa Program Studi Statistika Universitas Mataram Menggunakan Two-Stage Cluster Sampling (Jawaban).xlsx")
View(data)
```

### 2. Uji Validitas & Reliabilitas Instrumen Penelitian
#### Uji Validitas Instrumen Penelitian

Uji validitas dilakukan untuk mengetahui apakah setiap butir pernyataan mampu mengukur variabel yang diteliti.
```
library(psych)

hasil_validitas <- data.frame(
  Item = colnames(item),
  r_hitung = sapply(1:ncol(item), function(i){
    cor(
      item[, i],
      rowSums(item[, -i]),
      use = "complete.obs"
    )
  })
)

r_tabel <- 0.30

hasil_validitas$Keterangan <- ifelse(
  hasil_validitas$r_hitung > r_tabel,
  "Valid",
  "Tidak Valid"
)

hasil_validitas
```

#### Uji Reliabilitas Instrumen Penelitian

Uji reliabilitas dilakukan untuk mengetahui tingkat konsistensi instrumen penelitian.
```
library(psych)

# Menghitung Cronbach's Alpha
hasil_reliabilitas <- alpha(item)

# Menampilkan nilai Cronbach's Alpha
cronbach_alpha <- hasil_reliabilitas$total$raw_alpha

cat("Nilai Cronbach's Alpha =", round(cronbach_alpha, 3), "\n")

# Memberikan keterangan
if (cronbach_alpha >= 0.70) {
  cat("Keterangan : Instrumen Reliabel\n")
} else {
  cat("Keterangan : Instrumen Tidak Reliabel\n")
}
```

### 3. Menghitung Skor Total

Perhitungan skor total dilakukan untuk memperoleh skor keseluruhan setiap responden berdasarkan jumlah skor dari seluruh butir pernyataan pada kuesioner.
```
data$Skor_Total <- rowSums(item)

hist(
  data$Skor_Total,
  main = "Histogram Skor Total Distraksi Digital",
  xlab = "Skor Total",
  ylab = "Frekuensi",
  col = "skyblue",
  border = "black"
)
```
#### Statistika Deskriptif Skor Total

Statistika deskriptif skor total digunakan untuk menggambarkan secara umum karakteristik data tingkat distraksi digital mahasiswa berdasarkan nilai rata-rata, minimum, maksimum, dan sebaran skor total.
```
summary(data$Skor_Total)
mean(data$Skor_Total)
sd(data$Skor_Total)
min(data$Skor_Total)
max(data$Skor_Total)
```
### 4. Cleaning Data

Cleaning data dilakukan untuk memeriksa keberadaan missing value, data duplikat, dan outlier sebelum dilakukan analisis lebih lanjut.
#### Cek Missing Value

Pemeriksaan missing value dilakukan untuk mengetahui apakah terdapat data yang hilang pada setiap variabel.
```
colSums(is.na(data))
```
#### Cek Data Duplikat

Pemeriksaan data duplikat dilakukan untuk memastikan tidak terdapat data yang tercatat lebih dari satu kali.
```
sum(duplicated(data))
```
#### Cek Outlier

Pemeriksaan outlier dilakukan untuk mengidentifikasi data yang memiliki nilai ekstrem sehingga dapat diketahui pengaruhnya terhadap hasil analisis.
```
boxplot(
  data$Skor_Total,
  main = "Boxplot Skor Total Distraksi Digital",
  ylab = "Skor Total"
)
boxplot.stats(data$Skor_Total)$out
```

### 5. Penerapan Two-Stage Cluster Sampling

Penerapan Two-Stage Cluster Sampling dilakukan untuk membentuk desain survei sesuai dengan proses pengambilan sampel dua tahap.
#### Pembentukan Primary Sampling Unit (PSU) & Secondary Sampling Unit (SSU)

Pembentukan PSU & SSU dilakukan untuk menentukan cluster yang menjadi unit sampling tahap pertama serta untuk mengidentifikasi unit sampling tahap kedua pada setiap cluster yang terpilih.
```
# Primary Sampling Unit (PSU)
data$Cluster <- paste(
  data$Angkatan,
  data$Kelas,
  sep = "_"
)
table(data$Cluster)

# Secondary Sampling Unit (SSU)
data$SSU <- ave(
  seq_len(nrow(data)),
  data$Cluster,
  FUN = seq_along
)
data$SSU <- as.numeric(data$SSU)
table(data$Cluster, data$SSU)
```

#### Pembobotan Sampel

Pembobotan sampel dilakukan berdasarkan peluang pemilihan pada setiap tahap pengambilan sampel untuk memperoleh bobot masing-masing responden.
```
# Tahap pertama
M <- 6      # jumlah cluster populasi
m <- 2      # jumlah cluster yang dipilih

P1 <- m/M

# Tahap kedua
N2023 <- 18
N2024 <- 26

n2023 <- 11
n2024 <- 19

P2_2023 <- n2023/N2023
P2_2024 <- n2024/N2024

# Bobot
Weight2023 <- 1/(P1 * P2_2023)
Weight2024 <- 1/(P1 * P2_2024)

# Menambahkan bobot ke data
data$Bobot <- ifelse(
  data$Cluster == "2023_A",
  Weight2023,
  Weight2024
)

table(data$Cluster, data$Bobot)
```
#### Pembentukan Desain Survei

Pembentukan desain survei dilakukan untuk mendefinisikan struktur sampling yang digunakan dalam proses estimasi menggunakan package survey.
```
library(survey)

desain <- svydesign(
  id = ~Cluster,
  weights = ~Bobot,
  data = data
)

desain
```
### 6. Estimasi Rata-rata

Estimasi rata-rata dilakukan untuk memperkirakan nilai rata-rata populasi berdasarkan data sampel yang diperoleh.
```
estimasi <- svymean(~Skor_Total, desain)
estimasi
```
### 7. Evaluasi Hasil Estimasi

Evaluasi hasil estimasi dilakukan untuk menilai tingkat ketelitian dan keandalan hasil estimasi yang diperoleh dari sampel terhadap parameter populasi.
#### Standard Error

Standard error digunakan untuk mengukur tingkat ketidakpastian dari hasil estimasi rata-rata yang diperoleh dari sampel.
```
SE(estimasi)
```
#### Interval Kepercayaan 95%

Interval kepercayaan 95% digunakan untuk menunjukkan rentang nilai yang diperkirakan mencakup rata-rata populasi sebenarnya dengan tingkat kepercayaan 95%.
```
confint(estimasi)
```
#### Design Effect (DEFF)

Design effect digunakan untuk mengukur seberapa besar pengaruh desain sampling kompleks terhadap varians estimasi dibandingkan dengan simple random sampling.
```
svymean(
  ~Skor_Total,
  desain,
  deff = TRUE
)
```
#### Relative Standard Error (RSE)

Relative Standard Error digunakan untuk menyatakan tingkat presisi estimasi dalam bentuk persentase terhadap nilai rata-rata estimasi.
```
mean_est <- coef(estimasi)

se_est <- SE(estimasi)

RSE <- (se_est / mean_est) * 100

RSE
if (RSE < 25) {
  cat("Keterangan: Estimasi layak digunakan")
} else if (RSE < 50) {
  cat("Keterangan: Estimasi perlu digunakan dengan hati-hati")
} else {
  cat("Keterangan: Estimasi kurang andal")
}
```
### Interpretasi Tingkat Distraksi Digital

Interpretasi Tingkat Distraksi Digital dilakukan untuk mengubah hasil estimasi rata-rata ke dalam skala Likert (1–5) sehingga lebih mudah diinterpretasikan dalam konteks tingkat distraksi digital mahasiswa.
```
# Mengubah hasil estimasi dari skala 10–50 ke skala Likert 1–5
mean_est_likert <- as.numeric(mean_est) / ncol(item)

cat("Estimasi rata-rata (Skala 10-50) =", round(as.numeric(mean_est), 3), "\n")
cat("Estimasi rata-rata (Skala 1-5) =", round(mean_est_likert, 3), "\n")
```



## Hasil dan Pembahasan
### Hasil Uji Validitas

Berdasarkan hasil pengujian, diperoleh hasil uji validitas sebagai berikut.
| Item | r<sub>hitung</sub> | Keterangan |
|:----:|-------------------:|:----------:|
| P1  | 0.5385 | Valid |
| P2  | 0.6414 | Valid |
| P3  | 0.3655 | Valid |
| P4  | 0.4981 | Valid |
| P5  | 0.3380 | Valid |
| P6  | 0.5921 | Valid |
| P7  | 0.5155 | Valid |
| P8  | 0.5560 | Valid |
| P9  | 0.7078 | Valid |
| P10 | 0.5835 | Valid |

Berdasarkan hasil uji validitas tersebut, seluruh item pernyataan (P1–P10) memiliki nilai r_hitung lebih dari 0.3, sehingga seluruh item dinyatakan valid. Nilai 0.3 merupakan nilai batas teoritis (rule of thumb) yang umum digunakan dalam penelitian untuk menunjukkan bahwa suatu item memiliki korelasi yang cukup dengan skor total, sehingga dianggap layak dalam mengukur variabel yang diteliti. Dengan demikian, seluruh butir pernyataan dapat digunakan untuk analisis selanjutnya.
### Hasil  Uji Reliabilitas

Uji reliabilitas dilakukan untuk mengetahui tingkat konsistensi internal dari instrumen penelitian dalam mengukur variabel yang sama. Berdasarkan hasil pengujian, diperoleh nilai Cronbach’s Alpha sebagai berikut.
| Cronbach's Alpha | Keterangan |
|-----------------:|:----------:|
| 0.839 | Reliabel |

Berdasarkan hasil tersebut, nilai Cronbach’s Alpha sebesar 0.839 menunjukkan bahwa instrumen penelitian memiliki tingkat konsistensi yang tinggi. Oleh karena itu, seluruh item pernyataan dinyatakan reliabel dan layak digunakan untuk analisis lebih lanjut.

### Hasil Perhitungan dan Distribusi Skor Total

Berdasarkan hasil pengolahan data, diperoleh skor total masing-masing responden yang kemudian digunakan untuk analisis lebih lanjut. Berikut ditampilkan cuplikan data (head data) dan visualisasi distribusi skor total.
Head Skor Total (6 Data Pertama)
| No | Skor_Total |
|:--:|-----------:|
| 1  | 29 |
| 2  | 40 |
| 3  | 39 |
| 4  | 42 |
| 5  | 35 |
| 6  | 36 |

#### Visualisasi Distribusi Skor Total

![Histogram Skor Total Distraksi Digital](Histogram%20Skor%20Total.png)

### Hasil Cleaning Data

### Hasil Penerapan Two-Stage Cluster Sampling
Hasil Pembentukan Primary Sampling Unit (PSU)
|  Item  | Jumlah Responden | Keterangan |
| :----: | ---------------: | :--------: |
| 2023 A |               11 |  Terpilih  |
| 2024 A |               19 |  Terpilih  |

Hasil Pembentukan Secondary Sampling Unit (SSU)
| Cluster |  SSU |    Keterangan    |
| :-----: | :--: | :--------------: |
|  2023 A | 1–11 | Urutan responden |
|  2024 A | 1–19 | Urutan responden |

Probabilitas Tahap 1
|  M  |  m  |    P1 |
| :-: | :-: | ----: |
|  6  |  2  | 0.333 |

Probabilitas Tahap 2
| Cluster |  N |  n |    P2 |
| :-----: | -: | -: | ----: |
|  2023 A | 18 | 11 | 0.611 |
|  2024 A | 26 | 19 | 0.731 |

Hasil Pembobotan
| Cluster |  Bobot |
| :-----: | -----: |
|  2023 A | 4.1053 |
|  2024 A | 4.9091 |

Hasil Pembentukan Desain Survei
|   Item   |            Hasil           |
| :------: | :------------------------: |
|  Desain  | Two-stage cluster sampling |
| Struktur |  (2 cluster, 30 responden) |

### Estimasi Rata-rata

|         Item        |  Nilai |
| :-----------------: | -----: |
|   Mean (rata-rata)  | 37.582 |
| Standard Error (SE) | 0.9369 |

### Hasil Evaluasi Estimasi

Nilai Standard Error
|         Item        |   Nilai |
| :-----------------: | ------: |
| Standard Error (SE) |  0.9369 |

Nilai Interval Kepercayaan 95%
|         Item        |   Nilai |
| :-----------------: | ------: |
|  Lower Bound (2.5%) | 35.7460 |
| Upper Bound (97.5%) | 39.4184 |

Nilai Design Effect (DEFF)
| Item |  Nilai |
| :--: | -----: |
| DEFF | 1.5562 |

Nilai Relative Standard Error (RSE)
| Item |   Nilai |
| :--: | ------: |
|  RSE | 2.4929% |

### Interpretasi Tingkat Distraksi Digital

Hasil Estimasi Rata-rata Skor Total
|           Item          |  Nilai |
| :---------------------: | -----: |
|    Mean (Skala 10–50)   | 37.582 |
| Mean (Skala Likert 1–5) |  3.758 |

Skala Pengukuran dan Interval Kategori
|          Item          | Nilai |
| :--------------------: | ----: |
|  Skor Minimum (Likert) |     1 |
| Skor Maksimum (Likert) |     5 |
|     Jumlah Kategori    |     5 |
|    Panjang Interval    |   0.8 |

Batas Kategori Interpretasi
|    Kategori   | Batas Bawah | Batas Atas |
| :-----------: | ----------: | ---------: |
| Sangat Rendah |         1.0 |        1.8 |
|     Rendah    |         1.8 |        2.6 |
|     Sedang    |         2.6 |        3.4 |
|     Tinggi    |         3.4 |        4.2 |
| Sangat Tinggi |         4.2 |        5.0 |

Kategori Tingkat Distraksi Digital
|     Item    |  Nilai |
| :---------: | -----: |
| Mean Likert |  3.758 |
|   Kategori  | Tinggi |

