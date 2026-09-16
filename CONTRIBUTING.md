# Đóng góp cho MapLibre GL JS

Xin chào, và cảm ơn bạn trước vì đã đóng góp cho MapLibre GL JS. Dưới đây là cách chúng tôi làm việc. Vui lòng tuân theo các quy ước này khi gửi issue hoặc pull request.

## Không được vi phạm bản quyền của Mapbox!

Vào tháng 12 năm 2020, Mapbox đã quyết định phát hành các phiên bản mapbox-gl-js trong tương lai theo giấy phép độc quyền (proprietary license). **Bạn không được phép backport code từ các dự án Mapbox đã được đóng góp theo giấy phép mới này**. Các backport trái phép là mối đe dọa lớn nhất đối với dự án MapLibre. Nếu bạn không chắc chắn về vấn đề này, [hãy hỏi ở đây](https://github.com/maplibre/maplibre-gl-js/discussions)!

## Các thực hành tốt nhất khi đóng góp

MapLibre chào đón sự đóng góp từ cộng đồng! Codebase này lớn và phức tạp, và việc tuân theo các thực hành tốt nhất dưới đây sẽ giúp đội ngũ maintainer review đóng góp của bạn dễ dàng hơn. Nhìn chung, dự án đề cao thảo luận và giao tiếp hơn là quy trình và tài liệu. Tuy nhiên, do quy mô và độ phức tạp của code, dưới đây là một số thực hành tốt đã giúp ích cho các contributor.

Nên thảo luận về các thay đổi được đề xuất trước khi tiến hành tạo issue ticket hoặc PR. Đội ngũ dự án hoạt động tích cực tại các diễn đàn sau:

* Để trò chuyện không chính thức, hãy ghé [Slack Channel](https://osmus.slack.com/archives/C01G3D28DAB) của dự án.
* Đối với các thảo luận mà kết quả và nội dung không nên chỉ tồn tại nhất thời, hãy cân nhắc mở một thread trên [GitHub Discussions](https://github.com/maplibre/maplibre-gl-js/discussions). Điều này giúp việc tìm kiếm và tham chiếu lại thảo luận trong tương lai dễ dàng hơn.

Phần mềm MapLibre phụ thuộc rất nhiều vào automated testing, và dự án bao gồm một bộ unit test và integration test. Đối với cả tính năng mới lẫn bugfix, các đóng góp nên cập nhật hoặc thêm test case để ngăn ngừa regression.

### Tính năng mới

Đối với các tính năng mới, thường nên bắt đầu bằng một issue ticket. Nếu tính năng đòi hỏi thay đổi style specification, một issue ticket nên được tạo trong [repository GitHub của style specification](https://github.com/maplibre/maplibre-gl-style-spec). Các thay đổi trong style specification rất khó thay đổi lại sau này, vì vậy sẽ có sự xem xét đặc biệt kỹ lưỡng đối với các thay đổi liên quan đến specification.

Nếu có thể, việc demo các tính năng mới được đề xuất và đánh giá tác động hiệu năng của thay đổi đó sẽ rất hữu ích. Bạn có thể dùng `npm install <location-of-maplibre-source-code>` để test thay đổi trong một ngữ cảnh npm, hoặc `npm run build-prod` để build một package .js cho mục đích này.

Đối với các tính năng phức tạp hơn cần thảo luận sâu, bạn nên cân nhắc đưa vấn đề ra cuộc họp [Technical Steering Committee](https://maplibre.org/categories/steering-committee/) để trao đổi qua video với đội ngũ về thay đổi được đề xuất. Chúng tôi nhận thấy đôi khi việc thảo luận trực tiếp, tập trung sẽ dễ dàng hơn đối với các quyết định có hệ quả lớn.

Các cuộc họp Technical Steering Committee mở cho bất kỳ ai muốn tham gia vào định hướng kỹ thuật của dự án. Các cuộc họp này là cơ hội để thảo luận và hợp tác về nhiều chủ đề kỹ thuật khác nhau. Chúng tôi hoan nghênh bạn tham gia các cuộc họp nếu bạn quan tâm đến việc tham gia sâu hơn.

### Sửa lỗi (Bug Fixes)

Nếu bạn phát hiện một lỗi nghiêm trọng, hoặc một lỗi mà bạn không định tự sửa, vui lòng viết một issue ticket mô tả vấn đề. Đối với các lỗi nhỏ hoặc đơn giản, bạn có thể tiến thẳng tới việc tạo PR.

Một số thực hành tốt cho PR sửa lỗi như sau:

1. Bắt đầu bằng việc viết một test thất bại (failing test) để chứng minh phần mềm hiện tại hoạt động không như mong đợi. Commit và push branch.
2. Tạo một draft PR ghi lại hành vi sai đó. Điều này sẽ hiển thị failing test bạn vừa viết trong continuous integration của dự án và chứng minh sự tồn tại của lỗi.
3. Sửa lỗi, và cập nhật PR với các ghi chú khác cần thiết để mô tả thay đổi trong phần mô tả PR.
4. Đừng quên đánh dấu PR là sẵn sàng để review khi bạn hài lòng với các thay đổi code.

Đây không phải là một quy trình bắt buộc nghiêm ngặt mà chỉ là hướng dẫn giúp xây dựng sự tin tưởng rằng PR của bạn đang giải quyết đúng vấn đề.

## Đóng góp có sự hỗ trợ của AI

MapLibre chào đón các contributor sử dụng công cụ AI coding, nhưng chúng tôi phải cảnh giác để không đưa vào các nội dung có bản quyền. Bạn chịu trách nhiệm cho mọi thứ bạn gửi lên. Maintainer sẽ không merge code mà tác giả không thể giải thích hoặc bảo vệ được khi review, bất kể nó được tạo ra như thế nào, và sẽ phải đóng PR hoặc issue của bạn nếu bạn không đáp ứng được tiêu chuẩn này.

Chính sách đầy đủ nằm tại
[maplibre/maplibre/AI_POLICY.md](https://github.com/maplibre/maplibre/blob/main/AI_POLICY.md). Vui lòng xem lại chính sách này trước khi gửi PR hoặc báo cáo lỗi.

**Công khai (Disclosure):** Hãy công khai việc sử dụng AI đáng kể trong PR của bạn (mẫu PR có một checkbox cho việc này).

## Chuẩn bị môi trường phát triển

### CodeSpaces

Khi tạo một code space, bạn sẽ có thể bắt đầu làm việc ngay sau khi script post-create chạy xong.
Script này về cơ bản cài đặt mọi thứ được viết ở đây trong phần dành cho Linux.

### macOS

Cài đặt Xcode Command Line Tools Package
```bash
xcode-select --install
```

Cài đặt phiên bản [node.js](https://nodejs.org/) được chỉ định trong [.nvmrc](.nvmrc)
```bash
brew install node
```

Clone repository
```bash
git clone git@github.com:maplibre/maplibre-gl-js.git
```

Cài đặt các dependency cho node_canvas (https://github.com/Automattic/node-canvas)
```bash
brew install pkg-config cairo pango libpng jpeg giflib librsvg
```

Cài đặt các node module dependency
```bash
cd maplibre-gl-js &&
npm install
```

#### Apple silicon

Nếu bạn dùng một trong các máy arm64 đời mới, bạn có thể gặp trường hợp không tìm thấy canvas.node hoặc webgl.node cho kiến trúc của mình. Trong trường hợp đó, hãy vào `node_modules/canvas` và `node_modules/gl` rồi chạy:

```
npm install --build-from-source
```

Nếu bạn đã cài đặt từ một máy không phải M1 sang máy M1 bằng Migration Assistant và trước đó đã cài `brew`, và bạn gặp lỗi này khi chạy test:

```
dlopen(/Users/[...]/common/temp/node_modules/.pnpm/canvas@2.11.0/node_modules/canvas/build/Release/canvas.node, 0x0001): symbol not found in flat namespace '_cairo_fill'

      at Object.<anonymous> (../../common/temp/node_modules/.pnpm/canvas@2.11.0/node_modules/canvas/lib/bindings.js:3:18)
```

Hãy thử
- Gỡ cài đặt rồi cài lại `brew` [brew](https://brew.sh/)
- Chạy `arch -arm64 brew install pkg-config cairo pango libpng jpeg giflib librsvg`
- Xóa thư mục `node_modules` và chạy lại `npm install`

### Linux (và tương tự với GitHub codespaces)

Cài đặt [git](https://git-scm.com/), [GNU Make](https://www.gnu.org/software/make/), và libglew-dev
```bash
sudo apt-get update &&
sudo apt-get install build-essential git libglew-dev libxi-dev default-jre default-jdk xvfb
```

Nếu không có sẵn binary dựng sẵn (prebuilt) cho canvas và gl, bạn cũng sẽ cần:

```bash
sudo apt-get install python-is-python3 pkg-config libpixman-1-dev libcairo2-dev libpango1.0-dev libgif-dev
```

Cài đặt [nvm](https://github.com/nvm-sh/nvm)
```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.38.0/install.sh | bash
```

Cài đặt [Node.js](https://nodejs.org/) theo .nvmrc
```
nvm install
```

Clone repository
```bash
git clone git@github.com:maplibre/maplibre-gl-js.git
```

Cài đặt các node module dependency
```bash
cd maplibre-gl-js &&
npm install
```

Trước khi bạn có thể [chạy docs](./developer-guides/README-docs.md), bạn cần đảm bảo Docker đã được cài đặt và bạn có quyền chạy các lệnh `docker` mà không cần `sudo`, như được giải thích [ở đây trong tài liệu Docker](https://docs.docker.com/engine/install/linux-postinstall/).


### Windows

Cân nhắc sử dụng WSL và làm theo hướng dẫn Linux ở trên, hoặc làm theo các bước dưới đây

Cài đặt [git](https://git-scm.com/), [node.js](https://nodejs.org/) (phiên bản trong [.nvmrc](.nvmrc)), [npm và node-gyp](https://github.com/Microsoft/nodejs-guidelines/blob/master/windows-environment.md#compiling-native-addon-modules).

Clone repository
```bash
git clone git@github.com:maplibre/maplibre-gl-js.git
```

Cài đặt các node module dependency
```bash
cd maplibre-gl-js
npm install
```

Cài đặt các dependency của headless-gl https://github.com/stackgl/headless-gl#windows
```
copy node_modules/headless-gl/deps/windows/dll/x64/*.dll c:\windows\system32
```

## Tạo bản build độc lập (Standalone Build)

Một standalone build cho phép bạn chuyển nội dung của repository này thành các file `maplibre-gl.mjs`, `maplibre-gl-worker.mjs` và `maplibre-gl.css` có thể được nhúng vào một trang html.

Để tạo standalone build, chạy
```bash
npm run build-dist
```
Sau khi hoàn tất, bạn sẽ có một standalone build tại `dist/maplibre-gl.mjs`, `dist/maplibre-gl-worker.mjs` và `dist/maplibre-gl.css`. Hãy load nó thông qua `<script type="module">`; URL của worker sẽ được tự động phát hiện như một sibling của module đã load.

## Kiểm thử thay đổi và viết tài liệu

Xem [`developer-guides/README-docs.md`](./developer-guides/README-docs.md)

## Viết & chạy Test

Xem [`test/README.md`](./test/README.md).

## Viết & chạy Benchmark

Xem [`test/bench/README.md`](./test/bench/README.md).

Micro benchmark nằm ngay cạnh code mà chúng đo lường (`src/**/*.bench.ts`) và chạy bằng `npm run bench`; các benchmark end-to-end nằm trong `test/bench/e2e/`. Nếu PR của bạn tuyên bố có tác động về hiệu năng, hãy kèm theo một bảng before/after từ `npm run bench -- --compare` trong phần mô tả.

## Các hướng dẫn khác

Xem thư mục [`developer-guides`](./developer-guides) để biết các hướng dẫn về quy trình release và vòng đời của tile.

## Quy ước về code

* Chúng tôi sử dụng [`error` events](https://www.mapbox.com/mapbox-gl-js/api/#Map.event:error) để báo cáo lỗi của người dùng.
* Chúng tôi sử dụng những tính năng mới nhất mà ngôn ngữ TypeScript cung cấp, bao gồm nhưng không giới hạn ở:
  * `let`/`const`
  * Vòng lặp `for...of` (chỉ dùng cho việc lặp qua các đối tượng dạng mảng, tức là những gì được hỗ trợ bởi transform [`dangerousForOf` của Bublé](https://buble.surge.sh/guide/#dangerous-transforms))
  * Arrow function
  * Class
  * Template string
  * Computed và shorthand object property
  * Default parameter
  * Rest parameter
  * Destructuring
  * Module

Các quy ước cho module export là:

* Không export các "namespace object" -- module nên export class hoặc function, thỉnh thoảng có ngoại lệ khi cần để phục vụ việc stub.
* Nếu một module export thứ gì đó có tên trùng với tên file (không phân biệt hoa thường), nó nên là default export.
* Bất cứ thứ gì khác nên là named export.

Để giữ code có phong cách đồng nhất và tránh các lỗi phổ biến, bạn có thể kiểm tra một số file bằng các script sau:

```bash
npm run lint
npm run lint-css
```

Ngoài ra, nếu bạn dùng VSCode, thao tác "Format Document" hoặc "Editor: Format on Save" sẽ mặc định áp dụng định dạng js, ts và css cho dự án này.

### Quy ước về quản lý phiên bản (Version Control)

Dưới đây là cách được khuyến nghị để thiết lập:

1. Fork dự án này
2. Clone fork mới của bạn, `git clone git@github.com:GithubUser/maplibre-gl-js.git`
3. `cd maplibre-gl-js`
4. Thêm repository MapLibre làm upstream repository: `git remote add upstream git@github.com:maplibre/maplibre-gl-js.git`
5. Tạo một branch mới `git checkout -b your-branch` cho đóng góp của bạn
6. Viết code, mở một PR từ branch của bạn khi bạn đã sẵn sàng
7. Nếu bạn cần rebase branch PR của fork mình lên main để giải quyết conflict: `git fetch upstream`, `git rebase upstream/main` rồi force push lên Github `git push --force origin your-branch`

## Quy ước về Changelog

Điều gì cần một mục changelog?

- Bất kỳ thay đổi nào ảnh hưởng đến public API, giao diện hiển thị hoặc bảo mật người dùng *bắt buộc* phải có một mục changelog
- Bất kỳ cải thiện hiệu năng hoặc bugfix nào *nên* có một mục changelog
- Bất kỳ đóng góp nào từ thành viên cộng đồng *có thể* có một mục changelog, dù nhỏ đến đâu
- Bất kỳ thay đổi liên quan đến tài liệu nào *không nên* có mục changelog
- Bất kỳ regression nào được đưa vào và sửa trong cùng một release *không nên* có mục changelog
- Bất kỳ refactoring nội bộ, giảm nợ kỹ thuật (technical debt), render test, unit test hoặc benchmark nào *không nên* có mục changelog

Cách thêm changelog của bạn?

- Chỉnh sửa trực tiếp file [`CHANGELOG.md`](CHANGELOG.md), chèn một mục mới ở đầu danh sách phù hợp
- Bất kỳ mục changelog nào cũng nên mô tả rõ ràng và súc tích; nó nên giải thích thay đổi cho một người đọc không có ngữ cảnh nào

## Tài liệu đề xuất đọc thêm

### Học WebGL

- [Các bài viết WebGL của Greggman](https://webglfundamentals.org/)
- [Thẻ tham khảo WebGL](https://www.khronos.org/files/webgl/webgl-reference-card-1_0.pdf)

### Hiệu năng GL

- [Debug và tối ưu hóa ứng dụng WebGL](https://docs.google.com/presentation/d/12AGAUmElB0oOBgbEEBfhABkIMCL3CUX7kdAPLuwZ964)

### Khác

- [Vẽ đường khử răng cưa (antialiased lines)](https://blog.mapbox.com/drawing-antialiased-lines-with-opengl-8766f34192dc)
- [Vẽ text bằng signed distance field](https://blog.mapbox.com/drawing-text-with-signed-distance-fields-in-mapbox-gl-b0933af6f817)
- [Đặt vị trí label (label placement)](https://www.mapbox.com/blog/placing-labels/)
- [Distance field](https://bytewrangler.blogspot.com/2011/10/signed-distance-fields.html)
