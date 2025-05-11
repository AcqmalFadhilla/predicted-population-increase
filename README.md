# Laporan Proyek Machine Learning-Muh.Acqmal Fadhilla Latief

## Bussines Understanding

Seperti kita ketahui jumlah peningkatan populasi dapat mengakibatkan meningkatkan jumlah *demand* berbagai sektor seperti sektor properti rumah,jika jumlah populasi bertambah pastinya peningkatkan minat pembelian di daerah itu disektor property juga pasti meningkat

### Problem Statements

Berdasarkan kondisi yang telah di uraikan,

1. Apakah jumlah penduduk pada negara amerika akan terus naik atau turun?

### Goal

1. Membuat model machine learning yang dapat memprediksi jumlah populasi pada negara amerika
    
    ### Solution statements
    
    1. cara untuk sampai ke goals tersebut dengan metode regression dan membandingkan beberapa algoritma model seperti neural network Regression, linear regression, dan SVR
    2. solusi di ukur dengan metrik mean absolute error(mae)

## Data Understanding

dataset yang digunakan dataset Population warga amerika serikat dari tanggal 1 januari 1952 sampai 1 desember 2019

link: [https://www.kaggle.com/datasets/census/population-time-series-data](https://www.kaggle.com/datasets/census/population-time-series-data)

### Data loading

Ada 816 baris(record atau jumlah pengamatan) dalam data set

Terdapat 4 kolom yaitu realtime_start, value, date, realtime_end 

### Deskripsi Variabel

realtime_start = tanggal awal pengamatan 6 desember 2019

value = Jumlah populasi warga amerika dari tanggal 1 januari 1952 - 1 desember 2019

date = tanggal data 1 januari 1952 - 1 desemeber 2019

realtime_end = tanggal akhir pengamatan 6 desember 2019

informasi statistik pada kolom value

|  | value |
| --- | --- |
| count | 816 |
| mean | 243847.767826 |
| std | 50519.140567 |
| min | 156309 |
| 25% | 201725.25 |
| 50% | 239557.5 |
| 75% | 289364.25 |
| max | 330309.946 |

### Missing value

seperti yang di perlihatkan pada informasi statistik kolom value terlihat bahwa tidak ada nya  missing value

### Outlinear

seperti di lihat pada code bahwa tidak ada data outlinear,untuk mengeceknya saya pakai teknik boxplot

### Kriteria tambahan

Untuk memahami  beberapa varibel di butuh teknik visualisasi contoh nya value dan date

Seperti yang terlihat pada gambar di code  bahwa jumlah populasi pada negara amerika serikat terus meningkat tahun ke tahun

## Data Preparation

Dalam data preparation yang saya lakukan pertamakali adalah membuat windowed, melakukan standard scalerd dan melakukan train test split

windowed sendiri berguna untuk membuat deret waktu berdasarkan kolom target yang di inginkan

teknik standart scaler melakukan proses standarisasi fitur dnegan mengurangkan mean(nilai rata-rata) kemudian membanginya dengan standar deviasi untuk menggeser distribusi.teknik standart scaler berguna untuk  meningkatkan performa machine learning lebih baik

teknik train test split untuk membagi dataset menjadi data training dan data test,di dalam kasus ini saya membagi dengan rasio 8:2, 8 untuk data training nya dan 2 untuk data setnya

### Modeling

Dalam tahap modeling saya memakai 3 algoritma

1. Neural Network Regression
    
    Neural Network Regression saya memakai 5 Layer dimana layer pertama adalah memakai teknik LSTM dengan neural 128 dan berfungsi sebagai layer input,layer ke 2 melakukan teknik dropout dengan konfigurasi 40% dropout supaya tidak terjadi overfitting, di layer kedua memakai hidden layer dengan 120 neural dengan activation relu,sama seperti layer pertama juga memakai teknik dropout dengan konfigurasi 20% dropout,pada layer terakhir sebagai layer output 
    
    teknik LSTM mampu mengingat kumpulan informasi yang telah disimpan dalam jangka waktu panjang, sekaligus menghapus informasi yang tidak lagi relevan. LSTM lebih efisien dalam memproses, memprediksi, sekaligus mengklasifikasikan data berdasarkan urutan waktu tertentu.dan teknik dropout cukup populer untuk menagani overfitting dimana pada teknik ini ia menonaktifkan beberapa neural untuk mencegah adaptasi yang begitu kompleks saat training
    
    pada teknik NNR saya memakai  matriks mae dimana mae sendiri adalah nilai kesalahan rata-rata eror dari nilai sebenarya dengan nilai prediksi,mae yang di dapatkan kurang dari 5%
    
    seperti yang terlihat pada gambar 1 bahwa mae yang di dapatkan kurang dari 5%
    
    ![                                                Gambar 1](Laporan%20Proyek%20Machine%20Learning-Muh%20Acqmal%20Fadhillah%Latief/Screen_Shot_2022-10-12_at_13.46.20.png)
    
                                                    Gambar 1
    
    setelah melakukan data pelatihan hasil di prediksi dapatkan adalah
    
    ![                                                Gambar 2](Laporan%20Proyek%20Machine%20Learning-Muh%20Acqmal%20Fadhillah%Latief/Screen_Shot_2022-10-11_at_14.07.23.png)
    
                                                    Gambar 2
    
2. Linear Regression
    
    Model linear yang di latih adalah x_train dan y_train dengan paramter reshape(-1,window), window nya memiliki nilai 5 dan nilai pada reshape(-1, 1)
    
    x_train.reshape(-1,window) sebagai data pelatihan
    
    y_train sebagai nilai target
    
    score yang di dapatkan model linear regression adalah 0.999999732772761 hampir mendekati nilai 1
    
    setelah melakukan data pelatihan hasil di prediksi dapatkan adalah
    
    ![                                              Gambar 3](Laporan%20Proyek%20Machine%20Learning-Muh%20Acqmal%20Fadhillah%Latief/Screen_Shot_2022-10-11_at_14.10.54.png)
    
                                                  Gambar 3
    
3. SVR
    
    Model SVR yang di latih adalah x_train dan y_train dengan paramter reshape(-1,window), window nya memiliki nilai 5 dan nilai pada reshape(-1, 1)
    
    x_train.reshape(-1,window) sebagai data pelatihan
    
    y_train sebagai nilai target
    
    score yang di dapatkan model SVR adalah 0.9938395409724174,score yang didapatkan lebih rendah dari model linear regression
    
    setelah melakukan data pelatihan hasil di prediksi dapatkan adalah
    
    ![                                              Gambar 4](Laporan%20Proyek%20Machine%20Learning-Muh%20Acqmal%20Fadhillah%Latief/Screen_Shot_2022-10-11_at_14.11.36.png)
    
                                                  Gambar 4
    

## Evaluasi

Dalam tahap evaluasi saya mencoba untuk membuat metrik predict 10 tahun kedepan,dimana  dalam tahap evaluasi ini saya mencoba evaluasi 3 model tersebut Neural Network Regression,Linear Regression, dan SVR dan membadingkan secara langsung.

Test prediksi model NNR

![                                             Gambar 5](Laporan%20Proyek%20Machine%20Learning-Muh%20Acqmal%20Fadhillah%Latief/Screen_Shot_2022-10-12_at_07.08.19.png)

                                             Gambar 5

seperti terlihat pada gambar 5 bahwa prediksi model NNR yang di dapatkan cenderung ke bawah dan sedikit melengkung

Test prediksi model linear regression

![                                              Gambar 6](Laporan%20Proyek%20Machine%20Learning-Muh%20Acqmal%20Fadhillah%Latief/Screen_Shot_2022-10-11_at_14.26.42.png)

                                              Gambar 6

seperti terlihat pada gamar 6 bahwa prediksi model linear regeression yang di dapatkan cederung naik dan terlihat berkesinambungan

Test prediksi model SVR

![                                               Gambar 7](Laporan%20Proyek%20Machine%20Learning-Muh%20Acqmal%20Fadhillah%Latief/Screen_Shot_2022-10-11_at_14.40.39.png)

                                               Gambar 7

seperti terlihat pada gamabr 7 bahwa prediksi model SVR terlihat tidak cocok untuk dataset ini di kerenakan mendapatkan hasil yang abnormal

### kesimpulan

setelah memprediksi 10 tahun ke depan hasilnya terlihat pada gambar 6  bahwa model linear regression lebih baik dalam memprediksi dataset ini dari pada model NNR, dan SVR,dimana prediksi kedepannya populasi negara amerika kedepannya akan terus meningkat sampai 2030.

 Setelah melakukan pelatihan kita dapat menyimpulkan bahwa Linear regression lebih baik performanya untuk dataset ini,tapi untuk memastikan akan melakukan evaluasi terhadap model NNR,Linear regression,dan SVR di
