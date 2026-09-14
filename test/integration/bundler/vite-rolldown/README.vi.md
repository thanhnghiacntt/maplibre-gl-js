# Ví dụ Vite 8+ (Rolldown)

Ứng dụng Vite 8+ (Rolldown) tối giản để kiểm chứng bản build ESM:

- `import {Map} from 'maplibre-gl'` và `import 'maplibre-gl/dist/maplibre-gl.css'` được phân giải thông qua trường `exports` của package.
- `import workerUrl from 'maplibre-gl/dist/maplibre-gl-worker.mjs?worker&url'` đóng gói worker (bao gồm cả chunk dùng chung mà nó phụ thuộc) thành một file duy nhất và trả về URL. `setWorkerUrl(workerUrl)` trỏ MapLibre đến file đó.

## Cài đặt

Từ thư mục gốc của repo, build package cha một lần để tạo `dist/`:

```bash
npm install
npm run build-dist
```

Sau đó, trong thư mục này:

```bash
npm install
npm run dev
```
