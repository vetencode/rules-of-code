# Rules of Code

## 1. Database
- Kolom Primary Key harus bernama 'id'.
- Kolom Foreign Key disarankan memiliki nama yang sama dengan nama tabel yang berelasi. Gunakan entitas yang berelasi jika perlu (contoh: berelasi ke tabel users, namun karena di tabel users ada banyak akses seperti pegawai, maka bisa menggunakan pegawai_id).
- Gunakan softDelete pada setiap tabel yang membutuhkan data historis. Disarankan menggunakan softDelete di semua tabel.
- Ketentuan penamaan kolom harus disesuaikan, namun sangat disarankan untuk tetap konsisten. Jika menggunakan bahasa Inggris, gunakan bahasa Inggris secara konsisten.
- Penamaan kolom timestamps dan softdelete umumnya menggunakan:
  - created_by, created_date, updated_by, updated_date, deleted_by
  Untuk Codeigniter3, sangat direkomendasikan menggunakan kolom timestamp bawaan Laravel. Atau penamaan dapat disesuaikan, namun yang terpenting adalah konsistensi untuk seluruh tabel yang menggunakan timestamps dan softdelete.

## 2. Modul (Codeigniter 3)
- Buat modul yang sesuai dengan fiturnya, dengan nama yang sesuai.
- Jika memungkinkan untuk menggabungkan modul, silakan digabungkan. Contoh, modul report dapat menyatukan report A, report B, dll. Dalam hal ini, dapat disatukan dengan nama modul report. Kemudian buat controller, model, dan folder views masing-masing untuk setiap report.

## 3. Routes
- Gunakan penamaan route yang konsisten dan mudah dimengerti oleh pengembang lain.
- Untuk route/endpoint API, sangat disarankan mengikuti arsitektur Restful API dengan membuat endpoint berupa nomina (kata benda). Contoh: https://ourdomain.com/api/products
- Manfaatkan setiap metode HTTP untuk satu endpoint:
  - Get /products => Mengembalikan daftar semua produk.
  - Get /products/{id} => Mengembalikan detail satu produk secara spesifik.
  - Post /products => Endpoint untuk menyisipkan data produk baru.
  - Patch products/{id} => Memperbarui produk tertentu secara sederhana, misalnya hanya mengubah satu kolom status.
  - Put /products/{id} => Untuk memperbarui data secara massal dari satu baris di database, seperti nama, harga, dan kolom lainnya.
  - Delete /products/{id} => Untuk menghapus produk tertentu.
- **Catatan:** Karena metode Put, Patch, Delete menggunakan Http Method Spoofing, terkadang data tidak terkirim dengan benar. Teknis penanganannya adalah dengan menyertakan header: 'X-HTTP-Method-Override: Put/Patch/Delete' dalam setiap request masing-masing. Namun, jika dianggap merepotkan dan berisiko terutama untuk metode Put, bisa diganti dengan metode Post.

## 4. Views
- Kelompokkan dalam folder yang sesuai.
- Gunakan templating untuk views yang memiliki struktur yang sama (header, navbar, footer, dll.).
- Minimalisir proses komputasi yang kompleks di views.
- Beri nama class dan id untuk form, tombol, modal, dan elemen lain secara konsisten untuk setiap views guna mengurangi kebingungan.

## 5. Javascript and jQuery
- Sangat disarankan untuk menulis file js pada file.js yang terpisah dan dipanggil melalui asset (tidak disatukan dengan file views) untuk optimalisasi proses caching dan meminimalkan jumlah request.

## 6. Gunakan vendor plugin yang konsisten dan sesuai kebutuhan.

## 7. Helpers
- Klasifikasikan fungsi dari helper untuk manipulasi data seperti apa (contoh: date_helper.php, number_helper.php, formatter_helper.php, generator_helper.php).
- Pastikan helper yang dibuat belum ada sebelumnya. Jika sudah ada, gunakan yang ada. Jika ada, namun kurang maksimal, dapat dimaksimalkan dengan syarat tidak menimbulkan error. Jika perlu, buat helper baru.
- Hati-hati saat mengubah file helper yang digunakan secara global untuk menghindari konflik saat merge ke main branch project.

## 8. Libraries
- Buat libraries sesuai dengan kebutuhan, seperti untuk payment gateway, mail messaging, dan layanan lainnya.
- Buat dokumentasi yang baik untuk setiap method (fungsi) di library yang dibuat.

## 9. API
- Buat API seaman mungkin, sangat direkomendasikan untuk menggunakan Authentication dengan metode JWT (JSON Web Token)
- Untuk proteksi tambahan bisa gunakan path key, (Setiap endpoint request harus disertai property ?key=YourPathKey (Optional,Recommended)
- Pastikan buat template response yang konsisten, dan selalu sertakan property message, example:
```
{
  "success": true,
  "message": "Your Request Completed",
  "data": [],
}
```
- Gunakan HTTP Status Code yang sesuai
  - **200 OK**: Permintaan berhasil.
  - **201 Created**: Permintaan berhasil dan sumber daya baru telah dibuat.
  - **400 Bad Request**: Permintaan tidak dapat diproses karena kesalahan klien yang dapat diidentifikasi (misalnya, data yang tidak valid).
  - **401 Unauthorized**: Permintaan membutuhkan autentikasi atau autentikasi gagal.
  - **403 Forbidden**: Server mengerti permintaan, tetapi menolak untuk mengotorisasi akses.
  - **404 Not Found**: Sumber daya yang diminta tidak ditemukan.
  - **405 Method Not Allowed**: Metode yang diminta tidak diizinkan untuk sumber daya yang diminta.
  - **500 Internal Server Error**: Kesalahan umum pada server.
  - **503 Service Unavailable**: Layanan tidak tersedia, server tidak dapat menangani permintaan.
    
## 10. Naming Functions dan Variabel
- Beri nama fungsi yang mudah dimengerti. Disarankan menambah 1-2 baris dokumentasi serta contoh penggunaan, terutama jika fungsi berpotensi digunakan oleh banyak orang.
- Sertakan tipe data pada parameter input functions dan return functions untuk memberikan gambaran lebih jelas tentang bagaimana fungsi digunakan
  - contoh: **int**, **string**, **array**, **callable**, **nullable**
  - jika memungkinkan menggunakan 2 tipe data sekaligus gunakan sesuatu seperti: **int|string**, **array|string**
  - jika membuat null sebagai value default gunakan: **?string**, **?int**
  ```php
  function calculateAndFormat(int $harga_per_unit, int $jumlah_item, ?string $prefix = null): string {
      $total = $harga_per_unit * $jumlah_item;
      return ($prefix ? "$prefix " : '') . number_format($total, 0, ',', '.');
  }
  ```
- Namakan variabel sesuai dengan isinya dan hindari penggunaan nama variabel yang terlalu singkat tanpa keterangan dokumentasi di samping atau di dekatnya.
- Gunakan gaya penulisan yang konsisten seperti camelCase atau snake_case, namun dapat disesuaikan sesuai kebutuhan dan gaya penulisan pribadi.
