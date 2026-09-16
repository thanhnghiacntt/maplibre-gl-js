# Hướng dẫn di chuyển từ Mapbox

Phần tài liệu này dành riêng cho việc di chuyển (migration) từ `mapbox-gl` sang `maplibre-gl`.

Hướng dẫn này có thể không hoàn toàn chính xác tùy thuộc vào phiên bản `mapbox-gl` bạn đang dùng, nhưng nhìn chung khá đơn giản.

Hai thư viện này rất giống nhau nhưng bắt đầu khác biệt với các tính năng mới xuất hiện từ phiên bản v2 trở đi ở cả hai thư viện, khi Mapbox chuyển sang giấy phép độc quyền (proprietary).

Nhìn chung, việc di chuyển được thực hiện bằng cách gỡ cài đặt `mapbox-gl` và cài đặt `maplibre-gl` trong các package Node của bạn (hoặc xem link CDN bên dưới), sau đó thay thế `mapboxgl` bằng `maplibregl` trong toàn bộ code TypeScript, JavaScript và HTML/CSS của bạn.

```diff
-    var map = new mapboxgl.Map({
+    var map = new maplibregl.Map({

-    <button class="mapboxgl-ctrl">
+    <button class="maplibregl-ctrl">
```

#### Nhánh tương thích (Compatibility branch)

MapLibre GL JS v1 hoàn toàn tương thích ngược với Mapbox GL JS v1. Nhánh tương thích này (có tên 1.x) được gắn tag v1 trên npm, và phiên bản hiện tại của nó là 1.15.3.

#### Link CDN

> MapLibre GL JS được phân phối thông qua [unpkg.com](https://unpkg.com).

```diff
-    <script src="https://api.mapbox.com/mapbox-gl-js/v#.#.#/mapbox-gl.js"></script>
-    <link
-      href="https://api.mapbox.com/mapbox-gl-js/v#.#.#/mapbox-gl.css"
-      rel="stylesheet"
-    />


+    <script type="module">
+      import * as maplibregl from 'https://unpkg.com/maplibre-gl@#.#.#/dist/maplibre-gl.mjs';
+    </script>
+    <link
+      href="https://unpkg.com/maplibre-gl@#.#.#/dist/maplibre-gl.css"
+      rel="stylesheet"
+    />

```

Đừng quên thay thế phiên bản ở trên `#.#.#` bằng phiên bản mà bạn muốn sử dụng.
Bạn có thể tìm số phiên bản mới nhất ở góc trên bên phải của trang này.
</content>
