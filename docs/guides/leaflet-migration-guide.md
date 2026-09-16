# Hướng dẫn di chuyển từ Leaflet

Phần tài liệu này dành riêng cho việc di chuyển (migration) từ `leaflet` sang `maplibre-gl`.

Hướng dẫn này có thể không hoàn toàn chính xác tùy thuộc vào phiên bản `leaflet` bạn đang sử dụng.

Khác biệt chính về mặt chức năng là khả năng hỗ trợ xoay bản đồ (map rotation), vector tile và chế độ globe (quả địa cầu). Với các tập dữ liệu lớn, MapLibre nhanh hơn nhờ sử dụng công nghệ WebGL.

## Thiết lập MapLibre

Cài đặt MapLibre GL JS và thay thế Leaflet bằng MapLibre trong dự án của bạn:

```
npm install maplibre-gl
```

## Khởi tạo bản đồ

### Leaflet

```js
const map = L.map('map').setView([0, 0], 2);

L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
  attribution: '&copy; OpenStreetMap contributors'
}).addTo(map);
```

### MapLibre

```js
import 'maplibre-gl/dist/maplibre-gl.css';
import {Map} from 'maplibre-gl';

const map = new Map({
  container: 'map',
  style: 'https://demotiles.maplibre.org/style.json',
  center: [0, 0],
  zoom: 2
});
```

## Thêm Marker

### Leaflet

```js
L.marker([0, 0]).addTo(map);
```

### MapLibre

```js
new maplibregl.Marker()
  .setLngLat([0, 0])
  .addTo(map);
```

## Thêm GeoJSON Layer

### Leaflet

```js
L.geoJSON('data.geojson').addTo(map);
```

### MapLibre

```js
map.on('load', function () {
  map.addSource('geojson-source', {
    type: 'geojson',
    data: 'data.geojson',
  });

  map.addLayer({
    id: 'geojson-layer',
    type: 'fill',
    source: 'geojson-source',
    paint: {
      'fill-color': '#0080ff',
      'fill-opacity': 0.5,
    },
  });
});
```

## Xử lý sự kiện Click

### Leaflet

```js
map.on('click', function (event) {
  console.log('Clicked coordinates:', event.latlng);
});
```

### MapLibre

```js
map.on('click', function (event) {
  console.log('Clicked coordinates:', event.lngLat);
});
```

## Hiển thị Popup

### Leaflet

```js
L.popup()
  .setLatLng([0, 0])
  .setContent('Hello, Leaflet!')
  .openOn(map);
```

### MapLibre

```js
new maplibregl.Popup()
  .setLngLat([0, 0])
  .setHTML('<p>Hello, MapLibre!</p>')
  .addTo(map);
```

## Thêm Custom Tile Layer

### Leaflet

```js
L.tileLayer('https://tile.openstreetmap.org/{z}/{x}/{y}.png').addTo(map);
```

### MapLibre

```js
map.on('load', function () {
  map.addSource('osm', {
    type: 'raster',
    tiles: ['https://tile.openstreetmap.org/{z}/{x}/{y}.png'],
    tileSize: 256
  });

  map.addLayer({
    id: 'osm-layer',
    type: 'raster',
    source: 'osm',
  });
});
```

## Thêm Polygon

### Leaflet

```js
L.polygon([
  [51.5, -0.1],
  [51.5, -0.12],
  [51.52, -0.12]
]).addTo(map);
```

### MapLibre

```js
map.on('load', function () {
  map.addSource('polygon', {
    type: 'geojson',
    data: {
      type: 'Feature',
      geometry: {
        type: 'Polygon',
        coordinates: [[[ -0.1, 51.5 ], [ -0.12, 51.5 ], [ -0.12, 51.52 ], [ -0.1, 51.5 ]]]
      }
    }
  });

  map.addLayer({
    id: 'polygon-layer',
    type: 'fill',
    source: 'polygon',
    paint: {
      'fill-color': '#ff0000',
      'fill-opacity': 0.5
    }
  });
});
```
</content>
