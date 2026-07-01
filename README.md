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
data_kuesioner <- read_excel("C:/Users/ACER/Downloads/Estimasi Tingkat Distraksi Digital dalam Aktivitas Pembelajaran Mahasiswa Program Studi Statistika Universitas Mataram Menggunakan Two-Stage Cluster Sampling.xlsx")
View(data_kuesioner)
```
### Pengecekan Data
```
str(data_kuisioner)
summary(data_kuisioner)
```

### Uji Validitas Instrumen Penelitian
```
library(psych)

skor_total <- rowSums(data_kuisioner)

hasil_validitas <- data.frame(
  Item = colnames(data_kuisioner),
  r_hitung = sapply(1:ncol(data_kuisioner), function(i){
    cor(data_kuisioner[,i],
        rowSums(data_kuisioner[,-i]))
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

### Uji Reliabilitas Instrumen Penelitian
```
library(psych)

# Uji reliabilitas
hasil <- alpha(data_kuisioner)

# Menampilkan nilai Cronbach's Alpha
alpha <- hasil$total$raw_alpha

cat("Nilai Cronbach's Alpha =", round(alpha, 3), "\n")

# Memberikan keterangan
if(alpha >= 0.70){
  cat("Keterangan : Instrumen Reliabel\n")
} else {
  cat("Keterangan : Instrumen Tidak Reliabel\n")
}
```

### Menghitung Skor Total
```
data_kuisioner$Skor_Total <- rowSums(data_kuisioner)
```

### Statistika Deskriptif
```
summary(data_kuisioner$Skor_Total)

mean(data_kuisioner$Skor_Total)

sd(data_kuisioner$Skor_Total)

min(data_kuisioner$Skor_Total)

max(data_kuisioner$Skor_Total)
```

### 

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
