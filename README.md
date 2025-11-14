# Dokploy

Dokploy — repositori ini berisi konfigurasi dan dokumentasi untuk menjalankan proyek menggunakan Docker Compose.

> Catatan: Saya mengasumsikan proyek ini dideploy menggunakan `docker-compose.yml` yang ada di repo. Jika makna "dokploy" berbeda, beri tahu saya agar saya sesuaikan dokumentasinya.

## Ringkasan

Dokumentasi ini berisi petunjuk cepat untuk menjalankan layanan lokal atau di server menggunakan Docker Compose, penjelasan konfigurasi, serta tautan ke dokumentasi teknis lebih lengkap.

## Badges (opsional)

Tambahkan badge pipeline / coverage jika ada. Contoh placeholder:

![build](https://img.shields.io/badge/build-passing-brightgreen)

## Daftar isi

- Prasyarat
- Quick start
- Konfigurasi
- Menjalankan & memeriksa layanan
- Pengembangan
- Dokumentasi teknis
- Kontribusi

## Prasyarat

Pastikan terinstal di mesin Anda:

- Docker
- Docker Compose (jika Docker Desktop, biasanya sudah termasuk)

Periksa versi dasar:

```powershell
docker --version
docker-compose --version
```

## Quick start

1. Clone repository ini:

```powershell
git clone <repo-url>
cd dokploy
```

2. (Opsional) Salin file environment contoh dan sesuaikan variabel:

```powershell
copy .env.example .env
# lalu edit .env sesuai kebutuhan
```

3. Jalankan Docker Compose:

```powershell
docker-compose up -d --build
```

4. Periksa status layanan:

```powershell
docker-compose ps
docker-compose logs -f
```

Untuk menghentikan dan membersihkan:

```powershell
docker-compose down
```

## Konfigurasi

- File utama: `docker-compose.yml` berada di root repo.
- Variabel lingkungan disarankan untuk diletakkan di `.env` atau file yang direferensikan oleh Compose.
- Jika ada layanan yang memerlukan volume atau data persisten, periksa bagian `volumes` di `docker-compose.yml`.

## Menjalankan & memeriksa layanan

- Lihat container berjalan: `docker ps` atau `docker-compose ps`.
- Lihat log: `docker-compose logs -f <service>`.
- Menjalankan perintah di dalam container: `docker-compose exec <service> sh` atau `bash`.

## Pengembangan

- Gunakan branch fitur (feature/\*) lalu buat PR ke branch `main` atau `master` sesuai kebijakan repo.
- Untuk perubahan kode, rebuild image lokal: `docker-compose up -d --build <service>`

## Dokumentasi teknis

Panduan teknis lebih lengkap ada di `dokumentasi.md`. File itu berisi deskripsi arsitektur, variabel lingkungan, dan troubleshooting.

## Kontribusi

Baca `CONTRIBUTING.md` untuk panduan singkat kontribusi.

## Lisensi

Tambahkan file `LICENSE` jika proyek ini perlu lisensi terbuka. Saat ini tidak ada lisensi ditentukan di repo ini.

---

Jika Anda ingin saya menambahkan badge CI (GitHub Actions), contoh konfigurasi workflow, atau menyesuaikan README ke bahasa Inggris, beri tahu saya dan saya akan tambahkan.
