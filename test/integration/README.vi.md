Các integration test này kiểm tra tính đúng đắn và nhất quán của [maplibre-gl-js](https://github.com/maplibre/maplibre-gl-js) và
[maplibre-gl-native](https://github.com/maplibre/maplibre-gl-native) trong việc render.

## Tổ chức

Các test được chứa trong một cây thư mục, thường được tổ chức theo thuộc tính của [style specification](https://maplibre.org/maplibre-style-spec/): `background-color`, `line-width`, v.v., với một cấp thư mục thứ hai bên dưới đó cho từng test riêng lẻ. Ví dụ, test cho việc chỉ định một giá trị literal `circle-radius` nằm tại [`test/integration/render/tests/circle-radius/literal/`](./render/tests/circle-radius/literal).

Bên trong một thư mục lá (leaf directory) là một file `style.json` (ví dụ [`circle-radius/literal/style.json`](./render/tests/circle-radius/literal/style.json)), chứa style tối thiểu cần thiết cho test case đó. Style có thể chỉ định kích thước bản đồ, tâm, bearing, và pitch, cùng với metadata bổ sung của test (ví dụ: kích thước hình ảnh đầu ra).

Đầu ra mong đợi cho một test case nhất định nằm trong `expected.png`, ví dụ [`circle-radius/literal/expected.png`](./render/tests/circle-radius/literal/expected.png).
Có thể có nhiều file với tiền tố `expected` vì đầu ra có thể khác nhau đôi chút giữa các nền tảng.

Các file hỗ trợ -- glyph, sprite, và tile -- nằm trong các thư mục con tương ứng của thư mục [`test/integration/assets`](./assets). Test harness thiết lập môi trường sao cho các request đến những tài nguyên này được chuyển hướng đến đúng vị trí. Ví dụ, các hình ảnh trong thư mục con `assets/tiles` có thể được tham chiếu bằng `"local://tiles/{z}-{x}-{y}.satellite.png"` trong file `style.json`.

Nội dung của các vector tile fixture có thể được đọc bằng công cụ [`vt2geojson`](https://github.com/mapbox/vt2geojson) (xem bên dưới).

## Chạy test trên GitHub

Tất cả các test được chạy cho mỗi PR. Nếu bạn chưa chắc test đã ổn hay chưa, bạn có thể dùng Draft PR để cho biết công việc vẫn đang trong quá trình thực hiện.
Mỗi job, hay một nhóm test, sẽ tạo ra một artifact nếu có bất kỳ test nào trong đó thất bại. Các artifact này nằm ở cuối phần tổng kết (summary) của job.

<img width="80%" src="https://github.com/maplibre/maplibre-gl-js/assets/1304610/bc313a30-cdec-4de5-b6c9-90637ffbf79a" alt="" />

Tải artifact tương ứng về dưới dạng file zip, mở ra và xem file `results.html` bên trong.
Hình ảnh "Actual" của một test thất bại có thể được lưu lại và dùng làm hình ảnh "Expected" mới.

## Chạy test trong môi trường phát triển

Để chạy các render test:

```sh
npm run test-render
```

Mặc định các render test chạy lần lượt từng test một, nhưng nếu bạn có nhiều nhân CPU, bạn có thể thêm concurrency bằng:

```sh
RENDER_TEST_CONCURRENCY=4 npm run test-render
```

Để chạy các integration test (ngoại trừ render test):

```sh
npm run test-integration
```

Lệnh này bao gồm cả các browser test.

Để chạy các build test

```
npm run test-build
```

Để chạy một tập con của test, bạn có thể dùng các filter của vitest, ví dụ

```
npm run test-integration -- browser
```

Ngoài ra, việc sử dụng giao diện trực quan ([Vitest UI](https://vitest.dev/guide/ui.html)) có thể hữu ích. Giao diện này có thể được khởi động bằng cách thay `run` bằng `--ui` trong package.json:

```diff
- "test-unit": "vitest run --config vitest.config.unit.ts",
+ "test-unit": "vitest --ui --config vitest.config.unit.ts",
```


### Thông báo debug chi tiết cho render test

Render test được thực thi trong trình duyệt, và mặc định các console message bị ẩn. Nếu một test thất bại, nó sẽ tự động thử lại với console được bật.

### Xem kết quả render test

Trong lúc chạy render test, test harness sẽ dùng puppeteer để điều khiển một trình duyệt thật và tạo ra một hình ảnh `actual.png` từ `style.json` đã cho, sau đó sử dụng [pixelmatch](https://github.com/mapbox/pixelmatch) để so sánh hình ảnh đó với `expected.png`, sinh ra một `diff.png` tô đỏ các pixel không khớp (nếu có).

Mặc định các render test sinh báo cáo trong thư mục <code>./test/integration/render/</code>:
```
npm run test-render
...
Results logged to './test/integration/render/results.html'
```
...bạn có thể xem kết quả một cách trực quan bằng cách mở file `results.html` do harness sinh ra:

```
open ./test/integration/render/results.html
```

### Cập nhật kết quả render test

Lưu ý rằng CI đang chạy các render test. Nếu chúng thất bại, `report.html` sẽ được upload dưới dạng artifact. File này có thể được tải xuống, mở trong trình duyệt và bằng cách click chuột phải - lưu hình ảnh, kết quả render test thực tế từ CI có thể được lưu lại làm hình ảnh expected.

Để thực hiện việc này thủ công, bạn có thể dùng các lệnh sau
Trên Linux:
```
xvfb-run -a UPDATE=true npm run test-render
```
Trên Mac:
```
UPDATE=true npm run test-render
```
Hoặc trên Windows với PowerShell:
```
$env:UPDATE=$true; npm run test-render
```

#### Ghi chú về các integration test truy vấn (query)

Trong test/integration/browser/browser.test.ts, một web server được tự động khởi động để phục vụ các static asset từ thư mục integration. Để tự khởi động một server tương tự thủ công, dùng `npm run start`.

Hiện tại chúng ta chạy mỗi test trong một tab mới. Một cách khác là chúng ta có thể tăng tốc bằng cách xóa webgl context thay vì vậy, và chạy mọi thứ trong một tab.

```
delete map.painter.context.gl;
```

Đầu ra của mỗi test là true/false, cho biết đầu ra mong đợi và đầu ra thực tế có bằng nhau hoàn toàn (deep equality) hay không. Để có đầu ra test tốt hơn, chúng ta có thể dùng:

```
generateDiffLog(fixture.expected, actual);
```

## Chạy test trong trình duyệt

Query test có thể được chạy trong trình duyệt, server phục vụ trang test và các fixture test sẽ khởi động khi bạn chạy
```
npm run start
```

### Chạy các test cụ thể

Một filter có thể được chỉ định bằng cách dùng query param `filter` trong url. Ví dụ, thêm
```
?filter=circle-pitch
```
vào cuối url sẽ chỉ chạy các test có chứa `circle-pitch` trong tên.

### Thông báo Build

Cửa sổ terminal có thể trở nên rất ồn ào khi cả build server và test server cùng chạy trong một session. Vì vậy server sử dụng thông báo của nền tảng (platform notification) để báo khi build đã hoàn tất. Nếu hành vi này gây phiền, nó có thể được tắt bằng cách thiết lập biến môi trường sau
```
DISABLE_BUILD_NOTIFICATIONS=true
```

## Viết test mới

_Lưu ý: Kết quả mong đợi luôn được sinh bằng bản triển khai **js**. Điều này chỉ đơn thuần vì tính nhất quán và không có nghĩa
là trong trường hợp có sự khác biệt về render, bản triển khai js luôn luôn đúng._

Để thêm một render test mới:
1. Tạo một thư mục mới `test/integration/render/tests/<property-name>/<new-test-name>`

2. Tạo một file `style.json` mới trong thư mục đó, chỉ định bản đồ cần tải. Bạn có thể sao chép & chỉnh sửa một trong các file `style.json` hiện có từ các thư mục con `render/tests`. Trong file này, bạn có thể thêm thông tin bổ sung để mô tả test và kết quả mong đợi bằng trường metadata [`description`](https://github.com/maplibre/maplibre-gl-js/blob/11811ee4da938cb823a018b1301168d99aa4a74b/test/integration/render/tests/regressions/mapbox-gl-js%236706/style.json#L7).

3. Sinh một hình ảnh `expected.png` từ style đã cho bằng cách chạy test mới với cờ `UPDATE` được bật:
   ```
   UPDATE=1 npm run test-render -- -t "<property-name>/<new-test-name>"
   ```

4. Kiểm tra thủ công `expected.png` để xác nhận nó trông như mong đợi, và tùy chọn chạy lại test mà không có cờ update (`npm run test-render -t "<property-name>/<new-test-name>"`) để xem nó pass (tận hưởng liều dopamine đó!)

5. Commit `style.json` và `expected.png` mới :rocket:

## Cập nhật kết quả của query-test

Bạn có thể cập nhật kết quả mong đợi của query-test bằng cách chạy chúng với cờ `UPDATE` được bật, ví dụ trên Linux:
```
UPDATE=true npm run test-integration
```
Hãy kiểm tra cẩn thận xem tất cả các thay đổi có đúng như dự định hay không.

## Đọc Vector Tile Fixture

Đọc nội dung của toàn bộ một vector tile

```
npx vt2geojson -z 14 -y 8803 -x 5374 test/integration/assets/tiles/14-8803-5374.mvt
```

Đọc nội dung của một layer cụ thể trong một vector tile

```
npx vt2geojson --layer poi_label -z 14 -y 8803 -x 5374 test/integration/assets/tiles/14-8803-5374.mvt
```
