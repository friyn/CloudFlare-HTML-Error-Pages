# CloudFlare HTML Error Pages

Koleksi halaman HTML statis yang meniru tampilan error page Cloudflare.
Project ini dibuat untuk belajar / eksperimen (misalnya untuk demo, prank ringan ke teman, atau testing UI), **bukan** untuk dipakai menipu pengguna sungguhan.

## Fitur

- **Halaman error statis** yang mirip Cloudflare, misalnya:
  - `500-Internal-server-error.html`
  - `523-Origin-is-unreachable.html`
  - `526-Invalid-SSL-certificate.html`
  - `1014-CNAME-Cross-User-Banned.html`
- **Detail dinamis dengan JavaScript** di setiap halaman error:
  - Ray ID dummy (random hex 16 karakter setiap reload)
  - IP pengunjung (diambil via `https://api.ipify.org?format=json`)
  - Waktu kunjungan (UTC) di header/footer
  - Hostname diambil dari `window.location.hostname`
- **Halaman index bergaya Cloudflare** (`index.html`):
  - Menampilkan daftar beberapa error page yang didefinisikan di array `files` (JavaScript)
  - Setiap baris bisa diklik untuk membuka file terkait
  - Menggunakan ikon dan layout yang mirip tampilan error page Cloudflare

## Struktur Project

Struktur utama:

```text
CloudFlare-HTML-Error-Pages/
├─ 500-Internal-server-error.html
├─ 523-Origin-is-unreachable.html
├─ 526-Invalid-SSL-certificate.html
├─ 1014-CNAME-Cross-User-Banned.html
├─ index.html               # list Error
└─ cdn-cgi/
   └─ images/              # ikon browser/cloud/server/error/ok
```

## Menjalankan Secara Lokal

Project ini tidak butuh framework khusus. Kamu bisa:

- Menjalankan PHP built-in server:

  ```bash
  php -S 127.0.0.1:80
  ```

  Lalu buka di browser:

  - `http://127.0.0.1/` → halaman index (`index.html`) berisi daftar error page.
  - Klik salah satu file di daftar, misalnya:
    - `http://127.0.0.1/500-Internal-server-error.html`
    - `http://127.0.0.1/523-Origin-is-unreachable.html`

- Atau pakai static file server lain (misalnya dari Node, Python, atau langsung double-click `index.html`).

> Jika port 80 bentrok, ganti menjadi port lain (misalnya `127.0.0.1:8080`).

## Menambahkan Halaman Error Baru

1. Buat file HTML baru di root, misalnya `520-Unknown-error.html`.
2. Salin struktur dari salah satu file yang sudah ada (`500-...` atau `523-...`).
3. Sesuaikan:
   - Title dan heading (judul error dan kode error)
   - Teks "What happened?" dan "What can I do?"
   - Link dokumentasi Cloudflare (kalau ada) di bagian bantuan.
4. Simpan file.
5. Edit `index.html` dan tambahkan nama file baru ke array `files` di script:

   ```js
   const files = [
     { name: "500-Internal-server-error.html" },
     // ...
     { name: "520-Unknown-error.html" }  // tambahkan di sini
   ];
   ```

Setelah itu halaman index (`index.html`) akan menampilkan entri baru di daftar.

## Catatan Penting

- Ini bukan produk resmi Cloudflare.
- Gunakan hanya untuk tujuan belajar, demo, atau eksperimen pribadi.
- Jangan gunakan untuk phishing atau aktivitas yang melanggar hukum / ToS.
