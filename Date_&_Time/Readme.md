Fungsi **Date and Time** dalam DAX memungkinkan kita bekerja dengan tanggal dan waktu untuk melakukan perhitungan seperti menghitung umur, menentukan hari tertentu, atau mengambil bagian spesifik dari suatu tanggal. Mari kita bahas beberapa fungsi Date and Time DAX yang umum dengan bahasa yang sederhana:

### 1. **DATE**  
   Fungsi **DATE** digunakan untuk membuat tanggal baru berdasarkan tahun, bulan, dan hari yang ditentukan. Formatnya adalah `DATE(year, month, day)`.

   **Contoh:**
   Jika kita ingin membuat tanggal 1 Januari 2024, kita bisa menuliskannya seperti ini:

   ```dax
   New Date = DATE(2024, 1, 1)
   ```

### 2. **YEAR, MONTH, DAY**  
   Fungsi ini digunakan untuk mengambil bagian spesifik dari suatu tanggal, yaitu tahun, bulan, atau hari.

   - **YEAR** mengambil tahun dari tanggal tertentu.
   - **MONTH** mengambil bulan dari tanggal tertentu.
   - **DAY** mengambil hari dari tanggal tertentu.

   **Contoh:**
   Misalkan kita punya tanggal `2024-01-15`, dan ingin tahu tahunnya.

   ```dax
   Tahun = YEAR(Dates[Date])
   ```

   Fungsi ini akan mengembalikan `2024`.

### 3. **TODAY** dan **NOW**  
   - **TODAY** mengembalikan tanggal hari ini tanpa jam.
   - **NOW** mengembalikan tanggal dan waktu saat ini (termasuk jam, menit, dan detik).

   **Contoh:**
   Untuk menampilkan tanggal hari ini tanpa jam:

   ```dax
   Hari Ini = TODAY()
   ```

   Untuk menampilkan tanggal dan waktu saat ini:

   ```dax
   Waktu Sekarang = NOW()
   ```

### 4. **DATEDIFF**  
   Fungsi ini menghitung selisih antara dua tanggal dalam unit tertentu (tahun, bulan, hari, dll.).

   **Sintaks:**
   ```dax
   DATEDIFF(Start_Date, End_Date, Interval)
   ```
   
   **Interval** bisa berupa DAY, MONTH, YEAR, dll.

   **Contoh:**
   Misalkan kita ingin tahu berapa hari antara tanggal `2024-01-01` dan `2024-02-01`.

   ```dax
   SelisihHari = DATEDIFF(DATE(2024, 1, 1), DATE(2024, 2, 1), DAY)
   ```

   Fungsi ini akan mengembalikan `31` (jumlah hari).

### 5. **EOMONTH**  
   Fungsi **EOMONTH** digunakan untuk mencari tanggal akhir bulan tertentu, baik di bulan yang sama atau beberapa bulan ke depan/ke belakang.

   **Sintaks:**
   ```dax
   EOMONTH(Start_Date, Months)
   ```

   - **Start_Date**: Tanggal awal
   - **Months**: Jumlah bulan yang ingin digeser (negatif untuk mundur, positif untuk maju)

   **Contoh:**
   Jika kita ingin mencari akhir bulan dua bulan setelah Januari 2024:

   ```dax
   Akhir Bulan = EOMONTH(DATE(2024, 1, 1), 2)
   ```

   Ini akan mengembalikan `2024-03-31`.

### 6. **WEEKDAY**  
   Fungsi **WEEKDAY** mengembalikan angka yang mewakili hari dalam seminggu dari tanggal tertentu (1 untuk Minggu hingga 7 untuk Sabtu, atau format lain sesuai pilihan).

   **Contoh:**
   Untuk mengetahui hari dari tanggal `2024-01-15`:

   ```dax
   HariDalamMinggu = WEEKDAY(DATE(2024, 1, 15))
   ```

   Jika hasilnya `2`, artinya tanggal tersebut adalah hari Senin.

### 7. **WEEKNUM**  
   Fungsi **WEEKNUM** mengembalikan nomor minggu dalam tahun tertentu. Misalnya, jika sebuah tanggal jatuh pada minggu pertama Januari, maka akan mengembalikan angka 1.

   **Contoh:**
   ```dax
   Nomor Minggu = WEEKNUM(DATE(2024, 1, 15))
   ```

   Jika hasilnya `3`, artinya tanggal tersebut berada di minggu ketiga tahun tersebut.

### 8. **HOUR, MINUTE, SECOND**  
   Fungsi-fungsi ini mengambil bagian waktu dari suatu nilai tanggal-waktu.

   - **HOUR** mengambil jam.
   - **MINUTE** mengambil menit.
   - **SECOND** mengambil detik.

   **Contoh:**
   Jika kita punya waktu `12:30:45` dan ingin mengambil menitnya:

   ```dax
   Menit = MINUTE(TIME(12, 30, 45))
   ```

   Ini akan mengembalikan `30`.

### 9. **TIME**  
   Fungsi **TIME** membuat waktu baru berdasarkan jam, menit, dan detik yang kita tentukan.

   **Contoh:**
   Untuk membuat waktu `14:15:00`:

   ```dax
   Jam_Baru = TIME(14, 15, 0)
   ```

### 10. **YEARFRAC**  
   Fungsi **YEARFRAC** menghitung fraksi tahun antara dua tanggal, yang berguna untuk menghitung umur atau masa pakai.

   **Sintaks:**
   ```dax
   YEARFRAC(Start_Date, End_Date)
   ```

   **Contoh:**
   Jika kita ingin menghitung umur seseorang yang lahir pada `2000-01-01` hingga hari ini:

   ```dax
   Umur = YEARFRAC(DATE(2000, 1, 1), TODAY())
   ```

   Fungsi ini akan mengembalikan umur dalam tahun, misalnya `24.8` (jika umur hampir mencapai 25 tahun).

### Kesimpulan:
Fungsi Date and Time dalam DAX ini membantu kita untuk mengolah data tanggal dan waktu. Beberapa fungsi seperti **YEAR**, **MONTH**, **DAY** berguna untuk memisahkan komponen tanggal. Fungsi seperti **TODAY** dan **NOW** memberi kita informasi waktu saat ini. Sementara **DATEDIFF**, **WEEKDAY**, dan **YEARFRAC** membantu kita melakukan perhitungan berdasarkan waktu.

**WEEKDAY** dan **WEEKNUM** adalah dua fungsi DAX yang bekerja dengan data tanggal, tetapi fungsinya berbeda.

### 1. **WEEKDAY**  
   - **WEEKDAY** digunakan untuk mendapatkan **hari dalam seminggu** dari suatu tanggal tertentu. Misalnya, apakah tanggal tersebut jatuh pada hari Senin, Selasa, atau Minggu.
   - **Hasilnya** adalah angka yang mewakili hari dalam seminggu. Default-nya adalah:
     - 1 untuk Minggu
     - 2 untuk Senin
     - dan seterusnya sampai 7 untuk Sabtu.
   - Anda juga dapat mengatur awal minggu pada hari yang berbeda (misalnya, Senin menjadi 1) jika diinginkan.
   
   **Sintaks**:
   ```dax
   WEEKDAY(<Date>, [Return_Type])
   ```
   - **Return_Type** menentukan awal minggu, seperti 1 (Minggu sebagai hari pertama), 2 (Senin sebagai hari pertama), dan lainnya.

   **Contoh**:
   Jika kita ingin tahu hari dalam seminggu untuk tanggal `2024-01-17`:

   ```dax
   HariDalamMinggu = WEEKDAY(DATE(2024, 1, 17))
   ```

   Jika hasilnya `4`, artinya tanggal tersebut adalah hari Rabu.

### 2. **WEEKNUM**  
   - **WEEKNUM** digunakan untuk mendapatkan **nomor minggu dalam tahun** dari suatu tanggal. Misalnya, tanggal tertentu berada di minggu ke berapa dalam satu tahun (1 sampai 52 atau 53 minggu).
   - **Hasilnya** adalah nomor minggu, dimulai dari minggu pertama dalam tahun tersebut.
   - Mirip dengan WEEKDAY, Anda juga bisa menentukan apakah minggu pertama dalam tahun dimulai pada 1 Januari atau Senin pertama dalam tahun.

   **Sintaks**:
   ```dax
   WEEKNUM(<Date>, [Return_Type])
   ```
   - **Return_Type** mengatur awal minggu, misalnya 1 (Minggu sebagai awal minggu), atau 2 (Senin sebagai awal minggu).

   **Contoh**:
   Jika kita ingin tahu minggu ke berapa dari tanggal `2024-01-17`:

   ```dax
   NomorMinggu = WEEKNUM(DATE(2024, 1, 17))
   ```

   Jika hasilnya `3`, artinya tanggal tersebut berada di minggu ketiga tahun 2024.

### Perbedaan Utama:

| Fungsi       | Tujuan                                      | Hasil                                           |
|--------------|--------------------------------------------|-------------------------------------------------|
| **WEEKDAY**  | Menunjukkan hari dalam seminggu (Senin, dll.) | Angka hari dalam seminggu (1 untuk Minggu, 2 untuk Senin, dst.) |
| **WEEKNUM**  | Menunjukkan nomor minggu dalam tahun        | Angka minggu dalam tahun (1-52 atau 1-53)       |

Jadi, **WEEKDAY** memberitahu hari apa dalam minggu, sedangkan **WEEKNUM** memberitahu minggu ke berapa dalam tahun.
