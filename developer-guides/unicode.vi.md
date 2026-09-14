## Unicode

MapLibre GL&nbsp;JS hỗ trợ hiển thị văn bản Unicode với các lưu ý sau:

* Một codepoint đơn lẻ bị giả định (không chính xác) là luôn tương ứng với một glyph duy nhất trong bất kỳ font nào, và ngược lại.
* Việc tạo hình văn bản phức tạp (complex text shaping) chưa được triển khai.
* Các hệ thống chữ viết từ phải sang trái (right-to-left), như tiếng Ả Rập và tiếng Hebrew, cần plugin riêng [mapbox-gl-rtl-text](https://github.com/mapbox/mapbox-gl-rtl-text/).

Một style có thể mở rộng tập hợp các hệ chữ viết mà nó hỗ trợ thông qua thuộc tính [`font-faces`](https://maplibre.org/maplibre-style-spec/root/#font-faces), thuộc tính này khai báo tên các file font dùng để vẽ mỗi tên `text-font`, và tùy chọn, phạm vi `unicode-range` mà mỗi file bao phủ. Các file này được giao cho CSS Font Loading API của trình duyệt, do đó bất kỳ định dạng nào mà trình duyệt có thể dùng để hiển thị văn bản đều được. Lưu ý rằng điều này chỉ mở rộng phạm vi bao phủ: các glyph vẫn được rasterize từng codepoint một, vì vậy nó không thể bù đắp cho việc thiếu complex text shaping, và điều tương tự cũng đúng với tùy chọn bản đồ `localIdeographFontFamily`.

### Cập nhật để tuân thủ Unicode Standard

Chúng tôi sử dụng nhiều thuộc tính từ Unicode Character Database để xác định hành vi của một ký tự trong nhãn (label), chẳng hạn như liệu nó có giữ hướng thẳng đứng trong văn bản dọc hay không. Khi một phiên bản chính mới của Unicode Standard được phát hành, hãy làm theo các bước sau để đảm bảo hành vi bố cục văn bản (text layout) luôn được cập nhật:

1. Ghi nhận phiên bản của [Unicode Standard mới nhất](https://www.unicode.org/versions/enumeratedversions.html).
2. Tìm [gói Unicode](https://www.npmjs.com/org/unicode) trên NPM tương ứng với phiên bản ở bước 1. Lưu ý rằng mỗi phiên bản của chuẩn này được phát hành thành một gói riêng, và mỗi gói lại có phiên bản (version) của riêng nó. Hãy tìm gói có **tên** chứa phiên bản ở bước 1, bất kể phiên bản của gói đó theo NPM là gì.
3. Trong package.json, cập nhật mục `devDependencies` để trỏ tới `@unicode/unicode-x.y.z`, trong đó _x.y.z_ là phiên bản từ bước 1.
4. Trong build/generate-unicode-data.ts, cập nhật hằng số `unicodeVersion` để khớp với phiên bản từ bước 1.
5. Trong build/generate-unicode-data.ts, cập nhật các hàm `hasUprightVerticalOrientation()` và `hasNeutralVerticalOrientation()` để phản ánh các hệ chữ viết (script), khối (block), và ký tự riêng lẻ được liệt kê trong file VerticalOrientation.txt mới nhất của Unicode Character Database. Để xác định những thay đổi cần thiết, hãy mở `https://www.unicode.org/Public/x.y.z/ucd/VerticalOrientation.txt`, trong đó _x.y.z_ là giá trị trước đó của `unicodeVersion` ở bước 4, và so sánh (diff) file đó với [file mới nhất](https://www.unicode.org/Public/UCD/latest/ucd/VerticalOrientation.txt). Nếu có bất kỳ phạm vi codepoint mới nào được liệt kê là `U` hoặc `Tu`, nó có thể cần được thêm vào một trong hai hàm trên, tùy thuộc vào việc nó bắt buộc phải viết thẳng đứng hay mang tính trung lập hơn.
6. Chạy `npm run generate-unicode-data` và kiểm tra rằng tất cả unit test và render test đều pass.
