# Customer-Segmentation
## Business Understanding
Superstore berusaha untuk mengidentifikasi segmen pelanggan mana yang harus diprioritaskan dalam upaya pemasaran mereka dan mana yang harus dihindari agar dapat meningkatkan profitabilitas mereka. Perusahaan membutuhkan wawasan berbasis data untuk menjawab pertanyaan berikut:
- Segmen pelanggan mana yang paling menguntungkan?
- Segmen pelanggan mana yang berisiko berhenti berlangganan?
- Strategi pemasaran apa yang paling berhasil untuk setiap segmen?

Dengan menganalisis perilaku pelanggan, supermarket dapat mengidentifikasi pola dan mengoptimalkan upaya pemasaran mereka. Segmentasi yang efektif memungkinkan perusahaan mengalokasikan sumber daya secara efisien, dengan fokus pada pelanggan yang bernilai tinggi dan menghindari segmen yang kurang menguntungkan.

## Tujuan
Tujuan utama dari proyek ini adalah mengelompokkan pelanggan berdasarkan karakteristik perilaku pembeliannya. Dengan menggunakan teknik analisis RFM (Recency, Frequency, Monetary) dan K-Means Clustering dengan memanfaatkan nilai RFM dan penambahan feature diskon agar identifikasi perilaku pelanggan dapat lebih mendalam, proyek ini bertujuan untuk:
- Mengidentifikasi dan memprioritaskan segmen pelanggan yang bernilai tinggi.
- Menyoroti segmen pelanggan dengan keterlibatan rendah atau profitabilitas rendah, sehingga memungkinkan untuk mengevaluasi kembali strategi pemasarannya atau mengurangi upaya terhadap segmen yang kurang produktif.
- Mengembangkan wawasan untuk menciptakan kampanye pemasaran yang dipersonalisasi.

Kriteria Keberhasilan
- Identifikasi setiap segmen pelanggan berdasarkan data perilaku pembelian.
- Implementasi kampanye pemasaran yang dipersonalisasi berdasarkan segmen pelanggan meningkatkan keterlibatan pelanggan sebesar 15% selama enam bulan.
- Pengurangan pengeluaran pemasaran yang diarahkan ke segmen pelanggan yang bernilai rendah atau tidak terlibat, meningkatkan laba atas investasi pemasaran (ROMI) sebesar 20%.
- Menurunkan tingkat churn rate di antara nasabah bernilai tinggi melalui strategi retensi yang ditargetkan.

## Data Understanding
Data penjualan superstore dataset dari tahun 2014 hingga tahun 2017, yang berisi kolom berikut:
- Row ID => Unique ID for each row.
- Order ID => Unique Order ID for each Customer.
- Order Date => Order Date of the product.
- Ship Date => Shipping Date of the Product.
- Ship Mode=> Shipping Mode specified by the Customer.
- Customer ID => Unique ID to identify each Customer.
- Customer Name => Name of the Customer.
- Segment => The segment where the Customer belongs.
- Country => Country of residence of the Customer.
- City => City of residence of of the Customer.
- State => State of residence of the Customer.
- Postal Code => Postal Code of every Customer.
- Region => Region where the Customer belong.
- Product ID => Unique ID of the Product.
- Category => Category of the product ordered.
- Sub-Category => Sub-Category of the product ordered.
- Product Name => Name of the Product
- Sales => Sales of the Product.
- Quantity => Quantity of the Product.
- Discount => Discount provided.
- Profit => Profit/Loss incurred.

Sumber data: [Dataset.csv](https://www.kaggle.com/datasets/vivek468/superstore-dataset-final)

## Data Wrangling
- Memastikan tidak terdapat data duplikat dan null values
- Menyesuaikan tipe data
- Mengelompokkan data berdasarkan customer_id
- Menerapkan metode yeo-johnson transformation dan standarisasi untuk mengurangi skewness dan outliers

## Exploratory Data Analysis
- Bagaimana performa dari penjualan saat ini?
  
![Revenue](https://github.com/user-attachments/assets/56bf7d3f-459a-49e3-94cf-d9f4023e825f)

Grafik garis di atas menunjukkan revenue yang dihasilkan dari tahun 2014 hingga 2017 yang mana mengalami peningkatan. Setiap tahunnya memiliki pola yang mirip, dengan lonjakkan setiap bulan April, Oktober, dan Desember.

![Profit](https://github.com/user-attachments/assets/0463ce8f-bbfd-44fd-8a73-587ef89b6596)
Profit terendah terjadi pada bulan februari 2015, dan yang tertinggi pada bulan januari 2017. Namun yang menarik disini, pada bulan-bulan yang revenue nya selalu meningkat setiap tahun tidak selalu memiliki lonjakan profit, mungkin ini dikarenakan kampanye pemasaran yang menerapkan harga diskon. Kemudian pada akhir tahun 2017 memiliki profitabilitas yang lesu meskipun revenue yang dihasilkan meningkat signifikan.

![Categorical Distribution](https://github.com/user-attachments/assets/7c474c46-b3f8-4d66-86ad-4fced7f292fb)

Pelanggan paling banyak adalah pelanggan dengan tipe konsumen (consumer), pelanggan didominasi pelanggan yang berasal dari wilayah timur dan barat. Kemudian produk yang paling banyak terjual adalah kategori produk peralatan kantor (office supplies), sedangkan jenis pengiriman standard adalah jenis pengiriman yang paling banyak digunakan.

## RFM Analysis
Dengan analisis RFM kita dapat mengidentifikasi perilaku pembelian pelanggan dilihat dari metrik berikut:
- Recency = Kapan terakhir kali pelanggan melakukan pembelian.
- Frequency = Seberapa sering pelanggan melakukan pembelian.
- Monetary = Berapa banyak nilai uang yang pelanggan gunakan untuk melakukan pembelian.

Skor RFM ditetapkan dengan rentang nilai 1-5, nilai 1 paling rendah dan 5 paling tinggi, dengan rasio pembobotan:
- 20% dari recency score.
- 30% dari frequency score.
- 50% dari monetary score.

Dari skor RFM yang dihasilkan, kemudian disegmentasikan menjadi 4 segmen:
- Skor RFM 3.76 - 5    ---> Top Customers
- Skor RFM 2.51 - 3.75 ---> High Value Customers
- Skor RFM 1.26 - 2.5  ---> Medium Value Customers
- Skor RFM 0 - 1.25    ---> Low Value Customers

![rfm](https://github.com/user-attachments/assets/dd1ce511-54e3-4646-b5c0-d65434389392)

Berdasarkan rasio diatas, segmen pelanggan paling banyak adalah high value customer. Dari hasil segmentasi tersebut muncul pertanyaan: 'Strategi apa yang dapat dilakukan agar pelanggan pada segmen high value customer bisa berubah menjadi top customer?'

![dist_rfm_num](https://github.com/user-attachments/assets/f93ddb5c-c3c7-4d93-9191-e3c07f582553)

Dari grafik tersebut dapat disimpulkan bahwa semakin tinggi hirarki segmen, semakin tinggi juga nilai diskon yang digunakan. Maka diskon ini mungkin bisa menjadi daya tarik agar pelanggan dapat bertransaki lebih banyak dan lebih sering.

## K-Means Clustering
K-Means Clustering merupakan algoritma unsupervised learning yang dapat digunakan untuk mengelompokkan data tanpa label ke dalam K cluster (jumlah cluster/segmen yang ditentukan) sedemikian rupa berdasarkan karakteristik serupa.

Algoritma K-Means memiliki limitasi sebagai berikut:
- Sangat sensitif terhadap outlier.
- Sangat sensitif terhadap perbedaan skala data.
- Hanya bisa memproses data numerik.

Karena data set yang akan diproses memiliki distribusi yang timpang (skewed) dan terdapat cukup banyak outlier serta memiliki skala yang jauh berbeda, maka kita lakukan transformasi data dengan metode yeo-johnson transformation dan standarisasi menggunakan power transform dari scikit-learn.

### Mencari jumlah cluster yang optimal
Pada algoritma K-Means Clustering kita perlu mencari cluster yang optimal agar dapat menghasilkan segmentasi yang maksimal.
Untuk itu kita gunakan Elbow Method dan Silouette Method.

![Elbow method](https://github.com/user-attachments/assets/891ee3ff-1039-499c-97a1-43851cd3bf53)

Berdasarkan kedua grafik diatas, dilihat dari perubahan nilai inertia yang paling signifikan atau titik number of cluster sebelum perubahan nilai inertia menjadi landai pada grafik elbow method yang mana biasanya membentuk siku/elbow, dan diperkuat dengan grafik silhouette method yang mana semakin tinggi nilai silhouette coeffient-nya maka semakin baik pula pembagian segmen-nya, maka jumlah cluster yang paling optimal adalah 4.

# Interpretasi Hasil Segmentasi
Kita gunakan snake plot untuk memahami perbedaan antar segmennya.

![Snake Plot](https://github.com/user-attachments/assets/54f4d88c-703d-495b-9cdd-96a8e306d6c3)

Distribusi setiap segmen:

![K-means](https://github.com/user-attachments/assets/59382539-992e-464f-b4ea-b910a10473eb)

| Segmen | Label | % | Interpretasi | Actionable Insight |
| --- | --- | --- | --- | --- |
| 0 | Top Customers | 28% | Pelanggan yang sangat loyal, cenderung melakukan transaksi dalam jumlah besar, dan sering memanfaatkan discount, segmen ini yang paling banyak menghasilkan revenue. | Fokus pada peningkatkan pembelian pelanggan, untuk itu penting untuk melakukan strategi cross selling atau up selling. |
| 1 | Medium Value Customers | 25% | Pelanggan yang jarang melakukan transaksi, terakhir melakukan pembelian juga sudah sangat lama, namun menghasilkan revenue yang cukup besar, dan sering memanfaatkan discount. | Segmen ini sangat rentan untuk berhenti berlangganan (churn), maka sebaiknya fokus untuk mengaktivasi mereka agar kembali melakukan pembelian dengan merancang Reactivation Strategy dan Retention Strategy. |
| 2 | High Value Customers | 30% | Pelanggan yang sering melakukan transaksi dan memiliki potensi sangat besar untuk menjadi 'top customers'. Merupakan customer yang melakukan pembelian paling terkini, dan sering melakukan pembelian, cukup banyak menghasilkan revenue, serta jarang menggunakan discount. | Tim bisnis perlu mengoptimasi sumber daya kampanye pemasaran untuk segmen ini untuk menjaga loyalitas dan meningkatkan nilai mereka sehingga dapat berubah menjadi top customer. |
| 3 | Low Value Customers | 16% | Pelanggan yang paling jarang melakukan transaksi, terakhir melakukan pembelian sudah cukup lama dan menghasilkan revenue paling sedikit, serta sangat jarang menggunakan discount. | Ini merupakan segmen bernilai rendah, oleh karena itu lebih baik sumber daya dialokasikan untuk melakukan kampanye pemasaran pada segmen lain. |
