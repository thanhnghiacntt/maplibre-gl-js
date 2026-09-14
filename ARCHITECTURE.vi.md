# Kiến trúc của MapLibre GL JS

## `Map` và các hệ thống con của nó

## Phân chia main thread / worker

## Cách hoạt động của việc render (vector tile)

### Parsing và layout

Vector tile được fetch và parse trên các WebWorker thread. "Parsing" một vector tile bao gồm:

 - Deserializing source layer, feature property, và feature geometry từ PBF. Việc này được xử lý bởi thư viện [`vector-tile-js`](https://github.com/mapbox/vector-tile-js).
 - Biến đổi dữ liệu đó thành dữ liệu _sẵn sàng để render_ (render-ready) mà WebGL shader có thể dùng để vẽ bản đồ. Chúng ta gọi quá trình này là "layout", và nó được thực hiện bởi `WorkerTile`, các class `Bucket`, và `ProgramConfiguration`.
 - Lập chỉ mục (indexing) các feature geometry vào một `FeatureIndex`, dùng cho các truy vấn không gian (ví dụ `queryRenderedFeatures`).

`WorkerTile#parse()` nhận vào một vector tile (đã deserialize), fetch thêm các tài nguyên nếu cần (font, image), rồi tạo một `Bucket` cho mỗi "họ" (family) các style layer dùng chung feature và các thuộc tính 'layout' (xem `group_by_layout.js`).

[Bucket](./src/data/bucket.ts) là điểm duy nhất nắm giữ toàn bộ tri thức về việc chuyển đổi vector tile thành các WebGL buffer. Mỗi bucket giữ dữ liệu mảng đỉnh (vertex) và mảng phần tử (element) cần thiết để render nhóm style layer của nó (xem [ArrayGroup](./src/data/bucket.ts)). Từng loại bucket cụ thể biết cách điền dữ liệu đó cho loại layer tương ứng của mình.

### Render bằng WebGL

Sau khi dữ liệu bucket đã được chuyển sang main thread, nó trông như thế này:

```
Tile
  |
  +- buckets[layer-id]: Bucket
  |    |
  |    + ArrayGroup {
  |        globalProperties: { zoom }
  |        layoutVertexArray,
  |        indexArray,
  |        indexArray2,
  |        layerData: {
  |          [style layer id]: {
  |            programConfiguration,
  |            paintVertexArray,
  |            paintPropertyStatistics
  |          }
  |          ...
  |        }
  |    }
  |
  +- buckets[...]: Bucket
        ...
```
_Lưu ý rằng một bucket cụ thể có thể xuất hiện nhiều lần trong `tile.buckets` — mỗi lần cho một layer trong một "họ" (family) layout nhất định._

 - Việc render diễn ra theo từng style layer, trong `Painter#renderPass()`, hàm này ủy quyền cho các method `drawXxxx()` đặc thù theo layer trong `src/render/draw_*.js`.
 - Các method `drawXxxx()`, đến lượt mình, render một layer theo từng tile, bằng cách:
   - Lấy một shader program đã được cấu hình sẵn thuộc tính từ `Painter`
   - Thiết lập các giá trị _uniform_ dựa trên thuộc tính của style layer
   - Bind dữ liệu buffer layout (thông qua `BufferGroup`) và gọi `gl.drawElements()`

Việc biên dịch và cache các GL shader program được quản lý bởi các class `Painter` và `ProgramConfiguration`. Cụ thể, một instance của `ProgramConfiguration` xử lý, cho một cặp (tile, style layer) nhất định:

 - Mở rộng một câu lệnh `#pragma maplibre` trong mã nguồn shader của chúng ta thành khai báo biến _uniform_ hoặc _attribute_, _varying_ và biến _local_, tùy thuộc vào việc thuộc tính style liên quan có phải là data-driven hay không.
 - Tạo và điền dữ liệu cho một _paint_ vertex array cho các thuộc tính data-driven, tương ứng với các `attributes` được khai báo trong shader. (Việc này xảy ra ở thời điểm layout, phía worker.)

## TileManager

## Transform

## Controls
