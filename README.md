# Dokploy + PostgreSQL di Docker

Dokumentasi ini menjelaskan cara memasang [Dokploy](https://dokploy.com/) dengan database PostgreSQL menggunakan Docker Compose.

> ⚠️ Pastikan Docker dan Docker Compose sudah terinstall di sistem Anda.

---

## 📋 Prasyarat

- Docker (v20.10.0 ke atas)
- Docker Compose (v2.0.0 ke atas)

---

## 🚀 Instalasi

1.  Buat direktori baru untuk Dokploy:

    ```bash
    mkdir dokploy-docker
    cd dokploy-docker
    ```

2.  Clone repository ini:

        git clone <repo-url>
        cd dokploy

3.  Jalankan Dokploy:

    ```bash
    docker-compose up -d
    ```

4.  Tunggu proses inisialisasi selesai (ambil kopi 😊). Anda bisa cek log dengan:

    ```bash
    docker-compose logs -f dokploy
    ```

5.  Buka browser dan akses:

    ```
    http://localhost:3000
    ```

---

## 🛠️ Troubleshooting

### 1. Tidak bisa akses `http://localhost:3000`

- Pastikan tidak ada aplikasi lain yang menggunakan port 3000.
- Cek log Dokploy: `docker-compose logs dokploy`
- Jika muncul error Swarm, jalankan `docker swarm init` lalu ulangi langkah 3.

### 2. Error `ENOTFOUND dokploy-postgres`

- Pastikan Anda menggunakan `docker-compose.yml` yang menyertakan layanan `postgres`.
- Pastikan `depends_on` dan `DATABASE_URL` di `dokploy` mengarah ke `postgres`.

---

## 🧹 Hapus Instalasi

Jika ingin menghapus Dokploy beserta datanya:

```bash
docker-compose down -v
```
