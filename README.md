# Submission 1: # StressPredictionTextBased
Nama: Reynaldo Arya Budi Trisna
Username dicoding: reynaldoabt

## Deskripsi
**Dataset**: (https://www.kaggle.com/datasets/kreeshrajani/human-stress-prediction/data)

**Masalah**: Memprediksi tingkat stres seseorang berdasarkan data sensor seperti detak jantung, aktivitas fisik, dan pola tidur.

**Solusi Machine Learning**: Model klasifikasi teks berbasis Neural Network dengan embedding dan lapisan dense.  untuk memprediksi tingkat stres berdasarkan fitur-fitur yang diekstrak dari data sensor.

## Arsitektur Model 
Model yang digunakan memiliki arsitektur sebagai berikut:

1. Input Layer: Menerima teks mentah dalam bentuk string.
2. Text Vectorization: Tokenisasi dan standarisasi teks menggunakan TextVectorization.
3. Embedding Layer: Menerjemahkan teks menjadi representasi vektor.
4. Global Average Pooling: Mereduksi dimensi embedding untuk mendapatkan representasi yang padat.
5. Dense Layers: Dua lapisan dense dengan aktivasi ReLU untuk menangkap pola non-linear.
6. Output Layer: Lapisan dense dengan aktivasi sigmoid untuk menghasilkan probabilitas biner.

## Evaluasi dan Performa Model 
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
