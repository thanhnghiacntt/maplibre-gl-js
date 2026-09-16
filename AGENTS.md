# Quy ước dành cho Agent

## Comment

Giải thích code trong **TSDoc comment ở khai báo (declaration)**, không phải trong comment bên trong thân hàm.

Người đọc tiếp cận một hàm thông qua chữ ký (signature) và doc block của nó, và tài liệu API được sinh tự động cũng vậy. Một comment nằm sâu ba dòng bên trong một method sẽ vô hình với cả hai. Bất cứ điều gì đáng nói về *cái gì* một hàm làm, *tại sao* nó tồn tại, hoặc caller cần biết điều gì, đều thuộc về phía trên nó:

```ts
/**
 * Returns the offsets, counted in UTF-16 code units, at which a word begins.
 *
 * Leaving this to the segmenter rather than to a table of punctuation brings word wrapping to
 * writing systems that do not put spaces between words, because the browser has the dictionaries.
 */
export function wordBoundaries(text: string): Set<number> {
```

Điều tương tự áp dụng cho một type, một field, hay một constant: hãy tài liệu hóa nó ngay tại nơi nó được khai báo.

```ts
type Entry = {
    /** One TinySDF per `font-faces` file this stack draws with, keyed by the file's CSS family. */
    fontFaceTinySDFs?: {[family: string]: Promise<TinySDF>};
};
```

Một comment bên trong thân hàm chỉ nên là phương án cuối cùng, dành cho một bước riêng lẻ mà lý do không thể thấy được từ code và không khái quát hóa cho toàn bộ hàm — ví dụ như một cách khắc phục (workaround) cho một lỗi trình duyệt cụ thể. Nếu bạn thấy mình viết nhiều comment như vậy, phần giải thích nên thuộc về doc block, hoặc thân hàm cần được tách thành các hàm có tên riêng, mỗi hàm mang một comment.

Đừng diễn giải lại code (`// increment i`), và đừng tường thuật lại thay đổi bạn đang thực hiện (`// now uses the segmenter`) — diff đã nói điều đó rồi, và nó sẽ ngừng đúng ngay khi thay đổi tiếp theo xảy ra.

**Mô tả code làm gì, không phải nó đã trở thành như vậy bằng cách nào.** Có hai kiểu nội dung đọc giống như tài liệu nhưng thực chất không phải.

Kiểu thứ nhất là bản thân sự thay đổi. Một comment đối chiếu cách tiếp cận hiện tại với cách tiếp cận trước đó — "reads the derived table rather than `ArabicShaping.txt`", "no longer needs the plugin", "this used to be done per codepoint" — là một mục changelog dành cho bất kỳ ai đến sau khi thay đổi đã xảy ra, và thứ nó đang đối chiếu lại không còn tồn tại trong file để họ so sánh.

Kiểu thứ hai là quyết định đằng sau sự thay đổi. Một comment biện luận cho lựa chọn — "the package that carries this unpacks to more than 250 MB", "we went with this because the alternative was too slow" — là lập luận cho một pull request, viết cho reviewer đang cân nhắc các phương án. Người đọc code đã merge không còn cân nhắc gì nữa, và lý do nên nằm trong PR hoặc issue theo dõi nó.

Hãy viết như thể code luôn trông như vậy và không có cách nào khác từng được cân nhắc. Ở nơi mà một người bảo trì trong tương lai lẽ ra sẽ sa vào một cái bẫy, hãy nêu cái bẫy đó như một sự thật về vấn đề — "a glyphs URL serves codepoints, so it has no way to serve a cluster" — thay vì như câu chuyện về cách nó đã được tránh né.

**Không có phần mở đầu (preamble) ở cấp file.** Một comment thuộc về thứ nằm ngay bên dưới nó, không thuộc về cả file. Một khối văn bản ở đầu module giải thích chủ đề một cách tổng quát không có gì để gắn vào: nó không xuất hiện trong tài liệu API, không ai cuộn lên lại để đọc nó từ hàm họ đang đọc, và nó sẽ trở nên lạc hậu ngay khi file có thêm một hàm mà phần mở đầu chưa từng lường trước.

Mọi điều mà một preamble như vậy muốn nói đều thuộc về một trong các khai báo bên dưới nó. Lý do tại sao một grapheme cluster là đơn vị của layout thuộc về hàm tạo ra chúng. `Intl.Segmenter` làm gì thuộc về constant giữ nó. Hãy chia nhỏ và đặt từng phần vào nơi người đọc gặp đoạn code mà nó giải thích — nếu một phần không phù hợp ở đâu cả, thì đó là bối cảnh (background) chứ không phải tài liệu, và mô tả PR là nơi nó nên thuộc về.

## Nesting (lồng nhau)

**Giữ độ thụt lề nông.** Mỗi cấp mà người đọc phải đi xuống là một điều kiện nữa họ phải ghi nhớ trong đầu để biết dòng trước mặt họ có chạy hay không. Ba cấp bên trong một hàm thường là điểm cần dừng lại và tái cấu trúc.

Hai kỹ thuật xử lý được phần lớn trường hợp. **Nâng những gì không thay đổi lên trên (hoist)** — một điều kiện không phụ thuộc vào bất kỳ biến vòng lặp nào thì được tính một lần, phía trên vòng lặp, dưới một cái tên:

```ts
const needsVerticalForms = (textAlongLine || allowVerticalPlacement) && doesAllowVerticalWritingMode;

for (const grapheme of toGraphemes(text)) {
```

**Biến một `if` bao quanh thành một guard.** `if (!ready) continue;` trong một vòng lặp, hoặc một `return` sớm trong một hàm, đưa trường hợp ngoại lệ ra khỏi đường đi và để phần công việc quan trọng nằm ở cấp ngoài thay vì bên trong một khối:

```ts
for (const char of grapheme) {
    stack[char] = true;
    if (!needsVerticalForms) continue;

    const verticalChar = verticalizedCharacterMap[char];
    if (verticalChar) stack[verticalChar] = true;
}
```

Trích xuất một hàm có tên là kỹ thuật thứ ba, và là lựa chọn đúng khi một khối đã phát triển thành chủ đề của riêng nó chứ không chỉ đơn thuần là độ thụt lề riêng.

Việc làm phẳng (flattening) không được thay đổi hành vi. Việc tách một pass thành hai pass sẽ sắp xếp lại thứ tự công việc, điều này ổn với một phép tính thuần túy (pure computation) nhưng không ổn ở nơi mà một thứ gì đó phía sau có thể quan sát được thứ tự — ví dụ như thứ tự chèn (insertion order) vào một object được dùng như một set. Nếu bạn không thể chắc chắn điều đó an toàn, hãy giữ nguyên cấu trúc lồng.

## Types

**Diễn đạt một map dưới dạng `Record<K, V>`, không phải index signature.** `Record<string, Promise<TinySDF>>` đọc như một thứ duy nhất; `{[family: string]: Promise<TinySDF>}` buộc người đọc phải phân tích một type literal để nhận ra đó là một map, và lồng nhau rất tệ — một map của các map là bốn dòng nếu viết dưới dạng index signature và chỉ một dòng nếu dùng `Record`.

```ts
glyphs: Record<string, StyleGlyph | null>;
export type GetGlyphsResponse = Record<string, Record<string, StyleGlyph>>;
```

Chỉ giữ index signature ở những nơi nó mang lại điều mà `Record` không thể: một key có tên tự giải thích trong một type có các thành viên khác, hoặc một numeric key đi kèm với các property đã khai báo.

## Changelog

**Mỗi mục một dòng.** Nói thay đổi là gì và ý nghĩa của nó đối với người dùng thư viện, rồi dừng lại. Changelog được lướt qua, không phải đọc kỹ, và một đoạn văn dài sẽ chôn vùi mệnh đề duy nhất mà người đọc đang tìm kiếm.

```md
- Support `font-faces` style spec property and improve text rendering for complex script languages ([#6637](https://github.com/maplibre/maplibre-gl-js/issues/6637))
```

Tránh giải thích cơ chế hoạt động, liệt kê mọi ngôn ngữ/script bị ảnh hưởng, hay tường thuật quyết định thiết kế — những điều đó thuộc về mô tả PR và doc comment của chính code. Nếu một thay đổi thực sự cần hai câu để hiểu được, thì thường đó là hai mục, hoặc một mục kèm một link.

## Test

**Khai báo test helper bằng `function`, không phải lambda gán vào `const`.** Một hàm có tên, được hoisted, đọc như một phần từ vựng của file và có thể được định nghĩa bên dưới các test sử dụng nó; `const helper = () => {...}` phải nằm ở trên và khiến tên với các tham số cách xa nhau hơn.

```ts
function createGlyphManager(remoteEnabled: boolean, font?: string | false): GlyphManager {
```

**Bao phủ code, rồi dừng lại.** Mỗi nhánh đáng có tên xứng đáng có một test, nhưng hai test chỉ khác nhau ở một giá trị đầu vào thực chất là một test — hãy gộp chúng lại và chọn giá trị đầu vào nói lên nhiều nhất. Điều bạn đang phòng tránh là một bộ test mà một thay đổi duy nhất khiến mười lăm test cùng báo đỏ trong khi tất cả đều đang nói cùng một điều.

**Giữ test theo hướng DAMP thay vì DRY.** Một test nên đọc được từ trên xuống dưới mà người đọc không phải đi tìm xem một fixture dùng chung chứa gì. Lặp lại ba dòng setup trong mỗi test rẻ hơn cho người đọc so với một builder tinh vi mà mọi test đều gọi với các tham số khác nhau. Chỉ tách riêng những gì thực sự không liên quan trực tiếp — ví dụ một stub của một collaborator không liên quan — và để phần mà test thực sự nói về nằm ngay tại chỗ (inline).

**Test thông qua public API.** Đừng truy cập các field hay method có tiền tố `_`. Nếu một hành vi chỉ có thể quan sát được thông qua nội bộ (internals), đó là dấu hiệu class đang thiếu một accessor hoặc test đang assert sai đối tượng — hãy assert vào thứ mà caller có thể thấy được.

**Giả lập mạng bằng một fake server, không phải bằng cách mock các hàm request.** `fakeServer` của `nise` là thứ phần còn lại của bộ test sử dụng. Việc mock `getArrayBuffer` hay `getJSON` bỏ qua phần xây dựng request mà code đang được test thực hiện — URL nó tạo ra, header nó thiết lập, `transformRequest` nó đi qua — thường lại chính là phần đáng để assert.

```ts
let server: FakeServer;

beforeEach(() => {
    global.fetch = null;   // sends the request down the XHR path the fake server intercepts
    server = fakeServer.create();
});

afterEach(() => {
    server.restore();
});
```

**Stub các collaborator, không bao giờ stub đơn vị đang được test.** Việc thay thế một method trên chính class bạn đang test có nghĩa là test không còn thực thi thứ mà nó mang tên nữa. Hãy thay thế những gì class đó *sử dụng* — các dependency của nó, mạng, đồng hồ hệ thống — và để bản thân đơn vị đó chạy thật.
