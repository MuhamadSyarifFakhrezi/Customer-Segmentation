# Customer-Segmentation
## Business Understanding
Superstore berusaha untuk mengidentifikasi segmen pelanggan mana yang harus diprioritaskan dalam upaya pemasaran mereka dan mana yang harus dihindari agar dapat meningkatkan profitabilitas mereka. Perusahaan membutuhkan wawasan berbasis data untuk menjawab pertanyaan berikut:
- Segmen pelanggan mana yang paling menguntungkan?
- Segmen pelanggan mana yang berisiko mengalami perputaran?
- Strategi pemasaran apa yang paling berhasil untuk setiap segmen?

Dengan menganalisis perilaku pelanggan, supermarket dapat mengidentifikasi pola yang berharga dan mengoptimalkan upaya pemasaran mereka. Segmentasi yang efektif memungkinkan perusahaan mengalokasikan sumber daya secara efisien, dengan fokus pada pelanggan yang bernilai tinggi dan menghindari segmen yang kurang menguntungkan.

## Tujuan
Tujuan utama dari proyek ini adalah mengelompokkan pelanggan berdasarkan karakteristik perilaku pembeliannya. Dengan menggunakan teknik seperti analisis RFM (Recency, Frequency, Monetary) dan K-Means Clustering, ini bertujuan untuk:
- Mengidentifikasi dan memprioritaskan segmen pelanggan yang bernilai tinggi.
- Menyoroti segmen pelanggan dengan keterlibatan rendah atau profitabilitas rendah, sehingga memungkinkan toko untuk mengevaluasi kembali strategi pemasarannya atau mengurangi upaya terhadap segmen yang kurang produktif.
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
