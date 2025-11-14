## Dokumentasi Teknis — Dokploy

Dokumentasi ini menjelaskan aspek teknis dari repositori, konfigurasi Docker Compose, variabel lingkungan, alur deployment, dan troubleshooting.

Catatan singkat: saya mengasumsikan struktur repo menggunakan `docker-compose.yml` di root dan variabel lingkungan di `.env`. Sesuaikan bila struktur berbeda.

### 1. Gambaran umum

`dokploy` berisi konfigurasi untuk menjalankan satu atau beberapa layanan menggunakan Docker Compose. Layanan bisa berupa web app, database, worker, dan lain-lain. File utama: `docker-compose.yml`.

Tujuan dokumentasi ini:

- Menjelaskan cara menjalankan proyek secara lokal dan di server.
- Menyediakan contoh variabel lingkungan dan instruksi debugging.

### 2. Arsitektur

Periksa `docker-compose.yml` untuk melihat layanan, jaringan, dan volume yang didefinisikan. Biasanya ada beberapa blok layanan seperti:

- web (server aplikasi)
- db (database: postgres/mysql)
- redis (cache/queue)
- worker (background jobs)

Contoh inspeksi singkat:

```powershell
# lihat isi docker-compose
type docker-compose.yml

# lihat ringkasan layanan
docker-compose config --services
```

### 3. Variabel lingkungan (.env)

Letakkan konfigurasi sensitif pada file `.env` (jangan commit ke repo). Contoh minimal `.env.example`:

```
POSTGRES_USER=postgres
POSTGRES_PASSWORD=secret
POSTGRES_DB=appdb
APP_ENV=development
APP_PORT=8000
```

Jika repo belum punya `.env.example`, buat satu dan gunakan `copy .env.example .env` lalu sesuaikan.

### 4. Langkah deployment (server atau lokal)

1. Pastikan Docker & Docker Compose terpasang di mesin target.
2. Clone repo ke server:

```powershell
git clone <repo-url>
cd dokploy
```

3. Atur variabel lingkungan:

```powershell
copy .env.example .env
# edit .env
```

4. Jalankan compose di background dan build image bila perlu:

```powershell
docker-compose up -d --build
```

5. Periksa apakah layanan berjalan:

```powershell
docker-compose ps
docker-compose logs -f
```

6. Jika ada migrasi database, jalankan perintah migrasi sesuai instruksi proyek (mis. `docker-compose exec web alembic upgrade head`). Lihat bagian layanan di `docker-compose.yml` untuk nama service yang tepat.

### 5. Backup & Restore (umum)

- Untuk database berbasis volume Docker, gunakan `docker exec` dan `pg_dump`/`mysqldump` atau mount volume ke container sementara.
- Selalu tes restore di environment non-produksi terlebih dahulu.

### 6. Troubleshooting

- Container tidak mau start: lihat `docker-compose logs <service>`.
- Port conflict: cek port host yang digunakan di `docker-compose.yml` dan pastikan tidak ada service lain memakai port sama.
- Environment variable tidak terbaca: pastikan `.env` ada di folder yang sama dengan `docker-compose.yml` dan tidak ada spasi ekstra pada nama/isi variabel.

Common commands:

```powershell
docker-compose up -d --build      # jalankan (rebuild)
docker-compose down              # stop dan hapus network/containers
docker-compose logs -f <service> # lihat log service
docker-compose exec <service> sh # buka shell di container
```

### 7. FAQ singkat

- Q: Di mana saya mengubah port? — A: di `ports:` pada `docker-compose.yml` untuk layanan terkait.
- Q: Bagaimana menambah service baru? — A: tambahkan blok service baru di `docker-compose.yml`, tentukan image/build, env, ports, dan volumes.

### 8. Kontak

Untuk pertanyaan terkait repo, buka issue di GitHub atau buat pull request dengan deskripsi jelas mengenai perubahan.

---

Jika Anda ingin, saya bisa juga:

- Membuat `.env.example` berdasarkan `docker-compose.yml` secara otomatis.
- Menambahkan contoh GitHub Actions workflow untuk build image dan menjalankan test.
