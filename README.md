# NLP-Sentiment-Analysis
## Analisis Sentimen Aplikasi Kesehatan di Google Play Store dengan IndoBERT


## Deskripsi Proyek

<p align="justify">
Proyek ini merupakan penelitian analisis sentimen terhadap ulasan pengguna aplikasi kesehatan di Google Play Store menggunakan model IndoBERT. Penelitian dilakukan untuk memahami bagaimana persepsi masyarakat terhadap layanan kesehatan digital di Indonesia berdasarkan opini yang diberikan pengguna secara langsung melalui fitur ulasan aplikasi.
</p>

<p align="justify">
Seiring meningkatnya penggunaan aplikasi kesehatan setelah pandemi COVID-19, jumlah ulasan pengguna juga mengalami peningkatan yang signifikan. Ulasan tersebut mengandung banyak informasi penting mengenai kualitas layanan, pengalaman pengguna, kemudahan penggunaan aplikasi, hingga berbagai kendala yang dialami pengguna. Namun, banyaknya ulasan membuat pengguna maupun pengembang sulit memahami keseluruhan opini secara manual.
</p>

<p align="justify">
Melalui analisis sentimen, ulasan dapat diklasifikasikan menjadi sentimen positif dan negatif secara otomatis sehingga membantu proses evaluasi aplikasi secara lebih cepat, efisien, dan terstruktur.
</p>

<p align="justify">
Penelitian ini menggunakan model IndoBERT karena mampu memahami konteks Bahasa Indonesia dengan lebih baik dibandingkan model BERT umum yang dilatih menggunakan korpus Bahasa Inggris.
</p>
---

## Latar Belakang

<p align="justify">
Digital health atau layanan kesehatan berbasis teknologi menjadi salah satu solusi penting dalam meningkatkan akses layanan kesehatan masyarakat. Berbagai aplikasi kesehatan seperti konsultasi dokter online, pembelian obat, layanan kesehatan keluarga, hingga monitoring kesehatan kini banyak digunakan masyarakat Indonesia.
</p>

<p align="justify">
Google Play Store menyediakan fitur ulasan yang memungkinkan pengguna memberikan pengalaman, kritik, maupun saran terhadap aplikasi yang digunakan. Informasi tersebut sangat berharga untuk mengetahui tingkat kepuasan pengguna dan kualitas layanan aplikasi.
</p>

<p align="justify">
Namun, jumlah ulasan yang sangat besar dapat menyebabkan information overload, yaitu kondisi ketika pengguna kesulitan memahami informasi penting karena terlalu banyak data yang tersedia. Oleh karena itu, diperlukan pendekatan otomatis untuk menganalisis opini pengguna secara efisien.
</p>

<p align="justify">
Analisis sentimen dengan pendekatan Deep Learning, khususnya Transformer dan IndoBERT, dipilih karena memiliki kemampuan memahami konteks bahasa secara lebih baik dibandingkan metode tradisional.
</p>

---

## Tujuan Penelitian

Penelitian ini bertujuan untuk:

1. Menganalisis kecenderungan opini masyarakat terhadap aplikasi kesehatan di Google Play Store.
2. Mengevaluasi performa model IndoBERT dalam melakukan klasifikasi sentimen.
3. Mengidentifikasi persepsi pengguna berdasarkan sentimen positif dan negatif terhadap aplikasi kesehatan.

---

## Dataset

Dataset yang digunakan berupa ulasan aplikasi kesehatan dari Google Play Store dengan kategori:

- Aplikasi Medis
- Aplikasi Kesehatan & Kebugaran

Total aplikasi yang digunakan:
- 50 aplikasi kesehatan
- 25 aplikasi pada masing-masing kategori

Rentang waktu pengambilan data:
- Agustus 2024 – Januari 2025

Total data awal:
- 51.998 ulasan

Total data setelah preprocessing dan pembersihan:
- 45.883 ulasan

---

## Metode yang Digunakan

### 1. Web Scraping
Pengambilan data dilakukan menggunakan library `google-play-scraper` untuk mengumpulkan ulasan pengguna dari Google Play Store.

### 2. Preprocessing Teks
Tahapan preprocessing meliputi:

- Case Folding
- Penghapusan simbol tidak penting
- Konversi emoji menjadi teks
- Normalisasi kata slang
- Tokenisasi
- Stopword Removal

### 3. Pelabelan Sentimen
Label sentimen ditentukan berdasarkan rating pengguna:

| Rating | Label |
|---|---|
| 1–2 | Negatif |
| 3 | Netral |
| 4–5 | Positif |

Label netral kemudian dihapus agar klasifikasi lebih fokus pada dua kelas utama.

### 4. Model IndoBERT
Model utama yang digunakan adalah:

`indobenchmark/indobert-base-p2`

Model ini melakukan fine-tuning untuk tugas klasifikasi sentimen menggunakan arsitektur Transformer berbasis BERT.

### 5. Evaluasi Model
Evaluasi model dilakukan menggunakan beberapa metrik:

- Accuracy
- Precision
- Recall
- F1-Score
- Confusion Matrix
- Classification Report
- Log Loss

### 6. Visualisasi Hasil Analisis Sentimen
Visualisasi hasil dilakukan menggunakan:
- WordCloud
- Grafik distribusi sentimen
- Tabel hasil sentimen per aplikasi
  
Visualisasi digunakan untuk membantu interpretasi hasil analisis secara lebih mudah dan informatif.

---

## Arsitektur Model

Penelitian menggunakan IndoBERT Base dengan spesifikasi:

- 12 Encoder Layer
- 12 Attention Head
- Hidden Size 768
- Maximum Token Length 128
- Vocabulary Size 50.000 token

Optimizer yang digunakan:
- AdamW

Regularisasi:
- Weight Decay
- Dropout
- Early Stopping

---

## Pembagian Dataset

Dataset dibagi menjadi:

| Dataset | Persentase |
|---|---|
| Train | 70% |
| Validation | 15% |
| Test | 15% |

Distribusi label dibuat seimbang menggunakan teknik:
- Stratified Sampling
- Undersampling

---

## Eksperimen Tambahan

Selain menggunakan embedding bawaan IndoBERT, penelitian ini juga melakukan eksperimen tambahan menggunakan FastText embedding sebagai validasi tambahan untuk membandingkan performa representasi teks.

Tujuan eksperimen ini adalah mengetahui apakah embedding tradisional yang lebih ringan masih mampu menghasilkan performa yang kompetitif dibandingkan embedding kontekstual dari IndoBERT.

---

## Teknologi dan Library

Beberapa teknologi dan library yang digunakan dalam proyek ini:

- Python
- PyTorch
- Transformers (Hugging Face)
- Scikit-learn
- Pandas
- NumPy
- NLTK
- Sastrawi
- Matplotlib
- WordCloud
- Google Play Scraper

---

## Hasil Penelitian

Model IndoBERT berhasil melakukan klasifikasi sentimen terhadap ulasan aplikasi kesehatan dengan performa yang sangat baik dalam memahami konteks Bahasa Indonesia.

Hasil penelitian menunjukkan bahwa:

- Akurasi model pada data testing mencapai 95%

| Label | Precision | Recall | F1-Score | Support |
|---|---|---|---|---|
| Negative (0) | 0.94 | 0.96 | 0.95 | 750 |
| Positive (1) | 0.96 | 0.94 | 0.95 | 750 |
| Accuracy |  |  | 0.95 | 1500 |
| Macro Avg | 0.95 | 0.95 | 0.95 | 1500 |
| Weighted Avg | 0.95 | 0.95 | 0.95 | 1500 |

<p align="justify">
Berdasarkan hasil eksperimen yang dilakukan, model terbaik diperoleh pada konfigurasi hyperparameter berupa batch size sebesar 32, learning rate 1e-6, epoch sebanyak 9, dropout sebesar 0.3, dan weight decay sebesar 0.01. Kombinasi parameter tersebut mampu menghasilkan proses pelatihan yang stabil serta meminimalkan risiko overfitting selama proses fine-tuning model IndoBERT.
</p>

<p align="justify">
Model terbaik berhasil mencapai akurasi sebesar 95% pada data testing, dengan nilai precision, recall, dan F1-score yang juga mencapai 95%. Hasil evaluasi menunjukkan bahwa model mampu mengklasifikasikan sentimen positif dan negatif secara seimbang tanpa bias terhadap salah satu kelas. Selain itu, nilai test loss yang relatif rendah menunjukkan bahwa model memiliki kemampuan generalisasi yang baik terhadap data yang belum pernah dilihat sebelumnya.
</p>

<p align="justify">
Hasil confusion matrix juga menunjukkan bahwa sebagian besar data berhasil diprediksi dengan benar. Dari total 1.500 data testing, model mampu mengklasifikasikan 723 data negatif dan 702 data positif secara tepat, dengan jumlah kesalahan klasifikasi yang relatif kecil. Hal tersebut menunjukkan bahwa model IndoBERT mampu memahami konteks ulasan pengguna aplikasi kesehatan dengan baik.
</p>

- Perbandingan IndoBERT dan FastText

<p align="justify">
Sebagai validasi tambahan, penelitian ini juga melakukan eksperimen dengan mengganti embedding bawaan IndoBERT menggunakan embedding FastText. Pada eksperimen ini, arsitektur utama IndoBERT tetap dipertahankan, sementara perubahan dilakukan pada bagian representasi awal token sebelum diproses oleh encoder Transformer.
</p>

| Embedding | Accuracy | Precision | Recall | F1-Score | Test Loss |
|---|---|---|---|---|---|
| IndoBERT (Default) | 95.00% | 95.00% | 95.00% | 95.00% | 0.1884 |
| FastText | 92.67% | 92.60% | 92.67% | 92.61% | 0.2382 | 

<p align="justify">
Hasil pengujian menunjukkan bahwa model dengan embedding FastText memperoleh akurasi sebesar 92,67% dengan F1-score sebesar 92,61%. Meskipun performanya cukup baik, hasil tersebut masih berada di bawah embedding bawaan IndoBERT yang mencapai akurasi dan F1-score sebesar 95%.
</p>

<p align="justify">
Perbedaan performa tersebut disebabkan oleh karakteristik representasi yang digunakan oleh masing-masing embedding. Embedding bawaan IndoBERT menggunakan representasi kontekstual yang mampu memahami makna kata berdasarkan konteks kalimat secara keseluruhan. Sementara itu, FastText menggunakan representasi statis berbasis subword n-gram yang tidak sepenuhnya mempertimbangkan konteks kalimat.
</p>

<p align="justify">
Meskipun demikian, hasil eksperimen menunjukkan bahwa FastText tetap mampu memberikan performa klasifikasi yang cukup kompetitif. Hal ini menunjukkan bahwa embedding tradisional seperti FastText masih memiliki potensi untuk digunakan pada sistem dengan kebutuhan komputasi yang lebih ringan, meskipun performanya masih sedikit di bawah embedding kontekstual milik IndoBERT.
</p>

- Sebagian besar ulasan pengguna memiliki sentimen positif
<p align="justify">
Klasifikasi sentimen data ulasan aplikasi kesehatan pada rentang waktu 1 Agustus 2024 hingga 31 Januari 2025, sebanyak 30.883 ulasan menggunakan model IndoBERT terbaik, didapatkan bahwa kelas terbanyak pada kelas positif, yang dimana sebanyak 20.101 ulasan bersentimen positif dan 10.782 ulasan bersentimen negatif. 
</p>
<p align="justify">
Hasil ini menunjukkan bahwa kecenderungan opini masyarakat terhadap aplikasi kesehatan di Indonesia cenderung bersifat positif selama periode Agustus 2024 hingga Januari 2025. 
</p>

<p align="center">
  <img src="assets/wc negatif final.png" width="300">
</p>

<p align="center">
  <i>Gambar 1. Wordcloud Hasil Sentimen Negatif</i>
</p>

<p align="center">
  <img src="assets/wc positif final.png" width="300">
</p>

<p align="center">
  <i>Gambar 2. Wordcloud Hasil Sentimen Positif</i>
</p>

- Keluhan negatif umumnya berkaitan dengan:
  - Error aplikasi
  - Loading lambat
  - Kendala login
  - Verifikasi akun
- IndoBERT mampu memahami konteks ulasan Bahasa Indonesia secara efektif

## Kesimpulan
Penelitian ini menunjukkan bahwa model IndoBERT memiliki performa yang sangat baik dalam melakukan analisis sentimen terhadap ulasan aplikasi kesehatan berbahasa Indonesia.

Dengan pendekatan berbasis Transformer, model mampu memahami konteks kalimat secara lebih mendalam dibandingkan metode tradisional. Hasil penelitian diharapkan dapat membantu pengembang aplikasi kesehatan dalam memahami kebutuhan pengguna dan meningkatkan kualitas layanan digital kesehatan di Indonesia.

## Author
Syakira Tsania Muthmainnah

syakiratsania24@gmail.com








