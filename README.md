# Submission 1: # StressPredictionTextBased
Nama: Reynaldo Arya Budi Trisna
Username dicoding: reynaldoabt

## Deskripsi
**Dataset**: (https://www.kaggle.com/datasets/kreeshrajani/human-stress-prediction/data)

**Masalah**: Stres adalah salah satu kondisi psikologis yang sangat umum dialami oleh individu dalam kehidupan sehari-hari. Dalam banyak kasus, stres dapat menjadi pemicu berbagai gangguan kesehatan mental dan fisik, seperti kecemasan, depresi, hingga gangguan kardiovaskular. Di era digital saat ini, media sosial dan platform online seperti Reddit atau platform lainnya sering digunakan oleh individu untuk mencurahkan pikiran, perasaan, dan pengalaman mereka, termasuk yang berkaitan dengan stres dari text.

Namun, mengidentifikasi tingkat stres seseorang berdasarkan teks yang mereka tulis di media sosial bukanlah tugas yang mudah. Teks yang ditulis sering kali bersifat subjektif, penuh dengan emosi, dan terkadang tidak langsung mengindikasikan stres secara eksplisit. Oleh karena itu, diperlukan pendekatan berbasis teknologi, seperti machine learning dan natural language processing (NLP), untuk menganalisis teks secara otomatis dan mendeteksi tanda-tanda stres.

Proyek ini bertujuan untuk membangun model machine learning yang dapat memprediksi tingkat stres seseorang berdasarkan teks yang mereka tulis di sebuah platform. Dengan menggunakan data tersebut, kita dapat melatih model untuk mengenali pola-pola linguistik yang sering dikaitkan dengan stres. Pendekatan ini tidak hanya membantu dalam memahami bagaimana stres diekspresikan secara verbal, tetapi juga dapat menjadi alat yang berguna bagi para profesional kesehatan mental.

**Solusi Machine Learning**: Model klasifikasi teks berbasis Neural Network dengan embedding dan lapisan dense.  untuk memprediksi tingkat stres berdasarkan fitur-fitur yang diekstrak dari data sensor.

**Metode Pengolahan** : 
1. Data Preparation
   Menghapus Kolom yang Tidak Relevan
   Dataset awal memiliki beberapa kolom seperti subreddit, post_id, sentence_range, confidence, dan social_timestamp yang tidak relevan untuk model prediksi stres. Kolom-kolom ini dihapus untuk menyederhanakan dataset, hanya menyisakan dua kolom:
   text: Teks yang akan digunakan sebagai fitur input.
   label: Label biner (0 atau 1) yang menunjukkan apakah teks terkait stres.
   Menyimpan Dataset yang Telah Diproses
   Dataset yang telah dibersihkan disimpan kembali dalam format CSV untuk digunakan dalam pipeline.

2. Data Ingestion (ExampleGen)
Deskripsi:
Komponen CsvExampleGen digunakan untuk membaca dataset dari file CSV dan mengonversinya ke format TFRecord yang dapat digunakan oleh komponen TFX lainnya.
Konfigurasi Split Data:
Dataset dibagi menjadi dua bagian:
Train (80%): Untuk melatih model.
Eval (20%): Untuk evaluasi model.

3. Data Validation
a. StatisticsGen
Deskripsi:
Komponen ini menghitung statistik deskriptif pada dataset, seperti distribusi nilai, jumlah nilai yang hilang, dan outlier. Statistik ini digunakan untuk memahami dataset dan mendeteksi potensi masalah.
b. SchemaGen
Deskripsi:
Komponen ini menghasilkan skema (schema) untuk dataset berdasarkan statistik yang dihasilkan oleh StatisticsGen. Skema ini mencakup tipe data, nilai yang diharapkan, dan batasan lainnya.
c. ExampleValidator
Deskripsi:
Komponen ini membandingkan dataset dengan skema yang dihasilkan untuk mendeteksi anomali, seperti nilai yang hilang atau tipe data yang tidak sesuai.

4. Data Preprocessing (Transform)
Deskripsi:
Komponen Transform digunakan untuk melakukan preprocessing pada data. Proses ini mencakup:
Transformasi Label: Label dikonversi menjadi tipe data int64.
Transformasi Fitur Teks: Teks diubah menjadi huruf kecil untuk konsistensi.
Fungsi preprocessing_fn:
Fungsi ini mendefinisikan transformasi yang akan diterapkan pada data. Output dari transformasi ini akan digunakan untuk melatih model.

5. Model Training (Trainer)
Deskripsi:
Komponen Trainer digunakan untuk melatih model machine learning. Berikut adalah langkah-langkahnya:
a. Input Pipeline
Data dalam format TFRecord diproses menjadi batch menggunakan fungsi input_fn.
Fitur teks ditokenisasi dan diubah menjadi representasi numerik menggunakan layer TextVectorization.
b. Arsitektur Model
Embedding Layer: Untuk merepresentasikan kata-kata dalam bentuk vektor dengan dimensi 16.
Dense Layers: Dua lapisan fully connected dengan 64 dan 32 neuron, masing-masing menggunakan fungsi aktivasi ReLU.
Output Layer: Lapisan output dengan 1 neuron dan fungsi aktivasi sigmoid untuk prediksi biner.
c. Training
Model dilatih menggunakan:
Loss Function: Binary cross-entropy.
Optimizer: Adam dengan learning rate 0.01.
Metrics: Binary accuracy.
Callback seperti EarlyStopping dan ModelCheckpoint digunakan untuk mengoptimalkan proses pelatihan.

6. Model Resolver
Deskripsi:
Komponen ini memilih model terbaik dari iterasi sebelumnya (jika ada) untuk dibandingkan dengan model baru. Hal ini memastikan bahwa model yang di-deploy adalah model yang memiliki performa terbaik.

7. Model Evaluation (Evaluator)
Deskripsi:
Komponen Evaluator mengevaluasi performa model menggunakan metrik seperti:
AUC
Binary Accuracy
Precision
Recall
F1 Score
Hasil evaluasi divisualisasikan menggunakan TensorFlow Model Analysis (TFMA).

9. Model Deployment (Pusher)
Deskripsi:
Komponen Pusher digunakan untuk mendeploy model ke direktori tertentu jika model tersebut memenuhi kriteria evaluasi. Model yang di-deploy dapat digunakan untuk prediksi di lingkungan produksi.

## Arsitektur Model 
Model yang digunakan memiliki arsitektur sebagai berikut:

1. Input Layer: Menerima teks mentah dalam bentuk string.
2. Text Vectorization: Tokenisasi dan standarisasi teks menggunakan TextVectorization.
3. Embedding Layer: Menerjemahkan teks menjadi representasi vektor.
4. Global Average Pooling: Mereduksi dimensi embedding untuk mendapatkan representasi yang padat.
5. Dense Layers: Dua lapisan dense dengan aktivasi ReLU untuk menangkap pola non-linear.
6. Output Layer: Lapisan dense dengan aktivasi sigmoid untuk menghasilkan probabilitas biner.

## Evaluasi Model 
Berikut adalah metrik yang digunakan untuk mengevaluasi performa model:

1. Binary Accuracy :Mengukur persentase prediksi yang benar.
2. Loss : Mengukur tingkat kesalahan prediksi model.
3. Area Under Curve (AUC) : Mengukur kemampuan model dalam membedakan antara kelas positif dan negatif.
4. Confusion Matrix
   ```
   True Positives (TP): Jumlah sampel positif yang diprediksi benar.
   False Positives (FP): Jumlah sampel negatif yang diprediksi salah sebagai positif.
   True Negatives (TN): Jumlah sampel negatif yang diprediksi benar.
   False Negatives (FN): Jumlah sampel positif yang diprediksi salah sebagai negatif.
   ```
6. Precision : Proporsi prediksi positif yang benar.
7. Recall : Proporsi sampel positif yang diklasifikasikan dengan benar.
8. F1 Score : Kombinasi antara precision dan recall untuk mengukur keseimbangan performa model.

## Performa Model 
Hasil evaluasi model berdasarkan metrik yang telah dihitung:

1. Binary Accuracy: 0.746 (74.61%) – Model memprediksi dengan benar sekitar 74.61% dari keseluruhan data.
2. Loss: 1.3648 – Nilai loss menunjukkan tingkat kesalahan model dalam prediksi.
3. AUC: 0.8262 – Model memiliki kemampuan yang sangat baik dalam membedakan antara kelas positif dan negatif.
4. False Positives (FP): 66 – Sebanyak 66 sampel negatif salah diklasifikasikan sebagai positif.
5. True Positives (TP): 219 – Sebanyak 219 sampel positif diklasifikasikan dengan benar.
6. False Negatives (FN): 80 – Sebanyak 80 sampel positif salah diklasifikasikan sebagai negatif.
7. True Negatives (TN): 210 – Sebanyak 210 sampel negatif diklasifikasikan dengan benar.
8. Precision: 0.7684 (76.84%) – Dari semua prediksi positif, sekitar 76.84% adalah benar.
9. Recall: 0.7324 (73.24%) – Dari semua sampel positif, sekitar 73.24% diklasifikasikan dengan benar.
10. F1 Score: 0.75 (75%) – Kombinasi antara precision dan recall menunjukkan performa keseluruhan model yang baik.

Model memiliki performa yang cukup baik dengan AUC sebesar 0.8262, yang menunjukkan kemampuan klasifikasi yang baik. Precision dan recall yang masing-masing sebesar 76.84% dan 73.24% menunjukkan bahwa model cukup andal dalam memprediksi kelas positif, meskipun masih terdapat beberapa kesalahan (false positives dan false negatives). Nilai F1 Score sebesar 75% menunjukkan keseimbangan yang baik antara precision dan recall.

Testing Model : 

**Text** : 'We will be using THE RESPECTFUL PROSTITUTE by Jean Paul Sartre This is to be one presentation that includes all of these elements. I HIGHLY recommend a PowerPoint. Take a good, clear picture or scan of your ground plan and sketch and add those as slides. Organization of your presentation is important.'

**Prediction** : Stress
