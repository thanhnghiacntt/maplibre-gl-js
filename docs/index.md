# Giới thiệu

MapLibre GL JS là một thư viện TypeScript sử dụng WebGL để hiển thị bản đồ tương tác từ vector tile trong trình duyệt.
Giao diện của bản đồ được điều khiển bởi một tài liệu style (style document), có cấu trúc và thuộc tính được định nghĩa bởi [MapLibre Style Spec](https://maplibre.org/maplibre-style-spec).
Đây là một phần của hệ sinh thái MapLibre, có phiên bản tương ứng cho Android, iOS và các nền tảng khác gọi là [MapLibre Native](https://github.com/maplibre/maplibre-native).

## Bắt đầu nhanh

<iframe src="./examples/display-a-globe-with-a-vector-map.html" width="100%" height="400px" style="border:none"></iframe>

```html
<link rel="stylesheet" href="https://unpkg.com/maplibre-gl@^6.3.0/dist/maplibre-gl.css" />
<div id="map" style="height: 400px"></div>
<script type="module">
    import * as maplibregl from 'https://unpkg.com/maplibre-gl@^6.3.0/dist/maplibre-gl.mjs';

    const map = new maplibregl.Map({
        container: 'map', // container id
        style: 'https://demotiles.maplibre.org/globe.json', // style URL
        center: [0, 0], // starting position [lng, lat]
        zoom: 2 // starting zoom
    });
</script>
```

## Đọc tài liệu này

Tài liệu này được chia thành nhiều phần:

* [**Main**](./API/README.md) - Phần Main (Chính) chứa các lớp sau
    * Đối tượng [`Map`](./API/classes/Map.md) chính là bản đồ trên trang của bạn. Nó cho phép bạn truy cập các phương thức và thuộc tính để tương tác với style và layer của bản đồ, phản hồi sự kiện, và điều chỉnh góc nhìn của người dùng thông qua camera.
    * [`Global Functions`](./API/functions/addProtocol.md) (các hàm toàn cục) cho phép bạn thiết lập các thuộc tính và tùy chọn toàn cục mà bạn có thể cần truy cập khi khởi tạo bản đồ hoặc lấy thông tin về trạng thái của nó.
* [**Markers and Controls**](./API/README.md#markers-and-controls) (Marker và Control) - Phần này mô tả các thành phần giao diện người dùng mà bạn có thể thêm vào bản đồ. Các mục trong phần này tồn tại bên ngoài phần tử `canvas` của bản đồ. Bao gồm `Marker`, `Popup` và tất cả các control.
* [**Geography and geometry**](./API/README.md#geography-and-geometry) (Địa lý và hình học) - Phần này bao gồm các tiện ích và kiểu dữ liệu chung liên quan đến việc làm việc và thao tác với thông tin địa lý hoặc hình học.
* [**User interaction handlers**](./API/README.md#handlers) (Trình xử lý tương tác người dùng) - Các mục trong phần này liên quan đến cách bản đồ phản hồi lại thao tác của người dùng.
* [**Sources**](./API/README.md#sources) (Nguồn dữ liệu) - Phần này mô tả các loại source mà MapLibre GL JS có thể xử lý, bên cạnh những loại đã được mô tả trong [MapLibre Style Specification](https://maplibre.org/maplibre-style-spec/).
* [**Event Related**](./API/README.md#event-related) (Liên quan đến sự kiện) - Phần này mô tả các loại sự kiện khác nhau mà MapLibre GL JS có thể phát sinh.

Mỗi phần mô tả các lớp hoặc đối tượng cùng với **properties** (thuộc tính), **parameters** (tham số), **instance members** (thành viên instance), và các **events** (sự kiện) liên quan. Nhiều phần cũng bao gồm ví dụ code trực tiếp và các tài nguyên liên quan.

Trong các ví dụ, chúng tôi sử dụng vector tile từ [Demo tiles repository](https://github.com/maplibre/demotiles) của chúng tôi và từ [MapTiler](https://maptiler.com). Hãy lấy API key riêng nếu bạn muốn dùng dữ liệu MapTiler trong dự án của mình.

## npm

Cài đặt package MapLibre GL JS thông qua [npm](https://www.npmjs.com/package/maplibre-gl).

```bash
npm install maplibre-gl
```

Sau đó bạn có thể import module MapLibre GL JS vào dự án của mình.

```html
<div id="map"></div>
```

```javascript
import {Map} from 'maplibre-gl';
import 'maplibre-gl/dist/maplibre-gl.css';

const map = new Map({
    container: 'map', // container id
    style: 'https://demotiles.maplibre.org/globe.json', // style URL
    center: [0, 0], // starting position [lng, lat]
    zoom: 1 // starting zoom
});
```

Xem phần [ESM](#esm) bên dưới để thiết lập worker URL với bundler của bạn.

## ESM

MapLibre GL JS v6 chỉ được phân phối dưới dạng ES module (`maplibre-gl.mjs`). Trường `"module"` trong `package.json` trỏ đến bundle ESM, nên các bundler sẽ tự động nhận diện.

Để xem các ứng dụng chạy được tối thiểu cho từng bundler (Vite, webpack, esbuild, Rollup, Turbopack), xem [`test/integration/bundler/`](https://github.com/maplibre/maplibre-gl-js/tree/main/test/integration/bundler).

Đang nâng cấp từ v5? Xem [hướng dẫn di chuyển từ v5 sang v6](./guides/v5-to-v6-migration-guide.md).

### Cài đặt

Chọn cách thiết lập phù hợp với bạn:

=== "Vite"

    Sử dụng query `?worker&url` của Vite để lấy một worker URL đã được đóng gói (bundle), độc lập (self-contained):

    ```ts
    import {Map, setWorkerUrl} from 'maplibre-gl';
    import 'maplibre-gl/dist/maplibre-gl.css';
    import workerUrl from 'maplibre-gl/dist/maplibre-gl-worker.mjs?worker&url';

    setWorkerUrl(workerUrl);

    const map = new Map({/* … */});
    ```

    Hãy dùng `?worker&url` thay vì `?url` thông thường: worker trong bản dist import file
    `maplibre-gl-shared.mjs` đi kèm, và `?url` sẽ xuất ra file worker nguyên bản trong các
    bản build production mà không kèm theo file đó — khi đó worker sẽ lỗi ngay lần import
    đầu tiên và không có vector tile nào được tải. `?worker&url` sẽ định tuyến file qua
    pipeline worker của Vite, tạo ra một chunk độc lập. Ở chế độ dev, cả hai cách đều
    hoạt động được.

    Nếu bản build của bạn sử dụng SSR (TanStack Start, Astro, v.v.) và Vite phân giải entry CommonJS ở phía server, hãy thêm:

    ```ts title="vite.config.ts"
    export default defineConfig({
        ssr: {noExternal: ['maplibre-gl']}
    });
    ```

=== "webpack 5+"

    ```ts
    import {Map, setWorkerUrl} from 'maplibre-gl';
    import 'maplibre-gl/dist/maplibre-gl.css';

    setWorkerUrl(new URL('maplibre-gl/dist/maplibre-gl-worker.mjs', import.meta.url).toString());

    const map = new Map({/* … */});
    ```

    rspack và rsbuild sử dụng cùng cách làm này.

    Next.js là một ngoại lệ, kể cả ở chế độ `next build --webpack`. Xem tab Turbopack.

=== "esbuild"

    ```js title="build.js"
    import * as esbuild from 'esbuild';
    import {copyFileSync} from 'fs';

    await esbuild.build({
        entryPoints: ['src/main.ts'],
        bundle: true,
        outdir: 'dist',
        format: 'esm'
    });

    copyFileSync(
        'node_modules/maplibre-gl/dist/maplibre-gl-worker.mjs',
        'dist/maplibre-gl-worker.mjs'
    );
    ```

    ```ts title="src/main.ts"
    import {Map, setWorkerUrl} from 'maplibre-gl';
    import 'maplibre-gl/dist/maplibre-gl.css';

    setWorkerUrl(new URL('./maplibre-gl-worker.mjs', import.meta.url).toString());

    const map = new Map({/* … */});
    ```

=== "Rollup"

    ```ts title="rollup.config.js"
    import copy from 'rollup-plugin-copy';

    export default {
        plugins: [
            copy({
                targets: [
                    {src: 'node_modules/maplibre-gl/dist/maplibre-gl-worker.mjs', dest: 'dist'}
                ]
            }),
            /* ... */
        ]
    };
    ```

    ```ts title="src/main.ts"
    import {Map, setWorkerUrl} from 'maplibre-gl';
    import 'maplibre-gl/dist/maplibre-gl.css';

    setWorkerUrl(new URL('./maplibre-gl-worker.mjs', import.meta.url).toString());

    const map = new Map({/* … */});
    ```

=== "Turbopack"

    Turbopack là bundler mặc định trong Next.js — đây cũng là nơi bạn nhiều khả năng gặp nó nhất, nên phần thiết lập dưới đây được viết cho một ứng dụng Next.js.

    Turbopack biến `new URL('maplibre-gl/dist/maplibre-gl-worker.mjs', import.meta.url)` thành một asset có hash mà không xuất kèm file `maplibre-gl-shared.mjs` đi cùng worker. Khi đó worker sẽ lỗi ngay lần import đầu tiên, bản đồ vẫn mount được nhưng không bao giờ gửi yêu cầu tải tile. Thay vào đó, hãy phục vụ cả hai file từ thư mục `public/` và trỏ `setWorkerUrl` đến worker:

    ```js title="scripts/copy-maplibre-worker.mjs"
    import {copyFileSync, mkdirSync} from 'node:fs';
    import {createRequire} from 'node:module';
    import path from 'node:path';

    const dist = path.join(path.dirname(createRequire(import.meta.url).resolve('maplibre-gl/package.json')), 'dist');
    const dest = path.join(process.cwd(), 'public', 'maplibre');

    mkdirSync(dest, {recursive: true});
    for (const file of ['maplibre-gl-worker.mjs', 'maplibre-gl-shared.mjs']) {
        copyFileSync(path.join(dist, file), path.join(dest, file));
    }
    ```

    ```json title="package.json"
    {
        "scripts": {
            "prebuild": "node ./scripts/copy-maplibre-worker.mjs",
            "predev": "node ./scripts/copy-maplibre-worker.mjs"
        }
    }
    ```

    ```ts title="app/map.tsx"
    'use client';

    import {Map, setWorkerUrl} from 'maplibre-gl';
    import 'maplibre-gl/dist/maplibre-gl.css';

    setWorkerUrl('/maplibre/maplibre-gl-worker.mjs');

    const map = new Map({/* … */});
    ```

    Script này copy cả hai file, không chỉ riêng worker.
    Lý do là vì worker import `maplibre-gl-shared.mjs` bằng đường dẫn tương đối, nên cả hai file phải nằm cùng một thư mục.

    Việc copy diễn ra tại thời điểm build, lấy từ `node_modules`, nên luôn khớp với phiên bản đã cài đặt.
    Các tiền tố lifecycle của npm khớp chính xác với tên script, nên `prebuild` và `predev` sẽ chạy trước `build` và `dev`, nhưng **không** chạy trước một script tùy chỉnh như `build:local` - nếu cần, hãy thêm hook `pre` tương ứng cho các script đó.
    Chỉ dùng `postinstall` thôi thì chưa đủ, vì trình quản lý package sẽ bỏ qua lifecycle script khi việc cài đặt không có gì thay đổi, và `--ignore-scripts` sẽ bỏ qua chúng hoàn toàn.

    Next.js cần thiết lập này ở cả hai chế độ bundler của nó, `next build` (Turbopack) và `next build --webpack`, vì cách xử lý asset nêu trên là do Next.js quyết định chứ không chỉ riêng Turbopack.

=== "CDN / No bundler"

    Tải MapLibre trực tiếp từ UNPKG dưới dạng ES module thông qua thẻ `<script type="module">`. Xem [unpkg.com](https://unpkg.com) để biết hướng dẫn chọn phiên bản cụ thể và dải semver.

    ```html
    <link rel="stylesheet" href="https://unpkg.com/maplibre-gl@^6.3.0/dist/maplibre-gl.css" />
    <div id="map" style="height: 400px"></div>
    <script type="module">
        import * as maplibregl from 'https://unpkg.com/maplibre-gl@^6.3.0/dist/maplibre-gl.mjs';

        const map = new maplibregl.Map({
            container: 'map',
            style: 'https://demotiles.maplibre.org/style.json',
            center: [0, 0],
            zoom: 1
        });
    </script>
    ```

    Worker được tự động phát hiện từ URL của module đã import, và được chuyển đổi qua một Blob URL cùng origin, nên việc tải từ CDN khác origin hoạt động được ngay mà không cần cấu hình thêm.

    Trong trường hợp CSP nghiêm ngặt không cho phép `blob:` trong `worker-src`, hãy đặt worker URL một cách tường minh về một vị trí cùng origin:

    ```js
    maplibregl.setWorkerUrl('/path/to/maplibre-gl-worker.mjs');
    ```

    Xem ví dụ [Display a map](./examples/display-a-map.md) để có phiên bản chạy được đầy đủ.

## Các chỉ thị CSP

Để giảm thiểu nguy cơ Cross-Site Scripting và các lỗ hổng bảo mật web khác, bạn có thể sử dụng [Content Security Policy (CSP)](https://developer.mozilla.org/en-US/docs/Web/Security/CSP) để chỉ định các chính sách bảo mật cho website của mình. Nếu làm vậy, MapLibre GL JS yêu cầu các chỉ thị CSP sau:

```
worker-src 'self' ;
img-src data: blob: 'self' ;
```

## CSS của MapLibre

CSS được nhắc đến trong phần Bắt đầu nhanh dùng để tạo style cho các phần tử DOM do MapLibre tạo ra. Nếu thiếu CSS này, các phần tử như Popup và Marker sẽ không hoạt động đúng.

Việc thêm CSS bằng thẻ `<link>` trong phần head của tài liệu thông qua UNPKG CDN là cách đơn giản và dễ dàng nhất để cung cấp CSS, nhưng CSS này cũng đã được đóng gói sẵn trong module MapLibre — nghĩa là nếu bạn có một bundler hỗ trợ xử lý CSS, bạn có thể import CSS trực tiếp từ `maplibre-gl/dist/maplibre-gl.css`.

Cũng lưu ý rằng nếu CSS chưa sẵn sàng tại lần render đầu tiên, thì ngay khi CSS được cung cấp, các phần tử DOM phụ thuộc vào CSS này sẽ tự khôi phục lại đúng giao diện.
</content>
