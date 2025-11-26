# CloudFlare HTML Error Pages

Koleksi halaman HTML statis yang meniru tampilan error page Cloudflare.
Project ini dibuat untuk belajar / eksperimen (misalnya untuk demo, prank ringan ke teman, atau testing UI), **bukan** untuk dipakai menipu pengguna sungguhan.

## Fitur

- **Halaman error statis** yang mirip Cloudflare, misalnya:
  - `500-Internal-server-error.html`
  - `523-Origin-is-unreachable.html`
  - `526-Invalid-SSL-certificate.html`
  - `1014-CNAME-Cross-User-Banned.html`
- **Detail dinamis dengan JavaScript**:
  - Ray ID dummy (random hex 16 karakter setiap reload)
  - IP pengunjung (diambil via `https://api.ipify.org?format=json`)
  - Waktu kunjungan (UTC) di header/footer
  - Hostname diambil dari `window.location.hostname`
- **Index otomatis** dengan `index.php`:
  - Menampilkan daftar semua file `.html` di folder
  - Menandai folder (misalnya `cdn-cgi/`)
  - Menampilkan size dan tanggal modifikasi
  - Seluruh baris bisa diklik, bukan cuma nama file

## Struktur Project

Struktur utama:

```text
CloudFlareHostError/
├─ 500-Internal-server-error.html
├─ 523-Origin-is-unreachable.html
├─ 526-Invalid-SSL-certificate.html
├─ 1014-CNAME-Cross-User-Banned.html
├─ index.php                # index otomatis (file manager mini)
└─ cdn-cgi/
   ├─ styles/main.css       # CSS mirip Cloudflare
   └─ images/               # ikon browser/cloud/server/error/ok
```

## Menjalankan Secara Lokal

Project ini tidak butuh framework khusus, cukup PHP built-in server.

```bash
php -S 127.0.0.1:80
```

Kemudian buka di browser:

- `http://127.0.0.1/` → halaman index (`index.php`) berisi daftar file HTML.
- Klik salah satu file, misalnya:
  - `http://127.0.0.1/500-Internal-server-error.html`
  - `http://127.0.0.1/523-Origin-is-unreachable.html`

> Jika port 80 bentrok, ganti menjadi port lain (misalnya `127.0.0.1:8080`).

## Menambahkan Halaman Error Baru

1. Buat file HTML baru di root, misalnya `520-Unknown-error.html`.
2. Salin struktur dari salah satu file yang sudah ada (`500-...` atau `523-...`).
3. Sesuaikan:
   - Title dan heading (judul error dan kode error)
   - Teks "What happened?" dan "What can I do?"
   - Link dokumentasi Cloudflare (kalau ada) di bagian bantuan.
4. Simpan file.

Halaman index (`index.php`) akan otomatis menampilkan file `.html` baru tersebut di daftar, tanpa perlu di-edit manual.

## Catatan Penting

- Ini bukan produk resmi Cloudflare.
- Gunakan hanya untuk tujuan belajar, demo, atau eksperimen pribadi.
- Jangan gunakan untuk phishing atau aktivitas yang melanggar hukum / ToS.
