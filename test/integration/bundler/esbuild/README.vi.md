# Ví dụ esbuild

Ứng dụng esbuild tối giản để kiểm chứng bản build ESM:

- Tất cả các import của thư viện (`maplibre-gl`, `maplibre-gl/dist/maplibre-gl.css`) được phân giải thông qua trường `exports` của package.
- `build.js` chạy esbuild và copy file worker từ `node_modules/maplibre-gl/dist/maplibre-gl-worker.mjs` sang `dist/`. `setWorkerUrl(new URL('./maplibre-gl-worker.mjs', import.meta.url).toString())` tham chiếu đến file đó một cách tương đối so với bundle tại runtime.

esbuild không nhận diện được pattern `new URL(..., import.meta.url)` như một tham chiếu asset, vì vậy worker được copy một cách tường minh trong build script.

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
