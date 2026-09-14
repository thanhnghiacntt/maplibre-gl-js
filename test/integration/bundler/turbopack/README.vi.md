# Ví dụ Turbopack

Ứng dụng tối giản kiểm chứng bản build ESM dưới Turbopack. Turbopack được dùng làm bundler mặc định trong Next.js và không thực tế để chạy độc lập, vì vậy ví dụ này là một ứng dụng Next.js:

- `import {Map} from 'maplibre-gl'` và `import 'maplibre-gl/dist/maplibre-gl.css'` được phân giải thông qua trường `exports` của package, từ một client component.
- `scripts/copy-maplibre-worker.mjs` copy worker đã build sẵn và các file dùng chung vào `public/maplibre/`, và `setWorkerUrl` trỏ tới đường dẫn được phục vụ đó. Câu lệnh `import from './maplibre-gl-shared.mjs'` bên trong worker được phân giải thành công vì cả hai file đều được copy cạnh nhau.

Cách dùng `new URL('maplibre-gl/dist/maplibre-gl-worker.mjs', import.meta.url)` như trong ví dụ webpack không hoạt động ở đây. Turbopack xuất worker dưới dạng một asset có hash mà không xuất kèm file `maplibre-gl-shared.mjs` đi cùng, nên worker bị lỗi 404 ngay lần import đầu tiên và bản đồ sẽ không yêu cầu bất kỳ tile nào. Việc phục vụ cả hai file từ `public/` giúp tránh vấn đề này. Chế độ bundler khác của Next, `next build --webpack`, cũng có hành vi tương tự, vì vậy đây là cách Next xử lý asset chứ không riêng gì Turbopack.

`output: 'export'` giữ cho bản build là một trang tĩnh (static site) đơn thuần, để bộ khung kiểm thử bundler có thể phục vụ nó giống như cách nó phục vụ các ví dụ khác.

`.npmrc` thiết lập `install-links=true`. Nếu không có tùy chọn này, npm sẽ symlink dependency `file:` vào thư mục gốc của repo, Turbopack sẽ suy ra project root từ lockfile gốc và coi `dist/` của chính thư viện là mã nguồn first-party, và `new URL(..., import.meta.url)` động của worker sẽ trở thành lỗi build cứng (hard build error) thay vì chỉ là cảnh báo như đối với một package đã publish.

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

`predev` và `prebuild` chạy script copy, vì vậy worker đã sẵn sàng cho cả `next dev` lẫn `next build`.
