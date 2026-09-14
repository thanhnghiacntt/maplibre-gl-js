# Build Scripts

Thư mục này chứa các script build chung, được gọi thông qua các lệnh `npm run` khác nhau.
Codegen được thực thi khi chạy `npm install` nhằm sinh ra tất cả các artifact cần thiết để quá trình build thành công.

## Đóng gói (bundling) toàn bộ mã nguồn

Quá trình bundling có thể chia thành nhiều bước:

`npm run build-css`
Lệnh này sẽ biên dịch mã CSS và tạo ra file CSS.

`npm run build-prod` và `npm run build-dev`
Các lệnh này sử dụng [rolldown](https://rolldown.rs/) để đóng gói mã nguồn thành các ES module. Kết quả đầu ra gồm hai file:

- `dist/maplibre-gl.mjs` (bundle chính, entry: `src/index.ts`)
- `dist/maplibre-gl-worker.mjs` (bundle worker, entry: `src/source/worker.ts`)

Bundle chính tạo worker thông qua `new Worker(url, {type: 'module'})`. URL này mặc định là một file cùng thư mục với module được load (được phân giải qua `import.meta.url`) và có thể được ghi đè bằng cách gọi `setWorkerUrl()`. Các URL cross-origin được fetch qua CORS và chuyển đổi thành một Blob URL cùng origin, vì hàm khởi tạo `Worker` từ chối các URL cross-origin ngay cả khi CORS cho phép fetch.

`banner.ts` được dùng để tạo phần banner ở đầu file đầu ra.

<hr>

### `npm run codegen`

Lệnh `codegen` chạy ba script sau, nhằm cập nhật các file mã nguồn tương ứng dựa trên nguồn style `v8.json` và các file dữ liệu khác. Người đóng góp nên chạy lệnh này thủ công khi dữ liệu style bên dưới có thay đổi. Các file mã nguồn được sinh ra sau đó sẽ được commit vào repo.

#### generate-struct-arrays.ts

Sinh ra file `data/array_types.ts`, bao gồm:

 - Các lớp con `StructArrayLayout_*`, mỗi lớp ứng với một layout bộ nhớ cụ thể
 - Các export có tên, ánh xạ mỗi kiểu mảng khái niệm (ví dụ: `CircleLayoutArray`) tới lớp `StructArrayLayout` tương ứng
 - Các lớp con `StructArray` cụ thể, khi cần các accessor struct đặc thù cho từng kiểu (ví dụ: `CollisionBoxArray`)

#### generate-style-code.ts

Sinh ra các file mã nguồn `style/style_layer/[loại layer]_style_layer_properties.ts` dựa trên nội dung của `v8.json`. Các file này cung cấp signature kiểu (type signature) cho các thuộc tính paint và layout của từng loại style layer.

<hr>
