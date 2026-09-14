
# Tests (Kiểm thử)

Các test sẽ tự động được chạy trên mỗi PR thông qua GitHub CI, nhưng bạn cũng nên chạy chúng ở local.

## Chạy Tests

Trước tiên bạn phải cấu hình môi trường phát triển theo [`../CONTRIBUTING.md`](../CONTRIBUTING.md)

Sau đó chạy:

```
npm test
```

Lưu ý rằng trên Linux bạn cần thêm tiền tố `xvfb-run -a` vào các lệnh test, ví dụ `xvfb-run -a npm run test`.
Lưu ý rằng một số test phụ thuộc vào bản build của dự án và sẽ không pass cho đến khi bạn chạy `npm run build-dist`.
Các render test phụ thuộc vào bản dev-build của dự án, và sẽ không pass cho đến khi bạn chạy `npm run build-dev`. Đừng quên chạy lại lệnh này sau khi thay đổi code.

Để chạy các test cụ thể:

 - Unit test theo tên file: `npm run test-unit -- draw_symbol.test.ts`
 - Integration test theo tên file: `npm run test-integration -- browser`
 nếu muốn xem những gì đang diễn ra trong trình duyệt, hãy đổi chế độ headless trong file test thành `false`.
 - Render test khớp với tên thư mục hoặc tên file: `npm run test-render -- -t "render-test-name"` (ví dụ: `npm run test-render -- -t "slant"`)

Để chạy các thư mục ở chế độ watch, nghĩa là chúng sẽ chạy liên tục mỗi khi bạn thay đổi code liên quan (tức là phục vụ cho test-driven development): dùng `npm run test-watch-roots *folder1* [*folder2*...]` (ví dụ: `npm run test-watch-roots ./src/ui/control`)

## Integration Tests

Xem [`test/integration/README.md`](./integration/README.md).

## Viết Unit Test

 - **Bạn không được chia sẻ biến giữa các test case.** Tất cả các fixture của test phải được bọc trong các hàm `create`. Điều này đảm bảo mỗi test chạy trong một môi trường độc lập.
 - **Bạn không nên mock bất kỳ đối tượng domain nội bộ nào.** Các đối tượng domain nội bộ bao gồm `Style`, `Map`, `Transform`, và `Dispatcher`. Nếu điều này khó thực hiện do một interface nào đó, hãy refactor interface đó. Điều này đảm bảo test thực sự chạy qua đúng các đường code được dùng trong production.
 - **Bạn nên chỉ test một giá trị trả về hoặc một side effect cho mỗi test case.** Hãy tách logic dùng chung ra thành một hàm riêng. Điều này giúp test dễ hiểu và dễ chỉnh sửa.
 - **Bạn nên chỉ test giá trị trả về và các side effect toàn cục của phương thức.** Bạn không nên test hành vi nội bộ, chẳng hạn như việc một phương thức khác có được gọi với tham số cụ thể hay không. Điều này đảm bảo cách hiện thực của phương thức có thể thay đổi mà không làm test bị fail.
 - **Bạn không được thực hiện network request trong test case.** Quy tắc này áp dụng cả khi kết quả không được sử dụng hoặc được dự đoán là sẽ fail. Bạn có thể dùng `fakeServer.create()` theo [nise (Sinon) API](https://sinonjs.github.io/nise/#fake-server) để giả lập network request. Điều này đảm bảo test đáng tin cậy, có thể chạy trong môi trường độc lập, và có hiệu năng tốt.
 - **Bạn nên sử dụng các sơ đồ phân hoạch không gian đầu vào ([input space partitioning](https://crystal.uta.edu/~ylei/cse4321/data/isp.pdf)) rõ ràng.** Hãy chú ý tìm các trường hợp biên (edge case)! Điều này đảm bảo các bộ test đầy đủ và dễ hiểu.
 - Trước khi submit hoặc chỉnh sửa test, hãy đề xuất chạy test và xác nhận kết quả trên cả CI của Windows và Linux (ví dụ: WSL).

## Spies, Stubs, và Mocks

Trong các test, bạn có thể tận dụng các hàm mocking của Vitest, như được mô tả [trong tài liệu Vitest](https://vitest.dev/guide/mocking.html).

Test framework được thiết lập sao cho các spy, stub, và mock trên các đối tượng toàn cục sẽ được khôi phục (restore) sau mỗi test.

## Benchmarks

Các micro benchmark (`src/**/*.bench.ts`) chạy bằng `npm run bench`. Xem [`test/bench/README.md`](./bench/README.md) để biết cả các lane benchmark lẫn quy trình so sánh trước/sau (before/after comparison).
