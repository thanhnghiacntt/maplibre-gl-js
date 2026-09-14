# Tài liệu MapLibre GL JS

Thư mục này chứa mã nguồn cho [tài liệu MapLibre GL JS](https://maplibre.org/maplibre-gl-js/docs/) được host trên trang MapLibre.

Ngoài README này, mỗi file `.md` khác trong thư mục này tương ứng với một trang trên site. Mỗi file được chuyển đổi thành một file `.html` bởi [Zensical](https://zensical.org/).

!!! info
    Để chạy docs, bạn cần đảm bảo Docker đã được cài đặt và bạn có quyền chạy các lệnh `docker` mà không cần `sudo`, như được giải thích [ở đây trong tài liệu Docker](https://docs.docker.com/engine/install/linux-postinstall/).

## Chạy Documentation Server cục bộ

Để khởi động một documentation server cục bộ, trước tiên hãy cài đặt các dependency:

```bash
npm install
```

Sau đó đảm bảo bạn có một bản build cập nhật:

```bash
npm run build-prod
npm run build-css
```

Tiếp theo, sinh ra các file docs:

```bash
npm run generate-docs
```

Cuối cùng, chạy:

```bash
npm run start-docs
```

Truy cập [http://0.0.0.0:8000/](http://0.0.0.0:8000/) để xem docs. Sau khi thực hiện thay đổi, chạy lại `npm run generate-docs` để áp dụng chúng.

Phần examples của tài liệu chạy cục bộ sẽ sử dụng phiên bản GL JS đã được release có cùng phiên bản với phiên bản trong package.json.

## Viết tài liệu API

Tài liệu API được viết dưới dạng [TSDoc comment](https://tsdoc.org/) và được xử lý bằng [TypeDoc](https://typedoc.org/)

* Class, method, event, và bất cứ thứ gì khác trong public interface phải được tài liệu hóa bằng TSDoc comment, và từ khóa typescript `public` có thể được dùng để chỉ rằng nó là public API.
* Tag `@internal` có thể được dùng để chỉ rằng một class, method, hoặc event không phải là một phần của public interface và không nên được tài liệu hóa.
* Các method triển khai một interface cần có một `{@inheritDoc reference}` để kế thừa tài liệu từ interface.
* Sử dụng `@group` để chỉ định class cụ thể đó thuộc nhóm nào, các nhóm này được định nghĩa trong file `typedoc.json` và quan trọng đối với file giới thiệu (intro) của tài liệu API.
* Văn bản bên trong TSDoc comment có thể dùng định dạng markdown. Các identifier trong code phải được bao quanh bởi dấu \`backtick\`.
* Tài liệu phải được viết bằng các câu đúng ngữ pháp và kết thúc bằng dấu chấm.
* Tài liệu phải chỉ định đơn vị đo lường khi có áp dụng.
* Mô tả trong tài liệu phải chứa nhiều thông tin hơn những gì đã hiển nhiên từ tên định danh (identifier) và metadata JSDoc.
* Mô tả class nên mô tả class *là gì*, hoặc instance của nó *là gì*. Chúng không tài liệu hóa constructor, mà tài liệu hóa class. Chúng nên bắt đầu bằng một câu hoàn chỉnh hoặc một cụm từ có thể hoàn thành câu bắt đầu bằng "A `T` is..." hoặc "The `T` class is...". Ví dụ: "Lists are ordered indexed dense collections." "A class used for asynchronous computations."
* Mô tả function nên bắt đầu bằng một động từ ở ngôi thứ ba số ít thì hiện tại, như thể hoàn thành câu bắt đầu bằng "This function...". Nếu mục đích chính của function là trả về một giá trị, mô tả nên bắt đầu bằng "Returns...". Ví dụ: "Returns the layer with the specified id." "Sets the map's center point."
* Mô tả `@param` và `@returns` nên được viết hoa chữ cái đầu và kết thúc bằng dấu chấm. Chúng nên bắt đầu như thể hoàn thành câu bắt đầu bằng "This is..." hoặc "This...".
* Các function không trả về giá trị (trả về `void`) thì không nên có annotation `@returns`.
* Mô tả member nên tài liệu hóa member đó đại diện cho gì hoặc get/set cái gì. Chúng cũng nên chỉ rõ member đó có phải chỉ đọc (read-only) hay không.
* Mô tả event nên bắt đầu bằng "Fired when..." và do đó nên mô tả khi nào event được phát ra. Các mục event nên tài liệu hóa rõ ràng bất kỳ dữ liệu nào được truyền cho handler, kèm link đến tài liệu MDN về các đối tượng Event gốc nếu có áp dụng.
* Các danh sách (list) cần một dòng trống phía trên để được định dạng thành HTML list.
* Toàn bộ tài liệu được kiểm tra chính tả bằng [cSpell](https://cspell.org/) như một phần của quá trình lint thông qua một [GitHub Action](https://github.com/marketplace/actions/cspell-action). Chúng tôi khuyến nghị dùng extension VS Code để phát hiện lỗi chính tả trước khi tạo PR. Bạn có thể chạy `npx cspell "docs/**/*.html" "docs/**/*.md"` từ CLI để kiểm tra toàn bộ file. Nếu có một false-positive (một thuật ngữ kỹ thuật không có trong từ điển mặc định), bạn có thể thêm nó vào mảng words trong file `.spell.json` ở thư mục gốc.

## Viết Examples

Examples được viết dưới dạng các file HTML thông thường trong `test/examples`.
Mỗi example nên có một title, og:description, og:category và og:created.

* `title`: Một tiêu đề ngắn cho example, viết theo **sentence case** dưới dạng một **cụm động từ (verb phrase)**.
* `description`: Một câu mô tả ngắn gọn cho example dưới dạng plain text. Mô tả này sẽ xuất hiện cùng với một thumbnail và title trên trang examples.
* `category`: Chủ đề mà example được nhóm vào trên trang tổng quan. Phải là một trong các category được định nghĩa trong `docs/example-categories.json`.
* `created`: Định dạng ngày YYYY-MM-DD chỉ thời điểm example này được tạo, giúp docs hiển thị những gì mới.
* `order` (tùy chọn): Một con số dùng để sắp xếp các example trong category của chúng trên trang tổng quan. Số nhỏ hơn xuất hiện trước, sau đó là sắp xếp theo alphabet đối với các example không có số này.

Khi bạn tạo một example mới, bạn **bắt buộc** phải tạo một hình ảnh đi kèm.

1. Chạy `npm run generate-images <example-file-name>`. Script sẽ chụp ảnh màn hình của bản đồ trong example và lưu vào `docs/assets/examples/`.
2. Tối ưu hóa hình ảnh bằng [compresspng](https://compresspng.com/) để giảm kích thước file. (Tùy chọn)
3. Commit hình ảnh.

Đối với một số example, `npm run generate-images` không tạo ra hình ảnh lý tưởng. Trong những trường hợp này, bạn có thể tương tác với bản đồ sau khi chạy lệnh trước khi ảnh chụp màn hình được lấy, hoặc tự chụp ảnh màn hình bằng cách chạy site cục bộ với `npm start`, chụp ảnh màn hình và lưu vào thư mục `docs/assets/examples/`.

Để tạo lại toàn bộ hình ảnh, chạy `npm run generate-images`. Lưu ý rằng lệnh này không hỗ trợ tương tác và các example cần tương tác thủ công (ví dụ: popup) sẽ cần được làm lại thủ công sau đó. Tính năng này đang trong giai đoạn thử nghiệm và có thể bị crash trước khi tạo thành công tất cả các example.

## Commit và xuất bản tài liệu

Khi một phiên bản MapLibre GL JS mới được phát hành, tài liệu sẽ được phát hành cùng với nó.

Để cập nhật hoặc thêm một example mới, hãy gửi PR các thay đổi liên quan vào repo này. Example sẽ hoạt động (live) khi một phiên bản mới được phát hành. Nếu example này sử dụng một phiên bản GL JS chưa được phát hành, PR không nên được merge cho đến khi phiên bản đó được release.

## Mọi thứ này hoạt động như thế nào?

Nó sử dụng 3 công cụ:

1. CLI [TypeDoc](https://typedoc.org/)
2. [Zensical](https://zensical.org/)
3. Script `generate-docs.ts`

TypeDoc CLI được dùng để sinh ra các file markdown của API từ các TSDoc comment và đặt kết quả đầu ra vào thư mục API của docs.
`generate-docs.ts` thực hiện một số thao tác biến đổi trên đầu ra API này và cũng sử dụng các file html example từ thư mục test để sinh markdown cho file index của examples và toàn bộ các file markdown example.
Các file markdown khác trong thư mục docs được sử dụng nguyên trạng.
[Zensical](https://zensical.org/) được dùng để build trang tài liệu cho production và phục vụ (serve) nó ở chế độ debug. Nó có live reload và các file markdown có thể được xem để hiểu tại sao mọi thứ hiển thị như vậy.
