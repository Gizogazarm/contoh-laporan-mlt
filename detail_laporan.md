# MENCARI POSISI PEMAIN TERHADAP _SKILL_ SEPAK BOLA 

## Domain Proyek

Latar belakang proyek untuk tema ini adalah berdasarkan penilaian yang diambil dan digunakan oleh _Game Developer_ EA Sport sebagai _Skill_ pemain pada game FIFA yaitu game Sepak Bola. 

Penilaian _Skill_ yang digunakan pada pemain dalam permainan tersebut , FIFA ,  yaitu berdasarkan standar yang dimiliki oleh _Game Developer_ dalam menentukan besar atau kecil penilain _Skill_ Pemain berdasarkan realita pemain tersebut. 

Ambil contoh untuk seorang Lionel Messi , seorang pemain hebat yang bisa dikatakan sebagai pemain terbaik yang pernah ada , mempunyai pernilaian yang bagus dan mempunyai beberapa kategori penilaian _Skill_ individu yang sangat baik sehingga kriteria skill yang dibuat seperti _Shooting, Finishing, Dribling ,etc_ mempunyai nilai yang sangat baik. 

Penilaian pemain dalam game FIFA memberikan aspek latar belakang pada proyek saya ini , karena penilaian yang diberikan pada game FIFA ini ,  mencerminkan _Skill_ individu pemain yang bisa diolah menjadi suatu informasi yang penting dalam hal menentukan tingkatan level pemain , harga pemain , posisi pemain dll . Sehingga mengambil keputusan untuk mengambil tema mencari posisi pemain terhadap _Skill_ sepak bola .

Pengolahan informasi dan analisa yang baik terhadap data permainan sepak bola bahkan membandingkan dengan game FIFA untuk mengaplikasikan pada dunia nyata dapat memberikan aspek yang belum pernah dilakukan atau mengalami perkembangan seperti riset mencari data pemain atau kisah Will Still , yang menggemari Game sepak bola lainnya yaitu _Football Manager_ sehingga memproyeksikan dirinya seperti manager sepak bola dan mengembangkan bakatnya menjadi manager sepak bola yang nyata [Referensi](https://www.idntimes.com/sport/soccer/satria-permana-1/kisah-will-still-penggila-football-manager-jadi-pelatih-di-ligue-1-c1c2?page=all)


## Business Understanding

Hal yang harus dicermati dalam klasifikasi masalah yang terdapat dalam pencarian posisi terhadap _Skill_ pemain yang didapat dataset yang berdasarkan game FIFA ini adalah : 


### Problem Statements

- Bagaimana hubungan antara _Skill_ pemain dengan posisi pemain ? 
- Apakah dapat memperkirakan posisi pemain dengan _Skill_ pemain sepak bola berdasarkan dataset game FIFA  ?
- Apakah terdapat perbedaan _Skill_ pemain pada tiap posisi berbeda sehingga menjadi satu acuan pemain tersebut menempati posisi tersebut ? 

### Goals

- Analisis korelasi antara skill pemain, seperti shooting, passing, dan defending, dengan posisi pemain dapat memberikan wawasan tentang seberapa besar pengaruh keterampilan tertentu terhadap pemilihan posisi pemain. Misalnya, dapat ditemukan bahwa pemain dengan shooting yang baik cenderung lebih sering berposisi sebagai striker
  
- Untuk memperkirakan posisi pemain terhadap _Skill_ pemain yang didapat dari dataset game FIFA bisa dilakukan dengan menggunakan _Machine Learning_ , akan tetapi perlu kajian lebih dalam untuk memperkirakan posisi pemain secara nyata karena mempunyai faktor - faktor eksternal yang tidak terdapat pada dataset game FIFA lainnya selain skill sepak bola yang di _Standardisasi_ oleh EA SPORT
  
- Analisis perbedaan rata-rata skill pemain pada setiap posisi dapat memberikan pemahaman yang lebih baik tentang karakteristik keterampilan yang diharapkan untuk setiap posisi. Misalnya, dapat ditemukan bahwa defending lebih ditekankan untuk posisi bek, sementara shooting lebih penting untuk posisi striker. Hal ini dapat menjadi acuan bagi pemain atau tim dalam menentukan penempatan yang optimal sesuai dengan keahlian individu

    ### Solution statements
    - Proses yang dilakukan adalah Klasifikasi karena menggunakan data kategorikal dengan label posisi dari pemain sepak bola dengan menggunakan 2 algoritma multiclass yaitu _Random Forest_ dan _Decision Tree_.
      

## Data Understanding
Dataset yang digunakan adalah berdasarkan dari game FIFA , yang didapat dari
 [(Kaggle.com)](https://www.kaggle.com/datasets/maso0dahmed/football-players-data) hasil dari web scrapping [sofifa.com](https://sofifa.com/).

Terdapat 51 kolom dengan 17954 dataset yang terdapat pada dataset tersebut , jadi hanya menyebutkan sebagian fitur saja 

### Variabel-variabel dataset adalah sebagai berikut:
- name : Nama Pemain
- full_name : Nama lengkap pemain 
- birth_date : Tanggal lahir pemain
- age : Umur pemain
- height_cm : Tinggi pemain
- weight_kgs : Berat pemain
- positions : Posisi pemain
- nationality : Negara Pemain
- overall_rating : Rating keseluruhan pemain
- potential : Nilai potensi pemain berdasarkan pemain
- value_euro : Nilai harga pemain
- wage_euro : Gaji pemain
- preferred_foot : pilihan kaki pemain saat bermain
- international_reputation(1-5) : reputasi bermain yang dinilai dalam bentuk data ordinal
- weak_foot(1-5) : Penggunaan kaki pemain yang dinilai tidak biasa / dianggap kurang dalam penilaian bentuk data ordinal
- skill_move(1-5) : Penilain skill bermain dalam bentuk data ordinal
- body_type : Bentuk badan pemain
- release_clause_euro : Ketentuan nilai/Harga pemain yang dapat ditebus tanpa negosiasi dengan klub
- national_team : Tim nasional pemain
- national_rating : Rating penilaian pemain di tim nasional
- national_team_position : Posisi pemain di timnas
- national_jersey_number : Nomor pemain di timnas
- dst (adalah fitur skill pemain sepak bola)

## Data Preparation
Pada tahap ini , sesuai dengan proyek di Google Collab bahwa pada data preparation di bagi dengan Data Cleaning , Transformasi data target , Data Cleaning Part 2, One Head Encoding , Split Data dan Normalisasi 

### Data Cleaning 
- Mencari nilai yang _null_ pada dataset sehingga tidak terdapat anomali pada dataset dan terdapat pada fitur _value_euro, wage_euro, release_clause_euro, national_team, national_rating, national_team_position, national_jersey_number_
- mendrop beberapa fitur value_euro, wage_euro, release_clause_euro karena tidak ada relevansi dengan posisi pemain
- Mendrop beberapa fitur termasuk fitur yang mempunyai nilai _null_ yang banyak diantara nya fitur _national_team, national_rating, national_team_position, national_jersey_number_ dikarenakan sebanyak 17097 pemain tidak bermain di timnas
- serta mendrop 3 fitur yang tidak ada relevansi dengan posisi pemain yaitu _full_name, birth_date, nationality_
- Mengecek dataset ada yang duplicate / redundant pada dataset dan hasil menggunakan fungsi duplicated() mempunyai nilai null
- sehingga terdapat 17954 data dengan 41 kolom

### Transformasi Data Target
- Setelah dirasa cukup untuk melakukan data cleaning terhadap dataset yang mempunyai nilai null , serta beberapa fitur yang tidak relevan terhadap target , maka melihat data sebaran pada posisi target
- Setelah menggunakan fungsi value_counts() untuk mengetahui sebaran data pada kolom target, terdapat 890 klasifikasi / kelas sesuai pada visualisasi di collab
- Melihat hal tersebut , untuk klasifikasi dimana terdapat 890 terlalu banyak sehingga harus digeneralisasi untuk klasifikasi label machine learning
- klasifikasi yang akan digeneralisasi adalah menjadi 6 kelas dengan ketentuan yaitu Kiper , Bek , Bek Sayap, Gelandang, Striker.
- Penyederhanaan Klasifikasi yang dilakukan dengan cara mengambil posisi pertama pada posisi pemain sebagai posisi pemain natural sehingga terdapat posisi pemain dengan nilai GK,CB,CDM,CM,CAM,LB,RB,LWB,RWB,LM,RM,RW,LW,CF,ST.
- Setelah melakukan hal tersebut , maka dikelompokkan ke dalam 6 kelas dengan ketentuan : GK sebagai Kiper, CB sebagai Bek, CDM, CM , CAM sebagai Gelandang, LB,RB,LWB,RWB sebagai Bek Sayap, LM,RM,RW,LW sebagai Winger, CF,ST sebagai striker
- Proses tersebut berhasil dilakukan dan sebaran data untuk label target terdapat Gelandang sebanyak 4587, Bek sebanyak 3084 , Winger sebanyak 2815, Bek Sayap sebanyak 2799, Striker sebanyak 2604, Kiper sebanyak 2065 data sehingga dijumlahkan akan sama persis dengan 17954 dataset
- Terakhir , mencocokkan data target dengan posisi pemain agar sesuai dengan realita seperti : Lionel Messi seorang striker, Christian Eriksen seorang gelandang , Paul Pogba seorang Gelandang

### Data Cleaning Part 2
- Setelah mengubah label target , melakukan pengecekan pada fitur yang dirasa belum di cleaning sehingga dataset dianggap sudah bersih dengan mengecek fitur categorical dalam sebaran datanya
- tedapat anomali pada sebaran data fitur body yang tedapat sebaran data yang dianggap bisa seperti tipe bodi messi , ronaldo dan shaqiri sehingga fitur tersebut perlu didrop dan dianggap tidak mempunyai korelasi yang tinggi dengan target begitu juga dengan fitur name dan age
  
### One Head Encoding 
- setelah melakukan describe() pada dataset terdapat data kategorikal yang perlu diubah menjadi data numerik agar dapat diproses oleh algoritma pada fitur target position_transform serta preferred foot
- setelah berhasil mengubah dengan fungsi pandas yaitu getdummies() maka mendrop fitur position_transform dan prefferred foot

### Split Data 
- Terdapat 17954 data dengan 41 kolom , maka perlu memisahkan dataset menjadi label serta target dimana 6 fitur dijadikan satu dataframe yaitu sebagai y (target) dan 35 fitur dijadikan satu data frame sebagi x (feature)
- Komposisi untuk split data yaitu perbandingan 70 train : 30 validasi
- Sebanyak 12567 sebagai data train dan 5387 sebagai data validasi

### Normalisasi 
- Pada tahap ini menggunakan MinMaxScaler sebagai algoritma untuk menormalisasi data train serta data testing karena pada standar deviasi serta min dan max pada fungsi describe() terdapat skala yang jauh berbeda antara satu sama lain sehingga perlu disamakan agar memudahkan algoritma untuk memproses data 

## Modeling
- Pada tahap ini model yang digunakan adalah _Random Forest_ dan _Decision Tree_ untuk mengelola model yang klasifikasi multiclass. Pemilihan _Random Forest_ berdasarkan pada kemampuan untuk menangani kategori yang banyak karena data train sekitar 35 fitur dengan 6 target dan penggunaan Decision Tree dikarenakan interpretabilitas yang tinggi dengan menggunakan pohon keputusan agar dapat mempengaruhi keputusan klasifikasi.
- Pada penerapan tuning model , hyperparameter yang digunakan adalah default untuk menguji output model terlebih dahulu terhadap dua model.
- Diambil kesimpulan pada penerapan model yang akan digunakan adalah hasil dari model _Random Forest_ ( untuk pengambilan keputusan pemilihan model dapat dijelaskan pada bagian evaluasi )

## Evaluation
Metrik yang digunakan dalam menganalisa dari model yang digunakan _Random Forest_ dan _Decision Tree_ adalah Akurasi, Precision, Recall dan F1 Score sebagai metrik evaluasi untuk kedua model tersebut.

[Metrik Evaluasi](/assets/images/download.png)

- Akurasi 

Sebagai contoh, Anda memiih kasus klasifikasi dan menggunakan metrik **akurasi, precision, recall, dan F1 score**. Jelaskan mengenai beberapa hal berikut:
- Penjelasan mengenai metrik yang digunakan
- Menjelaskan hasil proyek berdasarkan metrik evaluasi

Ingatlah, metrik evaluasi yang digunakan harus sesuai dengan konteks data, problem statement, dan solusi yang diinginkan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan formula metrik dan bagaimana metrik tersebut bekerja.

**---Ini adalah bagian akhir laporan---**

_Catatan:_
- _Anda dapat menambahkan gambar, kode, atau tabel ke dalam laporan jika diperlukan. Temukan caranya pada contoh dokumen markdown di situs editor [Dillinger](https://dillinger.io/), [Github Guides: Mastering markdown](https://guides.github.com/features/mastering-markdown/), atau sumber lain di internet. Semangat!_
- Jika terdapat penjelasan yang harus menyertakan code snippet, tuliskan dengan sewajarnya. Tidak perlu menuliskan keseluruhan kode project, cukup bagian yang ingin dijelaskan saja.

