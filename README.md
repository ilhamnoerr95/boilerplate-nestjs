# Boilerplate NestJS

Boilerplate project menggunakan [NestJS](https://nestjs.com/) framework yang sudah dikonfigurasi dengan berbagai fitur siap pakai untuk mempercepat development backend API.

## Tech Stack

- **NestJS 11** — Framework Node.js untuk membangun server-side application
- **TypeScript** — Static typing untuk JavaScript
- **Winston** — Logging library dengan file & console transport
- **Swagger (OpenAPI)** — Auto-generated API documentation
- **class-validator & class-transformer** — Request DTO validation
- **Jest** — Unit & E2E testing framework
- **ESLint + Prettier** — Code linting & formatting

## Fitur yang Sudah Tersedia

### 1. Global API Prefix & URI Versioning
Semua route otomatis menggunakan prefix `/api` dan mendukung URI versioning (`/api/v1/...`).

### 2. Swagger API Documentation
Dokumentasi API otomatis tersedia di `/api/docs` dengan dukungan API Key authentication (`x-client-id`, `x-client-secret`).

### 3. Global Validation Pipe
- Whitelist mode — property yang tidak ada di DTO akan otomatis dibuang
- `forbidNonWhitelisted` — request ditolak jika ada property tidak dikenal
- Auto-transform — request body otomatis di-transform sesuai tipe DTO
- Custom error response format untuk validation error

### 4. Structured Logging (Winston)
- Console transport dengan format timestamp & colorize
- File transport: `logs/error.log` (error only) dan `logs/combined.log` (semua level)
- Format JSON untuk file log agar mudah di-parse

### 5. HTTP Logging Interceptor
Setiap request otomatis di-log dengan format: `[status] METHOD /path - duration ms`

### 6. Global HTTP Exception Filter
Response error yang konsisten dengan format:
```json
{
  "success": false,
  "status": 400,
  "message": { "field": "error message" }
}
```

### 7. Modular Structure
Struktur folder yang terorganisir:
```
src/
├── common/
│   ├── filter/       # Global exception filters
│   ├── guard/        # Auth guards
│   └── utils/        # Utility functions
├── logger/           # Winston & interceptor config
├── modules/
│   └── example/      # Contoh module CRUD lengkap (controller, service, dto, entity)
├── app.module.ts
└── main.ts
```

### 8. Example CRUD Module
Module `example` sebagai referensi pembuatan module baru dengan:
- Controller dengan full CRUD endpoints
- DTO dengan validasi (`class-validator`)
- Service layer
- Unit test boilerplate

## Cara Penggunaan

### Prerequisites
- Node.js >= 18
- pnpm

### Install Dependencies
```bash
pnpm install
```

### Menjalankan Aplikasi
```bash
# development (watch mode)
pnpm run start:dev

# production
pnpm run build
pnpm run start:prod
```

### Akses Swagger
Setelah server berjalan, buka: http://localhost:3000/api/docs

### Menjalankan Test
```bash
# unit tests
pnpm run test

# e2e tests
pnpm run test:e2e

# test coverage
pnpm run test:cov
```

### Linting & Formatting
```bash
pnpm run lint
pnpm run format
```

## Membuat Module Baru

Gunakan NestJS CLI untuk generate module baru:
```bash
npx nest g resource modules/nama-module
```

Module baru akan otomatis ter-generate dengan controller, service, dto, dan entity.

## Environment Variables

| Variable | Default | Keterangan |
|----------|---------|------------|
| `PORT`   | `3000`  | Port server |

## License

UNLICENSED
