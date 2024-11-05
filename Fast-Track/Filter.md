Berikut penjelasan yang lebih lengkap dan mendalam mengenai setiap fungsi filter DAX di [DAX Guide](https://dax.guide/functions/filter/). Fungsi-fungsi ini sangat penting dalam DAX untuk menyaring data, mengatur filter, dan menentukan nilai tertentu berdasarkan konteks laporan atau tabel.

---

### 1. **ALL**
   - **Deskripsi**: Menghapus semua filter dari tabel atau kolom tertentu yang disebutkan, mengembalikan seluruh data dalam tabel atau kolom tanpa filter.
   - **Sintaks**:
     ```dax
     ALL(<Table> / <Column>)
     ```
   - **Contoh**:
     ```dax
     TotalSalesAllProducts = CALCULATE(SUM(Sales[SalesAmount]), ALL(Sales[ProductID]))
     ```
   - **Kegunaan**: Digunakan untuk menghitung total nilai tanpa terpengaruh oleh filter yang sedang aktif, seperti menghitung total penjualan dari semua produk meskipun filter produk tertentu diterapkan di visualisasi atau laporan.

---

### 2. **ALLEXCEPT**
   - **Deskripsi**: Menghapus semua filter pada tabel kecuali kolom tertentu. Fungsinya serupa dengan `ALL` namun lebih fleksibel karena mempertahankan filter pada kolom tertentu.
   - **Sintaks**:
     ```dax
     ALLEXCEPT(<Table>, <Column1>, <Column2>, ...)
     ```
   - **Contoh**:
     ```dax
     SalesExceptDate = CALCULATE(SUM(Sales[SalesAmount]), ALLEXCEPT(Sales, Sales[Date]))
     ```
   - **Kegunaan**: Berguna ketika Anda ingin menghapus semua filter dari tabel kecuali satu atau beberapa kolom tertentu. Misalnya, Anda mungkin hanya ingin menghitung total penjualan untuk semua produk dalam tanggal tertentu.

---

### 3. **ALLNOBLANKROW**
   - **Deskripsi**: Menghapus semua filter, seperti `ALL`, tetapi tidak memasukkan baris kosong dalam hasil. Berguna untuk menganalisis data tanpa nilai kosong (blank).
   - **Sintaks**:
     ```dax
     ALLNOBLANKROW(<Table> / <Column>)
     ```
   - **Contoh**:
     ```dax
     TotalSalesNoBlank = CALCULATE(SUM(Sales[SalesAmount]), ALLNOBLANKROW(Sales))
     ```
   - **Kegunaan**: Berguna untuk mendapatkan hasil tanpa data kosong, cocok untuk menganalisis data bersih.

---

### 4. **ALLSELECTED**
   - **Deskripsi**: Menghapus semua filter pada tabel atau kolom yang telah dipilih dalam konteks visualisasi. Namun, tetap mempertahankan filter luar (external filters) yang mungkin diterapkan di luar visualisasi.
   - **Sintaks**:
     ```dax
     ALLSELECTED(<Table> / <Column>)
     ```
   - **Contoh**:
     ```dax
     TotalSalesSelectedProducts = CALCULATE(SUM(Sales[SalesAmount]), ALLSELECTED(Sales[ProductID]))
     ```
   - **Kegunaan**: Cocok untuk menghitung total dalam konteks visualisasi dengan mempertahankan filter di luar visualisasi.

---

### 5. **CROSSFILTER**
   - **Deskripsi**: Mengatur arah filter di antara dua tabel yang memiliki hubungan. Fungsi ini dapat membatasi atau memperluas arah filter untuk memungkinkan analisis yang lebih fleksibel.
   - **Sintaks**:
     ```dax
     CROSSFILTER(<Column1>, <Column2>, <Direction>)
     ```
   - **Contoh**:
     ```dax
     TotalSalesWithCrossFilter = CALCULATE(SUM(Sales[SalesAmount]), CROSSFILTER(Sales[ProductID], Product[ProductID], BOTH))
     ```
   - **Kegunaan**: Berguna untuk mengontrol bagaimana dua tabel mempengaruhi satu sama lain dalam perhitungan, terutama jika tabel memiliki hubungan dua arah.

---

### 6. **FILTER**
   - **Deskripsi**: Mengaplikasikan filter untuk menyaring data dalam tabel berdasarkan kondisi tertentu, mengembalikan baris yang memenuhi kondisi tersebut.
   - **Sintaks**:
     ```dax
     FILTER(<Table>, <Condition>)
     ```
   - **Contoh**:
     ```dax
     HighSalesOnly = FILTER(Sales, Sales[SalesAmount] > 1000)
     ```
   - **Kegunaan**: Untuk memilih baris spesifik dari tabel berdasarkan kondisi. Misalnya, hanya menampilkan transaksi dengan nilai penjualan di atas 1000.

---

### 7. **HASONEFILTER**
   - **Deskripsi**: Mengecek apakah kolom tertentu hanya memiliki satu nilai yang difilter. Berguna untuk validasi atau kondisi logika jika satu nilai aktif dalam filter.
   - **Sintaks**:
     ```dax
     HASONEFILTER(<Column>)
     ```
   - **Contoh**:
     ```dax
     HasOneProductFilter = IF(HASONEFILTER(Sales[ProductID]), "Single Product", "Multiple Products")
     ```
   - **Kegunaan**: Berguna dalam memastikan hanya satu produk yang difilter atau aktif dalam visualisasi atau perhitungan.

---

### 8. **HASONEVALUE**
   - **Deskripsi**: Mengecek apakah kolom hanya mengandung satu nilai unik dalam konteks filter. Fungsinya mirip dengan HASONEFILTER, namun hanya memeriksa nilai unik.
   - **Sintaks**:
     ```dax
     HASONEVALUE(<Column>)
     ```
   - **Contoh**:
     ```dax
     HasOneCategoryValue = IF(HASONEVALUE(Product[Category]), "One Category", "Multiple Categories")
     ```
   - **Kegunaan**: Cocok untuk kondisi logika dan validasi bahwa hanya ada satu nilai unik dalam filter.

---

### 9. **KEEPFILTERS**
   - **Deskripsi**: Menjaga filter yang diterapkan pada kolom tertentu meskipun fungsi CALCULATE akan mencoba menghapus filter pada kolom tersebut.
   - **Sintaks**:
     ```dax
     KEEPFILTERS(<Expression>)
     ```
   - **Contoh**:
     ```dax
     SalesWithFilter = CALCULATE(SUM(Sales[SalesAmount]), KEEPFILTERS(Sales[ProductID] = "A"))
     ```
   - **Kegunaan**: Mengunci filter agar tidak diabaikan oleh CALCULATE, meskipun CALCULATE umumnya menghapus filter kolom.

---

### 10. **REMOVEFILTERS**
   - **Deskripsi**: Menghapus semua filter dari kolom atau tabel tertentu tanpa mempengaruhi filter lainnya.
   - **Sintaks**:
     ```dax
     REMOVEFILTERS(<Table> / <Column>)
     ```
   - **Contoh**:
     ```dax
     TotalSalesNoFilter = CALCULATE(SUM(Sales[SalesAmount]), REMOVEFILTERS(Sales[ProductID]))
     ```
   - **Kegunaan**: Berguna saat ingin menonaktifkan filter pada kolom tertentu dalam perhitungan.

---

### 11. **SELECTEDVALUE**
   - **Deskripsi**: Mengambil nilai tunggal dari kolom yang difilter atau mengembalikan nilai alternatif jika lebih dari satu atau tidak ada nilai yang dipilih.
   - **Sintaks**:
     ```dax
     SELECTEDVALUE(<Column>, <AlternateResult>)
     ```
   - **Contoh**:
     ```dax
     SelectedProduct = SELECTEDVALUE(Sales[ProductID], "No Product Selected")
     ```
   - **Kegunaan**: Memastikan ada satu nilai yang aktif atau memberikan nilai default.

---

### 12. **USERELATIONSHIP**
   - **Deskripsi**: Mengaktifkan hubungan khusus di antara tabel yang memiliki lebih dari satu hubungan (menggunakan hubungan tidak aktif).
   - **Sintaks**:
     ```dax
     USERELATIONSHIP(<Column1>, <Column2>)
     ```
   - **Contoh**:
     ```dax
     SalesByInactiveRelationship = CALCULATE(SUM(Sales[SalesAmount]), USERELATIONSHIP(Sales[Date], Calendar[SpecialDate]))
     ```
   - **Kegunaan**: Untuk memilih hubungan alternatif atau yang tidak aktif dalam perhitungan.

---

### 13. **VALUES**
   - **Deskripsi**: Mengembalikan nilai unik dalam kolom berdasarkan filter yang diterapkan, menghasilkan kolom atau tabel dari nilai unik yang aktif dalam konteks.
   - **Sintaks**:
     ```dax
     VALUES(<Column>)
     ```
   - **Contoh**:
     ```dax
     ProductList = VALUES(Sales[ProductID])
     ```
   - **Kegunaan**: Berguna untuk membuat daftar nilai unik dari filter aktif.

---

### 14. **EARLIER**
   - **Deskripsi**: Mengambil nilai dari baris sebelumnya dalam konteks row-level calculation. Biasanya digunakan dalam perhitungan yang membutuhkan konteks iterasi.
   - **Sintaks**:
     ```dax
     EARLIER(<Column>)
     ```
   - **Contoh**:
     ```dax
     Rank = CALCULATE(COUNTROWS(Sales), Sales[SalesAmount] > EARLIER(Sales[SalesAmount]))
     ```
   - **Kegunaan**: Berguna untuk perhitungan dalam konteks row-by-row yang perlu merujuk pada nilai sebelumnya atau konteks iteratif.

---

### Kesimpulan

Dengan menggunakan fungsi filter DAX ini, Anda bisa memodifikasi dan
