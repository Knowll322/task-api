# Deploy ke Clever Cloud

## Environment variables (mode EXPERT)

```
CC_WEBROOT="/public"
APP_ENV="production"
APP_DEBUG="false"
APP_KEY="<APP_KEY>"
DB_CONNECTION="mysql"
DB_HOST="bebtng.dnccudinus.org"
DB_PORT="3307"
DB_DATABASE="db_mentor_ilham"
DB_USERNAME="usr_mentor_ilham"
DB_PASSWORD="<DB_PASSWORD>"
CC_PRE_RUN_HOOK="php artisan config:clear && php artisan migrate --force"
```

- `APP_KEY` — ambil dari `.env` lokal (`php artisan key:generate --show`).
- `DB_PASSWORD` — isi dengan password database. Nilainya sengaja tidak ditulis di repo karena repo ini publik.

## Langkah deploy

1. Buat aplikasi PHP di Clever Cloud.
2. Buka **Environment variables** → mode **EXPERT**.
3. Paste blok di atas, isi `<APP_KEY>` dan `<DB_PASSWORD>`.
4. Klik **UPDATE CHANGES**.
5. Hubungkan repo GitHub `Knowll322/task-api`, branch `main`.
6. Deploy.
7. Tes: `GET https://<domain>/api/tasks`.

## Catatan

- `CC_WEBROOT=/public` wajib. Tanpa ini Clever Cloud mengarah ke root project dan muncul 403 Forbidden.
- `CC_PRE_RUN_HOOK` menjalankan migrasi setiap aplikasi start. Kalau kredensial database salah, aplikasi gagal start — cek log di Clever Cloud.
- Panduan menulis `DB_PORT=3007`, tetapi server yang benar adalah `3307`.
