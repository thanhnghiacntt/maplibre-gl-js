<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://maplibre.org/img/maplibre-logos/maplibre-logo-for-dark-bg.svg">
    <source media="(prefers-color-scheme: light)" srcset="https://maplibre.org/img/maplibre-logos/maplibre-logo-for-light-bg.svg">
    <img alt="MapLibre Logo" src="https://maplibre.org/img/maplibre-logos/maplibre-logo-for-light-bg.svg" width="200">
  </picture>
</p>

# MapLibre GL JS

[![License](https://img.shields.io/badge/License-BSD_3--Clause-blue.svg?style=flat)](LICENSE.txt) [![Version](https://img.shields.io/npm/v/maplibre-gl?style=flat)](https://www.npmjs.com/package/maplibre-gl) [![CI](https://github.com/maplibre/maplibre-gl-js/actions/workflows/test-all.yml/badge.svg)](https://github.com/maplibre/maplibre-gl-js/actions/workflows/test-all.yml) [![PRs](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat)](https://opensource.org/licenses/BSD-3-Clause) [![codecov](https://codecov.io/gh/maplibre/maplibre-gl-js/branch/main/graph/badge.svg)](https://codecov.io/gh/maplibre/maplibre-gl-js)

**[MapLibre GL JS](https://maplibre.org/maplibre-gl-js/docs/API/)** là một thư viện mã nguồn mở để hiển thị bản đồ trên website hoặc ứng dụng webview. Việc hiển thị bản đồ nhanh có được là nhờ khả năng render vector tile tăng tốc bằng GPU.

Thư viện này bắt nguồn từ một nhánh (fork) mã nguồn mở của [mapbox-gl-js](https://github.com/mapbox/mapbox-gl-js), trước khi Mapbox chuyển sang giấy phép không mã nguồn mở vào tháng 12/2020. Các phiên bản đầu tiên (1.x) được thiết kế để thay thế trực tiếp cho phiên bản OSS của Mapbox (1.x) kèm thêm tính năng mới, nhưng từ đó đến nay đã phát triển thêm rất nhiều.

## Bắt đầu

Thêm file CSS vào phần `<head>` trong file HTML của bạn.

```html
<link href='https://unpkg.com/maplibre-gl@latest/dist/maplibre-gl.css' rel='stylesheet' />
```

Thêm đoạn code sau vào phần `<body>` trong file HTML của bạn.

```html
<div id='map' style='width: 400px; height: 300px;'></div>
<script type='module'>
import * as maplibregl from 'https://unpkg.com/maplibre-gl@latest/dist/maplibre-gl.mjs';

const map = new maplibregl.Map({
  container: 'map',
  style: 'https://demotiles.maplibre.org/style.json', // stylesheet location
  center: [-74.5, 40], // starting position [lng, lat]
  zoom: 9 // starting zoom
});
</script>
```

Vậy là xong, tận hưởng bản đồ của bạn!

<br />

## Tài liệu

Tài liệu đầy đủ cho thư viện này [có tại đây](https://maplibre.org/maplibre-gl-js/docs/API/).

Khám phá các tính năng qua các [ví dụ mẫu](https://maplibre.org/maplibre-gl-js/docs/examples/).

| Ví dụ minh họa                                                                                                              |                                                                                                                            |
| ---------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------- |
| ![Display a map](https://maplibre.org/maplibre-gl-js/docs/assets/examples/display-a-map.png)                           | ![Third party vector tile source](https://maplibre.org/maplibre-gl-js/docs/assets/examples/3d-terrain.png)                 |
| ![Animate a series of images](https://maplibre.org/maplibre-gl-js/docs/assets/examples/animate-a-series-of-images.png) | ![Create a heatmap layer](https://maplibre.org/maplibre-gl-js/docs/assets/examples/create-a-heatmap-layer.png)             |
| ![3D buildings](https://maplibre.org/maplibre-gl-js/docs/assets/examples/display-buildings-in-3d.png)                  | ![Visualize population density](https://maplibre.org/maplibre-gl-js/docs/assets/examples/visualize-population-density.png) |

<br />

Muốn xem thêm ví dụ? Hãy tham khảo [Tài liệu chính thức của MapLibre GL JS](https://maplibre.org/maplibre-gl-js/docs/examples/).

Sử dụng các binding của MapLibre GL JS cho [React](https://visgl.github.io/react-map-gl/docs/get-started) và [Angular](https://github.com/maplibre/ngx-maplibre-gl). Tìm hiểu thêm tại [awesome-maplibre](https://github.com/maplibre/awesome-maplibre).

<br />

## Hiển thị mô hình 3D (OBJ/GLB) và 3D Tiles

MapLibre GL JS không có sẵn loader cho OBJ/GLB hay renderer cho 3D Tiles. Cả hai đều thực hiện được thông qua cơ chế **Custom Layer** (`CustomLayerInterface`), cho phép vẽ trực tiếp vào WebGL context của map bằng ma trận camera mà MapLibre cung cấp.

### 1. Vẽ model OBJ/GLB bằng Three.js + CustomLayerInterface

Tạo một `CustomLayerInterface` với `renderingMode: '3d'`, bên trong dùng Three.js `WebGLRenderer` chia sẻ chung context GL với MapLibre, đồng bộ camera bằng `modelViewProjectionMatrix`.

```js
import * as THREE from 'three';
import { GLTFLoader } from 'three/examples/jsm/loaders/GLTFLoader.js';

const modelOrigin = [lng, lat];
const modelAltitude = 0;
const modelAsMercatorCoordinate = maplibregl.MercatorCoordinate.fromLngLat(
  modelOrigin, modelAltitude
);
const modelTransform = {
  translateX: modelAsMercatorCoordinate.x,
  translateY: modelAsMercatorCoordinate.y,
  translateZ: modelAsMercatorCoordinate.z,
  scale: modelAsMercatorCoordinate.meterInMercatorCoordinateUnits(),
};

const customLayer = {
  id: '3d-model',
  type: 'custom',
  renderingMode: '3d',
  onAdd(map, gl) {
    this.camera = new THREE.Camera();
    this.scene = new THREE.Scene();
    this.scene.add(new THREE.DirectionalLight(0xffffff, 1));

    new GLTFLoader().load('model.glb', (gltf) => {
      this.scene.add(gltf.scene);
    });

    this.renderer = new THREE.WebGLRenderer({
      canvas: map.getCanvas(),
      context: gl, // dùng chung context với MapLibre
      antialias: true,
    });
    this.renderer.autoClear = false;
  },
  render(gl, { modelViewProjectionMatrix }) {
    const m = new THREE.Matrix4().fromArray(modelViewProjectionMatrix);
    const l = new THREE.Matrix4()
      .makeTranslation(modelTransform.translateX, modelTransform.translateY, modelTransform.translateZ)
      .scale(new THREE.Vector3(modelTransform.scale, -modelTransform.scale, modelTransform.scale));

    this.camera.projectionMatrix = m.multiply(l);
    this.renderer.resetState();
    this.renderer.render(this.scene, this.camera);
    map.triggerRepaint();
  },
};

map.on('load', () => map.addLayer(customLayer));
```

Lưu ý: OBJ dùng `OBJLoader` (+ `MTLLoader` nếu có material), GLB/GLTF dùng `GLTFLoader` — cả hai đều nằm trong `three/examples/jsm/loaders/`.

### 2. Hiển thị 3D Tiles

MapLibre core không parse định dạng 3D Tiles (`tileset.json`, `.b3dm`, `.i3dm`...). Cách thực tế và ổn định nhất hiện nay là dùng **deck.gl**:

```js
import { MapboxOverlay } from '@deck.gl/mapbox';
import { Tile3DLayer } from '@deck.gl/geo-layers';
import { Tiles3DLoader } from '@loaders.gl/3d-tiles';

const overlay = new MapboxOverlay({
  interleaved: true,
  layers: [
    new Tile3DLayer({
      id: 'tile-3d-layer',
      data: 'https://.../tileset.json', // Cesium 3D Tiles hoặc I3S
      loader: Tiles3DLoader,
    }),
  ],
});

map.addControl(overlay); // MapboxOverlay tương thích với MapLibre
```

`MapboxOverlay` của `@deck.gl/mapbox` hoạt động được với MapLibre vì MapLibre implement cùng interface mà deck.gl cần. Đây là hướng được cộng đồng MapLibre khuyến nghị vì deck.gl đã có sẵn `Tile3DLayer` xử lý streaming, LOD, culling theo chuẩn Cesium 3D Tiles.

Nếu muốn tự viết renderer 3D Tiles riêng (không phụ thuộc deck.gl) sẽ phức tạp hơn nhiều: phải tự parse `tileset.json`, quản lý LOD/refine, decode `.b3dm` (glTF nhúng trong binary), và tự cull/stream tile theo camera — chỉ nên làm nếu có yêu cầu đặc biệt mà deck.gl không đáp ứng được.

<br />

## Contribution

### Getting Involved

Join the #maplibre slack channel at OSMUS: get an invite at https://slack.openstreetmap.us/
Read the [CONTRIBUTING.md](CONTRIBUTING.md) guide in order to get familiar with how we do things around here.

### Avoid Fragmentation

If you depend on a free software alternative to `mapbox-gl-js`, please consider joining our effort! Anyone with a stake in a healthy community-led fork is welcome to help us figure out our next steps. We welcome contributors and leaders! MapLibre GL JS already represents the combined efforts of a few early fork efforts, and we all benefit from "one project" rather than "our way". If you know of other forks, please reach out to them and direct them here.

> **MapLibre GL JS** is developed following [Semantic Versioning (2.0.0)](https://semver.org/spec/v2.0.0.html).

## Sponsors

We thank everyone who supported us financially in the past and special thanks to the people and organizations who support us with recurring donations!

Read more about the MapLibre Sponsorship Program at [https://maplibre.org/sponsors/](https://maplibre.org/sponsors/).

Gold:

<a href="https://www.microsoft.com/"><img src="https://maplibre.org/img/msft-logo.svg" alt="Logo MSFT" width="25%"/></a>

<a href="https://aws.amazon.com/location"><img src="https://maplibre.org/img/aws-logo.svg" alt="Logo AWS" width="25%"/></a>


Silver:

<a href="https://www.mierune.co.jp/?lang=en"><img src="https://maplibre.org/img/mierune-logo.svg" alt="Logo MIERUNE" width="25%"/></a>

<a href="https://komoot.com/"><img src="https://maplibre.org/img/komoot-logo.svg" alt="Logo komoot" width="25%"/></a>

<a href="https://www.jawg.io/"><img src="https://maplibre.org/img/jawgmaps-logo.svg" alt="Logo JawgMaps" width="25%"/></a>

<a href="https://www.radar.com/"><img src="https://maplibre.org/img/radar-logo.svg" alt="Logo Radar" width="25%"/></a>

<a href="https://www.mapme.com/"><img src="https://maplibre.org/img/mapme-logo.svg" alt="Logo mapme" width="25%"/></a>

<a href="https://www.maptiler.com/"><img src="https://maplibre.org/img/maptiler-logo.svg" alt="Logo maptiler" width="25%"/></a>

<a href="https://www.caltopo.com/"><img src="https://maplibre.org/img/caltopo-logo.svg" alt="Logo Caltopo" width="25%"/></a>

<a href="https://www.caltopo.com/"><img src="https://maplibre.org/img/smartmaps-logo.svg" alt="Logo SmartMaps" width="25%"/></a>

Backers and Supporters:

<a href="https://opencollective.com/maplibre/backer/0/website?requireActive=false" target="_blank"><img src="https://opencollective.com/maplibre/backer/0/avatar.svg?requireActive=false"></a>
<a href="https://opencollective.com/maplibre/backer/1/website?requireActive=false" target="_blank"><img src="https://opencollective.com/maplibre/backer/1/avatar.svg?requireActive=false"></a>
<a href="https://opencollective.com/maplibre/backer/2/website?requireActive=false" target="_blank"><img src="https://opencollective.com/maplibre/backer/2/avatar.svg?requireActive=false"></a>
<a href="https://opencollective.com/maplibre/backer/3/website?requireActive=false" target="_blank"><img src="https://opencollective.com/maplibre/backer/3/avatar.svg?requireActive=false"></a>
<a href="https://opencollective.com/maplibre/backer/4/website?requireActive=false" target="_blank"><img src="https://opencollective.com/maplibre/backer/4/avatar.svg?requireActive=false"></a>
<a href="https://opencollective.com/maplibre/backer/5/website?requireActive=false" target="_blank"><img src="https://opencollective.com/maplibre/backer/5/avatar.svg?requireActive=false"></a>
<a href="https://opencollective.com/maplibre/backer/6/website?requireActive=false" target="_blank"><img src="https://opencollective.com/maplibre/backer/6/avatar.svg?requireActive=false"></a>
<a href="https://opencollective.com/maplibre/backer/7/website?requireActive=false" target="_blank"><img src="https://opencollective.com/maplibre/backer/7/avatar.svg?requireActive=false"></a>
<a href="https://opencollective.com/maplibre/backer/8/website?requireActive=false" target="_blank"><img src="https://opencollective.com/maplibre/backer/8/avatar.svg?requireActive=false"></a>
<a href="https://opencollective.com/maplibre/backer/9/website?requireActive=false" target="_blank"><img src="https://opencollective.com/maplibre/backer/9/avatar.svg?requireActive=false"></a>
<a href="https://opencollective.com/maplibre/backer/10/website?requireActive=false" target="_blank"><img src="https://opencollective.com/maplibre/backer/10/avatar.svg?requireActive=false"></a>
<a href="https://opencollective.com/maplibre/backer/11/website?requireActive=false" target="_blank"><img src="https://opencollective.com/maplibre/backer/11/avatar.svg?requireActive=false"></a>
<a href="https://opencollective.com/maplibre/backer/12/website?requireActive=false" target="_blank"><img src="https://opencollective.com/maplibre/backer/12/avatar.svg?requireActive=false"></a>
<a href="https://opencollective.com/maplibre/backer/13/website?requireActive=false" target="_blank"><img src="https://opencollective.com/maplibre/backer/13/avatar.svg?requireActive=false"></a>
<a href="https://opencollective.com/maplibre/backer/14/website?requireActive=false" target="_blank"><img src="https://opencollective.com/maplibre/backer/14/avatar.svg?requireActive=false"></a>
<a href="https://opencollective.com/maplibre/backer/15/website?requireActive=false" target="_blank"><img src="https://opencollective.com/maplibre/backer/15/avatar.svg?requireActive=false"></a>
<a href="https://opencollective.com/maplibre/backer/16/website?requireActive=false" target="_blank"><img src="https://opencollective.com/maplibre/backer/16/avatar.svg?requireActive=false"></a>
<a href="https://opencollective.com/maplibre/backer/17/website?requireActive=false" target="_blank"><img src="https://opencollective.com/maplibre/backer/17/avatar.svg?requireActive=false"></a>
<a href="https://opencollective.com/maplibre/backer/18/website?requireActive=false" target="_blank"><img src="https://opencollective.com/maplibre/backer/18/avatar.svg?requireActive=false"></a>
<a href="https://opencollective.com/maplibre/backer/19/website?requireActive=false" target="_blank"><img src="https://opencollective.com/maplibre/backer/19/avatar.svg?requireActive=false"></a>
<a href="https://opencollective.com/maplibre/backer/20/website?requireActive=false" target="_blank"><img src="https://opencollective.com/maplibre/backer/20/avatar.svg?requireActive=false"></a>
<a href="https://opencollective.com/maplibre/backer/21/website?requireActive=false" target="_blank"><img src="https://opencollective.com/maplibre/backer/21/avatar.svg?requireActive=false"></a>
<a href="https://opencollective.com/maplibre/backer/22/website?requireActive=false" target="_blank"><img src="https://opencollective.com/maplibre/backer/22/avatar.svg?requireActive=false"></a>
<a href="https://opencollective.com/maplibre/backer/23/website?requireActive=false" target="_blank"><img src="https://opencollective.com/maplibre/backer/23/avatar.svg?requireActive=false"></a>
<a href="https://opencollective.com/maplibre/backer/24/website?requireActive=false" target="_blank"><img src="https://opencollective.com/maplibre/backer/24/avatar.svg?requireActive=false"></a>
<a href="https://opencollective.com/maplibre/backer/25/website?requireActive=false" target="_blank"><img src="https://opencollective.com/maplibre/backer/25/avatar.svg?requireActive=false"></a>
<a href="https://opencollective.com/maplibre/backer/26/website?requireActive=false" target="_blank"><img src="https://opencollective.com/maplibre/backer/26/avatar.svg?requireActive=false"></a>
<a href="https://opencollective.com/maplibre/backer/27/website?requireActive=false" target="_blank"><img src="https://opencollective.com/maplibre/backer/27/avatar.svg?requireActive=false"></a>
<a href="https://opencollective.com/maplibre/backer/28/website?requireActive=false" target="_blank"><img src="https://opencollective.com/maplibre/backer/28/avatar.svg?requireActive=false"></a>
<a href="https://opencollective.com/maplibre/backer/29/website?requireActive=false" target="_blank"><img src="https://opencollective.com/maplibre/backer/29/avatar.svg?requireActive=false"></a>
<a href="https://opencollective.com/maplibre/backer/30/website?requireActive=false" target="_blank"><img src="https://opencollective.com/maplibre/backer/30/avatar.svg?requireActive=false"></a>

<br />

## Thank you Mapbox 🙏🏽

We'd like to acknowledge the amazing work Mapbox has contributed to open source. The open source community is sad to part ways with them, but we simultaneously feel grateful for everything they already contributed. `mapbox-gl-js` 1.x is an open source achievement that now lives on as `maplibre-gl`. We're proud to develop on the shoulders of giants, thank you Mapbox 🙇🏽‍♀️.

Please keep in mind: Unauthorized backports are the biggest threat to the MapLibre project. It is unacceptable to backport code from mapbox-gl-js, which is not covered by the former BSD-3 license. If you are unsure about this issue, [please ask](https://github.com/maplibre/maplibre-gl-js/discussions)!

<br />

## License

**MapLibre GL JS** is licensed under the [3-Clause BSD license](./LICENSE.txt).
