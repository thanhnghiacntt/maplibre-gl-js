# Ví dụ Rollup

Ứng dụng Rollup tối giản để kiểm chứng bản build ESM:

- Tất cả các import của thư viện (`maplibre-gl`, `maplibre-gl/dist/maplibre-gl.css`) được phân giải thông qua trường `exports` của package.
- `rollup-plugin-copy` copy file worker vào output của bundle. `setWorkerUrl(new URL('./maplibre-gl-worker.mjs', import.meta.url).toString())` tham chiếu đến file đó một cách tương đối so với bundle tại runtime.

## Cài đặt

Từ thư mục gốc của repo, build package cha một lần để tạo `dist/`:

```bash
npm install
npm run build-dist
```

Sau đó, trong thư mục này:

```bash
npm install
npm run build       # tạo ra dist/main.js, dist/main.css, dist/maplibre-gl-worker.mjs
npm run serve       # phục vụ tại http://localhost:3000
```

Để dùng chế độ watch, chạy `npm run dev` ở một terminal và `npm run serve` ở terminal khác.
