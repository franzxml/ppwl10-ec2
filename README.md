# PPWL9 Fullstack Monorepo (Docker)

## Deskripsi
Proyek ini adalah monorepo modern yang dikelola menggunakan **Bun**. Mengintegrasikan Backend (Elysia/Prisma), Frontend (React/Vite), dan Shared Packages untuk membangun aplikasi manajemen kelas (Classroom) dengan sistem autentikasi Google OAuth2. Proyek ini sudah dikontainerisasi menggunakan **Docker**.

## Materi & Fitur
- **Monorepo Architecture:** Pengelolaan aplikasi backend, frontend, dan shared logic dalam satu repositori menggunakan Bun Workspaces.
- **Backend (API):** Dibangun dengan **Elysia** (Bun), menggunakan **Prisma ORM** untuk manajemen database (SQLite), **Google OAuth2** untuk autentikasi, serta dokumentasi API via **Swagger**.
- **Frontend (UI):** Aplikasi web berbasis **React + TypeScript + Vite** dengan integrasi **Tailwind CSS** dan **Shadcn UI** untuk antarmuka yang modern dan responsif.
- **Shared Package:** Berisi tipe data yang digunakan bersama backend dan frontend untuk memastikan konsistensi kode.
- **Docker:** Setiap service dikontainerisasi dan dapat dijalankan sekaligus menggunakan **Docker Compose**.

## Struktur Folder
```
root/
├── apps/
│   ├── backend/       # API Server (Elysia, Prisma, Google OAuth2)
│   │   └── Dockerfile
│   └── frontend/      # Web Dashboard (React, Vite, Tailwind)
│       └── Dockerfile
├── packages/
│   └── shared/        # Shared types & utilities
├── docker-compose.yml # Konfigurasi Docker Compose
├── bun.lock           # Bun lockfile
├── package.json       # Workspace configuration
└── README.md          # Dokumentasi proyek
```

## URL Layanan
| Service  | URL                              |
|----------|----------------------------------|
| Backend  | http://localhost:3000            |
| Swagger  | http://localhost:3000/swagger    |
| Frontend | http://localhost:5173            |

## Cara Menjalankan

### Menggunakan Docker (Direkomendasikan)
Pastikan [Docker](https://www.docker.com/) sudah terinstal.

```bash
docker compose up --build
```

Untuk menjalankan di background:
```bash
docker compose up --build -d
```

Untuk menghentikan:
```bash
docker compose down
```

### Tanpa Docker (Development)
Pastikan [Bun](https://bun.sh/) sudah terinstal.

1. **Install Dependensi:**
   ```bash
   bun install
   ```

2. **Setup Database (Backend):**
   ```bash
   cd apps/backend
   bun x prisma migrate dev
   bun run prisma/seed.ts
   ```

3. **Jalankan Proyek:**
   Dari root direktori:
   ```bash
   bun dev
   ```
   Atau jalankan secara spesifik:
   - Backend: `bun dev:backend`
   - Frontend: `bun dev:frontend`

## Environment Variables (Backend)
| Variable             | Default Value                          |
|----------------------|----------------------------------------|
| `FRONTEND_URL`       | http://localhost:5173                  |
| `DATABASE_URL`       | file:/app/apps/backend/dev.db          |
| `GOOGLE_REDIRECT_URI`| http://localhost:3000/auth/callback    |

---
Dikembangkan oleh: @franzxml
