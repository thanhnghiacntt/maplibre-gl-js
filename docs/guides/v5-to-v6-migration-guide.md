# Hướng dẫn di chuyển từ v5 sang v6

MapLibre GL JS v6 chỉ được phân phối dưới dạng ES module. Bundle UMD, bản build CSP riêng, và entry CommonJS (`require('maplibre-gl')`) từ v5 đều đã bị loại bỏ. File bundle giờ đây là `maplibre-gl.mjs` (và `maplibre-gl-worker.mjs`). Nếu công cụ build hoặc test runner của bạn vẫn dùng `require()` (các script Node thuần, test runner không transform ESM, code phía server import package mà không qua bundler), lỗi sẽ xuất hiện dưới dạng `ERR_PACKAGE_PATH_NOT_EXPORTED`.

## Import

Nếu bạn import maplibre-gl từ npm bằng **named imports** (`import {Map} from 'maplibre-gl'`), các import của bạn vẫn hoạt động bình thường: v6 sẽ tự động phân giải về bundle ESM.

Nếu bạn dùng **default import** (`import maplibregl from 'maplibre-gl'`), hãy chuyển sang named import hoặc namespace import:

```ts
// before
import maplibregl from 'maplibre-gl';

// after
import * as maplibregl from 'maplibre-gl';
// or pull in just what you need
import {Map, setWorkerUrl} from 'maplibre-gl';
```

## Thẻ `<script>`

Nếu bạn tải maplibre-gl thông qua `<script src>`, hãy chuyển sang dùng module script:

```html
<!-- before -->
<script src="https://unpkg.com/maplibre-gl@^5/dist/maplibre-gl.js"></script>

<!-- after -->
<script type="module">
    import * as maplibregl from 'https://unpkg.com/maplibre-gl@^6.0.0/dist/maplibre-gl.mjs';
</script>
```

Hãy ghim (pin) một phiên bản major cụ thể (ví dụ ^6.0.0) thay vì dùng `@latest` hoặc không chỉ định phiên bản. Kể từ v6, một trang ghim vào `@latest` sẽ hiển thị màn hình xám trống với lỗi 404 trong console.

## `setWorkerUrl()` chỉ dành cho bundler

Với ESM trực tiếp trên trình duyệt (tải từ CDN như unpkg thông qua thẻ `<script type="module">`), worker URL được tự động phát hiện từ `import.meta.url` và được chuyển đổi qua một Blob URL cùng origin khi cần, nên không cần gọi [`setWorkerUrl()`](../API/functions/setWorkerUrl.md).

Với các bundler (Vite, webpack, esbuild, rspack, Rollup), `import.meta.url` không luôn phân giải chính xác đến file worker bên trong module graph của bundler, nên mỗi ứng dụng vẫn cần gọi `setWorkerUrl()` một lần. Xem [Installation](../index.md#installation) để biết đoạn code mẫu cho từng bundler.

## Các chỉ thị CSP

Bundle CSP riêng biệt từ v5 không còn cần thiết nữa.

Nếu bạn tải MapLibre từ một CDN khác origin với trang của bạn (ví dụ unpkg), worker được tạo từ một Blob URL cùng origin, nên CSP của bạn cần cho phép `blob:` trong `worker-src`:

```
worker-src 'self' blob: ;
img-src data: blob: 'self' ;
```

Nếu bạn tự host file worker (với bất kỳ cấu hình bundler nào), worker URL sẽ cùng origin và không cần `blob:`:

```
worker-src 'self' ;
img-src data: blob: 'self' ;
```

## zoomLevelsToOverscale

Trong phiên bản 5 có một tham số thử nghiệm (experimental) được thêm vào để cho phép cắt (slicing) vector tile thay vì overscale chúng.
Chúng tôi đã thử nghiệm và nhận thấy nó khắc phục được khá nhiều vấn đề về labeling (đặt nhãn), v.v.
Tham số này thay đổi cách render và kết quả của queryRenderedFeatures.
Nếu bạn muốn quay lại hành vi trước đây, có thể đặt `zoomLevelsToOverscale: undefined` khi khởi tạo bản đồ.

## Property GeoJSON lồng nhau (Nested)

Các object và array lồng nhau trong property của feature GeoJSON giờ đây được giữ nguyên: các feature trả về từ event và `queryRenderedFeatures` chứa chúng dưới dạng object thực sự thay vì chuỗi JSON. Nếu bạn từng gọi `JSON.parse` trên các property này, hãy loại bỏ nó — vì giờ đây nó sẽ ném ra lỗi `SyntaxError: "[object Object]" is not valid JSON`.

```diff
-const info = JSON.parse(e.features[0].properties.info);
+const info = e.features[0].properties.info;
```

## pragma mapbox

Nếu bạn đang sử dụng `#pragma mapbox` trong code dùng chung (shared code), hãy thay thế bằng `#pragma maplibre`.
```diff
-#pragma mapbox
+#pragma maplibre
```

## Sự kiện (Events)

Tất cả các event giờ đây đều là class; khuyến nghị không nên dùng `instanceof` mà thay vào đó kiểm tra trường `type`. Vì thay đổi này chỉ chuyển từ type sang class nên hầu hết các codebase sẽ không gặp vấn đề gì.

### styleimagemissing

Trong v6, các listener `styleimagemissing` không còn có thể resolve yêu cầu ảnh hiện tại bằng cách gọi `Map#addImage` nữa. Để di chuyển một listener chuyên cung cấp ảnh còn thiếu, hãy thay thế nó bằng [`Map#setMissingStyleImageResolver`](../API/classes/Map.md#setmissingstyleimageresolver):

```diff
-map.on('styleimagemissing', ({id}) => {
+map.setMissingStyleImageResolver((id) => {
     map.addImage(id, generateImage(id));
 });
```

Resolver có thể đồng bộ (synchronous) hoặc bất đồng bộ (asynchronous). Với việc tải bất đồng bộ, hãy gọi `Map#addImage` trước khi promise của resolver hoàn tất (settle). Sự kiện `styleimagemissing` vẫn có thể được dùng để theo dõi các ảnh chưa được resolve.

## WebGL2 giờ đây là bắt buộc

Hỗ trợ WebGL1 đã bị loại bỏ; giờ đây WebGL2 là bắt buộc. Trình duyệt hoặc thiết bị không hỗ trợ WebGL2 sẽ không thể render bản đồ với v6. Khi WebGL2 không khả dụng, constructor `Map` sẽ ném ra lỗi `GPUInitializationError` (kiểm tra bằng `instanceof GPUInitializationError`, được export từ `maplibre-gl`) thay vì trả về một map.

## `map.transform` đã bị loại bỏ

Property nội bộ `map.transform` đã bị loại bỏ; giờ đây `Map` compose (kết hợp) một `Camera` thay vì extend (kế thừa) nó. Hãy dùng public API của `Map` thay vì truy cập trực tiếp vào `transform`. Nếu bạn phụ thuộc vào điều gì đó mà `transform` từng cung cấp nhưng không có trong public API, vui lòng mở một issue hoặc PR.
</content>
