# Proyek1MLT - Salary Prediction
Proyek pertama Predictive Analytics untuk memenuhi submission Dicoding

#### Disusun oleh : Dery Dewantara

## Domain Proyek

Gaji merupakan sebuah hal umum yang dimiliki oleh seseorang yang bekerja. Gaji setiap orang juga berbeda beda, tergantung oleh lama bekerja, umur, jenis pekerjaan, hingga pendidikannya.

<br>

<div><img src="https://img.freepik.com/premium-vector/vector-cartoon-illustration-happy-office-employee-lettering-text-salary_194552-883.jpg" width="250"/></div>

[Referensi gambar](https://www.freepik.com/premium-vector/vector-cartoon-illustration-happy-office-employee-lettering-text-salary_24287721.htm)

<br>
Setiap gaji seseorang tidak selalu pasti sama walaupun memiliki jenis pekerjaan yang sama dan umur yang sama. Oleh karena itu sulit untuk melakukan prediksi gaji seseorang. Faktor ketidakpastian perlu dikurangi dengan membangun sistem prediksi yang dapat menentukan berapa gaji yang pantas dimiliki oleh seseorang dengan kualifikasi tertentu.

Dalam mencapai hal tersebut, maka dilakukan penelitian untuk memprediksi Gaji seseorang menggunakan model machine learning. Diharapkan model ini mampu memprediksi Gaji yang sesuai dengan pasar dan kualifikasi yang dimiliki. Prediksi ini nantinya dijadikan acuan bagi perusahaan dalam memberi gaji kepada pegawainya.

Referensi : [Salary Prediction Using Regression Techniques](https://dx.doi.org/10.2139/ssrn.3526707)

## Business Understanding

Proyek ini dibangun untuk mempermudah perusahaan dalam memberikan gaji pegawai sesuai kualifikasi pegawainya.

### Problem Statement

1. Fitur apa yang paling berpengaruh terhadap Gaji pegawai?
2. Bagaimana cara memproses data agar dapat dilatih dengan baik oleh model?
3. Berapa Gaji pasaran berdasarkan karakteristik tertentu?

### Goals

1. Mengetahui fitur yang paling berpengaruh terhadap gaji pegawai.
2. Melakukan persiapan data untuk dapat dilatih oleh model.
3. Membuat model machine learning yang dapat memprediksi gaji pegawai seakurat mungkin berdasarkan karakteristik tertentu.

### Solution Statement

1. Menganalisis data dengan melakukan univariate analysis dan multivariate analysis.
2. Menyiapkan data agar bisa digunakan dalam membangun model.
3. Melakukan hyperparameter tuning menggunakan grid search dan membangun model regresi menggunakan ALgoritma K-Nearest Neighbour, Random Forest, dan AdaBoost.

## Data Understanding & Removing Outlier

Dataset yang digunakan dalam proyek ini merupakan data Gaji pegawai yang dapat diunduh di [Kaggle : Salary Data](https://www.kaggle.com/datasets/mohithsairamreddy/salary-data/data).

Berikut informasi pada dataset :

+ Dataset memiliki format CSV.
+ Dataset memiliki 6704 sample dengan 6 fitur.
+ Dataset memiliki 3 fitur bertipe float64 dan 3 fitur bertipe object.
+ Terdapat missing value/null dalam semua fitur.

### Variable - variable pada dataset

+ Age: Umur Pegawai.
+ Gender: Jenis kelamin pegawai.
+ Education Level: Level pendidikan pegawai.
+ Job Title: Nama pekerjaan/posisi pegawai.
+ Year of Experience: Lama pengalaman atau lama kerja pegawai.
+ Salary: Gaji pegawai

Dari ke 6 fitur dapat dilihat bahwa fitur Gender tidak mempengaruhi Salary sehingga akan dihapus. 

### Univariate Analysis

Univariate Analysis adalah menganalisis setiap fitur secara terpisah.

#### Analisis jumlah nilai unique pada setiap fitur

<div><img src="https://github.com/illyosxy/Proyek1MLT/blob/main/SS/1.png?raw=true" width="220"/></div>
<div><img src="https://github.com/illyosxy/Proyek1MLT/blob/main/SS/2.png?raw=true" width="220"/></div>
<div><img src="https://github.com/illyosxy/Proyek1MLT/blob/main/SS/3.png?raw=true" width="220"/></div> 
<div><img src="https://github.com/illyosxy/Proyek1MLT/blob/main/SS/4.png?raw=true" width="220"/></div>
<div><img src="https://github.com/illyosxy/Proyek1MLT/blob/main/SS/5.png?raw=true" width="220"/></div>
<br />

+ Fitur Education Level memiliki 1 buah sample yang hanya berisi 1 buah data, dimana sample tersebut seharusnya dapat dijadikan satu dengan sample lainnya (phD dan PhD).
+ Sedangkan Fitur Job Title memiliki banyak sekali unique value sehingga alangkah baiknya fitur ini dihapus untuk menghindari high dimensional data.
+ Sedangkan Fitur lainnya memiliki sebaran sample yang cukup merata.

#### Analisis sebaran pada setiap fitur numerik

<div><img src="https://github.com/illyosxy/Proyek1MLT/blob/main/SS/6.png?raw=true" width="450"/></div><br />
Berikut analisis dari grafik di atas :

+ Sebagian besar pegawai berada pada rentang umur 25-30.
+ Sebagian besar pegawai memiliki pengalaman kurang dari 5 tahun.
+ Rentang Gaji cukup tinggi, yaitu dari 350 hingga 250000. Namun, rata-rata Gaji 115328.

### Multivariate Analysis

Multivariate Analysis menunjukkan hubungan antara dua atau lebih fitur dalam data.

#### Analisis fitur numerik
  
+ Melihat kolerasi antara semua fitur numerik
  <div><img src="https://github.com/illyosxy/Proyek1MLT/blob/main/SS/7.png?raw=true" width="350"/></div>
  Ketiga fitur numerik tersebut memiliki korelasi yang cukup tinggi seperti yang dilihat pada gambar diatas, sehingga hal ini akan sangat bagus dalam proses pembuatan model nanti.

#### Analisis fitur kategorik

Analisis ini dilakukan untuk melihat kolerasi antara fitur kategorik dengan fitur target (Salary).

+ Fitur Education Level
  <div><img src="https://github.com/illyosxy/Proyek1MLT/blob/main/SS/8.png?raw=true" width="500"/></div>
  Fitur Education Level memiliki pengaruh yang sangat tinggi terhadap gaji pegawai, semakin tinggi tingkat pendidikan pegawai maka semakin besar pula gaji pegawai yang didapatkan.

## Data preparation

+ One Hot Encoding

  One hot encoding adalah teknik mengubah data kategorik menjadi data numerik dimana setiap kategori menjadi kolom baru dengan nilai 0 atau 1. Fitur yang akan diubah menjadi numerik pada proyek ini adalah Fitur Education Level.
  
+ Train Test Split

  Train test split aja proses membagi data menjadi data latih dan data uji. Data latih akan digunakan untuk membangun model, sedangkan data uji akan digunakan untuk menguji performa model. Pada proyek ini dataset sebesar 6697 dibagi menjadi 6027 untuk data training dan 670 untuk data testing.

## Modeling

+ Algoritma
  Penelitian ini melakukan pemodelan dengan 3 algoritma, yaitu K-Nearest Neighbour, Random Forest, dan AdaBoost.
  + K-Nearest Neighbour
    K-Nearest Neighbour bekerja dengan membandingkan jarak satu sampel ke sampel pelatihan lain dengan memilih sejumlah k tetangga terdekat. Proyek ini menggunakan [sklearn.neighbors.KNeighborsRegressor](https://scikit-learn.org/stable/modules/generated/sklearn.neighbors.KNeighborsRegressor.html) dengan memasukkan X_train dan y_train dalam membangun model. Parameter yang digunakan pada proyek ini adalah :
    + `n_neighbors` = Jumlah k tetangga tedekat.

  + Random Forest
    Algoritma random forest adalah teknik dalam machine learning dengan metode ensemble. Teknik ini beroperasi dengan membangun banyak decision tree pada waktu pelatihan. Proyek ini menggunakan [sklearn.ensemble.RandomForestRegressor](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestRegressor.html) dengan memasukkan X_train dan y_train dalam membangun model. Parameter yang digunakan pada proyek ini adalah :
    + `n_estimators` = Jumlah maksimum estimator di mana boosting dihentikan.
    + `max_depth` = Kedalaman maksimum setiap tree.
    + `random_state` = Mengontrol seed acak yang diberikan pada setiap base_estimator pada setiap iterasi boosting.

  + Adaboost
    AdaBoost juga disebut Adaptive Boosting adalah teknik dalam machine learning dengan metode ensemble.  Algoritma yang paling umum digunakan dengan AdaBoost adalah pohon keputusan (decision trees) satu tingkat yang berarti memiliki pohon Keputusan dengan hanya 1 split. Pohon-pohon ini juga disebut Decision Stumps. Algoritma ini bertujuan untuk meningkatkan performa atau akurasi prediksi dengan cara menggabungkan beberapa model sederhana dan dianggap lemah (weak learners) secara berurutan sehingga membentuk suatu model yang kuat (strong ensemble learner). Proyek ini menggunakan [sklearn.ensemble.AdaBoostRegressor](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.AdaBoostRegressor.html) dengan memasukkan X_train dan y_train dalam membangun model. Parameter yang digunakan pada proyek ini adalah :
    + `n_estimators` = Jumlah maksimum estimator di mana boosting dihentikan.
    + `learning_rate` = Learning rate memperkuat kontribusi setiap regressor.
    + `random_state` = Mengontrol seed acak yang diberikan pada setiap base_estimator pada setiap iterasi boosting.

+ Hyperparameter Tuning (Grid Search)
  Hyperparameter tuning adalah cara untuk mendapatkan parameter terbaik dari algoritma dalam membangun model. Salah satu teknik dalam hyperparameter tuning yang digunakan dalam proyek ini adalah grid search. Berikut adalah hasil dari Grid Search pada proyek ini :
  | model    | best_params                                                     |
  |----------|-----------------------------------------------------------------|
  | knn      | {'n_neighbors': 6}                                              |
  | boosting | {'learning_rate': 0.1, 'n_estimators': 100, 'random_state': 11} |
  | rf       | {'max_depth': 32, 'n_estimators': 25, 'random_stste': 11}        |

## Evaluation

Metrik evaluasi yang digunakan pada proyek ini adalah akurasi dan mean squared error (MSE). Akurasi menentukan tingkat kemiripan antara hasil prediksi dengan nilai yang sebenarnya (y_test). Mean squared error (MSE) mengukur error dalam model statistik dengan cara menghitung rata-rata error dari kuadrat hasil aktual dikurang hasil prediksi.

Berikut hasil evaluasi model :

+ Akurasi
  | model    | accuracy |
  |----------|----------|
  | knn      | 0.94098  |
  | boosting | 0.775894 |
  | rf       | 0.93844  |

+ Mean Squared Error (MSE)
  <div><img src="https://github.com/illyosxy/Proyek1MLT/blob/main/SS/9.png?raw=true" width="300"/></div>

Dari hasil evaluasi dapat dilihat bahwa model dengan algoritma Random Forest memiliki akurasi lebih tinggi tinggi dibandingkan dengan AdaBoost dan KNN.
