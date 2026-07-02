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

### Import Data Kuesioner
```
library(readxl)

data <- read_excel("C:/Users/ACER/Downloads/Estimasi Tingkat Distraksi Digital dalam Aktivitas Pembelajaran Mahasiswa Program Studi Statistika Universitas Mataram Menggunakan Two-Stage Cluster Sampling (Jawaban).xlsx")
View(data)
```
### Pengecekan Struktur Data
```
str(data)
summary(data)
```
### Uji Validitas & Reliabilitas Instrumen Penelitian
#### Uji Validitas Instrumen Penelitian
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

### Menghitung Skor Total
```
data$Skor_Total <- rowSums(item)
```

### Statistika Deskriptif
```
summary(data$Skor_Total)

mean(data$Skor_Total)

sd(data$Skor_Total)

min(data$Skor_Total)

max(data$Skor_Total)
```

### Cleaning Data
#### Cek Missing Value
```
colSums(is.na(data))
```
#### Cek Data Duplikat
```
sum(duplicated(data))
```
#### Cek Outlier
```
boxplot(
  data$Skor_Total,
  main = "Boxplot Skor Total Distraksi Digital",
  ylab = "Skor Total"
)
boxplot.stats(data$Skor_Total)$out
```
### Penerapan Two-Stage Cluster Sampling
#### Pembentukan Variabel Cluster
```
data$Cluster <- paste(
  data$Angkatan,
  data$Kelas,
  sep = "_"
)

table(data$Cluster)
```

#### Response Rate
```
jumlah_sampel <- 30
jumlah_responden <- nrow(data)
response_rate <- (jumlah_responden / jumlah_sampel) * 100
cat("Response Rate =", response_rate, "%")
```
#### Pembobotan Sampel
```
data$Bobot <- ifelse(
  data$Cluster == "2023_A",
  18/11,
  26/19
)
table(data$Cluster, data$Bobot)
```
#### Pembentukan Desain Survei
```
library(survey)

desain <- svydesign(
  id = ~Cluster,
  weights = ~Bobot,
  data = data
)

desain
```
### Estimasi Rata-rata
```
estimasi <- svymean(~Skor_Total, desain)
estimasi
```
### Evaluasi Hasil Estimasi
#### Standard Error
```
SE(estimasi)
```
#### Interval Kepercayaan 95%
```
confint(estimasi)
```
#### Design Effect (DEFF)
```
svymean(
  ~Skor_Total,
  desain,
  deff = TRUE
)
```
#### Relative Standard Error (RSE)
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
```
# Mengubah hasil estimasi dari skala 10–50 ke skala Likert 1–5
mean_est_likert <- as.numeric(mean_est) / ncol(item)

cat("Estimasi rata-rata (Skala 10-50) =", round(as.numeric(mean_est), 3), "\n")
cat("Estimasi rata-rata (Skala 1-5) =", round(mean_est_likert, 3), "\n")
```



## Hasil dan Pembahasan
### Deskripsi Data
### Hasil Uji Validitas
| Item | r<sub>hitung</sub> | Keterangan |
|:----:|-------------------:|:----------:|
| P1  | 0.5492 | Valid |
| P2  | 0.6508 | Valid |
| P3  | 0.3783 | Valid |
| P4  | 0.5097 | Valid |
| P5  | 0.3500 | Valid |
| P6  | 0.6052 | Valid |
| P7  | 0.5267 | Valid |
| P8  | 0.5657 | Valid |
| P9  | 0.7154 | Valid |
| P10 | 0.5933 | Valid |
### Hasil  Uji Reliabilitas
| Cronbach's Alpha | Keterangan |
|-----------------:|:----------:|
| 0.868 | Reliabel |


###
