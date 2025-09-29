# Proyek Latihan: Profil Instagram dengan Bootstrap Grid

Proyek ini adalah implementasi halaman profil Instagram yang responsif menggunakan framework Bootstrap 5, dengan fokus utama pada pemanfaatan sistem Grid.

## Struktur File

-   `index.html`: File HTML utama yang berisi seluruh struktur halaman.
-   `assets/css/custom.css`: File CSS tambahan untuk styling kustom (misalnya, membuat foto profil menjadi bulat).
-   `assets/img/`: Folder untuk menyimpan aset gambar (saat ini tidak digunakan karena memakai gambar placeholder).

## Dependensi

-   [Bootstrap 5.3.2 (CSS & JS)](https://getbootstrap.com/): Digunakan melalui CDN untuk styling dan komponen.
-   [Bootstrap Icons](https://icons.getbootstrap.com/): Digunakan melalui CDN untuk ikon Instagram.

---

## Pertanyaan & Jawaban

### 1. Mengapa memilih konfigurasi `col-*` tertentu untuk tiap breakpoint?

Konfigurasi kolom grid (`col-12`, `col-md-6`, `col-lg-4`) dipilih berdasarkan prinsip *mobile-first* dan pengalaman pengguna (UX) yang optimal di berbagai ukuran layar.

-   **Mobile (`col-12`):** Di layar kecil (seperti smartphone), ruang horizontal sangat terbatas. Menggunakan 1 kolom (`col-12`) memastikan setiap postingan ditampilkan penuh selebar layar, sehingga gambar terlihat jelas dan mudah di-tap tanpa salah sentuh.
-   **Tablet (`col-md-6`):** Layar tablet memiliki ruang yang lebih lega. Menampilkan 2 kolom (`col-md-6`) adalah keseimbangan yang baik antara ukuran gambar yang masih cukup besar untuk dilihat detailnya dan efisiensi dalam menampilkan lebih banyak konten sekaligus tanpa harus banyak scrolling.
-   **Desktop (`col-lg-4`):** Di layar desktop yang sangat lebar, menampilkan 3 kolom (`col-lg-4`) atau bahkan 4 kolom (`col-lg-3`) menjadi sangat ideal. Ini memaksimalkan pemanfaatan ruang layar dan memberikan pengguna gambaran umum dari banyak postingan secara cepat, mirip dengan tampilan asli Instagram Web.

### 2. Bagaimana Anda memastikan tombol Follow/Edit Profile tetap mudah dijangkau di mobile? Jelaskan pendekatannya.

Pendekatan yang saya gunakan adalah **memisahkan struktur tombol untuk mobile dan desktop** menggunakan *responsive display utilities* dari Bootstrap (`d-block`, `d-md-none`, `d-none`, `d-md-block`).

**Pendekatannya:**

1.  **Struktur HTML Ganda:** Saya membuat dua blok div untuk tombol:
    -   Satu blok ditempatkan di samping username, khusus untuk tampilan desktop (`d-none d-md-block`).
    -   Satu blok lagi ditempatkan di bawah bio, khusus untuk tampilan mobile (`d-block d-md-none`).
2.  **Posisi di Mobile:** Di mobile, tombol Follow diletakkan di bawah informasi bio dan statistik. Tombol ini dibuat *full-width* (`w-100`). Ini membuatnya sangat mudah dijangkau oleh ibu jari pengguna (area *thumb-friendly*) karena posisinya ada di tengah konten utama dan ukurannya besar.
3.  **Posisi di Desktop:** Di desktop, tombol kembali ke posisi standarnya di sebelah kanan username, sesuai dengan desain UI Instagram yang umum.

Dengan cara ini, fungsionalitas utama (Follow) tetap prioritas di perangkat mobile tanpa mengorbankan tata letak yang lebih kompleks di layar yang lebih besar.

### 3. Jika postingan bertambah jadi 50, apa potensi masalah dan bagaimana solusi gridmu mengatasinya?

Jika postingan bertambah menjadi 50, akan muncul dua masalah utama:

1.  **Masalah Kinerja (Performance):** Memuat 50 gambar resolusi tinggi sekaligus akan membuat waktu muat halaman (*load time*) menjadi sangat lama. Ini berdampak buruk pada pengalaman pengguna dan SEO.
2.  **Masalah Pengalaman Pengguna (UX):** Pengguna harus melakukan *scrolling* yang sangat panjang (*endless scroll*) untuk melihat semua konten, yang bisa melelahkan dan membuat frustrasi.

**Solusi Menggunakan Sistem Grid dan Komponen Bootstrap:**

Solusi terbaik untuk mengatasi ini adalah **Pagination (Penomoran Halaman)**.

-   **Implementasi:** Alih-alih menampilkan semua 50 postingan dalam satu grid, kita bisa membaginya menjadi beberapa halaman. Misalnya, 12 postingan per halaman.
-   **Cara Kerja:**
    1.  Grid yang sudah kita buat (`<div class="row g-3">...</div>`) tetap digunakan untuk menampilkan 12 postingan.
    2.  Di bawah grid tersebut, kita tambahkan [Komponen Pagination Bootstrap](https://getbootstrap.com/docs/5.3/components/pagination/).
    3.  Secara fungsional (biasanya dengan bantuan JavaScript atau backend), setiap link pada pagination akan memuat 12 set gambar berikutnya ke dalam grid yang sama.

Dengan pagination, halaman awal akan memuat dengan sangat cepat karena hanya memuat 12 gambar. Pengguna juga mendapatkan kontrol yang jelas untuk menavigasi antar halaman, sehingga UX menjadi lebih baik dan terstruktur.