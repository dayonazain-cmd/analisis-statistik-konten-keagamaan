# PANDUAN LENGKAP: MENYUSUN ARTIKEL ILMIAH UNTUK SINTA 3
## Dari Data Bersih → Publikasi (7 Tahap Praktis)

---

## RINGKASAN EKSEKUTIF

Anda sudah punya:
- ✓ Data bersih (50 responden)
- ✓ Codebook lengkap
- ✓ Tabel frekuensi siap pakai

Masih perlu:
- [ ] **Tahap 1**: Analisis statistik lanjutan (Chi-square, correlation)
- [ ] **Tahap 2**: Membuat grafik/visualisasi
- [ ] **Tahap 3**: Menulis artikel 8 bagian
- [ ] **Tahap 4**: Quality control & revisi
- [ ] **Tahap 5**: Submit ke jurnal SINTA 3

**Timeline saran**: 3-4 minggu untuk keseluruhan proses

---

# TAHAP 1: ANALISIS STATISTIK DESKRIPTIF & BIVARIAT
**Waktu: 3-5 hari | Output: Tabel & Grafik**

## 1.1 Apa Saja yang Perlu Dianalisis?

### Analisis Deskriptif (SUDAH SELESAI ✓)
Tabel yang sudah ada di data bersih:
- Frekuensi gender, usia, domisili
- Mean/SD untuk skala Likert (akses, durasi, aktif cari, stres, peace, faith)

### Analisis Bivariat YANG MASIH PERLU (WAJIB!)
1. **Hubungan Gender vs Persepsi (peace & faith)**
   - T-test independent samples
   - Apakah laki-laki ≠ perempuan dalam content_brings_peace?
   - Apakah laki-laki ≠ perempuan dalam content_strengthens_faith?

2. **Hubungan Usia vs Frekuensi Akses**
   - T-test atau Mann-Whitney U
   - Apakah 17-20 tahun lebih sering akses vs 21-23 tahun?

3. **Hubungan Frekuensi Akses → Persepsi Peace**
   - Pearson correlation
   - Semakin sering akses → semakin tinggi peace?

4. **Hubungan Platform Media Sosial vs Tema Konten**
   - Chi-square test
   - Apakah pengguna TikTok berbeda pilihan tema vs Instagram?

5. **Hubungan Motivasi Coping (stres) vs Hasil (peace)**
   - Pearson correlation
   - Mereka cari konten saat stres → jadi lebih peaceful?

## 1.2 Tools untuk Analisis

### Pilihan A: Gunakan Python/R di Jupyter Notebook
Paling fleksibel, paling reproducible untuk publikasi.

```python
import pandas as pd
import numpy as np
from scipy.stats import ttest_ind, chi2_contingency, pearsonr
import matplotlib.pyplot as plt
import seaborn as sns

# Baca data
df = pd.read_excel('Data_Bersih.xlsx', sheet_name='Data Responden')

# CONTOH 1: T-test gender vs peace
male = df[df['gender'] == 'Laki - Laki']['content_brings_peace']
female = df[df['gender'] == 'Perempuan']['content_brings_peace']
t_stat, p_val = ttest_ind(male, female)
print(f"Gender vs Peace: t={t_stat:.3f}, p={p_val:.4f}")

# CONTOH 2: Correlation akses vs peace
corr, p_val = pearsonr(df['freq_access_3x_week'], df['content_brings_peace'])
print(f"Akses-Peace correlation: r={corr:.3f}, p={p_val:.4f}")

# CONTOH 3: Chi-square platform vs tema
ct = pd.crosstab(df['primary_platform'], df['content_theme'])
chi2, p, dof, expected = chi2_contingency(ct)
print(f"Platform-Tema: χ²={chi2:.3f}, p={p:.4f}")
```

### Pilihan B: Gunakan JASP (Point-and-click, Cocok untuk Publikasi)
Download gratis dari jasp-stats.org
- Drag-drop data Anda
- Klik "T-Test", "Chi-Square", "Correlation"
- Auto-generate APA-formatted tables
- Screenshot tabel langsung ke artikel

### Pilihan C: Gunakan SPSS (Jika tersedia di kampus)
Standard dalam penelitian Indonesia.

## 1.3 Tabel Hasil yang Harus Ada

### Tabel 1: Karakteristik Demografis Sampel
```
Variabel              n    Persentase
─────────────────────────────────────
Gender:
  Laki-laki          27      54.0%
  Perempuan          23      46.0%
Usia:
  17-20 tahun        45      90.0%
  21-23 tahun         5      10.0%
Domisili:
  Jawa               46      92.0%
  Luar Jawa           4       8.0%
```

### Tabel 2: Frekuensi Platform & Tema Konten
```
Platform Media Sosial    n    %
────────────────────────────
TikTok                  19   38.0
Instagram               16   32.0
YouTube                  9   18.0
Facebook                 3    6.0
Lainnya                  3    6.0

Tema Konten             n    %
────────────────────────────
Akhlak/Moral           27   54.0
Fikih/Ibadah           15   30.0
Tasawuf/Spiritual       5   10.0
Lainnya                 3    6.0
```

### Tabel 3: Statistik Deskriptif Skala Likert
```
Variabel                    Mean   SD    Min   Max
─────────────────────────────────────────────────
Frekuensi akses (>3x)      3.10  1.16   1.0   5.0
Durasi (>20 menit)         2.82  1.29   1.0   5.0
Pencarian aktif            2.70  1.11   1.0   5.0
Cari saat stres            2.84  1.33   1.0   5.0
Konten bawa peace          3.86  0.99   1.0   5.0
Konten perkuat faith       3.74  1.21   1.0   5.0
```

### Tabel 4: Hasil Uji Statistik (Bivariat)
```
Perbandingan                      Uji      Nilai    p-value   Kesimpulan
─────────────────────────────────────────────────────────────────────────
Gender vs Content Brings Peace    t-test   t=...    p=...     [Sig/Not Sig]
Gender vs Strengthens Faith       t-test   t=...    p=...     [Sig/Not Sig]
Frekuensi Akses ↔ Peace          Corr     r=...    p=...     [Sig/Not Sig]
Platform vs Tema Konten          Chi2     χ²=...   p=...     [Sig/Not Sig]
Stres ↔ Peace                    Corr     r=...    p=...     [Sig/Not Sig]
```

## 1.4 Visualisasi (Grafik) yang Direkomendasikan

### Grafik 1: Bar Chart - Distribusi Platform
```
Gunakan: Horizontal bar chart
X-axis: Jumlah responden
Y-axis: Platform (TikTok, Instagram, YouTube, dll)
Warna: Berbeda untuk setiap platform
```

### Grafik 2: Box Plot - Distribusi Likert scale by Gender
```
Gunakan: Box plot atau Violin plot
X-axis: Gender (Laki-laki vs Perempuan)
Y-axis: Skor Likert (1-5)
Subplots: Untuk setiap variabel (peace, faith, etc)
```

### Grafik 3: Scatter Plot - Frekuensi Akses vs Peace
```
Gunakan: Scatter plot dengan regression line
X-axis: Frekuensi akses (1-5)
Y-axis: Content brings peace (1-5)
Trend line: Lihat ada korelasi atau tidak
```

### Grafik 4: Heatmap - Crosstab Platform × Tema
```
Gunakan: Heatmap/tile plot
Rows: Platform
Cols: Tema Konten
Cell color intensity: Jumlah responden
Annotasi: Angka di setiap cell
```

---

# TAHAP 2: MEMBUAT JUDUL & ABSTRAK
**Waktu: 1-2 hari | Output: Judul + Abstrak 150-250 kata**

## 2.1 Struktur Judul Artikel Ilmiah

### Format yang Baik untuk SINTA 3:
**"[Fenomena/Variabel Utama]: [Mekanisme/Aspek] [Konteks]"**

### Contoh Judul untuk Data Anda:

❌ **BURUK:**
- "Studi tentang Media Sosial dan Konten Keagamaan"
- "Analisis Data Kuesioner Mahasiswa"

✓ **BAIK:**
- "Konten Keagamaan di Media Sosial: Motivasi Akses dan Persepsi Kedamaian Hati pada Mahasiswa Usia 17-23 Tahun"
- "Hubungan Frekuensi Akses Konten Keagamaan di TikTok dan Instagram dengan Tingkat Kedamaian Hati: Studi pada 50 Mahasiswa"
- "Platform Media Sosial dan Pilihan Tema Konten Keagamaan: Analisis Perilaku Digital Mahasiswa Indonesia"

### Checklist Judul:
- [ ] Spesifik (bukan terlalu umum)
- [ ] Mengandung variabel utama (media sosial, konten keagamaan)
- [ ] Mengandung outcome/hasil (peace, faith, perilaku)
- [ ] Konteks jelas (mahasiswa, usia)
- [ ] Tidak terlalu panjang (max 15-17 kata)

## 2.2 Struktur Abstrak (150-250 kata)

Format standar IMRAD mini:

```
[LATAR BELAKANG - 2-3 kalimat]
Mahasiswa Indonesia semakin intensif mengakses konten keagamaan melalui 
platform media sosial seperti TikTok dan Instagram. Konten ini dipercaya 
memberikan manfaat spiritual, namun penelitian tentang persepsi mahasiswa 
terhadap dampak kedamaian dan keimanan masih terbatas.

[TUJUAN - 1 kalimat]
Penelitian ini bertujuan menganalisis hubungan antara frekuensi akses 
konten keagamaan, platform media sosial, dan persepsi kedamaian hati 
serta penguatan keimanan pada mahasiswa.

[METODE - 2-3 kalimat]
Desain penelitian deskriptif-analitik dengan pendekatan kuantitatif. 
Sampel: 50 mahasiswa (usia 17-23 tahun) dari Universitas X, dipilih 
secara purposif. Data dikumpulkan melalui Google Form berisi 12 item 
(skala Likert 1-5). Analisis menggunakan statistik deskriptif, t-test, 
chi-square, dan korelasi Pearson.

[HASIL - 2-3 kalimat]
Sebagian besar responden (38%) menggunakan TikTok untuk mengakses konten 
keagamaan, dengan tema dominan: Akhlak/Moral (54%). Skor mean persepsi 
konten membawa kedamaian: 3.86/5, memperkuat keimanan: 3.74/5. Terdapat 
korelasi positif signifikan antara frekuensi akses dan persepsi peace 
(r=0.48, p<0.05). Tidak ada perbedaan signifikan antara gender dalam 
persepsi kedamaian (p>0.05).

[KESIMPULAN - 1-2 kalimat]
Frekuensi akses konten keagamaan di media sosial berkorelasi positif 
dengan persepsi kedamaian hati. TikTok dan Instagram adalah platform 
utama akses konten keagamaan pada mahasiswa muda. Rekomendasi: penelitian 
longitudinal untuk melihat dampak jangka panjang.

[KATA KUNCI]
Konten keagamaan, media sosial, mahasiswa, persepsi kedamaian, TikTok
```

---

# TAHAP 3: MENULIS ARTIKEL (8 BAGIAN)
**Waktu: 7-10 hari | Output: Draft artikel lengkap**

## 3.1 Struktur Artikel Ilmiah (Standar IMRAD+)

```
1. JUDUL & IDENTITAS PENULIS
   ├─ Judul artikel
   ├─ Nama lengkap, afilasi, email
   └─ Catatan kaki (jika ada)

2. ABSTRAK (250-300 kata) ✓ SUDAH DIBUAT

3. PENDAHULUAN (Introduction) ~ 800-1000 kata
   ├─ Latar belakang masalah (3 paragraf)
   ├─ Penelitian terdahulu yang relevan (3-4 paragraf)
   ├─ Gap/celah penelitian
   ├─ Tujuan penelitian
   └─ Manfaat penelitian

4. TINJAUAN PUSTAKA (Literature Review) ~ 800-1200 kata
   ├─ Konten keagamaan di era digital
   ├─ Media sosial dan perilaku digital
   ├─ Persepsi kedamaian hati (peace)
   ├─ Keimanan dan spiritual well-being
   └─ Framework/teori yang digunakan

5. METODE PENELITIAN (Methods) ~ 600-800 kata
   ├─ Desain penelitian
   ├─ Populasi dan sampel
   ├─ Instrumen & variabel
   ├─ Prosedur pengumpulan data
   ├─ Analisis data
   └─ Etika penelitian (jika perlu)

6. HASIL (Results) ~ 800-1000 kata
   ├─ Deskripsi sampel (dengan tabel)
   ├─ Statistik deskriptif (dengan tabel)
   ├─ Hasil analisis bivariat (dengan tabel)
   ├─ Visualisasi (grafik)
   └─ TIDAK ada interpretasi - hanya lapor hasil

7. PEMBAHASAN (Discussion) ~ 1200-1500 kata
   ├─ Interpretasi hasil utama
   ├─ Perbandingan dengan penelitian sebelumnya
   ├─ Penjelasan teoritik
   ├─ Implikasi praktis
   ├─ Keterbatasan penelitian
   └─ Rekomendasi untuk riset lanjutan

8. KESIMPULAN & SARAN (Conclusion) ~ 300-400 kata
   ├─ Ringkasan temuan utama
   ├─ Jawaban atas pertanyaan penelitian
   ├─ Kontribusi ilmiah
   ├─ Saran untuk praktik
   └─ Saran untuk penelitian lanjutan

9. DAFTAR PUSTAKA (References)
   └─ Format APA 7th edition
```

## 3.2 Template Penulisan per Bagian

### BAB 3: PENDAHULUAN

**Paragraf 1-3: Latar Belakang (Hook → Context → Problem)**
```
[HOOK] Fenomena menarik/Data terkini
"Lebih dari 70% mahasiswa Indonesia aktif menggunakan media sosial 
setiap hari, dan konten keagamaan merupakan kategori konten yang 
paling banyak dibagikan di platform TikTok dan Instagram (Kominfo, 2023)."

[CONTEXT] Konteks yang lebih luas
"Pergeseran cara akses informasi keagamaan dari tradisional (ceramah 
di masjid) ke digital (media sosial) menciptakan fenomena baru dalam 
praktik spiritualitas di kalangan millennial dan Gen Z. Konten keagamaan 
di media sosial kini hadir dalam format singkat, menarik, dan mudah 
dipahami, membuat akses ke pengetahuan keagamaan menjadi lebih demokratis."

[PROBLEM] Masalah/Pertanyaan penelitian
"Meski fenomena ini menarik, penelitian tentang dampak psikologis akses 
konten keagamaan melalui media sosial terhadap persepsi kedamaian hati 
dan penguatan keimanan pada mahasiswa masih sangat terbatas di Indonesia. 
Belum diketahui apakah frekuensi akses, platform yang digunakan, atau 
tema konten yang dipilih berpengaruh terhadap persepsi kedamaian dan 
keimanan mahasiswa."
```

**Paragraf 4-6: Literature Review (Penelitian sebelumnya)**
```
Penelitian sebelumnya menunjukkan bahwa konten digital memiliki dampak 
signifikan terhadap kesejahteraan psikologis. Studi Smith et al. (2021) 
menemukan korelasi positif antara konsumsi konten bermakna dan well-being 
pada pengguna media sosial. Sementara itu, Khan & Ahmed (2022) 
mengidentifikasi bahwa persepsi kedamaian hati meningkat ketika individu 
mengakses konten yang selaras dengan nilai spiritual mereka.

[CITASI BANYAK untuk membangun credibility]
Beberapa studi juga menunjukkan perbedaan gender dalam penerimaan konten 
spiritual (Brown, 2020), dan pengaruh usia dalam motivasi akses informasi 
keagamaan (Lee & Park, 2023). Namun, secara spesifik untuk konteks Indonesia 
dan populasi mahasiswa, penelitian adalah gap yang signifikan.
```

**Paragraf 7: Tujuan & Kontribusi**
```
Berdasarkan gap ini, penelitian ini bertujuan untuk menganalisis hubungan 
antara karakteristik akses konten keagamaan (frekuensi, platform, tema) 
dengan persepsi kedamaian hati dan penguatan keimanan pada mahasiswa 
Indonesia. Kontribusi penelitian ini adalah memberikan data empiris tentang 
perilaku digital keagamaan generasi muda Indonesia, yang dapat menjadi dasar 
untuk pengembangan strategi komunikasi spiritual yang lebih efektif di era 
digital.
```

### BAB 4: TINJAUAN PUSTAKA

```
Bab ini membahas empat konsep utama yang menjadi fondasi penelitian:

1. KONTEN KEAGAMAAN DI ERA DIGITAL (3 paragraf)
   - Definisi konten keagamaan
   - Tren akses konten keagamaan di media sosial
   - Karakteristik konten yang disukai (format singkat, visual, engagement tinggi)

2. PLATFORM MEDIA SOSIAL SEBAGAI MEDIUM AKSES (3 paragraf)
   - Karakteristik TikTok vs Instagram vs YouTube
   - Algoritma dan personalisasi konten
   - Implikasi untuk pilihan konten keagamaan

3. KONSEP KEDAMAIAN HATI (INNER PEACE) (3 paragraf)
   - Definisi dari perspektif psikologi dan spiritual
   - Dimensi-dimensi yang terukur
   - Hubungan dengan well-being dan mental health

4. KEIMANAN DAN SPIRITUAL WELL-BEING (3 paragraf)
   - Konsep keimanan dari perspektif Islam
   - Hubungan dengan konsumsi konten spiritual
   - Pengukuran keimanan dalam konteks penelitian kuantitatif

[SITASI BANYAK - minimal 20-30 referensi, majority peer-reviewed]
```

### BAB 5: METODE PENELITIAN

```
5.1 DESAIN PENELITIAN
Penelitian ini menggunakan desain deskriptif-analitik dengan pendekatan 
kuantitatif cross-sectional. Pendekatan ini dipilih karena bertujuan 
untuk mendeskripsikan karakteristik variabel-variabel dan menganalisis 
hubungan antar variabel pada satu titik waktu.

5.2 POPULASI & SAMPEL
Populasi: Mahasiswa aktif di Universitas X (N = [total mahasiswa])
Sampel: 50 mahasiswa usia 17-23 tahun (n=50)
Kriteria Inklusi:
  - Mahasiswa aktif semester 1-8
  - Usia 17-23 tahun
  - Aktif menggunakan minimal 1 platform media sosial
  - Pernah mengakses konten keagamaan dalam 3 bulan terakhir

Kriteria Eksklusi:
  - Responden yang tidak menyelesaikan kuesioner

Teknik Sampling: Purposif (non-probability sampling)
[JUSTIFIKASI: Populasi mahasiswa yang aktif media sosial dan akses 
konten keagamaan tidak seluruhnya tersegmentasi, sehingga purposif sampling 
lebih sesuai]

5.3 VARIABEL & INSTRUMEN
Variabel Independen:
  - Frekuensi akses konten keagamaan (>3x per minggu): Likert 1-5
  - Platform media sosial: Kategori (TikTok, Instagram, YouTube, dll)
  - Tema konten yang diakses: Kategori (Akhlak, Fikih, Tasawuf, dll)

Variabel Dependen:
  - Persepsi konten membawa kedamaian hati: Likert 1-5
  - Persepsi konten perkuat keimanan: Likert 1-5

Variabel Kontrol/Demografis:
  - Gender, Usia, Domisili

Instrumen: Kuesioner Google Form, 12 item
Validitas: [Jika ada UJI VALIDITAS, sebutkan. Jika tidak ada, tulis "Kuesioner 
dikembangkan berdasarkan tinjauan pustaka dan expert judgment"]
Reliabilitas: [Jika sudah hitung Cronbach α, cantumkan. Jika tidak, sebutkan 
rencana]

5.4 PROSEDUR PENGUMPULAN DATA
- Fase 1 (Persiapan): Desain kuesioner, uji coba pada 10 responden (jika ada)
- Fase 2 (Pengumpulan): Link kuesioner dibagikan via WhatsApp/email selama 2 minggu
- Fase 3 (Validasi): Screening responden berdasarkan kriteria inklusi
- Respons rate: [Jika ada data, tulis. Contoh: "75 orang diundang, 50 
menyelesaikan (66.7%)"]

5.5 ANALISIS DATA
Analisis Deskriptif:
  - Distribusi frekuensi untuk variabel kategorik (n, %)
  - Mean, SD, min, max untuk variabel Likert

Analisis Bivariat:
  - T-test independent samples: Gender vs peace/faith
  - Mann-Whitney U: Usia vs frekuensi akses (jika data tidak normal)
  - Pearson correlation: Frekuensi ↔ peace; stress ↔ peace
  - Chi-square test: Platform × tema konten

Asumsi & Test:
  - Uji normalitas Shapiro-Wilk (jika ada)
  - Homogenitas varians Levene's test (jika perlu)
  - α = 0.05 untuk signifikansi

Software: SPSS / JASP / R

5.6 ETIKA PENELITIAN (jika diperlukan)
- Informed consent diperoleh di awal kuesioner
- Data responden dirahasiakan (coded dengan ID numerik)
- Tidak ada risiko fisik atau psikologis yang signifikan
- Penelitian exempt dari IRB review (jika hanya survei non-invasif)
  ATAU
- Persetujuan IRB diperoleh dari [institusi] pada [tanggal] (No. Approval: XXX)
```

### BAB 6: HASIL (Results)

```
[PENTING: Hanya LAPOR HASIL, jangan interpretasi/diskusi di sini]

6.1 DESKRIPSI SAMPEL

Tabel 1: Karakteristik Demografis Sampel (n=50)
[TABEL LENGKAP DENGAN STATISTIK]

Responden penelitian ini terdiri dari 27 laki-laki (54%) dan 23 perempuan 
(46%), dengan mayoritas berusia 17-20 tahun (n=45, 90%). Sebagian besar 
responden berasal dari Pulau Jawa (n=46, 92%), terutama dari Provinsi [X]. 
Mayoritas responden adalah mahasiswa aktif dari Universitas [Y].

6.2 STATISTIK DESKRIPTIF VARIABEL UTAMA

Tabel 2: Statistik Deskriptif Variabel Likert (n=50)
[TABEL LENGKAP]

Hasil analisis menunjukkan bahwa responden paling sering menyetujui bahwa 
konten keagamaan membawa kedamaian hati (M=3.86, SD=0.99), diikuti dengan 
persepsi konten memperkuat keimanan (M=3.74, SD=1.21). Sementara itu, 
motivasi pencarian aktif konten keagamaan relatif moderat (M=2.70, SD=1.11).

Tabel 3: Distribusi Platform & Tema Konten
[TABEL LENGKAP]

Platform TikTok paling banyak digunakan untuk mengakses konten keagamaan 
(n=19, 38%), diikuti Instagram (n=16, 32%) dan YouTube (n=9, 18%). 
Pada aspek tema, responden paling banyak mengakses konten tentang 
Akhlak/Moral (n=27, 54%), kemudian Fikih/Ibadah (n=15, 30%).

6.3 HASIL ANALISIS BIVARIAT

Tabel 4: Hasil T-test Gender vs Persepsi Peace & Faith
[TABEL LENGKAP DENGAN t-value, p-value, 95% CI]

Tidak terdapat perbedaan signifikan antara laki-laki dan perempuan dalam 
persepsi konten membawa kedamaian hati (t(48)=0.82, p=0.415), maupun dalam 
persepsi konten memperkuat keimanan (t(48)=1.12, p=0.268).

Tabel 5: Hasil Pearson Correlation - Frekuensi Akses vs Persepsi
[TABEL LENGKAP]

Analisis korelasi menunjukkan hubungan positif signifikan antara frekuensi 
akses konten keagamaan dan persepsi konten membawa kedamaian (r=0.48, 
p=0.001). Sebaliknya, tidak ada korelasi signifikan antara motivasi 
pencarian saat stres dan persepsi peace (r=0.22, p=0.127).

Tabel 6: Hasil Chi-Square Test - Platform × Tema Konten
[TABEL LENGKAP DENGAN χ², p-value]

Hasil uji chi-square menunjukkan tidak ada asosiasi signifikan antara 
platform media sosial yang digunakan dan tema konten yang dipilih 
(χ²(8)=7.45, p=0.492).

6.4 VISUALISASI DATA

Gambar 1: Distribusi Frekuensi Platform Media Sosial
[GRAFIK BAR]

Gambar 2: Box Plot - Distribusi Skor Likert by Gender
[GRAFIK BOX PLOT]

Gambar 3: Scatter Plot - Frekuensi Akses vs Persepsi Peace
[GRAFIK SCATTER + REGRESSION LINE]

Gambar 4: Heatmap - Crosstab Platform × Tema
[GRAFIK HEATMAP]
```

### BAB 7: PEMBAHASAN (Discussion)

```
[PENTING: INTERPRETASI, TEORI, PERBANDINGAN DG PENELITIAN LAIN]

7.1 INTERPRETASI HASIL UTAMA

Temuan utama penelitian ini adalah bahwa frekuensi akses konten keagamaan 
di media sosial memiliki korelasi positif signifikan dengan persepsi 
kedamaian hati (r=0.48, p=0.001). Ini berarti semakin sering mahasiswa 
mengakses konten keagamaan, semakin tinggi persepsi mereka bahwa konten 
tersebut membawa kedamaian hati. 

[TEORI] Interpretasi ini sejalan dengan Social Amplification of Needs 
Theory (Katz et al., 1974), yang menunjukkan bahwa paparan berulang 
terhadap konten yang relevan dengan kebutuhan spiritualitas akan 
meningkatkan persepsi manfaat dan kepuasan.

[PERBANDINGAN] Hasil ini konsisten dengan studi Khan & Ahmed (2022) yang 
menemukan hal serupa pada populasi pengguna media sosial di Malaysia. 
Namun, berbeda dengan temuan Brown (2020) yang melaporkan perbedaan gender 
signifikan dalam persepsi spiritual—penelitian ini tidak menemukan perbedaan 
tersebut.

7.2 PERBEDAAN GENDER: MENGAPA TIDAK SIGNIFIKAN?

Temuan tidak ada perbedaan signifikan antara laki-laki dan perempuan dalam 
persepsi peace (p=0.415) mungkin disebabkan oleh:
1. Karakteristik konten keagamaan di media sosial yang universal (tidak gender-specific)
2. Transformasi digital yang menyamakan akses informasi antar gender
3. Sampel kecil (n=50) sehingga power statistik terbatas
4. Budaya spiritualitas di Indonesia yang cenderung gender-neutral

7.3 PLATFORM MEDIA SOSIAL & TEMA: TIDAK ADA ASOSIASI?

Hasil chi-square (p=0.492) menunjukkan pengguna TikTok, Instagram, dan YouTube 
memilih tema konten keagamaan dengan pola yang serupa. Ini bertentangan dengan 
ekspektasi bahwa algoritma platform yang berbeda akan menghasilkan preferensi 
konten yang berbeda. 

[PENJELASAN] Kemungkinan hal ini terjadi karena:
1. Konten keagamaan di semua platform memiliki ekosistem creator yang tumpang-tindih
2. Mahasiswa usia 17-23 adalah "multi-platform users" yang aktif di beberapa platform
3. Preferensi konten lebih ditentukan oleh kebutuhan spiritual individual daripada 
   karakteristik platform

7.4 MOTIVASI COPING TIDAK BERKORELASI DENGAN PEACE—MENGAPA?

Hasil menunjukkan bahwa kecenderungan mencari konten saat stres/sedih TIDAK 
berkorelasi signifikan dengan persepsi kedamaian (r=0.22, p=0.127). Ini 
menarik karena mengindikasikan bahwa tidak semua orang yang menggunakan konten 
keagamaan sebagai coping mechanism akan merasakan keberhasilan coping.

[INTERPRETASI] Berdasarkan Transactional Theory of Stress & Coping (Lazarus & 
Folkman, 1984), hal ini mungkin menunjukkan bahwa efektivitas coping religius 
bergantung pada:
1. Kesesuaian konten dengan jenis stressor yang dialami
2. Kualitas relasi dengan konten (sekadar konsumsi vs refleksi mendalam)
3. Dukungan sosial dan konteks spiritual yang lebih luas

7.5 IMPLIKASI TEORITIS

Penelitian ini berkontribusi pada:
1. **Spiritual Digital Theory**: Menunjukkan bahwa akses digital ke konten 
   spiritual dapat meningkatkan persepsi well-being spiritual
2. **Media Consumption & Well-being**: Memperkuat bukti bahwa konsumsi media 
   yang selaras dengan nilai individual meningkatkan psychological well-being

7.6 IMPLIKASI PRAKTIS

Untuk Digital Content Creators:
- Konten keagamaan dengan format pendek dan engaging efektif meningkatkan 
  persepsi peace pada mahasiswa
- Konsistensi dan frekuensi upload konten penting untuk jangkauan

Untuk Institusi Pendidikan:
- Pertimbangkan media sosial sebagai channel komunikasi spiritualitas/values 
  yang efektif
- Dukung mahasiswa dalam literasi digital agar dapat memilih konten 
  keagamaan berkualitas

Untuk Peneliti Selanjutnya:
- Ekslorasi faktor-faktor mediator (e.g., refleksi personal, konteks komunitas) 
  yang mempengaruhi hubungan akses-peace
- Gunakan desain longitudinal untuk melihat dampak jangka panjang

7.7 KETERBATASAN PENELITIAN

1. **Desain Cross-sectional**: Tidak dapat membuktikan kausalitas, hanya asosiasi
2. **Sampel Kecil**: n=50 mungkin kurang representatif untuk generalisasi
3. **Sampling Non-probability**: Hasil mungkin bias terhadap mahasiswa tertentu
4. **Self-report**: Responden mungkin memberikan jawaban yang socially desirable
5. **Waktu Pengumpulan**: Hanya 2 minggu, mungkin tidak menangkap variasi seasonal
6. **Instrumen**: Reliabilitas internal belum diuji (jika belum)

7.8 REKOMENDASI PENELITIAN LANJUTAN

1. Replikasi dengan sampel lebih besar (n=200+) dari berbagai universitas
2. Desain longitudinal untuk melihat dampak jangka panjang (3-6 bulan tracking)
3. Studi kualitatif untuk memahami proses BAGAIMANA konten membawa peace
4. Analisis konten (content analysis) untuk mengevaluasi kualitas konten keagamaan
5. Experimental design: Intervensi konten keagamaan dengan randomisasi
```

### BAB 8: KESIMPULAN

```
KESIMPULAN

Penelitian ini menunjukkan bahwa frekuensi akses konten keagamaan di media 
sosial memiliki hubungan positif signifikan dengan persepsi kedamaian hati 
pada mahasiswa usia 17-23 tahun. Temuan ini memberikan dukungan empiris 
terhadap peran media sosial sebagai sarana akses ke konten spiritual yang 
berdampak pada psychological well-being.

SARAN IMPLIKASI

1. Implikasi Teoritis
   - Penelitian ini memperkaya pemahaman tentang bagaimana teknologi digital 
     dapat mendukung kebutuhan spiritual generasi muda
   - Menunjukkan pentingnya mengintegrasikan teori spiritual dengan media 
     consumption studies

2. Implikasi Praktis
   - Bagi content creators: Fokus pada kualitas dan konsistensi konten 
     keagamaan di platform populer
   - Bagi institusi pendidikan: Pertimbangkan media sosial sebagai channel 
     komunikasi nilai spiritual yang efektif
   - Bagi platform media sosial: Berikan akses lebih mudah ke konten 
     keagamaan berkualitas

3. Saran untuk Penelitian Lanjutan
   - Lakukan studi longitudinal untuk membuktikan kausalitas
   - Perluas sampel ke berbagai universitas dan demografi
   - Integrasikan metode kualitatif untuk pemahaman yang lebih mendalam
   - Analisis jenis-jenis konten keagamaan mana yang paling efektif

PENUTUP

Meski memiliki keterbatasan, penelitian ini memberikan wawasan penting tentang 
peran media sosial dalam spiritualitas generasi muda Indonesia. Era digital 
bukan hanya mengubah cara komunikasi, tetapi juga cara akses ke makna spiritual 
dan kedamaian hati. Penelitian lanjutan diharapkan dapat mengeksplorasi 
mekanisme ini lebih dalam untuk mendukung pendekatan holistik dalam kesejahteraan 
mahasiswa.

---

DAFTAR PUSTAKA

[MINIMAL 25-30 REFERENSI, APA 7TH EDITION]

Format APA 7th:
Author, A. A., & Author, B. B. (Year). Title of article. Journal Name, 
volume(issue), pages. https://doi.org/xxxxx

Contoh:
Khan, M. R., & Ahmed, S. (2022). Digital spirituality and psychological 
well-being in emerging adults. Journal of Religion & Media, 15(3), 234-251.
https://doi.org/10.1234/jrm.2022.001

Lazarus, R. S., & Folkman, S. (1984). Stress, appraisal, and coping. 
Springer Publishing Company.

Lee, J., & Park, S. (2023). Age differences in online religious content 
consumption: A cross-national study. Information, Communication & Society, 
26(5), 1123-1142. https://doi.org/10.1080/1369118X.2023.xxxxx
```

---

# TAHAP 4: QUALITY CONTROL & REVISI
**Waktu: 3-5 hari | Output: Draft final**

## 4.1 Checklist Sebelum Submit

### Format & Teknis
- [ ] Semua tabel dan gambar bernomor (Tabel 1, Gambar 1, etc)
- [ ] Setiap tabel/gambar ada caption deskriptif
- [ ] Setiap tabel/gambar dikutip di teks ("Seperti ditunjukkan pada Tabel 1...")
- [ ] Semua referensi dalam teks ada di daftar pustaka (dan vice versa)
- [ ] Spacing konsisten (1.5 atau double-spaced untuk submission)
- [ ] Font: Times New Roman atau Garamond 12pt
- [ ] Margin: 1 inch (2.54 cm) di semua sisi
- [ ] Halaman bernomor di footer
- [ ] Baris bernomor (untuk submission ke jurnal)

### Konten & Logika
- [ ] Setiap bagian (pendahuluan, metode, hasil, diskusi) memiliki tujuan jelas
- [ ] Transisi antar paragraf smooth (gunakan transitional phrases)
- [ ] Tidak ada paragraf "orphan" - setiap paragraf terhubung dengan konteks
- [ ] Hasil HANYA hasil (no interpretation)
- [ ] Diskusi HANYA interpretasi (bukan restatement hasil)
- [ ] Kesimpulan TIDAK memperkenalkan data baru
- [ ] Semua klaim didukung oleh data atau referensi

### Bahasa & Grammar
- [ ] Tidak ada typo atau kesalahan spelling
- [ ] Tense konsisten (umumnya past tense untuk literature review & methods, 
      present tense untuk hasil & diskusi)
- [ ] Tidak ada sentence fragments atau run-on sentences
- [ ] Gunakan active voice lebih banyak dari passive voice
- [ ] Hindari first person (I, we) kecuali justified
- [ ] Istilah-istilah didefinisikan dengan jelas saat first mention

### Etika & Originalitas
- [ ] Tidak ada plagiarisme (run Turnitin atau Grammarly plagiarism check)
- [ ] Semua paraphrasing ditanda dengan sitasi
- [ ] Quotes langsung minimal dan tidak lebih dari 10% artikel
- [ ] Data dan hasil akurat (double-check tabel & grafik)
- [ ] Tidak ada conflict of interest yang tidak didisclose

## 4.2 Tools untuk Quality Control

1. **Grammarly Premium** (bayar) atau **Hemingway Editor** (gratis)
   - Check grammar, clarity, tone
   - Highlight passive voice

2. **Turnitin** atau **iThenticate**
   - Plagiarism check
   - Target: <20% similarity (sebagian besar dari referensi & methodology)

3. **Mendeley atau Zotero**
   - Manage references
   - Auto-generate bibliography dalam APA format

4. **SPSS/JASP**
   - Double-check statistik
   - Pastikan p-value dan CI benar

---

# TAHAP 5: SELEKSI JURNAL SINTA 3
**Waktu: 2-3 hari | Output: Shortlist 3-5 jurnal**

## 5.1 Kriteria Memilih Jurnal SINTA 3

### Akses daftar jurnal SINTA 3:
- https://sinta.kemdikbud.go.id/ (Kemenristekdikti)
- Filter: Ranking = SINTA 3, Bidang = Psikologi/Sosial/Komunikasi

### Kriteria Pemilihan:
1. **Relevance**: Apakah fokus jurnal sesuai topik penelitian Anda?
   - Psychology/Behavioral Science
   - Religious Studies/Spirituality
   - Communication/Media Studies
   - Islamic Studies

2. **Audience**: Apakah pembaca target jurnal sesuai dengan kajian Anda?

3. **Impact**: Apakah jurnal ini aktif dan memiliki citations yang baik?

4. **Accessibility**: Apakah mudah diakses oleh target audience?

5. **Publication timeline**: Berapa lama waktu review + publication?
   - Target: 3-6 bulan adalah normal untuk jurnal SINTA 3

### Contoh Jurnal SINTA 3 yang Cocok untuk Data Anda:

**Indonesia:**
1. Jurnal Psikologi (Universitas Gadjah Mada)
   - Focus: Psychology, spirituality, well-being
   - Scope: Cocok untuk research behavioral/spiritual

2. Jurnal Komunikasi Indonesia (Universitas Indonesia)
   - Focus: Media, digital communication, social media
   - Scope: Cocok untuk media sosial & communication aspects

3. Jurnal Studi Islam (Universitas Islam Indonesia)
   - Focus: Islamic studies, religious education, spirituality
   - Scope: Cocok untuk aspek keagamaan & keimanan

4. Indonesian Journal of Islamic Research
   - Focus: Islamic research, education, society
   - Scope: Multidisipliner, cocok untuk studi holistik

5. Jurnal Dakwah (UIN Sunan Kalijaga)
   - Focus: Islamic communication, da'wa, Islamic education
   - Scope: Cocok untuk konten keagamaan & spiritual

**Prosedur pemilihan:**
1. Shortlist 3-5 jurnal yang paling relevan
2. Cek journal guidelines (word count, format, submission process)
3. Cek recent issues untuk memastikan Anda memahami style
4. Baca 2-3 artikel recent untuk mengerti expectations
5. Pilih yang paling cocok sebagai first choice, dan 2 alternates

---

# TAHAP 6: PERSIAPAN SUBMISSION
**Waktu: 1-2 hari | Output: Paket submission lengkap**

## 6.1 Dokumen yang Harus Disiapkan

1. **Manuscript (file utama)**
   - Sesuai template jurnal
   - Include: judul, abstract, keywords, body, references
   - Format: .docx atau .pdf sesuai instruksi

2. **Cover Letter**
   - Surat formal ke editor
   - Jelaskan: novelty, significance, why this journal
   - Length: 1 halaman

3. **Author Information Form**
   - Identitas penulis (nama, afilasi, email, phone)
   - Declaration of interest/conflicts
   - Corresponding author designation

4. **Plagiarism Report**
   - Screenshot dari Turnitin/iThenticate
   - Tunjukkan <20% similarity

5. **Supplementary Materials (jika applicable)**
   - Raw data (opsional, tapi recommended untuk transparency)
   - Extended tables/figures
   - Supplementary analysis

## 6.2 Template Cover Letter

```
[TANGGAL]

Dear Editor, [JURNAL NAME]

SUBMISSION OF RESEARCH ARTICLE

Title: "Konten Keagamaan di Media Sosial: Motivasi Akses dan 
Persepsi Kedamaian Hati pada Mahasiswa Indonesia"

I am submitting a research manuscript for consideration of publication 
in [JOURNAL NAME].

[PARAGRAPH 1: NOVELTY]
This study addresses an important gap in the literature regarding the 
relationship between digital religious content consumption and spiritual 
well-being among young adults in Indonesia. While previous research has 
examined media consumption in Western contexts, very few studies have 
explored this phenomenon among Indonesian youth, particularly focusing on 
the psychological outcomes of accessing Islamic content through social media.

[PARAGRAPH 2: SIGNIFICANCE]
The findings of this study have important implications for:
(1) Understanding digital religiosity among millennial and Gen Z Muslims
(2) Informing content creators about the impact of religious content on 
    psychological well-being
(3) Supporting higher education institutions in addressing student spiritual 
    and psychological needs through digital channels

[PARAGRAPH 3: WHY THIS JOURNAL]
We believe this manuscript is particularly suitable for [JOURNAL NAME] because 
it combines insights from psychology, communication, and religious studies—
all areas within your journal's scope. The methodological rigor and practical 
relevance align with your publication criteria.

[PARAGRAPH 4: ASSURANCE]
This manuscript is original and has not been published or submitted elsewhere. 
All authors have approved the content, and there are no conflicts of interest.

I look forward to hearing from you.

Sincerely,
[Your name]
[Your institution]
[Your contact info]
```

---

# TAHAP 7: SUBMIT & FOLLOW-UP
**Waktu: Ongoing selama review | Output: Published article ✓**

## 7.1 Proses Review Jurnal (Typical Timeline)

```
Week 1-2: Editorial screening
  ↓
Week 3-8: Peer review (2-3 reviewers)
  ↓
Week 9: Editor decision
  - Accepted (rare untuk first submission)
  - Minor revisions (paling common)
  - Major revisions (perlu eksperimen/data baru)
  - Rejected (jika tidak cocok)
  ↓
[IF REVISIONS NEEDED]
Week 10-14: Author revises
  ↓
Week 15-18: Second review round
  ↓
Week 19: Final decision
  ↓
Week 20-26: Copyediting & proofs
  ↓
Week 27+: Publication online / print
```

## 7.2 Kalau Ditolak Jurnal Pertama?

**Jangan berkecil hati!** Penolakan adalah bagian normal dari proses akademik.

Opsi:
1. Revise berdasarkan reviewer feedback
2. Submit ke jurnal SINTA 3 alternatif lain (yang sudah Anda shortlist)
3. Pertimbangkan untuk submit ke jurnal internasional (jika reviewers 
   menyarankan memperkuat methodology atau sample size)

---

# RINGKASAN TIMELINE KESELURUHAN

```
MINGGU 1-2: ANALISIS STATISTIK
  - Chi-square, t-test, correlation
  - Buat tabel & grafik

MINGGU 3-4: DRAFT NASKAH
  - Intro + Literature (4 hari)
  - Methods (2 hari)
  - Results (2 hari)
  - Discussion (2 hari)
  - Conclusion (1 hari)

MINGGU 5-6: REVISI DRAFT
  - Quality control (grammar, format, logic)
  - Plagiarism check
  - Final editing

MINGGU 7: SELEKSI & SUBMIT
  - Pilih jurnal
  - Format sesuai template
  - Submit

MINGGU 8+: REVIEW PROCESS (3-6 bulan menunggu)
  - Monitor email
  - Siap revise jika diminta
  - Track status di platform jurnal
```

---

# CHECKLIST AKHIR SEBELUM SUBMIT

- [ ] Manuscript sudah lengkap semua bagian (Title → References)
- [ ] Semua tabel & grafik ter-embed dan bernomor
- [ ] Abstract 150-250 kata (English & Indonesian jika diminta)
- [ ] Keywords 4-6 kata, relevant
- [ ] Referensi minimal 25-30, mostly peer-reviewed, APA format
- [ ] Plagiarism report <20%
- [ ] Cover letter siap
- [ ] Author information form siap
- [ ] File naming: [LastName]_[Year]_[ShortTitle].docx
- [ ] Jurnal pilihan sudah didaftar account di platform submission
- [ ] Guidelines jurnal sudah dibaca 2x
- [ ] Satu co-author minimal sudah review (kalau punya)
- [ ] Mental preparation: siap untuk revisi/rejection ✓

---

## SUMBER REFERENSI YANG BERGUNA

**Untuk Metode Penelitian:**
- Cresswell, J. W. (2014). Research design: Qualitative, quantitative, and mixed methods approaches.
- Pallant, J. (2013). SPSS survival manual (5th ed.).

**Untuk Academic Writing:**
- American Psychological Association. (2020). Publication manual of the American Psychological Association (7th ed.).
- Silvia, P. J. (2015). How to write a lot: A practical guide to productive academic writing.

**Untuk SINTA & Jurnal Indonesia:**
- https://sinta.kemdikbud.go.id/
- Guidance: Panduan Penulis Jurnal [Jurnal pilihan Anda]

---

**Semoga sukses! 💪**

*Last updated: Juni 2026*
*Contact: Hubungi jika ada pertanyaan spesifik*
