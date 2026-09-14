# Ví dụ về Bundler

Các ứng dụng độc lập kiểm chứng bản build ESM của `maplibre-gl` thông qua các bundler thực tế. Mỗi thư mục con là tự chứa (self-contained): nó phụ thuộc vào package cha thông qua `file:../../..`, do đó `npm install` sẽ copy `dist/` của package cha vào `node_modules` của ví dụ, và ví dụ đó sau đó sẽ phân giải `import 'maplibre-gl'` và `import 'maplibre-gl/dist/maplibre-gl.css'` đúng như cách một consumer ở downstream sẽ làm.

| Thư mục | Bundler | Cách thiết lập Worker URL |
|---|---|---|
| `vite-rollup-esbuild/` | Vite 7 (Rollup/esbuild) | `import workerUrl from 'maplibre-gl/dist/maplibre-gl-worker.mjs?url'` |
| `vite-rolldown/` | Vite 8+ (Rolldown) | `import workerUrl from 'maplibre-gl/dist/maplibre-gl-worker.mjs?url'` |
| `webpack/` | webpack | `setWorkerUrl(new URL('maplibre-gl/dist/maplibre-gl-worker.mjs', import.meta.url).toString())` |
| `rollup/` | Rollup | `setWorkerUrl(new URL('./maplibre-gl-worker.mjs', import.meta.url).toString())` (worker được copy cạnh bundle thông qua `rollup-plugin-copy`) |
| `esbuild/` | esbuild | `setWorkerUrl(new URL('./maplibre-gl-worker.mjs', import.meta.url).toString())` (worker được copy cạnh bundle trong `build.js`) |
| `turbopack/` | Turbopack (thông qua Next.js) | `setWorkerUrl('/maplibre/maplibre-gl-worker.mjs')` (worker được copy vào `public/` bởi một hook `prebuild`) |

Cả sáu ví dụ đều dùng chung cách import thư viện: `import {Map} from 'maplibre-gl'`, `import 'maplibre-gl/dist/maplibre-gl.css'`. Sự khác biệt nằm ở cách mỗi bundler phân giải Worker URL.

Để chạy bất kỳ ví dụ nào trong số đó:

```bash
# Từ thư mục gốc repo: build các bundle production của package cha. Bắt buộc vì
# mỗi ví dụ đều tham chiếu tới `dist/maplibre-gl-worker.mjs` (tên bản production);
# chỉ chạy `build-dev` sẽ chỉ tạo ra biến thể `-dev` và các ví dụ
# sẽ không copy được.
npm install
npm run build-dist

cd test/integration/bundler/<name>
npm install
npm run dev      # vite-rollup-esbuild, vite-rolldown, webpack
# hoặc:
npm run build && npm run serve   # rollup, esbuild
```

Các ví dụ này không nằm trong CI. Chúng tồn tại để kiểm chứng rằng cấu trúc package và trường `exports` của maplibre-gl hoạt động đúng với các công cụ bundler thực tế, và để ghi lại cách thiết lập worker URL của từng bundler.
