# rules-of-code
Rules

1. Database
~ Kolom Primary Key harus 'id'
~ Kolom Foreign Key sangat disarankan untuk sama dengan nama tabel yang berelasi. Atau gunakan entitas yang berelasi (misalnya berelasi ke tabel users, tapi karena di users ada banyak akses seperti pegawai, silahkan bisa gunakan pegawai_id)
~ Gunakan softDelete pada setiap tabel yang dirasa perlu data historis, tapi disarankan untuk gunakan saja softDelete di semua tabel
~ Ketentuan penamaan kolom: silahkan disesuaikan, tapi sangat disarankan untuk tetap konsisten. Jika ingin gunakan bahasa inggris, gunakan bahasa inggris seluruhnya
~ Penamaan kolom timestamps dan softdelete: Umum kami gunakan di Codeigniter3 adalah:
  created_by, created_date, updated_by, updated_date, deleted_by
Untuk laravel, sangat direkomendasikan untuk gunakan kolom timestamp bawaan
Atau silahkan disesuaikan yang penting konsisten untuk seluruh tabel yang menggunakan timestamps dan softdelete

2. Modul (Codeigniter 3)
     Buat modul yang sesuai dengan fitur, dengan nama yang cocok
     Jika masih memungkinkan untuk menyatukan suatu modul, silahkan disatukan. Seperti contoh modul report yang di dalamnya bisa ada report A, report B, ...
     maka bisa disatukan dengan nama modul report, kemudian buat controller, model, dan folder views masing masing untuk setiap report

3. Routes
~ Gunakan penamaan route yang konsisten, buat semudah mungkin dimengerti oleh developer lain
~ Untuk route/endpoint API. Untuk arsitektur Restful API sangat direkomendasikan untuk membuat endpoint berupa nomina (kata benda)
    Example: https://ourdomain.com/api/products
~ Manfaatkan setiap http method untuk satu endpoint:
     Get /products => Return list dari semua products
     Get /products/{id} => Return detail dari satu product secara spesifik
     Post /products => Endpoint untuk insert data produk baru
     Patch products/{id} => Update product tertentu secara sederhana seperti hanya ubah satu kolom status
     Put /products/{id} => Untuk update data yang banyak sekaligus dari suatu baris di database seperti name, price, dan kolom lain secara bersamaan sekaligus
     Delete /products/{id} => Untuk Delete product tertentu, 

*** Note penting, karena method Put, Patch, Delete dibuat dengan memanfaatkan Http Method Spoofing Terkadang data tidak terkirim dengan benar, teknis penanganan:
    Sertakan header: 'X-HTTP-Method-Override: Put/Patch/Delete' dalam setiap request masing-masing, tapi jika dirasa merepotkan dan rentan khususnya untuk method Put bisa              diganti dengan method Post

4. Views
~ Kelompokan dalam suatu folder yang tepat
~ Lakukan templating untuk views yang punya struktur sama (header, navbar, footer, .etc)
~ Minimalisir proses komputasi yang rumit di views
~ Beri nama class dan id untuk form, button, modal, dan element lain dengan konsisten untuk setiap views untuk meminimalisir kebingungan
   
5. Javascript and Jquery
~ Sangat direkomendasikan untuk menulis file js pada suatu file .js yang terpisah dan dipanggil melalui asset (tidak disatukan dengan file views)
Alasannya untuk membuat browser melakukan caching dan meringankan meminimalisir request

6. Gunakan vendor plugin yang konsisten dan sesuai kebutuhan

7. Helpers
~ Klasifikasikan functions dari helper untuk manipulasi data yang seperti apa, seperti date_helper.php, number_helper.php, formatter_helper.php, generator_helper.php
~ Selalu pastikan helper yang dibuat itu belum pernah ada, jika sudah ada gunakan yang ada, jika ada tapi kurang maksimal bisa dimaksimalkan dengan syarat tidak menimbulkan error, jika rentan buat helper baru
~ Hati-hati ketika mengubah file helper yang digunakan secara global dikhawatirkan adanya konflik ketika merge ke main branch project

8. Libraries
~ Buat libraries yang sesuai dengan kebutuhan, contohnya sepaket function dan property untuk untuk payment gateway, mail messaging, dan service lain
~ Buatkan dokumentasi yang baik untuk setiap method (functions) di library yang dibuat

9. Functions dan Variabel Naming
~ Buat nama function yang mudah dimengerti, sangat direkomendasikan untuk menambah 1-2 baris dokumentasi + example of usage apalagi jika function berpotensi digunakan oleh banyak orang
~ Sertakan tipe data pada parameter input functions, dan return functions hal itu untuk memberi gambaran lebih bagaimana function digunakan
Contohnya: int, string, array, callable,
  jika memungkinkan 2 tipe data int|string, ...
  jika menggunakan null sebagai default gunakan ?string, ?int, ...
~ Namakan variabel sesuai dengan isinya dan diharapkan agar tidak bias dalam penamaanya, dan jangan gunakan nama variabel yang terlalu singkat tanpa keterangan dokumentasi di samping atau di dekatnya
~ Jika memungkinkan, gunakan style yang konsisten seperti camelCase atau snack_case tapi hal itu boleh disesuaikan sesuai kebutuhan, style penulisan pribadi, dan sebagainya
