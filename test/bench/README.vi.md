# Benchmark

Benchmark giúp chúng ta phát hiện các regression về hiệu năng và cải thiện hiệu năng.

Có hai loại benchmark trong repository này:

* **Micro benchmark** nằm ngay cạnh code mà chúng đo lường dưới dạng các file `src/**/*.bench.ts` và chạy dưới [chế độ bench của Vitest](https://vitest.dev/guide/features.html#benchmarking). Chúng trả lời câu hỏi "thay đổi của tôi có làm code path này nhanh hơn trên máy của tôi, ngay bây giờ hay không" trong lúc bạn đang làm việc trên đó.
* **Benchmark end-to-end** trong `test/bench/e2e/` nạp các artifact production thực tế (bản build `dist/` của bạn, một release từ CDN) trong Chrome headless và đo thời gian một bản đồ đi qua public API. Chúng trả lời câu hỏi "thư viện có bị chậm đi giữa các phiên bản hay không".

## Micro benchmark

Chạy tất cả micro benchmark:

```bash
npm run bench
```

Chạy một file duy nhất, hoặc chỉ các benchmark khớp với một tên:

```bash
npm run bench -- src/render/subdivision.bench.ts
npm run bench -- -t mercator
```

Để đo lường một thay đổi, hãy ghi lại một baseline trước khi thực hiện thay đổi, rồi so sánh với baseline đó sau khi thực hiện:

```bash
git checkout main && npm run bench -- --outputJson bench-baseline.json
git checkout your-branch && npm run bench -- --compare bench-baseline.json
```

Lần chạy compare sẽ chú thích (annotate) mỗi kết quả với tỉ lệ so với baseline. Nếu PR của bạn tuyên bố có tác động về hiệu năng, hãy dán bảng đó vào mô tả PR để reviewer có thể tái hiện lại bằng cùng hai lệnh đó.

Kết quả chỉ có thể so sánh được trên cùng một máy trong cùng một phiên làm việc (session): cùng một đoạn code không đổi thường xuyên dao động vài phần trăm giữa các lần chạy, vì vậy hãy coi các chênh lệch nhỏ là nhiễu (noise). Vitest cũng chạy source code qua transform riêng của nó thay vì bản build production, khiến các con số micro benchmark hữu ích cho việc so sánh tương đối nhưng không phải là con số tuyệt đối cho production.

Để viết một micro benchmark, hãy tạo một file `*.bench.ts` ngay cạnh code bạn đang đo lường:

```ts
import {bench} from 'vitest';
import {subdividePolygon} from './subdivision.ts';

bench('subdividePolygon', () => {
    subdividePolygon(polygon, tileID, granularity, true);
});
```

Giữ công việc setup (dựng fixture, parse dữ liệu) ở cấp module để lời gọi được đo lường là thứ duy nhất bên trong `bench()`. Xem `src/geo/projection/covering_tiles.bench.ts` và `src/render/subdivision.bench.ts` để tham khảo ví dụ.

## Benchmark end-to-end

Bộ chạy (runner) e2e đo lường thư viện thực tế đã được build. Nó nạp các artifact production `.mjs` trong Chrome headless, điều khiển một bản đồ thông qua public API dựa trên các fixture hoàn toàn cục bộ (style, tile, glyph, sprite; không có mạng), và đọc timeline thông qua chính các sự kiện của bản đồ: bundle import, style load, first tile, load, first idle.

So sánh phiên bản release mới nhất với working copy của bạn (chạy `npm run build-dist` trước):

```bash
npm run bench-e2e
```

Các artifact được xác định theo vị trí (positional): `dist` là bản build cục bộ, `latest` được phân giải thông qua unpkg, một phiên bản trần như `6.0.0` sẽ fetch chính release đó, và bất kỳ URL nào trỏ đến một `maplibre-gl.mjs` sẽ được dùng nguyên trạng. `--runs N` điều khiển số lượng mẫu (sample) cho mỗi artifact (mặc định 8):

```bash
npm run bench-e2e -- 6.0.0 dist --runs 16
```

Các cột được đặt tên theo phiên bản mà chính artifact đó tự báo cáo. Với đúng hai artifact, bảng sẽ thêm một cột delta. Các artifact chạy tuần tự trên một máy, và lưu ý về nhiễu trong cùng session từ micro benchmark cũng áp dụng ở đây không đổi.
