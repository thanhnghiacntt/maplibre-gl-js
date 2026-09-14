# Ví dụ webpack

Ứng dụng webpack tối giản để kiểm chứng bản build ESM:

- `import {Map} from 'maplibre-gl'` và `import 'maplibre-gl/dist/maplibre-gl.css'` được phân giải thông qua trường `exports` của package.
- `copy-webpack-plugin` copy worker đã build sẵn và các file dùng chung vào thư mục output. Câu lệnh `import from './maplibre-gl-shared.mjs'` bên trong worker được phân giải thành công vì cả hai file đều được copy cạnh nhau.

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
