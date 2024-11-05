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

8. **OPENINGBALANCEYEAR, CLOSINGBALANCEYEAR**  
   Fungsi **OPENINGBALANCEYEAR** mencari nilai pertama di awal tahun, sementara **CLOSINGBALANCEYEAR** mencari nilai terakhir di akhir tahun. Fungsi ini sering digunakan untuk menghitung saldo pembukaan atau penutupan.

   **Contoh:**
   ```dax
   Opening Balance = OPENINGBALANCEYEAR(SUM(Sales[SalesAmount]), Dates[Date])
   ```

9. **DATEADD VS PARALLELPERIOD**  
   Keduanya mirip dalam menggeser waktu, tetapi **DATEADD** lebih fleksibel karena bisa menggeser dalam hitungan hari, sedangkan **PARALLELPERIOD** hanya bisa menggeser dalam hitungan bulan, kuartal, atau tahun.

