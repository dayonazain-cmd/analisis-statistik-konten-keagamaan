# Analisis Statistik: Konten Keagamaan & Media Sosial Mahasiswa

## Tentang Proyek
Repositori ini berisi *pipeline* analisis data end-to-end untuk penelitian berjudul **"Konten Keagamaan di Media Sosial: Motivasi Akses dan Persepsi Kedamaian Hati pada Mahasiswa"**. 

Proyek ini dirancang untuk mengotomatisasi proses analisis statistik dan menghasilkan output (tabel & grafik) yang siap digunakan untuk publikasi artikel ilmiah di jurnal terakreditasi (SINTA 3).

## Struktur Repositori
*   `analisis_statistik.py` : Script Python utama untuk menjalankan seluruh proses analisis (T-Test, Korelasi Pearson, Chi-Square) dan menghasilkan visualisasi secara otomatis.
*   `Data_Bersih.xlsx` : Dataset hasil pembersihan (50 responden, 13 variabel) yang siap dianalisis.
*   `Data_Cleaning_Report.txt` : Laporan dokumentasi proses *data cleaning* dan *quality assurance* untuk memenuhi standar *reproducibility* penelitian.
*   `Panduan_Menyusun_Artikel_SINTA3.md` : Panduan komprehensif (SOP) penulisan artikel ilmiah dari data hingga siap submit.

## Fitur Script Python
Script `analisis_statistik.py` akan secara otomatis:
1. Menghitung statistik deskriptif (Demografi & Skala Likert).
2. Melakukan Uji Bivariat (T-test, Korelasi Pearson, Chi-Square).
3. Menghasilkan 5 Grafik siap publikasi (Bar chart, Boxplot, Scatter plot, Heatmap).
4. Mengekspor hasil ke folder `output_analisis/` dalam format CSV (untuk tabel Word) dan PNG (untuk gambar artikel).
5. Menghasilkan laporan naratif otomatis (`Laporan_Analisis.txt`).

## Cara Menjalankan Script
1. Pastikan Python 3 terinstal.
2. Install *dependencies*:
   ```bash
   pip install pandas numpy scipy matplotlib seaborn openpyxl
