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
