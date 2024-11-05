Berikut adalah penjelasan lengkap untuk setiap fungsi agregasi DAX dari situs DAX Guide, dengan bahasa yang sederhana. Fungsi agregasi ini umumnya digunakan dalam perhitungan dasar, seperti menghitung total, rata-rata, atau nilai tertinggi dan terendah dari sekumpulan data di tabel Power BI atau Excel.

---

### 1. **APPROXIMATEDISTINCTCOUNT**
   - **Deskripsi**: Menghitung jumlah nilai unik dalam sebuah kolom tetapi menggunakan estimasi. Fungsi ini berguna untuk data sangat besar karena menghitung lebih cepat.
   - **Sintaks**:
     ```dax
     APPROXIMATEDISTINCTCOUNT(<Column>)
     ```
   - **Contoh**:
     ```dax
     EstUniqueCustomers = APPROXIMATEDISTINCTCOUNT(Sales[CustomerID])
     ```
   - **Catatan**: Hasilnya tidak selalu akurat, tetapi lebih cepat daripada **DISTINCTCOUNT**.

---

### 2. **AVERAGE**
   - **Deskripsi**: Menghitung rata-rata nilai dari semua angka dalam satu kolom.
   - **Sintaks**:
     ```dax
     AVERAGE(<Column>)
     ```
   - **Contoh**:
     ```dax
     AvgSalesAmount = AVERAGE(Sales[SalesAmount])
     ```
   - **Kegunaan**: Berguna untuk menghitung rata-rata penjualan, pengeluaran, atau metrik lain dalam dataset Anda.

---

### 3. **AVERAGEX**
   - **Deskripsi**: Menghitung rata-rata dari ekspresi yang dihitung pada setiap baris dalam tabel.
   - **Sintaks**:
     ```dax
     AVERAGEX(<Table>, <Expression>)
     ```
   - **Contoh**:
     ```dax
     AvgRevenuePerOrder = AVERAGEX(Sales, Sales[Quantity] * Sales[UnitPrice])
     ```
   - **Kegunaan**: Berguna jika ingin menghitung rata-rata dari suatu kalkulasi tertentu (misalnya rata-rata pendapatan per transaksi).

---

### 4. **COUNT**
   - **Deskripsi**: Menghitung jumlah baris dalam kolom yang berisi angka (tidak menghitung nilai teks atau kosong).
   - **Sintaks**:
     ```dax
     COUNT(<Column>)
     ```
   - **Contoh**:
     ```dax
     CountTransactions = COUNT(Sales[SalesAmount])
     ```

---

### 5. **COUNTA**
   - **Deskripsi**: Menghitung jumlah baris yang tidak kosong di sebuah kolom, termasuk nilai teks.
   - **Sintaks**:
     ```dax
     COUNTA(<Column>)
     ```
   - **Contoh**:
     ```dax
     CountAllEntries = COUNTA(Sales[ProductID])
     ```
   - **Kegunaan**: Menghitung jumlah entri yang berisi data, baik teks maupun angka.

---

### 6. **COUNTAX**
   - **Deskripsi**: Menghitung jumlah baris dalam tabel setelah menghitung ekspresi tertentu untuk setiap baris.
   - **Sintaks**:
     ```dax
     COUNTAX(<Table>, <Expression>)
     ```
   - **Contoh**:
     ```dax
     CountOrdersAbove100 = COUNTAX(Sales, IF(Sales[SalesAmount] > 100, 1, BLANK()))
     ```
   - **Kegunaan**: Digunakan saat ingin menghitung berdasarkan kondisi tertentu.

---

### 7. **COUNTBLANK**
   - **Deskripsi**: Menghitung jumlah baris kosong di kolom tertentu.
   - **Sintaks**:
     ```dax
     COUNTBLANK(<Column>)
     ```
   - **Contoh**:
     ```dax
     BlankEntries = COUNTBLANK(Sales[Comments])
     ```

---

### 8. **COUNTROWS**
   - **Deskripsi**: Menghitung total baris dalam tabel, baik ada nilainya maupun kosong.
   - **Sintaks**:
     ```dax
     COUNTROWS(<Table>)
     ```
   - **Contoh**:
     ```dax
     TotalRows = COUNTROWS(Sales)
     ```
   - **Kegunaan**: Berguna untuk mengetahui jumlah total baris dalam tabel, termasuk baris kosong.

---

### 9. **DISTINCTCOUNT**
   - **Deskripsi**: Menghitung jumlah nilai unik dalam kolom tertentu.
   - **Sintaks**:
     ```dax
     DISTINCTCOUNT(<Column>)
     ```
   - **Contoh**:
     ```dax
     UniqueCustomers = DISTINCTCOUNT(Sales[CustomerID])
     ```

---

### 10. **MAX**
   - **Deskripsi**: Mengambil nilai terbesar dari kolom angka.
   - **Sintaks**:
     ```dax
     MAX(<Column>)
     ```
   - **Contoh**:
     ```dax
     MaxSales = MAX(Sales[SalesAmount])
     ```

---

### 11. **MAXA**
   - **Deskripsi**: Mengambil nilai terbesar dari kolom, termasuk teks dan angka. Jika ada teks, dianggap 0.
   - **Sintaks**:
     ```dax
     MAXA(<Column>)
     ```
   - **Contoh**:
     ```dax
     MaxValue = MAXA(Data[Value])
     ```
   - **Kegunaan**: Menyertakan teks dalam perhitungan (teks dianggap 0).

---

### 12. **MAXX**
   - **Deskripsi**: Menghitung nilai maksimum dari ekspresi tertentu untuk setiap baris dalam tabel.
   - **Sintaks**:
     ```dax
     MAXX(<Table>, <Expression>)
     ```
   - **Contoh**:
     ```dax
     MaxRevenuePerOrder = MAXX(Sales, Sales[Quantity] * Sales[UnitPrice])
     ```

---

### 13. **MIN**
   - **Deskripsi**: Mengambil nilai terkecil dalam kolom angka.
   - **Sintaks**:
     ```dax
     MIN(<Column>)
     ```
   - **Contoh**:
     ```dax
     MinSales = MIN(Sales[SalesAmount])
     ```

---

### 14. **MINA**
   - **Deskripsi**: Mengambil nilai terkecil dalam kolom, termasuk teks dan angka (teks dianggap 0).
   - **Sintaks**:
     ```dax
     MINA(<Column>)
     ```
   - **Contoh**:
     ```dax
     MinValue = MINA(Data[Value])
     ```

---

### 15. **MINX**
   - **Deskripsi**: Menghitung nilai minimum dari ekspresi tertentu untuk setiap baris dalam tabel.
   - **Sintaks**:
     ```dax
     MINX(<Table>, <Expression>)
     ```
   - **Contoh**:
     ```dax
     MinRevenuePerOrder = MINX(Sales, Sales[Quantity] * Sales[UnitPrice])
     ```

---

### 16. **PRODUCT**
   - **Deskripsi**: Mengalikan semua nilai dalam kolom angka.
   - **Sintaks**:
     ```dax
     PRODUCT(<Column>)
     ```
   - **Contoh**:
     ```dax
     ProductOfSales = PRODUCT(Sales[SalesAmount])
     ```

---

### 17. **PRODUCTX**
   - **Deskripsi**: Mengalikan hasil ekspresi yang dihitung pada setiap baris dalam tabel.
   - **Sintaks**:
     ```dax
     PRODUCTX(<Table>, <Expression>)
     ```
   - **Contoh**:
     ```dax
     TotalProduct = PRODUCTX(Sales, Sales[Quantity] * Sales[UnitPrice])
     ```

---

### 18. **SUM**
   - **Deskripsi**: Menjumlahkan semua angka dalam satu kolom.
   - **Sintaks**:
     ```dax
     SUM(<Column>)
     ```
   - **Contoh**:
     ```dax
     TotalSales = SUM(Sales[SalesAmount])
     ```

---

### 19. **SUMX**
   - **Deskripsi**: Menjumlahkan hasil ekspresi yang dihitung pada setiap baris dalam tabel.
   - **Sintaks**:
     ```dax
     SUMX(<Table>, <Expression>)
     ```
   - **Contoh**:
     ```dax
     TotalRevenue = SUMX(Sales, Sales[Quantity] * Sales[UnitPrice])
     ```

---

### Kesimpulan

Fungsi agregasi DAX ini membantu Anda melakukan berbagai perhitungan pada data, mulai dari penjumlahan, rata-rata, hingga nilai unik dan minimum/maksimum. Beberapa fungsi seperti **SUMX** dan **AVERAGEX** memungkinkan perhitungan baris per baris, sedangkan fungsi seperti **MAX** dan **MIN** memberikan nilai tunggal tertinggi atau terendah dari seluruh kolom.
