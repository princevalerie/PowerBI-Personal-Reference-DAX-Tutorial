Time intelligence dalam DAX (Data Analysis Expressions) di Power BI dan alat Microsoft lainnya adalah sekelompok fungsi yang memudahkan analisis data seiring waktu, seperti melihat data per bulan, per tahun, atau menghitung pertumbuhan dari satu periode ke periode lainnya. DAX memiliki fungsi khusus untuk membuat perhitungan ini tanpa perlu menulis rumus yang rumit. Mari kita jelaskan beberapa fungsi time intelligence yang paling umum dalam bahasa sederhana:

1. **TOTALYTD, TOTALQTD, TOTALMTD**  
   Fungsi ini menghitung total akumulatif dari awal tahun, kuartal, atau bulan hingga titik tertentu.

   - **TOTALYTD** menghitung total dari awal tahun hingga tanggal tertentu. Misalnya, jika kita ingin melihat total penjualan dari Januari hingga Agustus.
   - **TOTALQTD** menghitung total dari awal kuartal hingga tanggal tertentu, misalnya dari awal kuartal (Januari-Maret) hingga akhir Februari.
   - **TOTALMTD** menghitung total dari awal bulan hingga tanggal tertentu, misalnya dari awal Maret hingga tanggal 15 Maret.

   **Contoh:** 
   ```dax
   Total Sales YTD = TOTALYTD(SUM(Sales[SalesAmount]), Dates[Date])
   ```

2. **SAMEPERIODLASTYEAR**  
   Fungsi ini mengambil periode yang sama di tahun sebelumnya. Ini berguna untuk membandingkan angka tahun ini dengan angka di periode yang sama tahun lalu. Jika kita sedang menganalisis penjualan di Januari 2024, kita bisa menggunakan fungsi ini untuk melihat data di Januari 2023.

   **Contoh:**
   ```dax
   Sales LY = CALCULATE(SUM(Sales[SalesAmount]), SAMEPERIODLASTYEAR(Dates[Date]))
   ```

3. **PREVIOUSYEAR, PREVIOUSQUARTER, PREVIOUSMONTH**  
   Fungsi-fungsi ini mengambil nilai dari tahun, kuartal, atau bulan sebelumnya. Misalnya, jika kita menganalisis penjualan di Februari 2024, kita bisa gunakan fungsi **PREVIOUSMONTH** untuk melihat data Januari 2024.

   **Contoh:**
   ```dax
   Sales Last Month = CALCULATE(SUM(Sales[SalesAmount]), PREVIOUSMONTH(Dates[Date]))
   ```

4. **DATEADD**  
   DATEADD menggeser tanggal dengan menambah atau mengurangi waktu tertentu (hari, bulan, kuartal, atau tahun). Misalnya, kita bisa melihat penjualan dua bulan yang lalu dari tanggal saat ini.

   **Contoh:**
   ```dax
   Sales 2 Months Ago = CALCULATE(SUM(Sales[SalesAmount]), DATEADD(Dates[Date], -2, MONTH))
   ```

5. **PARALLELPERIOD**  
   Fungsi ini mirip dengan DATEADD tetapi hanya mendukung pergeseran waktu dalam satuan bulan, kuartal, atau tahun. Misalnya, kita bisa gunakan **PARALLELPERIOD** untuk melihat penjualan tiga bulan sebelumnya atau satu kuartal ke belakang.

   **Contoh:**
   ```dax
   Sales 3 Months Ago = CALCULATE(SUM(Sales[SalesAmount]), PARALLELPERIOD(Dates[Date], -3, MONTH))
   ```

6. **FIRSTDATE, LASTDATE**  
   Fungsi **FIRSTDATE** dan **LASTDATE** berguna untuk menemukan tanggal pertama atau terakhir dalam periode tertentu. Misalnya, kita bisa mengetahui kapan penjualan pertama kali terjadi di suatu bulan.

   **Contoh:**
   ```dax
   First Sale Date = FIRSTDATE(Sales[SaleDate])
   ```

7. **DATESYTD, DATESQTD, DATESMTD**  
   Ketiga fungsi ini menghasilkan rangkaian tanggal dari awal tahun, kuartal, atau bulan hingga tanggal tertentu. Sering digunakan sebagai filter dalam perhitungan YTD, QTD, dan MTD.

   **Contoh:**
   ```dax
   Sales YTD = CALCULATE(SUM(Sales[SalesAmount]), DATESYTD(Dates[Date]))
   ```

   Contoh dengan Tahun Fiskal Berakhir pada Tanggal Khusus
Jika perusahaan Anda memiliki tahun fiskal yang berakhir pada 31 Maret, maka kita bisa menetapkan Year_End_Date menjadi 31-03.

   ```
   YTD Sales Fiscal = CALCULATE(SUM(Sales[SalesAmount]), DATESYTD(Sales[Date], "31-03"))
   ```
Dalam contoh ini, DATESYTD akan menghasilkan rangkaian tanggal dari awal tahun fiskal (1 April tahun sebelumnya) hingga tanggal tertentu dalam tahun fiskal yang sama.

8. **OPENINGBALANCEYEAR, CLOSINGBALANCEYEAR**  
   Fungsi **OPENINGBALANCEYEAR** mencari nilai pertama di awal tahun, sementara **CLOSINGBALANCEYEAR** mencari nilai terakhir di akhir tahun. Fungsi ini sering digunakan untuk menghitung saldo pembukaan atau penutupan.

   **Contoh:**
   ```dax
   Opening Balance = OPENINGBALANCEYEAR(SUM(Sales[SalesAmount]), Dates[Date])
   ```

9. **DATEADD VS PARALLELPERIOD**  
   Keduanya mirip dalam menggeser waktu, tetapi **DATEADD** lebih fleksibel karena bisa menggeser dalam hitungan hari, sedangkan **PARALLELPERIOD** hanya bisa menggeser dalam hitungan bulan, kuartal, atau tahun.


Mari kita bahas perbedaan antara **DATESBETWEEN** dan **DATESINPERIOD**, serta **DATEADD** dan **PARALLELPERIOD** dalam DAX, disertai dengan contoh-contoh yang mudah dipahami.

### 1. **DATESBETWEEN vs. DATESINPERIOD**

- **DATESBETWEEN**: Fungsi ini menghasilkan satu rangkaian tanggal dalam periode tertentu, mulai dari tanggal awal (start date) hingga tanggal akhir (end date) yang ditentukan. DATESBETWEEN sangat berguna untuk menetapkan periode waktu secara eksplisit, misalnya, dari tanggal 1 Januari hingga 31 Maret.

  **Sintaks:**
  ```dax
  DATESBETWEEN(<Date_Column>, <Start_Date>, <End_Date>)
  ```

  **Contoh Penggunaan:**
  Misalkan kita ingin menghitung total penjualan dari tanggal 1 Januari hingga 31 Maret.

  ```dax
  Sales Jan-Mar = CALCULATE(SUM(Sales[SalesAmount]), DATESBETWEEN(Dates[Date], DATE(2024, 1, 1), DATE(2024, 3, 31)))
  ```

- **DATESINPERIOD**: Fungsi ini juga menghasilkan rangkaian tanggal, tetapi berdasarkan periode relatif. Artinya, kita menentukan titik awal (anchor date) dan durasi (jumlah hari, bulan, kuartal, atau tahun), lalu fungsi ini menghitung periode dari titik awal tersebut ke belakang atau ke depan.

  **Sintaks:**
  ```dax
  DATESINPERIOD(<Date_Column>, <Anchor_Date>, <Number>, <Interval>)
  ```

  **Contoh Penggunaan:**
  Misalkan kita ingin melihat total penjualan dalam tiga bulan terakhir dari tanggal 31 Maret.

  ```dax
  Sales Last 3 Months = CALCULATE(SUM(Sales[SalesAmount]), DATESINPERIOD(Dates[Date], DATE(2024, 3, 31), -3, MONTH))
  ```

#### Perbedaan Utama:
- **DATESBETWEEN** menggunakan rentang tanggal yang spesifik dari awal hingga akhir tanggal yang ditentukan.
- **DATESINPERIOD** menggunakan titik awal dan bergerak ke depan atau ke belakang selama durasi tertentu (misalnya, 3 bulan ke belakang atau 2 tahun ke depan).

---

### 2. **DATEADD vs. PARALLELPERIOD**

- **DATEADD**: Fungsi ini menggeser tanggal berdasarkan interval waktu yang fleksibel (hari, bulan, kuartal, atau tahun). Fungsi ini bisa menggeser ke depan atau ke belakang selama jangka waktu tertentu, yang cocok untuk analisis tren jangka pendek atau jangka panjang.

  **Sintaks:**
  ```dax
  DATEADD(<Date_Column>, <Number_of_Intervals>, <Interval>)
  ```

  **Contoh Penggunaan:**
  Misalkan kita ingin melihat penjualan dua bulan sebelumnya dari setiap tanggal dalam tabel.

  ```dax
  Sales 2 Months Ago = CALCULATE(SUM(Sales[SalesAmount]), DATEADD(Dates[Date], -2, MONTH))
  ```

- **PARALLELPERIOD**: Mirip dengan DATEADD, tetapi hanya bisa menggeser dalam unit bulan, kuartal, atau tahun (tidak bisa dalam hitungan hari). Fungsi ini lebih sering digunakan untuk analisis periode yang setara atau paralel, seperti melihat penjualan kuartal sebelumnya atau tahun lalu.

  **Sintaks:**
  ```dax
  PARALLELPERIOD(<Date_Column>, <Number_of_Periods>, <Interval>)
  ```

  **Contoh Penggunaan:**
  Misalkan kita ingin menghitung penjualan dari kuartal yang sama tahun lalu.

  ```dax
  Sales Last Quarter = CALCULATE(SUM(Sales[SalesAmount]), PARALLELPERIOD(Dates[Date], -1, QUARTER))
  ```

#### Perbedaan Utama:
- **DATEADD** lebih fleksibel karena mendukung pergeseran dalam hari, selain bulan, kuartal, dan tahun.
- **PARALLELPERIOD** digunakan hanya untuk pergeseran dalam bulan, kuartal, atau tahun, yang cocok untuk analisis periode paralel atau musiman.

---

### Kesimpulan:

- **DATESBETWEEN** berguna saat kita tahu rentang tanggal yang spesifik.
- **DATESINPERIOD** berguna saat kita ingin bergerak relatif dari titik awal dengan durasi tertentu.
  
- **DATEADD** memberikan fleksibilitas karena mendukung pergeseran dalam satuan hari, bulan, kuartal, dan tahun.
- **PARALLELPERIOD** lebih tepat untuk analisis paralel, namun hanya bekerja pada bulan, kuartal, dan tahun, sehingga tidak mendukung pergeseran hari.



