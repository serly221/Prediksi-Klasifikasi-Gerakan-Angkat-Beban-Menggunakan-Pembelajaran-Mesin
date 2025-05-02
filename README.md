# Prediksi-Klasifikasi-Gerakan-Angkat-Beban-Menggunakan-Pembelajaran-Mesin
Tujuan dari proyek Anda adalah untuk memprediksi cara mereka melakukan latihan. 
# Prediksi Gerakan Angkat Beban

Proyek ini dibuat sebagai bagian dari kursus **Practical Machine Learning**. Tujuannya adalah untuk membangun model pembelajaran mesin yang mampu memprediksi cara seseorang melakukan latihan angkat beban berdasarkan data akselerometer.

## 📁 Struktur Folder

```
.
├── pml-project.Rmd       # File R Markdown (kode + penjelasan)
├── pml-project.html      # File HTML hasil dari knitting
└── README.md             # Penjelasan repositori ini
```

## 📌 Deskripsi Proyek

Model ini memanfaatkan data dari akselerometer pada berbagai bagian tubuh saat melakukan latihan angkat barbel. Proses mencakup:

- Pembersihan dan praproses data
- Pembagian data pelatihan dan validasi
- Validasi silang
- Pembuatan model Random Forest
- Evaluasi akurasi model
- Prediksi pada 20 data pengujian

## 🚀 Cara Menjalankan

1. Buka `pml-project.Rmd` di RStudio
2. Klik **Knit** untuk menghasilkan `pml-project.html`
3. Lihat hasil analisis di file HTML

## 🌐 Tampilan Online (jika menggunakan GitHub Pages)

Jika GitHub Pages diaktifkan, kamu bisa membuka file HTML di browser:
```
https://username.github.io/nama-repo/pml-project.html
```

## 📚 Sumber Data

- [Data Pelatihan](https://d396qusza40orc.cloudfront.net/predmachlearn/pml-training.csv)
- [Data Pengujian](https://d396qusza40orc.cloudfront.net/predmachlearn/pml-testing.csv)

---

*Dibuat oleh Serly sebagai bagian dari tugas akhir kursus Practical Machine Learning.*

---
title: "Prediksi Gerakan Angkat Beban dengan Random Forest"
author: "Serly"
output: html_document
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```

## **Pendahuluan**

Proyek ini bertujuan untuk membangun model prediksi guna mengklasifikasikan cara seseorang melakukan latihan angkat beban berdasarkan data dari akselerometer. Data yang digunakan diambil dari sensor pada sabuk, lengan bawah, lengan atas, dan dumbbell. Target dari model ini adalah variabel `classe`, yaitu jenis gerakan yang dilakukan (A hingga E). Proyek ini akan menggunakan pembelajaran mesin dan validasi silang untuk membangun model prediksi yang akurat.

## **Pengambilan dan Praproses Data**

```{r}
library(caret)
library(randomForest)
library(dplyr)

# Ambil data dari sumber
trainUrl <- "https://d396qusza40orc.cloudfront.net/predmachlearn/pml-training.csv"
testUrl <- "https://d396qusza40orc.cloudfront.net/predmachlearn/pml-testing.csv"

training <- read.csv(url(trainUrl), na.strings = c("NA", "", "#DIV/0!"))
testing <- read.csv(url(testUrl), na.strings = c("NA", "", "#DIV/0!"))

# Hapus kolom yang mengandung banyak NA
training <- training[, colSums(is.na(training)) == 0]

# Hapus kolom awal yang tidak relevan
training <- training[, -c(1:7)]

# Bagi data menjadi training dan validation
set.seed(123)
inTrain <- createDataPartition(training$classe, p = 0.6, list = FALSE)
trainSet <- training[inTrain, ]
valSet <- training[-inTrain, ]
```

## **Pembangunan Model**

```{r}
control <- trainControl(method = "cv", number = 5)
model_rf <- train(classe ~ ., data = trainSet, method = "rf", trControl = control)
```

## **Evaluasi Model**

```{r}
pred_val <- predict(model_rf, valSet)
confusionMatrix(pred_val, valSet$classe)
```

Model `Random Forest` menghasilkan akurasi yang sangat tinggi pada data validasi, yang menunjukkan model ini bekerja dengan baik dan tidak mengalami *overfitting*.

## **Prediksi Kasus Uji**

```{r}
# Samakan format kolom
testing_clean <- testing[, names(testing) %in% names(trainSet)]
predictions <- predict(model_rf, testing_clean)
predictions
```

## **Kesimpulan**

- Model `Random Forest` dipilih karena akurasinya tinggi dan cocok untuk data berukuran besar dengan banyak fitur.
- Validasi silang 5-fold digunakan untuk mencegah overfitting.
- Model memberikan performa tinggi pada data validasi, dengan akurasi mendekati 99%.
- Prediksi untuk 20 kasus pengujian telah dilakukan sesuai instruksi tugas.

## **Catatan Tambahan**

- Semua kode menggunakan `R` dan paket `caret` untuk konsistensi dengan pembelajaran di kursus ini.
- Untuk memastikan reproducibility, file ini bisa di-*knit* ke HTML dan dibagikan melalui GitHub.

