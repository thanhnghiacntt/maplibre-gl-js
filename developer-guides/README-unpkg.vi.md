# MapLibre GL JS trên unpkg.com

MapLibre GL JS được phân phối thông qua [unpkg.com](https://unpkg.com).

> *UNPKG là một mạng phân phối nội dung (CDN) toàn cầu, tốc độ cao cho mọi thứ trên npm.*

Các ghi chú này về unpkg được biên soạn riêng cho MapLibre GL JS. Để xem tài liệu cập nhật mới nhất, hãy truy cập [maplibre.org/maplibre-gl-js/docs](https://maplibre.org/maplibre-gl-js/docs). Tại đó bạn có thể xem các ví dụ trực tiếp (live examples) và ghi chú về cách đưa các file JavaScript và CSS vào dự án của mình.

Bạn cũng có thể dùng các ghi chú unpkg này để xem `CHANGELOG` hoặc các bản sửa đổi khác của MapLibre GL JS.

## Ví dụ

Sử dụng một phiên bản cố định:

* [https://unpkg.com/maplibre-gl@6.0.0/dist/maplibre-gl.mjs](https://unpkg.com/maplibre-gl@6.0.0/dist/maplibre-gl.mjs)

---

Bạn cũng có thể dùng [semver range](https://semver.org/) hoặc [tag](https://docs.npmjs.com/cli/dist-tag) thay vì một số phiên bản cố định, hoặc bỏ qua hoàn toàn phần phiên bản/tag để dùng tag `latest`.

* [https://unpkg.com/maplibre-gl@^6.0/dist/maplibre-gl.mjs](https://unpkg.com/maplibre-gl@^6.0/dist/maplibre-gl.mjs) - dùng ít nhất phiên bản `6.0.x`
* [https://unpkg.com/maplibre-gl/dist/maplibre-gl.mjs](https://unpkg.com/maplibre-gl/dist/maplibre-gl.mjs) - dùng tag `latest`

File worker tương ứng được phục vụ từ cùng thư mục `dist/`:

* [https://unpkg.com/maplibre-gl/dist/maplibre-gl-worker.mjs](https://unpkg.com/maplibre-gl/dist/maplibre-gl-worker.mjs)

---

Nếu bạn bỏ qua đường dẫn file (tức là dùng URL "trần"), unpkg sẽ phục vụ file được chỉ định trong trường `module` của `package.json`.

* [https://unpkg.com/maplibre-gl](https://unpkg.com/maplibre-gl)

---

Thêm dấu `/` vào cuối URL để xem danh sách tất cả các file trong một gói (package).

* [https://unpkg.com/maplibre-gl/](https://unpkg.com/maplibre-gl/)

Tại đó bạn có thể tìm thấy file `CHANGELOG`
* [https://unpkg.com/browse/maplibre-gl@6.0.0/CHANGELOG.md](https://unpkg.com/browse/maplibre-gl@6.0.0/CHANGELOG.md)

## Query Parameters (tham số truy vấn)

`?meta`
    Trả về metadata của bất kỳ file nào trong một gói dưới dạng JSON (ví dụ: `/dist/maplibre-gl.mjs?meta`)

* [https://unpkg.com/maplibre-gl@6.0.0/dist/maplibre-gl.mjs?meta](https://unpkg.com/maplibre-gl@6.0.0/dist/maplibre-gl.mjs?meta)

Kết quả ví dụ cho ra metadata `lastModified` và `size`.

```javascript
{
  "path": "/dist/maplibre-gl.mjs",
  "type": "file",
  "contentType": "application/javascript",
  "lastModified": "...",
  "size": ...
}
```
