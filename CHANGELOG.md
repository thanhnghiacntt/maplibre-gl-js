## main
### ✨ Tính năng và cải tiến
- _...Thêm nội dung mới vào đây..._

### 🐞 Sửa lỗi
- _...Thêm nội dung mới vào đây..._

## 6.9.0

### ✨ Tính năng và cải tiến

- Cải thiện hỗ trợ vẽ các ký tự của chữ Devanagari, Khmer, Miến Điện và các văn tự phức tạp khác, đồng thời vẽ đúng các nhãn chữ Ả Rập và Do Thái mà không cần tải plugin văn bản phải-sang-trái, điều này khiến `setRTLTextPlugin` và `getRTLTextPluginStatus` trở thành phương thức lỗi thời (deprecated) ([#8343](https://github.com/maplibre/maplibre-gl-js/pull/8343)) (by [@HarelM](https://github.com/HarelM))
- Đọc lại pixel của sprite và hình ảnh thông qua `OffscreenCanvas` khi có thể, giúp loại bỏ tình trạng luồng chính (main-thread) bị treo hàng chục mili giây trên các trình duyệt tăng tốc GPU khi sprite được tải ([#8339](https://github.com/maplibre/maplibre-gl-js/pull/8339)) (by [@cherenkov](https://github.com/cherenkov))
- Bỏ qua mặt nạ cắt (clipping mask) cho các layer bị ẩn ở mức zoom hiện tại và ngừng việc gắn lại (re-binding) các buffer động khi các lần gắn vertex array đã được cache, giúp loại bỏ các lệnh gọi WebGL dư thừa trong mỗi khung hình ([#8369](https://github.com/maplibre/maplibre-gl-js/pull/8369)) (by [@johncarmack1984](https://github.com/johncarmack1984))
- Chỉ render lại tối đa một lớp phủ địa hình (terrain drape) cũ mỗi khung hình và giữ lại các lớp phủ chỉ khác nhau về mức zoom trong khi bản đồ đang di chuyển, nhờ đó việc nhấc ngón tay ra khỏi màn hình trên địa hình không còn khiến tất cả các tile được render lại cùng lúc ([#8368](https://github.com/maplibre/maplibre-gl-js/pull/8368)) (by [@johncarmack1984](https://github.com/johncarmack1984))

### 🐞 Sửa lỗi
- Sửa lỗi `setStyle()` phát sinh lỗi khi địa hình vẫn đang tải vì một lần render trung gian cố gắng biên dịch shader địa hình trước khi style thay thế khởi tạo phép chiếu (projection) của nó ([#6824](https://github.com/maplibre/maplibre-gl-js/issues/6824)) (by [@miakh](https://github.com/miakh))
- Sửa lỗi các thao tác xóa thuộc tính GeoJSON `updateData` đang xếp hàng chờ phát sinh lỗi sau các cập nhật chỉ liên quan đến hình học, hoặc vẫn giữ lại các giá trị đã cập nhật trước đó ([#8372](https://github.com/maplibre/maplibre-gl-js/pull/8372)) (by [@jokrasno](https://github.com/jokrasno))
- Coi các camera options được truyền vào dưới dạng `undefined` là không được cung cấp trong `jumpTo`, `easeTo` và `flyTo`; trước đây chúng bị ép kiểu (coerced) thành NaN ([#8373](https://github.com/maplibre/maplibre-gl-js/pull/8373)) (by [@vlumi](https://github.com/vlumi))
- Sửa lỗi `Not implemented.` làm gián đoạn việc kéo (pan) và thu phóng (zoom) khi phép chiếu bị thay đổi trong lúc camera đang di chuyển, trên các bản đồ có bật địa hình hoặc có callback `transformCameraUpdate` ([#8351](https://github.com/maplibre/maplibre-gl-js/issues/8351)) (by [@lazerg](https://github.com/lazerg))
- Sửa lỗi bản đồ được tạo bên trong một container ẩn vẫn giữ nguyên kích thước mặc định `400x300` khi container được hiển thị trước khi thông báo đầu tiên của resize observer được gửi đến ([#8277](https://github.com/maplibre/maplibre-gl-js/issues/8277)) (by [@spliffone](https://github.com/spliffone))
- Sửa lỗi `MercatorTransform` phát sinh lỗi khi được thay đổi kích thước về chiều rộng bằng 0, và bỏ qua việc tính toán ma trận của mọi phép chiếu khi transform có chiều rộng hoặc chiều cao bằng 0 ([#8374](https://github.com/maplibre/maplibre-gl-js/pull/8374)) (by [@avosa](https://github.com/avosa))
- Sửa lỗi mỗi lần cập nhật style lại mở ra một quá trình chuyển tiếp (transition) bầu trời và ánh sáng dư thừa, khiến sự kiện `idle` không được kích hoạt trong suốt thời gian chuyển tiếp sau khi bản đồ đã hoàn tất các phần khác, và có thể làm cho bầu trời và ánh sáng chuyển tiếp theo một đường cong khác với các layer ([#8348](https://github.com/maplibre/maplibre-gl-js/issues/8348)) (by [@cherenkov](https://github.com/cherenkov))
- Sửa lỗi làm sạch DOM (DOM sanitization) đối với iframe và srcdoc ([#8396](https://github.com/maplibre/maplibre-gl-js/pull/8396)) (by [@HarelM](https://github.com/HarelM))

## 6.8.0

### ✨ Tính năng và cải tiến

- Thêm `map.getStyleUrl()`, trả về URL mà style được tải từ đó, hoặc `null` khi style được cung cấp dưới dạng object ([#7109](https://github.com/maplibre/maplibre-gl-js/issues/7109)) (by [@bradymadden97](https://github.com/bradymadden97) và [@giswqs](https://github.com/giswqs))
- Lấy mẫu đầu ra render-to-texture của địa hình thông qua mipmap với bộ lọc trilinear, giúp các layer đắp phủ (draped layers) không còn bị nhấp nháy và răng cưa (aliasing) khi pitch cao ([#8328](https://github.com/maplibre/maplibre-gl-js/pull/8328), tiếp nối [#7673](https://github.com/maplibre/maplibre-gl-js/pull/7673)) (by [@AveryanAlex](https://github.com/AveryanAlex))
- Xây dựng các instance `Intl.Segmenter` dùng cho việc tạo hình văn bản (text shaping) khi sử dụng lần đầu thay vì lúc import, giúp giảm vài mili giây thời gian tải MapLibre trên luồng chính ([#8337](https://github.com/maplibre/maplibre-gl-js/pull/8337)) (by [@cherenkov](https://github.com/cherenkov))
- Liên kết (link) các chương trình shader trước khi đọc trạng thái biên dịch của chúng, để driver có thể chồng lấn (overlap) các lần biên dịch và luồng chính chờ đợi việc biên dịch shader ít hơn ([#8338](https://github.com/maplibre/maplibre-gl-js/pull/8338)) (by [@cherenkov](https://github.com/cherenkov))
- Xây dựng pin `Marker` mặc định một lần và nhân bản (clone) nó cho từng marker, giúp việc tạo nhiều marker mặc định tốn khoảng một nửa thời gian gọi constructor ([#8340](https://github.com/maplibre/maplibre-gl-js/pull/8340)) (by [@cherenkov](https://github.com/cherenkov))
- Thêm hỗ trợ render SDF cho các fill pattern, sử dụng `fill-color` làm màu tiền cảnh ([#7747](https://github.com/maplibre/maplibre-gl-js/pull/7747)) (by [@bradymadden97](https://github.com/bradymadden97) và [@deniial00](https://github.com/deniial00))
- Cảnh báo một lần khi canvas bị giới hạn (clamped) về `maxCanvasSize`, trước đây điều này làm giảm độ phân giải render một cách âm thầm ([#8200](https://github.com/maplibre/maplibre-gl-js/issues/8200)) (by [@str0kes](https://github.com/str0kes))

### 🐞 Sửa lỗi

- Sửa lỗi popup của marker nhảy sang một bản sao thế giới (world copy) khác khi marker được di chuyển qua kinh tuyến đối cực (antimeridian) trên bản đồ đã thu nhỏ ([#5655](https://github.com/maplibre/maplibre-gl-js/issues/5655), [#8326](https://github.com/maplibre/maplibre-gl-js/pull/8326), tiếp nối [#5956](https://github.com/maplibre/maplibre-gl-js/pull/5956)) (by [@yuiseki](https://github.com/yuiseki))
- Sửa lỗi texture đắp phủ địa hình (terrain drape) không được làm mới sau khi mức zoom thay đổi, gây ra hiện tượng render cũ (stale) ở mức zoom mới ([#8251](https://github.com/maplibre/maplibre-gl-js/issues/8251)) (by [@patte](https://github.com/patte))
- Sửa lỗi khoảng hở giữa bầu trời và mặt đất khi pitch cao trong lúc globe chuyển tiếp sang mercator ([#7382](https://github.com/maplibre/maplibre-gl-js/issues/7382)) (by [@birkskyum](https://github.com/birkskyum))
- Coi một phản hồi tile trống (ví dụ HTTP 204) là không có dữ liệu: các tile raster-DEM giờ đây được tải mà không có dữ liệu độ cao thay vì thất bại với lỗi `dem dimension mismatch`, và các tile raster trống được render trong suốt ([#1551](https://github.com/maplibre/maplibre-gl-js/issues/1551)) (by [@clement-igonet](https://github.com/clement-igonet))
- Kiểm tra tính hợp lệ của layer `before` trong `map.moveLayer` trước khi sắp xếp lại, để khi truyền vào id của một layer không tồn tại, thứ tự layer sẽ giữ nguyên thay vì làm mất layer được di chuyển khỏi thứ tự ([#8301](https://github.com/maplibre/maplibre-gl-js/issues/8301)) (by [@lazerg](https://github.com/lazerg))
- Sửa lỗi các đường nối (seam) hiện rõ giữa các tile hillshade khi sử dụng nội suy tuyến tính (linear interpolation). ([#8302](https://github.com/maplibre/maplibre-gl-js/pull/8302)) (by [@Turbo87](https://github.com/Turbo87))
- Sửa lỗi bản đồ bị đóng băng khi một tác vụ render (render task) phát sinh lỗi ([#6093](https://github.com/maplibre/maplibre-gl-js/issues/6093)) (by [@UberMouse](https://github.com/UberMouse))
- Sửa lỗi `getCameraAltitude()` trả về `NaN` ở chế độ `globe` và `vertical-perspective`, khiến tính năng che khuất marker bởi địa hình (marker terrain occlusion) và kiểm tra địa hình của camera bị vô hiệu hóa; độ cao giờ đây bám theo hình cầu ([#6584](https://github.com/maplibre/maplibre-gl-js/issues/6584)) (by [@bigmistqke](https://github.com/bigmistqke) và [@patte](https://github.com/patte))
- Vẽ một biểu tượng (symbol) được nâng lên trên globe khi bản thân biểu tượng đó nằm trong tầm nhìn nhưng mặt đất bên dưới nó lại nằm sau đường chân trời; việc che khuất (occlusion) giờ đây tuân theo đường ngắm (line of sight) tới điểm được nâng lên ([#8253](https://github.com/maplibre/maplibre-gl-js/issues/8253)) (by [@clement-igonet](https://github.com/clement-igonet))
- Sửa lỗi `setTiles` tạo ra các URL tile cũ (stale) khi `loadTile` chạy trong cùng một khung hình ([#8323](https://github.com/maplibre/maplibre-gl-js/pull/8323)) (by [@johncarmack1984](https://github.com/johncarmack1984) và [@nostrorom](https://github.com/nostrorom))
- Ngăn tile bên dưới một biểu tượng được nâng lên bị loại bỏ (culled) gần đường chân trời, để một biểu tượng có `symbol-height-offset` lớn vẫn hiển thị cho đến khi nó nằm sau hành tinh ([#8316](https://github.com/maplibre/maplibre-gl-js/issues/8316)) (by [@clement-igonet](https://github.com/clement-igonet))

## 6.7.0

### ✨ Tính năng và cải tiến

- Hỗ trợ thuộc tính `font-faces` của đặc tả style, cùng với `map.setFontFaces` và `map.getFontFaces`, và cải thiện các ngôn ngữ có văn tự phức tạp như Devanagari, Khmer, Miến Điện và Do Thái ([#8237](https://github.com/maplibre/maplibre-gl-js/pull/8237)) (by [@HarelM](https://github.com/HarelM))
- Ngắt dòng các nhãn chữ Thái, Khmer, Miến Điện, Lào, Tây Tạng, Java và Bali tại ranh giới từ thay vì chạy liền thành một dòng, áp dụng cho mọi style dù có khai báo `font-faces` hay không ([#8237](https://github.com/maplibre/maplibre-gl-js/pull/8237)) (by [@HarelM](https://github.com/HarelM))
- Ném ra lỗi `GPUInitializationError` từ constructor của `Map` khi không thể tạo được ngữ cảnh (context) WebGL2, thay vì phát sự kiện `error` mà không có listener nào có thể bắt được và trả về một bản đồ được khởi tạo dở dang ([#8066](https://github.com/maplibre/maplibre-gl-js/issues/8066)) (by [@johncarmack1984](https://github.com/johncarmack1984))
- Cho phép thêm một image source mà không cần `url`. Source bắt đầu ở trạng thái rỗng và không thực hiện yêu cầu mạng nào; gọi `updateImage({image})` hoặc `updateImage({url})` sau đó để hiển thị hình ảnh ([#8167](https://github.com/maplibre/maplibre-gl-js/pull/8167)) (by [@mondsichtung](https://github.com/mondsichtung))
- Bỏ qua việc sắp xếp lại vị trí biểu tượng (symbol re-placement) khi đầu vào của nó không thay đổi, nhờ đó việc vẽ lại (repaint) do các hình ảnh style động hoặc các custom layer chỉ tốn một khung hình ([#8208](https://github.com/maplibre/maplibre-gl-js/pull/8208)) (by [@lucaswoj](https://github.com/lucaswoj))
- Thêm `Style#triggerSymbolPlacement`, giúp sắp xếp lại vị trí các biểu tượng khi có thứ gì đó bản đồ không thể tự nhận biết đã di chuyển chúng ([#8208](https://github.com/maplibre/maplibre-gl-js/pull/8208)) (by [@lucaswoj](https://github.com/lucaswoj))
- Làm cho `{validate: false}` bỏ qua bản chụp nhanh style (style snapshot) mà các hàm setter của style chỉ xây dựng để làm ngữ cảnh báo lỗi, nhờ đó việc thêm từng layer một không còn phải serialize toàn bộ style trong mỗi lần gọi ([#8259](https://github.com/maplibre/maplibre-gl-js/issues/8259)) (by [@lazerg](https://github.com/lazerg))

### 🐞 Sửa lỗi

- Vô hiệu hóa nút thu nhỏ (zoom-out) của navigation control khi các giới hạn của viewport ngăn không cho thu nhỏ thêm nữa ([#5316](https://github.com/maplibre/maplibre-gl-js/issues/5316)) (by [@miakh](https://github.com/miakh))
- Giữ lại etag của một vector tile khi tile được tải lại sau khi thay đổi style, để lần làm mới do hết hạn (expiry refresh) tiếp theo vẫn có thể bỏ qua các tile không thay đổi ([#3309](https://github.com/maplibre/maplibre-gl-js/issues/3309)) (by [@johncarmack1984](https://github.com/johncarmack1984))
- Sửa lỗi `project()` và `queryTerrainElevation` không khớp với bề mặt địa hình đã render khi phép tra cứu độ cao lấy mẫu từ một mức zoom DEM khác với lưới (mesh) đã vẽ ([#8212](https://github.com/maplibre/maplibre-gl-js/issues/8212)) (by [@johncarmack1984](https://github.com/johncarmack1984))
- Vẽ các con số (ví dụ "21" trong "반포대로21길") và các mã viết hoa ngắn (ví dụ "A1") theo chiều thẳng đứng trong các nhãn dòng dọc (vertical line labels) thay vì xoay chúng dọc theo đường ([#5404](https://github.com/maplibre/maplibre-gl-js/issues/5404)) (by [@NEKOYASAN](https://github.com/NEKOYASAN))
- Sửa lỗi camera bị giật ở cuối một cử chỉ (gesture) kéo hoặc thu phóng trên địa hình bằng cách lấy mẫu độ cao trung tâm từ bề mặt địa hình đã render ([#7989](https://github.com/maplibre/maplibre-gl-js/issues/7989), [#3982](https://github.com/maplibre/maplibre-gl-js/issues/3982)) (by [@johncarmack1984](https://github.com/johncarmack1984))
- Đảm bảo các giá trị mặc định của trạng thái style được serialize ([#8263](https://github.com/maplibre/maplibre-gl-js/pull/8263)) (by [@hiddewie](https://github.com/hiddewie))

## 6.6.0

### ✨ Tính năng và cải tiến

- Thêm hỗ trợ cho các thuộc tính layout `symbol-height-offset` và `symbol-height-anchor`, giúp nâng biểu tượng và văn bản lên phía trên bản đồ. `symbol-height-anchor` chọn xem khoảng lệch (offset) được đo từ bề mặt địa hình (`ground`, mặc định) hay từ mốc độ cao bằng 0 (`absolute`) ([#7827](https://github.com/maplibre/maplibre-gl-js/pull/7827)) (by [@HarelM](https://github.com/HarelM))
- Chọn tọa độ địa hình bằng phép dò tia (raycast) trên CPU đối với DEM thay vì đọc lại từ một framebuffer tọa độ: đạt độ phân giải DEM đầy đủ, không gây treo GPU khi có sự kiện con trỏ, và giảm khoảng 4MB bộ nhớ GPU ([#7640](https://github.com/maplibre/maplibre-gl-js/issues/7640)) (by [@johncarmack1984](https://github.com/johncarmack1984))

### 🐞 Sửa lỗi

- Sửa lỗi các nhãn chữ hiển thị tạm thời quá lớn khi thu nhỏ nhiều mức cùng lúc (ví dụ cuộn nhanh bằng con lăn chuột hoặc chụm hai ngón tay) với `text-size`/`icon-size` phụ thuộc mức zoom ([#8175](https://github.com/maplibre/maplibre-gl-js/pull/8175)) (by [@mondsichtung](https://github.com/mondsichtung))
- Sửa lỗi việc chọn tile trên globe đo khoảng cách từ điểm mặt đất bên dưới camera thay vì từ chính camera, khiến một số góc nhìn được tinh chỉnh (refine) vượt quá mức zoom yêu cầu trong khi các góc nhìn khác lại thô hơn ([#8187](https://github.com/maplibre/maplibre-gl-js/pull/8187)) (by [@Alchez](https://github.com/Alchez))
- Sửa lỗi `center`, `zoom`, `bearing`, `pitch` và `roll` của style bị bỏ qua khi bản đồ được tạo với tùy chọn `minZoom` hoặc `minPitch`, vì việc áp dụng các giới hạn đó đánh dấu transform là đã bị sửa đổi (modified) ([#5932](https://github.com/maplibre/maplibre-gl-js/issues/5932))
- Tải lên texture DEM của `color-relief` một lần cho mỗi tile thay vì trong mỗi khung hình ([#8209](https://github.com/maplibre/maplibre-gl-js/pull/8209))

## 6.5.0

### ✨ Tính năng và cải tiến

- Thêm `ImageSource.setWarp` và `ImageSource.getWarp` ở dạng thử nghiệm, cho phép lựa chọn giữa các kiểu biến dạng (warp) hình ảnh `auto`, `perspective` và `flat` ([#8172](https://github.com/maplibre/maplibre-gl-js/pull/8172)) (by [@HarelM](https://github.com/HarelM))

### 🐞 Sửa lỗi

- Sửa lỗi image source hiển thị sai trên phép chiếu globe ([#8172](https://github.com/maplibre/maplibre-gl-js/pull/8172)) (by [@HarelM](https://github.com/HarelM))
- Sửa lỗi globe tự thu phóng vào khi được kéo ra xa khỏi một cực ở mức zoom tối thiểu, nơi phần bù trừ zoom theo vĩ độ được áp dụng chồng lên trên giới hạn (clamp) riêng của constrain ([#8182](https://github.com/maplibre/maplibre-gl-js/pull/8182)) (by [@mondsichtung](https://github.com/mondsichtung))
- Sửa lỗi kéo globe từ khoảng không gian trống xung quanh nó, gần như không di chuyển bản đồ và thường đi sai hướng ([#8174](https://github.com/maplibre/maplibre-gl-js/pull/8174)) (by [@mondsichtung](https://github.com/mondsichtung))

## 6.4.1

### 🐞 Sửa lỗi

- Sửa lỗi `DOM.sanitize` để sót lại các thuộc tính nguy hiểm khi có nhiều thuộc tính liên tiếp nhau. Việc lặp qua `NamedNodeMap` trực tiếp (live) từ `elem.attributes` trong khi gọi `removeAttribute` đã bỏ qua thuộc tính ngay sau thuộc tính vừa bị xóa, nên một thuộc tính nguy hiểm thứ hai (ví dụ `ontoggle` trên một phần tử `<details open>`) có thể sống sót qua bước làm sạch (sanitisation) và sau đó bị thực thi ([#8189](https://github.com/maplibre/maplibre-gl-js/pull/8189)) (by [@0xKirisame](https://github.com/0xKirisame))
- Cung cấp cho custom layer trạng thái chuyển tiếp (transition) globe thực (live) trong `CustomRenderMethodInput.defaultProjectionData.projectionTransition`, giá trị này trước đây bị gán cứng bằng 1 cho toàn bộ quá trình chuyển tiếp globe/mercator, khiến custom layer nhảy thẳng tới trạng thái globe uốn cong hoàn toàn trong khi mọi layer khác đều chuyển tiếp mượt (ease) ([#8169](https://github.com/maplibre/maplibre-gl-js/pull/8169)) (by [@mondsichtung](https://github.com/mondsichtung))

## 6.4.0

### ✨ Tính năng và cải tiến

- Tránh gọi `Array.sort()` cho mỗi truy vấn trong việc khớp biểu tượng xuyên-tile (cross-tile symbol matching) (`TileLayerIndex.findMatches`), thay vào đó chọn ứng viên chưa được nhận (unclaimed) có chỉ số thấp nhất chỉ trong một lượt duyệt; giúp giảm chi phí xác định vị trí biểu tượng trên luồng chính đối với các layer biểu tượng dày đặc/trùng lặp ([#7797](https://github.com/maplibre/maplibre-gl-js/pull/7797)) (by [@pholmstr](https://github.com/pholmstr))
- Sử dụng `texelFetch` cho các phép tra cứu điểm dừng (stop) độ cao chính xác của DEM và color-relief thay vì tính toán tọa độ texture đã chuẩn hóa ([#7640](https://github.com/maplibre/maplibre-gl-js/issues/7640)) (by [@johncarmack1984](https://github.com/johncarmack1984))
- Làm cho các marker có thể kéo (draggable) mặc định có thể focus bằng bàn phím và di chuyển được bằng các phím mũi tên (1 px mỗi lần nhấn, 10 px khi giữ Shift); các phần tử marker tùy chỉnh vẫn do ứng dụng tự quản lý ([#8020](https://github.com/maplibre/maplibre-gl-js/issues/8020)) (by [@smmariquit](https://github.com/smmariquit))

### 🐞 Sửa lỗi

- Sửa lỗi tốc độ khung hình bị suy giảm vĩnh viễn sau khi chuyển đổi style: mỗi lần sprite được tải lại sẽ đánh dấu hình ảnh của nó là đã cập nhật mãi mãi, khiến mọi tile trong tầm nhìn phải kiểm tra lại và tải lên lại chúng trong mỗi khung hình. Đồng thời ngăn việc rò rỉ hình ảnh của một sprite đã bị thay thế, vốn trước đây không bao giờ được xóa khỏi image manager ([#8052](https://github.com/maplibre/maplibre-gl-js/issues/8052)) (by [@HarelM](https://github.com/HarelM))
- Ngăn một resolver hình ảnh style bị thiếu (missing) và bị từ chối (rejected) làm chặn các hình ảnh đã được resolve thành công trong cùng một lô (batch) ([#8146](https://github.com/maplibre/maplibre-gl-js/pull/8146/)) (by @birkskyum)
- Yêu cầu tường minh không quản lý màu sắc của trình duyệt (browser color management) khi giải mã các tile raster-DEM để giá trị độ cao được mã hóa RGB của chúng không bị thay đổi (điều mà lẽ ra sẽ xảy ra với `gfx.color_management.mode = 1` trong Firefox) ([#8125](https://github.com/maplibre/maplibre-gl-js/pull/8125)) (by [@tnikkel](https://github.com/tnikkel))
- Cho phép một thao tác abort tiếp cận được việc tải một image hoặc raster tile đang chờ (awaiting) `transformRequest` của nó, để `ImageSource.updateImage` không còn làm mất hình ảnh vừa được truyền vào và một tile bị abort sẽ không còn bị fetch nữa ([#8071](https://github.com/maplibre/maplibre-gl-js/pull/8071)) (by [@mondsichtung](https://github.com/mondsichtung))
- Sửa lỗi các raster tile bị mờ dần hiện lại (fading in) khi chúng được tải lại, gây chớp nháy nền bản đồ trong thời gian ngắn, dễ nhận thấy nhất khi chuyển đổi phép chiếu ([#8106](https://github.com/maplibre/maplibre-gl-js/pull/8106)) (by [@mondsichtung](https://github.com/mondsichtung))
- Sửa lỗi thao tác kéo (panning) globe bị đảo ngược và khựng lại gần và khi đi qua các cực, bằng cách xoay globe với một versor, giữ cho hướng kéo nhất quán ở mọi vĩ độ. Thao tác kéo cũng giảm dần (eases off) khi con trỏ tiến gần đến mép globe và tiếp tục vượt qua nó, thay vì dừng lại. Bearing vẫn được giữ nguyên trong khi kéo, như trước đây ([#5296](https://github.com/maplibre/maplibre-gl-js/issues/5296)) (by [@jcolot](https://github.com/jcolot))
- Sửa lỗi `fill-extrusion-rounded-corner-distance` tạo ra các điểm nhọn (spikes): các cung góc (corner arcs) giờ đây nằm đúng trên lưới tile số nguyên, và các góc được tạo ra bởi việc cắt tile (tile clipping) được giữ nguyên dạng sắc nhọn ([#8153](https://github.com/maplibre/maplibre-gl-js/issues/8153)) (by [@HarelM](https://github.com/HarelM))
- Sửa lỗi một cử chỉ (gesture) được giữ đứng yên trước khi thả ra vẫn khiến bản đồ bị văng đi (fling) ([#1303](https://github.com/maplibre/maplibre-gl-js/issues/1303)) (by [@zdila](https://github.com/zdila))

## 6.3.0

### ✨ Tính năng và cải tiến

- Làm cho các sự kiện bản đồ được phát/lắng nghe có kiểu (typed). Điều này có nghĩa là `map.on("something", ...)` (và `once`, `listens`) giờ đây sẽ báo lỗi TypeScript và tự động hoàn thành (autocomplete) tốt hơn nếu bạn dùng sai. Nếu bạn dựa vào việc phát/lắng nghe các sự kiện tùy chỉnh thông qua bản đồ, cách này vẫn hoạt động thông qua các lối thoát (escape hatches) `map.fire("something" as any)` -> `map.on("something" as any, ...)` ([#8072](https://github.com/maplibre/maplibre-gl-js/issues/8072)) (by [@CommanderStorm](https://github.com/CommanderStorm))
- Cho phép `StyleImageInterface` cung cấp một callback `{renderWithWebGL}` làm `data` của nó, một lối thoát (escape hatch) cho các nhà phát triển plugin và người dùng nâng cao, giúp render một hình ảnh style trên GPU thay vì di chuyển pixel của nó qua CPU. Không có gì mới có thể thực hiện được mà pixel chưa thể biểu diễn trước đây, nhưng một hình ảnh thay đổi thường xuyên, chẳng hạn như một biểu tượng động, sẽ có hiệu năng tốt hơn ([#7954](https://github.com/maplibre/maplibre-gl-js/pull/7954)) (by [@lucaswoj](https://github.com/lucaswoj))
- Sử dụng các thuộc tính vertex kiểu số nguyên (integer vertex attributes) cho dữ liệu đường (line) đã đóng gói thay vì chuyển đổi sang số thực (float conversion) ([#7640](https://github.com/maplibre/maplibre-gl-js/issues/7640)) (by [@johncarmack1984](https://github.com/johncarmack1984))
- Sử dụng các thuộc tính vertex kiểu số nguyên cho dữ liệu circle, heatmap, symbol và fill-extrusion đã đóng gói thay vì chuyển đổi sang số thực ([#7640](https://github.com/maplibre/maplibre-gl-js/issues/7640), [#8143](https://github.com/maplibre/maplibre-gl-js/pull/8143)) (by [@johncarmack1984](https://github.com/johncarmack1984))
- Thiết kế lại các bài đo hiệu năng (benchmarks) để sử dụng khả năng bench của vitest và loại bỏ bản build tùy chỉnh cho mã benchmark ([#982](https://github.com/maplibre/maplibre-gl-js/issues/982)) (by [@johncarmack1984](https://github.com/johncarmack1984))

### 🐞 Sửa lỗi

- Sửa lỗi các cử chỉ kéo/thu phóng (pan/zoom) trên địa hình làm mất điểm địa hình đang được nắm giữ: các cử chỉ giờ đây được giải quyết dựa trên độ cao của địa hình bên dưới cử chỉ đó thay vì độ cao trung tâm đã bị đóng băng, nhờ đó địa hình bên dưới con trỏ/ngón tay không còn bị trượt trong các thao tác chụm (pinch) và kéo có tâm di chuyển (moving-centroid) ([#8067](https://github.com/maplibre/maplibre-gl-js/pull/8067)) (by [@StrawberryJam22](https://github.com/StrawberryJam22))
- Sửa lỗi `ImageSource`, `VideoSource` và `CanvasSource` bị rò rỉ một texture GPU mỗi khi cập nhật hình ảnh và khi bị xóa, cũng như một texture đã đổi kích thước bị mất các thiết lập wrap và filter của nó ([#8094](https://github.com/maplibre/maplibre-gl-js/pull/8094)) (by [@mondsichtung](https://github.com/mondsichtung))
- Sửa lỗi `map.queryRenderedFeatures()` đôi khi gây ra lỗi "Out of bounds" do điều kiện tranh chấp (race condition) trong lúc đang tải dữ liệu tile ([#8064](https://github.com/maplibre/maplibre-gl-js/issues/8064)) (by [@smvjohansenbouvet](https://github.com/smvjohansenbouvet))
- Sửa lỗi việc thu phóng globe bằng con lăn chuột hoặc chụm hai ngón tay bị trôi dạt khỏi con trỏ khi globe nhỏ trên màn hình, thay vì giữ vị trí bên dưới con trỏ như khi đã zoom vào ([#8095](https://github.com/maplibre/maplibre-gl-js/pull/8095)) (by [@mondsichtung](https://github.com/mondsichtung))
- Sửa lỗi render phối cảnh (projective rendering) cho các tứ giác (quad) image source không phải hình bình hành ([#7887](https://github.com/maplibre/maplibre-gl-js/pull/7887)) (by [@i4innovationnet](https://github.com/i4innovationnet))

## 6.2.0

### ✨ Tính năng và cải tiến

- Thêm thuộc tính layout `fill-extrusion-rounded-corner-distance`, thay thế mỗi góc của fill-extrusion bằng một cung có độ dài cho trước (tính bằng mét) dọc theo các cạnh liền kề. Khoảng cách được giới hạn (clamp) ở mức 20% chiều dài mỗi cạnh liền kề để các cạnh ngắn không bị sụp, và các góc gần như thẳng (độ ngoặt dưới 5°) được giữ nguyên không thay đổi. Mặc định là `0`, giữ cho các góc sắc nhọn ([#7934](https://github.com/maplibre/maplibre-gl-js/issues/7934)) (by [@CommanderStorm](https://github.com/CommanderStorm))
- Cải thiện hiệu năng render Mercator bằng cách bỏ qua một lượt vẽ viền mặt nạ cắt (clipping mask border pass) dư thừa ([#8038](https://github.com/maplibre/maplibre-gl-js/pull/8038)) (by [@DoFabien](https://github.com/DoFabien))
- Thêm một dịch vụ docker-compose để build và phục vụ (serve) các ví dụ (#57) ([#8026](https://github.com/maplibre/maplibre-gl-js/pull/8026)) (by [@clement-igonet](https://github.com/clement-igonet))

### 🐞 Sửa lỗi

- Sửa lỗi render hiếm gặp khiến hai layer liền kề có thuộc tính data-driven khác nhau bị render sai ([#8068](https://github.com/maplibre/maplibre-gl-js/pull/8068)) (by [@CommanderStorm](https://github.com/CommanderStorm))
- Cải thiện hiệu năng lấy mẫu độ cao địa hình bằng cách cache các lần tra cứu DEM tile và các phép biến đổi tọa độ trong mỗi lần render ([#8025](https://github.com/maplibre/maplibre-gl-js/pull/8025)) (by [@DoFabien](https://github.com/DoFabien))

## 6.1.0

### ✨ Tính năng và cải tiến

- Thêm hỗ trợ cập nhật một `ImageSource` bằng một hình ảnh đã được giải mã sẵn (`HTMLImageElement`, `HTMLCanvasElement`, `ImageBitmap` hoặc `ImageData`) trực tiếp thông qua `ImageSource.updateImage({image})`, bỏ qua yêu cầu mạng ([#7944](https://github.com/maplibre/maplibre-gl-js/pull/7944)) (by [@mondsichtung](https://github.com/mondsichtung))
- Thêm `GeoJSONSource.getClusterOptions` để lấy các tùy chọn cluster hiện tại của một source (`cluster`, `clusterMaxZoom`, `clusterRadius`) ([#7948](https://github.com/maplibre/maplibre-gl-js/pull/7948)) (by [@lazerg](https://github.com/lazerg))
- Hỗ trợ biểu thức `global-state` trong các thuộc tính `sky.*`, `light.*` và `projection.type` ([#7966](https://github.com/maplibre/maplibre-gl-js/pull/7966), [#7967](https://github.com/maplibre/maplibre-gl-js/pull/7967), [#7968](https://github.com/maplibre/maplibre-gl-js/pull/7968)) (by [@CommanderStorm](https://github.com/CommanderStorm))
- Thêm `MapOptions.rotateSpeed` và `MapOptions.pitchSpeed`, số độ mà bearing/pitch thay đổi trên mỗi pixel được kéo ([#7949](https://github.com/maplibre/maplibre-gl-js/pull/7949)) (by [@clement-igonet](https://github.com/clement-igonet))
- Hiển thị con trỏ dạng nắm (grab cursor) trên các marker có thể kéo, kể cả trên các bản đồ không tương tác (non-interactive) ([#8019](https://github.com/maplibre/maplibre-gl-js/issues/8019)) (by [@hugosmoreira](https://github.com/hugosmoreira))

### 🐞 Sửa lỗi
- Sử dụng `role=img` cho các marker mặc định không tương tác và `role=button` khi chúng trở nên tương tác được ([#7790](https://github.com/maplibre/maplibre-gl-js/issues/7790)) (by [@cat0825](https://github.com/cat0825))
- Sửa lỗi phát sinh khi một thuộc tính paint chuyển tiếp (transition) giữa các mảng có độ dài khác nhau ([#6606](https://github.com/maplibre/maplibre-gl-js/issues/6606)) (by [@HarelM](https://github.com/HarelM))
- Sửa lỗi renderer bị crash khi `RasterTileSource.setTiles`/`setUrl` được gọi trong khi source chứa các tile bị lỗi ([#7911](https://github.com/maplibre/maplibre-gl-js/pull/7911)) (by [@lazerg](https://github.com/lazerg))
- Sửa lỗi các tòa nhà 3D biến mất khi camera nghiêng lên để nhìn gần đường chân trời, bằng cách mở rộng ranh giới loại bỏ tile (tile-culling) khi cạnh dưới của frustum (từ pitch và FOV) tiến gần đến phương ngang ([#7633](https://github.com/maplibre/maplibre-gl-js/issues/7633)) (by [@clement-igonet](https://github.com/clement-igonet))
- Sửa lỗi độ chính xác vĩ độ của globe trên một số GPU (ví dụ Mali) bằng cách công thức hóa lại tọa độ Y từ mercator sang hình cầu theo đại số (dùng `exp` + số học phân thức thay vì `atan`/`sin`/`cos`), tránh hiện tượng khử lẫn nhau (cancellation) do float32 và các hàm siêu việt phần cứng (hardware transcendentals) thiếu chính xác gần đường xích đạo; phép đo/hiệu chỉnh lỗi `atan` trên GPU lúc chạy (runtime) mà thay đổi này thay thế cũng đã được loại bỏ ([#7419](https://github.com/maplibre/maplibre-gl-js/issues/7419)) (by [@clement-igonet](https://github.com/clement-igonet))
- Sửa lỗi một điều kiện tranh chấp (race) trong `RasterTileSource.loadTile` và `ImageSource.load` khi một tile/hình ảnh bị abort trong lúc đang chờ (awaited) `transformRequest` đã truyền một `AbortController` undefined vào hàng đợi yêu cầu hình ảnh, khiến nó bị crash với lỗi `TypeError: Cannot read properties of undefined (reading 'signal')` ([#8004](https://github.com/maplibre/maplibre-gl-js/issues/8004)) (by [@jan-grzybek](https://github.com/jan-grzybek))
- Sửa lỗi `setTerrain` không hủy (destroy) địa hình đang hoạt động trước đó khi chuyển sang một cấu hình mới, gây rò rỉ tài nguyên GPU của nó và khiến source cũ vẫn được cấu hình là một terrain source ([#7990](https://github.com/maplibre/maplibre-gl-js/issues/7990)) (by [@lazerg](https://github.com/lazerg))
- Sửa lỗi các layer fill và line bị render hai lần gần kinh tuyến đối cực (antimeridian) trên globe khi nhìn về các cực hoặc khi đã thu nhỏ ([#6248](https://github.com/maplibre/maplibre-gl-js/issues/6248)) (by [@pabueco](https://github.com/pabueco))

## 6.0.0

Phiên bản này gộp tất cả các bản pre-release cho các thay đổi của phiên bản 6.
Xem [hướng dẫn di chuyển từ v5 sang v6](./docs/guides/v5-to-v6-migration-guide.md) để biết thêm thông tin.

### ✨ Tính năng và cải tiến

- ⚠️ Chuyển sang bản phân phối chỉ dùng ESM (`maplibre-gl.mjs`). Các bundle UMD (`maplibre-gl.js`, `maplibre-gl-csp.js`) không còn được phát hành nữa. Bundle dành riêng cho CSP cũng bị loại bỏ: bản build ESM tải worker của nó dưới dạng một URL thực, nên `worker-src blob:` không còn là bắt buộc nữa. Các bên sử dụng `<script src=".../maplibre-gl.js">` phải chuyển sang `<script type="module">`, và các bên sử dụng `import maplibregl from 'maplibre-gl'` phải chuyển sang `import * as maplibregl from 'maplibre-gl'` hoặc dùng named imports. Xem phần ESM trong tài liệu hoặc [hướng dẫn di chuyển](./docs/guides/v5-to-v6-migration-guide.md) của chúng tôi để biết các bước di chuyển. ([#6254](https://github.com/maplibre/maplibre-gl-js/pull/6254)) (by [@birkskyum](https://github.com/birkskyum))
- ⚠️ Nội suy vị trí ánh sáng theo tọa độ cầu (spherical coordinates) thay vì tọa độ Descartes (cartesian), để một quá trình chuyển tiếp giữ nguyên khoảng cách theo bán kính (radial distance) của nó. ([#7919](https://github.com/maplibre/maplibre-gl-js/pull/7919)) (by [@HarelM](https://github.com/HarelM))
- ⚠️ `styleimagemissing` giờ đây là một sự kiện chỉ để thông báo (notify-only) thay vì callback trước đây cho phép cung cấp một hình ảnh. Điều này giúp sự kiện phù hợp với ngữ nghĩa sự kiện chuẩn (thông báo, không phải giải quyết/resolve). Sử dụng `Map.setMissingStyleImageResolver` để cung cấp hình ảnh theo yêu cầu (on-demand) thông qua một hàm giờ đây cũng có thể là bất đồng bộ (async). ([#7892](https://github.com/maplibre/maplibre-gl-js/issues/7892)) (by [@birkskyum](https://github.com/birkskyum))
- ⚠️ `Map` giờ đây kết hợp (composes) một `Camera` thay vì kế thừa (extending) nó (`Map` kế thừa trực tiếp từ `Evented` và chuyển tiếp (forward) API của camera). Thuộc tính nội bộ `map.transform` đã bị loại bỏ — hãy sử dụng API công khai của map thay thế hoặc mở một PR nếu bạn cần thứ gì đó chưa được expose. Đã loại bỏ hàm hỗ trợ nội bộ `transform.getMatrixForModel` ([#7800](https://github.com/maplibre/maplibre-gl-js/pull/7800)) (by [@HarelM](https://github.com/HarelM))
- ⚠️ Tất cả các sự kiện bản đồ giờ đây là các class thực sự được khởi tạo (instantiated) khi chúng được phát ra. Đổi tên handler `BoxZoom` của `Map` từ `MapLibreZoomEvent` thành `MapBoxZoomEvent`, thêm các sự kiện `rollstart`/`roll`/`rollend` và `style.load` (dưới dạng `MapStyleLoadEvent`) vào `MapEventType`, và thêm các class sự kiện cùng type-map cho `Marker`, `Popup`, `GeolocateControl` và `FullscreenControl`. Loại bỏ `MapDataEvent`: các sự kiện `data`/`dataloading`/`dataabort` giờ đây là `MapSourceDataEvent | MapStyleDataEvent`, nên các sự kiện dữ liệu source giờ mang đầy đủ thông tin source (`sourceId`, `tile`, `sourceDataType`, …). Thêm `MapMovementEvent` làm kiểu cho tất cả các sự kiện chuyển tiếp camera (camera-transition) (`move`/`zoom`/`rotate`/`pitch`/`roll`/`drag` và các biến thể `start`/`end` của chúng). `Evented` giờ đây là generic theo một type-map sự kiện (`Evented<EventType>`) và là `abstract`, nhờ đó các lớp con tự động nhận được `on`/`once`/`off` có kiểu chặt chẽ (strongly-typed) mà không cần khai báo lại các overload — điều này cũng gán kiểu cho các sự kiện trên `Camera`/`Style` (thông qua `MapEventType`) và trên các source (thông qua `SourceEventType` mới) ([#7789](https://github.com/maplibre/maplibre-gl-js/pull/7789)) (by [@HarelM](https://github.com/HarelM))
- ⚠️ Cập nhật maplibre-gl-style-spec lên phiên bản 25, giờ đây sẽ ném ra lỗi với mức độ nghiêm trọng cảnh báo (warning severity) thay vì âm thầm thất bại khi gặp các biểu thức (expressions) kiểu cũ (legacy) ([#7792](https://github.com/maplibre/maplibre-gl-js/issues/7792)) (by [@HarelM](https://github.com/HarelM))
- ⚠️ Loại bỏ các tham chiếu mapbox còn sót lại trong mã nguồn và trong các bài test. Điều này thay đổi `#pragma mapbox` thành `#pragma maplibre` trong trường hợp bạn có mã shader dựa vào nó. ([#7761](https://github.com/maplibre/maplibre-gl-js/issues/7761)) (by [@HarelM](https://github.com/HarelM))
- ⚠️ Giá trị mặc định của `zoomLevelsToOverscale` đã được đổi thành 4 để hỗ trợ xử lý tốt hơn các mức zoom cao với nhãn dày đặc. Điều này có thể có tác dụng phụ là thay đổi đôi chút kết quả của `queryRenderedFeatures` và một số cách render nhãn trung tâm của đa giác (polygon center label). Để hoàn tác thay đổi này, hãy đặt giá trị thành `undefined` ([#7537](https://github.com/maplibre/maplibre-gl-js/issues/7537)) (by [@HarelM](https://github.com/HarelM))
- ⚠️ Loại bỏ tham số thứ hai của `GeoJSONSource.setData` (`waitForCompletion`) và loại bỏ giá trị trả về `this` để cho phép các thay đổi API trong tương lai ([#7538](https://github.com/maplibre/maplibre-gl-js/issues/7538)) (by [@HarelM](https://github.com/HarelM))
- ⚠️ Mục tiêu TypeScript đã được cập nhật lên ES2022.
  Điều này giúp tạo ra bundle nhỏ hơn và cải thiện hiệu năng thực thi (runtime) bằng cách dựa vào các tính năng JavaScript hiện đại và giảm việc chuyển mã (transpilation). Các bên nhắm đến các trình duyệt hoặc sử dụng một số công cụ (tooling) phát hành trước năm 2022 có thể cần chuyển mã MapLibre hoặc cập nhật. Thay đổi này cũng đồng bộ tất cả các cấu hình build nội bộ về một mục tiêu duy nhất thay vì ES2016 + ES2019, tránh sự không nhất quán trong mã được sinh ra. ([#7404](https://github.com/maplibre/maplibre-gl-js/pull/7404)) (by [@CommanderStorm](https://github.com/CommanderStorm))
- ⚠️ Hỗ trợ WebGL (v1) đã bị loại bỏ; giờ đây bắt buộc phải có WebGL2.
  Về mặt thực tế, điều này sẽ không thay đổi cách bạn tương tác với bản đồ.
  Điều này cho phép cải thiện hiệu năng (ví dụ line opacity), nâng cao Terrain3D, và một số bản sửa lỗi.
  Hỗ trợ WebGL2 đã được phổ biến rộng rãi trong nhiều năm, và việc sử dụng đường dẫn cũ (legacy path) đã chững lại, nên việc duy trì nó không còn hợp lý với độ phức tạp tăng thêm.
  Để giảm nhẹ thay đổi phá vỡ tương thích này, chúng tôi cũng đã tái cấu trúc cách xử lý trường hợp không có webgl khả dụng (ví dụ do hạn chế của trình duyệt).
  Giờ đây bạn có thể lắng nghe lỗi webgl thông qua `.on("error")`.
  Xem [caniuse.com/webgl2](https://caniuse.com/webgl2) để biết mức độ hỗ trợ trong hệ sinh thái và [RFC của chúng tôi để biết chi tiết](https://github.com/maplibre/maplibre-gl-js/discussions/6017). ([#7453](https://github.com/maplibre/maplibre-gl-js/pull/7453)) (by [@CommanderStorm](https://github.com/CommanderStorm))
- ⚠️ Hỗ trợ các object lồng nhau trong geojson, đây là một thay đổi phá vỡ tương thích vì nó mã hóa `__$json__` trước các thuộc tính từng là một object. Nó cũng phân tích ngược (parse back) lại chúng, nhưng đây vẫn là một thay đổi phá vỡ tương thích nếu bạn từng cho rằng lỗi này tồn tại. ([#6992](https://github.com/maplibre/maplibre-gl-js/pull/6992)) (by [HarelM](https://github.com/HarelM))
- ⚠️ Cải thiện kiểu cho `{get,set}LayoutProperty`, `{get,set}PaintProperty` để trả về kiểu thực tế thay vì `string`/`any` ([#7481](https://github.com/maplibre/maplibre-gl-js/pull/7481)) (by [@CommanderStorm](https://github.com/CommanderStorm))
- ⚠️ Tái cấu trúc phần điều khiển vị trí dựa trên `Hash` (tùy chọn đồng bộ trạng thái bản đồ vào URL như `#map=5/1/2`) để sử dụng `URLSearchParams` ở bên trong. Điều này cải thiện khả năng mở rộng cho các trường hợp sử dụng tùy chỉnh, nhưng có thể làm hỏng mã hiện có dựa vào cách triển khai trước đây. Nó cũng thay đổi cách một số trường hợp biên (edge case) được phân tích cú pháp — ví dụ, các chuỗi như `#10%2F3.00%2F-1.00` giờ đây được chấp nhận, và các hash như `#foo` được chuẩn hóa thành `#foo=`. ([#7073](https://github.com/maplibre/maplibre-gl-js/pull/7073)) (by [@CommanderStorm](https://github.com/CommanderStorm))
- Kiểm tra tính hợp lệ của terrain được truyền vào `map.setTerrain`, vốn trước đây được áp dụng mà không kiểm tra ([#7941](https://github.com/maplibre/maplibre-gl-js/pull/7941)) (by [@HarelM](https://github.com/HarelM))
- Cải thiện các cảnh báo lỗi lúc chạy (runtime) để chỉ ra đúng vị trí trong style gây ra lỗi (ví dụ `layers[3].paint.line-color`, `layers[3].filter`) thay vì chỉ ghi log thông báo lỗi trần trụi ([#7869](https://github.com/maplibre/maplibre-gl-js/pull/7869)) (by [@CommanderStorm](https://github.com/CommanderStorm))
- Cải thiện hiệu năng chuẩn bị render-to-texture của địa hình bằng cách bỏ qua các source không được render vào texture địa hình ([#7863](https://github.com/maplibre/maplibre-gl-js/pull/7863)) (by [@DoFabien](https://github.com/DoFabien))
- Thêm `Map.setMissingStyleImageResolver` để giải quyết (resolve) các hình ảnh style bị thiếu bằng các callback đồng bộ hoặc bất đồng bộ ([#7850](https://github.com/maplibre/maplibre-gl-js/pull/7850)) (by [@birkskyum](https://github.com/birkskyum))
- Thêm `RasterTileSource#setPremultiplyAlpha(false)` để giữ nguyên các giá trị RGBA gốc của tile khi alpha được dùng cho dữ liệu thay vì cho độ mờ (opacity) ([#7235](https://github.com/maplibre/maplibre-gl-js/pull/7235)) (by [@plantain](https://github.com/plantain)).
- Loại bỏ phụ thuộc `@mapbox/whoots-js` đã bị lưu trữ (archived) bằng cách nhúng trực tiếp (inlining) hàm hỗ trợ `getTileBBox` duy nhất của nó ([#7838](https://github.com/maplibre/maplibre-gl-js/pull/7838)) (by [@qorexdevs](https://github.com/qorexdevs))
- Gộp (debounce) việc phát broadcast `setImages` xuống còn một lần mỗi khung hình animation, sửa lỗi chi phí serialize theo cấp độ O(n²) khi thêm nhiều hình ảnh ([#7614](https://github.com/maplibre/maplibre-gl-js/pull/7614)) (by [@bradymadden97](https://github.com/bradymadden97))
- Cải thiện hiệu năng render địa hình bằng cách tránh các lượt tra cứu dữ liệu địa hình không cần thiết trong các lượt render-to-texture Mercator ([#7833](https://github.com/maplibre/maplibre-gl-js/pull/7833)) (by [@DoFabien](https://github.com/DoFabien))
- Giảm áp lực cấp phát bộ nhớ (allocation pressure) khi xây dựng dữ liệu DEM và lấy mẫu độ cao địa hình ([#7814](https://github.com/maplibre/maplibre-gl-js/pull/7814)) (by [@DoFabien](https://github.com/DoFabien))
- Tái sử dụng texture DEM địa hình khi chuẩn bị địa hình ([#7813](https://github.com/maplibre/maplibre-gl-js/pull/7813)) (by [@DoFabien](https://github.com/DoFabien))
- Thêm các thuộc tính paint `fill-layer-opacity` và `line-layer-opacity`, áp dụng độ mờ (opacity) đồng nhất cho toàn bộ đầu ra của layer ([#7570](https://github.com/maplibre/maplibre-gl-js/pull/7570)) (by [@CommanderStorm](https://github.com/CommanderStorm))
- Build main và worker trong cùng một ngữ cảnh build để trích xuất chunk dùng chung ([#7745](https://github.com/maplibre/maplibre-gl-js/pull/7745)) (by [@dangkyokhoang](https://github.com/dangkyokhoang))
- Hoàn tác (revert) tính năng render ra ngoài màn hình (offscreen rendering) được điều khiển bởi `line-opacity` đã được giới thiệu trong [#7490](https://github.com/maplibre/maplibre-gl-js/pull/7490) ([#7764](https://github.com/maplibre/maplibre-gl-js/pull/7764)) (by [@CommanderStorm](https://github.com/CommanderStorm)). Việc sửa lỗi hiện tượng chồng lấn (overlap artefact) giờ đây được điều khiển bởi `line-layer-opacity` thay thế.
- Cải thiện các kiểu ma trận nền tảng (backing types) cho `ProjectionData` dùng cho renderer và các ma trận phép chiếu của custom layer ([#6316](https://github.com/maplibre/maplibre-gl-js/issues/6316)) (by [@cat0825](https://github.com/cat0825))
- Tối ưu hóa: loại bỏ (culling) độ mờ trong vertex shader cho line và fill [#7711](https://github.com/maplibre/maplibre-gl-js/pull/7711) (by [@xavierjs](https://github.com/xavierjs))
- Sử dụng một FBO dùng chung cho việc render cache địa hình ra texture [#7637](https://github.com/maplibre/maplibre-gl-js/pull/7637) (by [@xavierjs](https://github.com/xavierjs))
- Sử dụng `flat` để bỏ qua nội suy (interpolation) cho các biến shader (varyings) không đổi ([#7661](https://github.com/maplibre/maplibre-gl-js/pull/7661)) (by [@birkskyum](https://github.com/birkskyum))
- Thay thế texImage2D bằng texStorage2D cho các texture bất biến (immutable) ([#7643](https://github.com/maplibre/maplibre-gl-js/pull/7643)) (by [@birkskyum](https://github.com/birkskyum))
- Bật mipmap cho các raster tile có kích thước không phải lũy thừa của 2, giảm hiện tượng răng cưa (aliasing) khi pitch cao ([#7641](https://github.com/maplibre/maplibre-gl-js/pull/7641)) (by [@birkskyum](https://github.com/birkskyum))
- Sử dụng các bộ định danh bố cục (layout qualifiers) của GLSL ES 3.00 cho vị trí thuộc tính vertex, thay thế các lệnh gọi `bindAttribLocation` lúc chạy ([#7644](https://github.com/maplibre/maplibre-gl-js/pull/7644)) (by [@birkskyum](https://github.com/birkskyum))
- Áp dụng isolatedDeclarations và chuyển bộ sinh (emitter) dts từ tsgo sang oxc ([#7566](https://github.com/maplibre/maplibre-gl-js/pull/7566)) (by [@birkskyum](https://github.com/birkskyum))
- Cải thiện hiệu năng địa hình 3D ([#7549](https://github.com/maplibre/maplibre-gl-js/pull/7549)) (by [@lucaswoj](https://github.com/lucaswoj))
- Thay thế dts-bundle-generator bằng rolldown-plugin-dts, giúp việc sinh file .d.ts nhanh hơn 78,2 lần. ([#7564](https://github.com/maplibre/maplibre-gl-js/pull/7564)) (by [@birkskyum](https://github.com/birkskyum))
- Thay thế ts-node bằng hỗ trợ TypeScript gốc (native) của Node 24 cho các script build. ([#7565](https://github.com/maplibre/maplibre-gl-js/pull/7565)) (by [@birkskyum](https://github.com/birkskyum))
- Nâng cấp typescript lên phiên bản beta v7 - kiểm tra kiểu (typecheck) nhanh hơn 3,5 lần ([#7556](https://github.com/maplibre/maplibre-gl-js/pull/7556)) (by [@birkskyum](https://github.com/birkskyum))
- Thêm một tùy chọn tạo bản đồ mới, `terrainSkirtLength`, cho phép loại bỏ các hiện tượng nhân tạo (artifact) dọc trông thiếu thẩm mỹ khi sử dụng địa hình cùng với nền trong suốt ([#7523](https://github.com/maplibre/maplibre-gl-js/pull/7523)) (by [@safwat-halaby](https://github.com/safwat-halaby))
- Đóng gói (bundle) bằng Rolldown thay vì Rollup ([#7555](https://github.com/maplibre/maplibre-gl-js/pull/7555)) (by [@birkskyum](https://github.com/birkskyum))
- Tối ưu hóa cho Feature State: Thay thế Object được đánh chỉ mục bằng chuỗi (String-Indexed Object) bằng Array (tăng tốc tới 3,4 lần) ([#7550](https://github.com/maplibre/maplibre-gl-js/pull/7550)) (by [@xavierjs](https://github.com/xavierjs))
- Expose hàm `getProjectionData` trong các object tham số (args) của custom layer ([#7471](https://github.com/maplibre/maplibre-gl-js/pull/7471)) (by [@kubapelc](https://github.com/kubapelc))
- Đánh dấu `sideEffects` của package là chỉ dành cho CSS trong metadata của package, điều này có thể cải thiện tree-shaking và giảm kích thước bundle ở một số bundler ([#7258](https://github.com/maplibre/maplibre-gl-js/pull/7258)) (by [@CommanderStorm](https://github.com/CommanderStorm))

### 🐞 Sửa lỗi

- ⚠️ Sửa lỗi các đường line trong suốt, chồng lấn lên nhau tạo ra hiện tượng nhân tạo (artefacts). Lỗi này được sửa cho `line-opacity`, nhưng cố tình không sửa cho các thuộc tính `line-color` trong suốt, do đó vẫn cho phép các màu trong suốt chồng hiệu ứng lên nhau. ([#7490](https://github.com/maplibre/maplibre-gl-js/pull/7490)) (by [@CommanderStorm](https://github.com/CommanderStorm))
- ⚠️ Vô hiệu hóa việc scale icon theo offset, đây là một thay đổi phá vỡ tương thích về mặt hiển thị (render breaking change) mà chúng tôi đã quyết định áp dụng đồng thời trong cả maplibre-gl-js và maplibre-native ([#7742](https://github.com/maplibre/maplibre-gl-js/issues/7742)) (by [@springmeyer](https://github.com/springmeyer) và [@HarelM](https://github.com/HarelM))
- Ghi log các cảnh báo kiểm tra hợp lệ (validation) của style thay vì coi chúng là lỗi, để một filter kết hợp cú pháp legacy và biểu thức (expression) không còn làm hủy bỏ việc tải style và làm trắng bản đồ ([#7941](https://github.com/maplibre/maplibre-style-spec/pull/7941)) (by [@HarelM](https://github.com/HarelM))
- Kiểm tra tính hợp lệ của các source `raster-dem` được truyền vào `map.addSource`, vốn trước đây bị bỏ qua. Ngăn một loại source mà đặc tả style không có schema (chẳng hạn một loại được đăng ký bằng `addSourceType`) làm hỏng toàn bộ style. Trước đây chỉ có `canvas` được cho phép đi qua ([#7941](https://github.com/maplibre/maplibre-gl-js/pull/7941)) (by [@HarelM](https://github.com/HarelM))
- Sửa lỗi `line-layer-opacity`/`fill-layer-opacity` cắt mất (clip away) một layer tiếp theo dùng chung source ([#7867](https://github.com/maplibre/maplibre-gl-js/pull/7867)) (by [@CommanderStorm](https://github.com/CommanderStorm))
- Sửa lỗi camera nhảy giật trong flyTo khi có đặt minZoom ([#7743](https://github.com/maplibre/maplibre-gl-js/pull/7743)) (by [@YuChunTsao](https://github.com/YuChunTsao))
- Sửa lỗi các framebuffer độ sâu và tọa độ của địa hình bị cũ (stale) khi các tile địa hình thay đổi mà camera không di chuyển ([#7812](https://github.com/maplibre/maplibre-gl-js/pull/7812)) (by [@DoFabien](https://github.com/DoFabien))
- Sửa lỗi rò rỉ bộ nhớ khi việc abort một yêu cầu worker (ví dụ một lần tải GeoJSON tile bị hủy trong khi đang kéo bản đồ) khiến promise của nó chờ mãi mãi, nên khung hình bất đồng bộ đang chờ và mọi thứ nó đã bắt giữ (captured) không bao giờ được giải phóng; `Actor.sendAsync` giờ đây sẽ reject với một `AbortError` khi bị abort ([#7826](https://github.com/maplibre/maplibre-gl-js/pull/7826)) (by [@kamil-sienkiewicz-asi](https://github.com/kamil-sienkiewicz-asi))
- Bỏ qua các thuộc tính `undefined` trong quá trình serialize dữ liệu cho worker ([#7801](https://github.com/maplibre/maplibre-gl-js/pull/7801)) (by [@xavierjs](https://github.com/xavierjs))
- Sửa lỗi tải worker dạng module xuyên nguồn gốc (cross-origin) để giữ đúng ngữ nghĩa ESM ([#7796](https://github.com/maplibre/maplibre-gl-js/pull/7796)) (by [@dangkyokhoang](https://github.com/dangkyokhoang))
- Sửa lỗi các lần tải lại (reload) tile xung đột gây ra lỗi trong `queryRenderedFeatures` ([#7765](https://github.com/maplibre/maplibre-gl-js/pull/7765)) (by [@ckolin](https://github.com/ckolin))
- Sửa lỗi điều kiện tranh chấp (race condition) trong geojson source sau khi khởi tạo và cập nhật dữ liệu nhanh ([#7734](https://github.com/maplibre/maplibre-gl-js/issues/7734)) (by [@HarelM](https://github.com/HarelM))
- Sửa lỗi camera nhảy giật khi dragend với globe + terrain ở pitch thấp ([#7736](https://github.com/maplibre/maplibre-gl-js/pull/7736)) (by [@kodeezabdullah](https://github.com/kodeezabdullah))
- Sửa lỗi hiển thị web font bằng cách chờ (awaiting) `document.fonts.load()` trước khi khởi tạo TinySDF ([#7735](https://github.com/maplibre/maplibre-gl-js/pull/7735)) (by [@kodeezabdullah](https://github.com/kodeezabdullah))
- Loại bỏ việc kiểm tra tính toàn vẹn (completeness check) của framebuffer, vốn ném ra một lỗi `Framebuffer is not complete` không được xử lý khi mất tài nguyên GPU tạm thời (ví dụ khi một tab thức dậy từ trạng thái ngủ); các framebuffer không hoàn chỉnh giờ đây tự phục hồi (self-heal) ở khung hình kế tiếp thay vào đó ([#7303](https://github.com/maplibre/maplibre-gl-js/pull/7303)) (by [@johanrd](https://github.com/johanrd))
- Sửa lỗi xử lý URL blob xuyên nguồn gốc (cross-origin) trong các tiện ích Ajax ([#7675](https://github.com/maplibre/maplibre-gl-js/pull/7675)) (by [@katemihalikova](https://github.com/katemihalikova))
- Tránh các TypeError phát sinh từ các phương thức của style khi ngữ cảnh (context) WebGL bị mất ([#7710](https://github.com/maplibre/maplibre-gl-js/issues/7710)) (by [@cyphercodes](https://github.com/cyphercodes))
- `querySourceFeatures()` ném ra lỗi 'Block overruns tile' trên các tile MLT bị overzoom vì mã hóa được báo cáo không khớp với dữ liệu MVT đã được mã hóa lại ([#7707](https://github.com/maplibre/maplibre-gl-js/pull/7707)) (by [@ted-piotrowski](https://github.com/ted-piotrowski))
- Sửa lỗi kiểm tra độ dài hình học (geometry length) cho đa giác và đường trong LineBucket sau khi cắt bớt các đỉnh (vertex) trùng lặp ([#7638](https://github.com/maplibre/maplibre-gl-js/pull/7638)) (by [@widefire](https://github.com/widefire))
- Quá trình chuyển tiếp theo bước (step transition) của `line-dasharray` bị chậm mất một mức zoom khi các nhánh của bước (step) là data-driven ([#7705](https://github.com/maplibre/maplibre-gl-js/pull/7705)) (by [@lucaswoj](https://github.com/lucaswoj))
- Sửa lỗi việc xóa hàng loạt (bulk remove) feature state cộng với thao tác đặt trạng thái theo từng id (per-id set) không xóa được trạng thái của feature đầu tiên ([#7554](https://github.com/maplibre/maplibre-gl-js/pull/7554)) (by [@xavierjs](https://github.com/xavierjs))
- Loại bỏ lỗi khi actor không có loại thông điệp (message type) được đăng ký, để cải thiện khả năng sử dụng các thông điệp tùy chỉnh trong worker ([#7589](https://github.com/maplibre/maplibre-gl-js/issues/7589)) (by [@HarelM](https://github.com/HarelM))
- Tự động tải module worker khi sử dụng qua CDN ([#7595](https://github.com/maplibre/maplibre-gl-js/pull/7595)) (by [@birkskyum](https://github.com/birkskyum))
- Sửa lỗi số lượng lớn các khóa feature state gây ra hiện tượng lag khi zoom lúc tải các tile đã cache ([#7590](https://github.com/maplibre/maplibre-gl-js/pull/7590)) (by [@xavierjs](https://github.com/xavierjs))
- Sửa lỗi khi mức zoom tối đa của bản đồ và mức zoom tối đa của source gần bằng nhau ([#7567](https://github.com/maplibre/maplibre-gl-js/issues/7567)) (by [@HarelM](https://github.com/HarelM))

## 6.0.0-22

### ✨ Tính năng và cải tiến

- Kiểm tra tính hợp lệ của terrain được truyền vào `map.setTerrain`, vốn trước đây được áp dụng mà không kiểm tra ([#7941](https://github.com/maplibre/maplibre-gl-js/pull/7941)) (by [@HarelM](https://github.com/HarelM))
- Cải thiện các cảnh báo lỗi lúc chạy để chỉ ra đúng vị trí trong style gây ra lỗi (ví dụ `layers[3].paint.line-color`, `layers[3].filter`) thay vì chỉ ghi log thông báo lỗi trần trụi ([#7869](https://github.com/maplibre/maplibre-gl-js/pull/7869)) (by [@CommanderStorm](https://github.com/CommanderStorm))
- ⚠️ Nội suy vị trí ánh sáng theo tọa độ cầu thay vì tọa độ Descartes, để một quá trình chuyển tiếp giữ nguyên khoảng cách theo bán kính. ([#7919](https://github.com/maplibre/maplibre-gl-js/pull/7919)) (by [@HarelM](https://github.com/HarelM))

### 🐞 Sửa lỗi

- Ghi log các cảnh báo kiểm tra hợp lệ của style thay vì coi chúng là lỗi, để một filter kết hợp cú pháp legacy và biểu thức không còn làm hủy bỏ việc tải style và làm trắng bản đồ ([#7941](https://github.com/maplibre/maplibre-style-spec/pull/7941)) (by [@HarelM](https://github.com/HarelM))
- Kiểm tra tính hợp lệ của các source `raster-dem` được truyền vào `map.addSource`, vốn trước đây bị bỏ qua. Ngăn một loại source mà đặc tả style không có schema (chẳng hạn một loại được đăng ký bằng `addSourceType`) làm hỏng toàn bộ style. Trước đây chỉ có `canvas` được cho phép đi qua ([#7941](https://github.com/maplibre/maplibre-gl-js/pull/7941)) (by [@HarelM](https://github.com/HarelM))

## 6.0.0-21

### ✨ Tính năng và cải tiến

- Cải thiện hiệu năng chuẩn bị render-to-texture của địa hình bằng cách bỏ qua các source không được render vào texture địa hình ([#7863](https://github.com/maplibre/maplibre-gl-js/pull/7863)) (by [@DoFabien](https://github.com/DoFabien))
- Thêm `Map.setMissingStyleImageResolver` để giải quyết các hình ảnh style bị thiếu bằng các callback đồng bộ hoặc bất đồng bộ ([#7850](https://github.com/maplibre/maplibre-gl-js/pull/7850)) (by [@birkskyum](https://github.com/birkskyum))
- ⚠️ Ngừng cho phép các listener của `styleimagemissing` giải quyết (resolve) yêu cầu hình ảnh hiện tại; hãy dùng `Map.setMissingStyleImageResolver` thay thế ([#7892](https://github.com/maplibre/maplibre-gl-js/issues/7892)) (by [@birkskyum](https://github.com/birkskyum))
- Thêm `RasterTileSource#setPremultiplyAlpha(false)` để giữ nguyên các giá trị RGBA gốc của tile khi alpha được dùng cho dữ liệu thay vì cho độ mờ ([#7235](https://github.com/maplibre/maplibre-gl-js/pull/7235)) (by [@plantain](https://github.com/plantain)).

## 6.0.0-20

### ✨ Tính năng và cải tiến

- ⚠️ `Map` giờ đây kết hợp một `Camera` thay vì kế thừa nó (`Map` kế thừa trực tiếp từ `Evented` và chuyển tiếp API của camera). Thuộc tính nội bộ `map.transform` đã bị loại bỏ — hãy sử dụng API công khai của map thay thế hoặc mở một PR nếu bạn cần thứ gì đó chưa được expose. Đã loại bỏ hàm hỗ trợ nội bộ `transform.getMatrixForModel` ([#7800](https://github.com/maplibre/maplibre-gl-js/pull/7800)) (by [@HarelM](https://github.com/HarelM))

### 🐞 Sửa lỗi

- Sửa lỗi `line-layer-opacity`/`fill-layer-opacity` cắt mất một layer tiếp theo dùng chung source ([#7867](https://github.com/maplibre/maplibre-gl-js/pull/7867)) (by [@CommanderStorm](https://github.com/CommanderStorm))
- Sửa lỗi camera nhảy giật trong flyTo khi có đặt minZoom ([#7743](https://github.com/maplibre/maplibre-gl-js/pull/7743)) (by [@YuChunTsao](https://github.com/YuChunTsao))

## 6.0.0-19

### ✨ Tính năng và cải tiến

- Loại bỏ phụ thuộc `@mapbox/whoots-js` đã bị lưu trữ bằng cách nhúng trực tiếp hàm hỗ trợ `getTileBBox` duy nhất của nó ([#7838](https://github.com/maplibre/maplibre-gl-js/pull/7838)) (by [@qorexdevs](https://github.com/qorexdevs))
- Gộp (debounce) việc phát broadcast `setImages` xuống còn một lần mỗi khung hình animation, sửa lỗi chi phí serialize theo cấp độ O(n²) khi thêm nhiều hình ảnh ([#7614](https://github.com/maplibre/maplibre-gl-js/pull/7614)) (by [@bradymadden97](https://github.com/bradymadden97))

### 🐞 Sửa lỗi

- Sửa lỗi các framebuffer độ sâu và tọa độ của địa hình bị cũ khi các tile địa hình thay đổi mà camera không di chuyển ([#7812](https://github.com/maplibre/maplibre-gl-js/pull/7812)) (by [@DoFabien](https://github.com/DoFabien))

## 6.0.0-18

### ✨ Tính năng và cải tiến

- Cải thiện hiệu năng render địa hình bằng cách tránh các lượt tra cứu dữ liệu địa hình không cần thiết trong các lượt render-to-texture Mercator ([#7833](https://github.com/maplibre/maplibre-gl-js/pull/7833)) (by [@DoFabien](https://github.com/DoFabien))
- Giảm áp lực cấp phát bộ nhớ khi xây dựng dữ liệu DEM và lấy mẫu độ cao địa hình ([#7814](https://github.com/maplibre/maplibre-gl-js/pull/7814)) (by [@DoFabien](https://github.com/DoFabien))
- Tái sử dụng texture DEM địa hình khi chuẩn bị địa hình ([#7813](https://github.com/maplibre/maplibre-gl-js/pull/7813)) (by [@DoFabien](https://github.com/DoFabien))

### 🐞 Sửa lỗi

- Sửa lỗi rò rỉ bộ nhớ khi việc abort một yêu cầu worker (ví dụ một lần tải GeoJSON tile bị hủy trong khi đang kéo bản đồ) khiến promise của nó chờ mãi mãi, nên khung hình bất đồng bộ đang chờ và mọi thứ nó đã bắt giữ không bao giờ được giải phóng; `Actor.sendAsync` giờ đây sẽ reject với một `AbortError` khi bị abort ([#7826](https://github.com/maplibre/maplibre-gl-js/pull/7826)) (by [@kamil-sienkiewicz-asi](https://github.com/kamil-sienkiewicz-asi))

## 6.0.0-17

### ✨ Tính năng và cải tiến

- ⚠️ Tất cả các sự kiện bản đồ giờ đây là các class thực sự được khởi tạo khi chúng được phát ra. Đổi tên `MapLibreZoomEvent` thành `MapBoxZoomEvent`, thêm các sự kiện `rollstart`/`roll`/`rollend` và `style.load` (dưới dạng `MapStyleLoadEvent`) vào `MapEventType`, và thêm các class sự kiện cùng type-map cho `Marker`, `Popup`, `GeolocateControl` và `FullscreenControl`. Loại bỏ `MapDataEvent`: các sự kiện `data`/`dataloading`/`dataabort` giờ đây là `MapSourceDataEvent | MapStyleDataEvent`, nên các sự kiện dữ liệu source giờ mang đầy đủ thông tin source (`sourceId`, `tile`, `sourceDataType`, …). Thêm `MapMovementEvent` làm kiểu cho tất cả các sự kiện chuyển tiếp camera (`move`/`zoom`/`rotate`/`pitch`/`roll`/`drag` và các biến thể `start`/`end` của chúng). `Evented` giờ đây là generic theo một type-map sự kiện (`Evented<EventType>`) và là `abstract`, nhờ đó các lớp con tự động nhận được `on`/`once`/`off` có kiểu chặt chẽ mà không cần khai báo lại các overload — điều này cũng gán kiểu cho các sự kiện trên `Camera`/`Style` (thông qua `MapEventType`) và trên các source (thông qua `SourceEventType` mới) ([#7789](https://github.com/maplibre/maplibre-gl-js/pull/7789)) (by [@HarelM](https://github.com/HarelM))

### 🐞 Sửa lỗi

- Bỏ qua các thuộc tính `undefined` trong quá trình serialize dữ liệu cho worker ([#7801](https://github.com/maplibre/maplibre-gl-js/pull/7801)) (by [@xavierjs](https://github.com/xavierjs))

## 6.0.0-16

### ✨ Tính năng và cải tiến

- ⚠️ Cập nhật maplibre-gl-style-spec lên phiên bản 25, có một thay đổi phá vỡ tương thích trong việc kiểm tra hợp lệ biểu thức legacy ([#7792](https://github.com/maplibre/maplibre-gl-js/issues/7792)) (by [@HarelM](https://github.com/HarelM))

### 🐞 Sửa lỗi

- Sửa lỗi tải worker dạng module xuyên nguồn gốc để giữ đúng ngữ nghĩa ESM ([#7796](https://github.com/maplibre/maplibre-gl-js/pull/7796)) (by [@dangkyokhoang](https://github.com/dangkyokhoang))

## 6.0.0-15

### ✨ Tính năng và cải tiến

- Thêm các thuộc tính paint `fill-layer-opacity` và `line-layer-opacity`, áp dụng độ mờ đồng nhất cho toàn bộ đầu ra của layer ([#7570](https://github.com/maplibre/maplibre-gl-js/pull/7570)) (by [@CommanderStorm](https://github.com/CommanderStorm))
- Build main và worker trong cùng một ngữ cảnh build để trích xuất chunk dùng chung ([#7745](https://github.com/maplibre/maplibre-gl-js/pull/7745)) (by [@dangkyokhoang](https://github.com/dangkyokhoang))

### 🐞 Sửa lỗi

- Sửa lỗi các lần tải lại tile xung đột gây ra lỗi trong `queryRenderedFeatures` ([#7765](https://github.com/maplibre/maplibre-gl-js/pull/7765)) (by [@ckolin](https://github.com/ckolin))

## 6.0.0-14

### ✨ Tính năng và cải tiến

- Hoàn tác tính năng render ra ngoài màn hình được điều khiển bởi `line-opacity` đã được giới thiệu trong [#7490](https://github.com/maplibre/maplibre-gl-js/pull/7490) ([#7764](https://github.com/maplibre/maplibre-gl-js/pull/7764)) (by [@CommanderStorm](https://github.com/CommanderStorm)). Việc sửa lỗi hiện tượng chồng lấn giờ đây được điều khiển bởi `line-layer-opacity` thay thế.
- ⚠️ Loại bỏ các tham chiếu mapbox còn sót lại trong mã nguồn và trong các bài test. Điều này thay đổi `#pragma mapbox` thành `#pragma maplibre` trong trường hợp bạn có mã shader dựa vào nó. ([#7761](https://github.com/maplibre/maplibre-gl-js/issues/7761)) (by [@HarelM](https://github.com/HarelM))

### 🐞 Sửa lỗi

- Sửa lỗi điều kiện tranh chấp trong geojson source sau khi khởi tạo và cập nhật dữ liệu nhanh ([#7734](https://github.com/maplibre/maplibre-gl-js/issues/7734)) (by [@HarelM](https://github.com/HarelM))

## 6.0.0-13

### ✨ Tính năng và cải tiến

- Cải thiện các kiểu ma trận nền tảng cho `ProjectionData` dùng cho renderer và các ma trận phép chiếu của custom layer ([#6316](https://github.com/maplibre/maplibre-gl-js/issues/6316)) (by [@cat0825](https://github.com/cat0825))

### 🐞 Sửa lỗi

- Sửa lỗi camera nhảy giật khi dragend với globe + terrain ở pitch thấp ([#7736](https://github.com/maplibre/maplibre-gl-js/pull/7736)) (by [@kodeezabdullah](https://github.com/kodeezabdullah))
- Sửa lỗi hiển thị web font bằng cách chờ document.fonts.load() trước khi khởi tạo TinySDF ([#7735](https://github.com/maplibre/maplibre-gl-js/pull/7735)) (by [@kodeezabdullah](https://github.com/kodeezabdullah))
- Loại bỏ việc kiểm tra tính toàn vẹn của framebuffer, vốn ném ra một lỗi `Framebuffer is not complete` không được xử lý khi mất tài nguyên GPU tạm thời (ví dụ khi một tab thức dậy từ trạng thái ngủ); các framebuffer không hoàn chỉnh giờ đây tự phục hồi ở khung hình kế tiếp thay vào đó ([#7303](https://github.com/maplibre/maplibre-gl-js/pull/7303)) (by [@johanrd](https://github.com/johanrd))
- ⚠️ Vô hiệu hóa việc scale icon theo offset, đây là một thay đổi phá vỡ tương thích về mặt hiển thị mà chúng tôi đã quyết định áp dụng đồng thời trong cả maplibre-gl-js và maplibre-native ([#7742](https://github.com/maplibre/maplibre-gl-js/issues/7742)) (by [@springmeyer](https://github.com/springmeyer) và [@HarelM](https://github.com/HarelM))

## 6.0.0-12

### ✨ Tính năng và cải tiến

- Tối ưu hóa: loại bỏ độ mờ trong vertex shader cho line và fill [#7711](https://github.com/maplibre/maplibre-gl-js/pull/7711) (by [@xavierjs](https://github.com/xavierjs))

### 🐞 Sửa lỗi

- Sửa lỗi xử lý URL blob xuyên nguồn gốc trong các tiện ích Ajax ([#7675](https://github.com/maplibre/maplibre-gl-js/pull/7675)) (by [@katemihalikova](https://github.com/katemihalikova))
- Tránh các TypeError phát sinh từ các phương thức của style khi ngữ cảnh WebGL bị mất ([#7710](https://github.com/maplibre/maplibre-gl-js/issues/7710)) (by [@cyphercodes](https://github.com/cyphercodes))
- `querySourceFeatures()` ném ra lỗi 'Block overruns tile' trên các tile MLT bị overzoom vì mã hóa được báo cáo không khớp với dữ liệu MVT đã được mã hóa lại ([#7707](https://github.com/maplibre/maplibre-gl-js/pull/7707)) (by [@ted-piotrowski](https://github.com/ted-piotrowski))
- Sửa lỗi kiểm tra độ dài hình học cho đa giác và đường trong LineBucket sau khi cắt bớt các đỉnh trùng lặp ([#7638](https://github.com/maplibre/maplibre-gl-js/pull/7638)) (by [@widefire](https://github.com/widefire))
- Quá trình chuyển tiếp theo bước của `line-dasharray` bị chậm mất một mức zoom khi các nhánh của bước là data-driven ([#7705](https://github.com/maplibre/maplibre-gl-js/pull/7705)) (by [@lucaswoj](https://github.com/lucaswoj))

## 6.0.0-11

### ✨ Tính năng và cải tiến

- Sử dụng một FBO dùng chung cho việc render cache địa hình ra texture [#7637](https://github.com/maplibre/maplibre-gl-js/pull/7637) (by [@xavierjs](https://github.com/xavierjs))
- Sử dụng `flat` để bỏ qua nội suy cho các biến shader không đổi ([#7661](https://github.com/maplibre/maplibre-gl-js/pull/7661)) (by [@birkskyum](https://github.com/birkskyum))

## 6.0.0-10

### ✨ Tính năng và cải tiến

- Thay thế texImage2D bằng texStorage2D cho các texture bất biến ([#7643](https://github.com/maplibre/maplibre-gl-js/pull/7643)) (by [@birkskyum](https://github.com/birkskyum))
- Bật mipmap cho các raster tile có kích thước không phải lũy thừa của 2, giảm hiện tượng răng cưa khi pitch cao ([#7641](https://github.com/maplibre/maplibre-gl-js/pull/7641)) (by [@birkskyum](https://github.com/birkskyum))
- Sử dụng các bộ định danh bố cục của GLSL ES 3.00 cho vị trí thuộc tính vertex, thay thế các lệnh gọi `bindAttribLocation` lúc chạy ([#7644](https://github.com/maplibre/maplibre-gl-js/pull/7644)) (by [@birkskyum](https://github.com/birkskyum))

## 6.0.0-9

### ✨ Tính năng và cải tiến

- Áp dụng isolatedDeclarations và chuyển bộ sinh dts từ tsgo sang oxc ([#7566](https://github.com/maplibre/maplibre-gl-js/pull/7566)) (by [@birkskyum](https://github.com/birkskyum))

### 🐞 Sửa lỗi

- Sửa lỗi việc xóa hàng loạt feature state cộng với thao tác đặt trạng thái theo từng id không xóa được trạng thái của feature đầu tiên ([#7554](https://github.com/maplibre/maplibre-gl-js/pull/7554)) (by [@xavierjs](https://github.com/xavierjs))
- Loại bỏ lỗi khi actor không có loại thông điệp được đăng ký, để cải thiện khả năng sử dụng các thông điệp tùy chỉnh trong worker ([#7589](https://github.com/maplibre/maplibre-gl-js/issues/7589)) (by [@HarelM](https://github.com/HarelM))
- Tự động tải module worker khi sử dụng qua CDN ([#7595](https://github.com/maplibre/maplibre-gl-js/pull/7595)) (by [@birkskyum](https://github.com/birkskyum))
- Sửa lỗi số lượng lớn các khóa feature state gây ra hiện tượng lag khi zoom lúc tải các tile đã cache ([#7590](https://github.com/maplibre/maplibre-gl-js/pull/7590)) (by [@xavierjs](https://github.com/xavierjs))

## 6.0.0-8

### ✨ Tính năng và cải tiến

- Cải thiện hiệu năng địa hình 3D ([#7549](https://github.com/maplibre/maplibre-gl-js/pull/7549)) (by [@lucaswoj](https://github.com/lucaswoj))

## 6.0.0-7

### ✨ Tính năng và cải tiến

- Thay thế dts-bundle-generator bằng rolldown-plugin-dts, giúp việc sinh file .d.ts nhanh hơn 78,2 lần. ([#7564](https://github.com/maplibre/maplibre-gl-js/pull/7564)) (by [@birkskyum](https://github.com/birkskyum))
- Thay thế ts-node bằng hỗ trợ TypeScript gốc của Node 24 cho các script build. ([#7565](https://github.com/maplibre/maplibre-gl-js/pull/7565)) (by [@birkskyum](https://github.com/birkskyum))
- Nâng cấp typescript lên phiên bản beta v7 - kiểm tra kiểu nhanh hơn 3,5 lần ([#7556](https://github.com/maplibre/maplibre-gl-js/pull/7556)) (by [@birkskyum](https://github.com/birkskyum))

### 🐞 Sửa lỗi

- ⚠️ Sửa lỗi các đường line trong suốt, chồng lấn lên nhau tạo ra hiện tượng nhân tạo. Lỗi này được sửa cho `line-opacity`, nhưng cố tình không sửa cho các thuộc tính `line-color` trong suốt, do đó vẫn cho phép các màu trong suốt chồng hiệu ứng lên nhau. ([#7490](https://github.com/maplibre/maplibre-gl-js/pull/7490)) (by [@CommanderStorm](https://github.com/CommanderStorm))
- Sửa lỗi khi mức zoom tối đa của bản đồ và mức zoom tối đa của source gần bằng nhau ([#7567](https://github.com/maplibre/maplibre-gl-js/issues/7567)) (by [@HarelM](https://github.com/HarelM))

## 6.0.0-6

### ✨ Tính năng và cải tiến

- Thêm một tùy chọn tạo bản đồ mới, `terrainSkirtLength`, cho phép loại bỏ các hiện tượng nhân tạo dọc trông thiếu thẩm mỹ khi sử dụng địa hình cùng với nền trong suốt ([#7523](https://github.com/maplibre/maplibre-gl-js/pull/7523)) (by [@safwat-halaby](https://github.com/safwat-halaby))
- Đóng gói bằng Rolldown thay vì Rollup ([#7555](https://github.com/maplibre/maplibre-gl-js/pull/7555)) (by [@birkskyum](https://github.com/birkskyum))
- Tối ưu hóa cho Feature State: Thay thế Object được đánh chỉ mục bằng chuỗi bằng Array (tăng tốc tới 3,4 lần) ([#7550](https://github.com/maplibre/maplibre-gl-js/pull/7550)) (by [@xavierjs](https://github.com/xavierjs))

## 6.0.0-5

### ✨ Tính năng và cải tiến

- ⚠️ Chuyển sang bản phân phối chỉ dùng ESM (`maplibre-gl.mjs`). Các bundle UMD (`maplibre-gl.js`, `maplibre-gl-csp.js`) không còn được phát hành nữa. Bundle dành riêng cho CSP cũng bị loại bỏ: bản build ESM tải worker của nó dưới dạng một URL thực, nên `worker-src blob:` không còn là bắt buộc nữa. Các bên sử dụng `<script src=".../maplibre-gl.js">` phải chuyển sang `<script type="module">`, và các bên sử dụng `import maplibregl from 'maplibre-gl'` phải chuyển sang `import * as maplibregl from 'maplibre-gl'` hoặc dùng named imports. Xem phần ESM trong tài liệu để biết các bước di chuyển. ([#6254](https://github.com/maplibre/maplibre-gl-js/pull/6254)) (by [@birkskyum](https://github.com/birkskyum))

## 6.0.0-4

### ✨ Tính năng và cải tiến

- ⚠️ Giá trị mặc định của `zoomLevelsToOverscale` đã được đổi thành 4 để hỗ trợ xử lý tốt hơn các mức zoom cao với nhãn dày đặc. Điều này có thể có tác dụng phụ là thay đổi đôi chút kết quả của `queryRenderedFeatures` và một số cách render nhãn trung tâm của đa giác. Để hoàn tác thay đổi này, hãy đặt giá trị thành `undefined` ([#7537](https://github.com/maplibre/maplibre-gl-js/issues/7537)) (by [@HarelM](https://github.com/HarelM))

## 6.0.0-3

### ✨ Tính năng và cải tiến

- ⚠️ Loại bỏ tham số thứ hai của `GeoJSONSource.setData` (`waitForCompletion`) và loại bỏ giá trị trả về `this` để cho phép các thay đổi API trong tương lai ([#7538](https://github.com/maplibre/maplibre-gl-js/issues/7538)) (by [@HarelM](https://github.com/HarelM))
- ⚠️ Mục tiêu TypeScript đã được cập nhật lên ES2022.
  Điều này giúp tạo ra bundle nhỏ hơn và cải thiện hiệu năng thực thi bằng cách dựa vào các tính năng JavaScript hiện đại và giảm việc chuyển mã. Các bên nhắm đến các trình duyệt hoặc sử dụng một số công cụ phát hành trước năm 2022 có thể cần chuyển mã MapLibre hoặc cập nhật. Thay đổi này cũng đồng bộ tất cả các cấu hình build nội bộ về một mục tiêu duy nhất thay vì ES2016 + ES2019, tránh sự không nhất quán trong mã được sinh ra. ([#7404](https://github.com/maplibre/maplibre-gl-js/pull/7404)) (by [@CommanderStorm](https://github.com/CommanderStorm))

## 6.0.0-2

### ✨ Tính năng và cải tiến

- ⚠️ Hỗ trợ WebGL (v1) đã bị loại bỏ; giờ đây bắt buộc phải có WebGL2.
  Về mặt thực tế, điều này sẽ không thay đổi cách bạn tương tác với bản đồ.
  Điều này cho phép cải thiện hiệu năng (ví dụ line opacity), nâng cao Terrain3D, và một số bản sửa lỗi.
  Hỗ trợ WebGL2 đã được phổ biến rộng rãi trong nhiều năm, và việc sử dụng đường dẫn cũ đã chững lại, nên việc duy trì nó không còn hợp lý với độ phức tạp tăng thêm.
  Để giảm nhẹ thay đổi phá vỡ tương thích này, chúng tôi cũng đã tái cấu trúc cách xử lý trường hợp không có webgl khả dụng (ví dụ do hạn chế của trình duyệt).
  Giờ đây bạn có thể lắng nghe lỗi webgl thông qua `.on("error")`.
  Xem [caniuse.com/webgl2](https://caniuse.com/webgl2) để biết mức độ hỗ trợ trong hệ sinh thái và [RFC của chúng tôi để biết chi tiết](https://github.com/maplibre/maplibre-gl-js/discussions/6017). ([#7453](https://github.com/maplibre/maplibre-gl-js/pull/7453)) (by [@CommanderStorm](https://github.com/CommanderStorm))

## 6.0.0-1

### ✨ Tính năng và cải tiến

- ⚠️ Hỗ trợ các object lồng nhau trong geojson, đây là một thay đổi phá vỡ tương thích vì nó mã hóa `__$json__` trước các thuộc tính từng là một object. Nó cũng phân tích ngược lại chúng, nhưng đây vẫn là một thay đổi phá vỡ tương thích nếu bạn từng cho rằng lỗi này tồn tại. ([#6992](https://github.com/maplibre/maplibre-gl-js/pull/6992)) (by [HarelM](https://github.com/HarelM))
- ⚠️ Cải thiện kiểu cho `{get,set}LayoutProperty`, `{get,set}PaintProperty` để trả về kiểu thực tế thay vì `string`/`any` ([#7481](https://github.com/maplibre/maplibre-gl-js/pull/7481)) (by [@CommanderStorm](https://github.com/CommanderStorm))

## 6.0.0-0

### ✨ Tính năng và cải tiến

- ⚠️ Tái cấu trúc phần điều khiển vị trí dựa trên `Hash` (tùy chọn đồng bộ trạng thái bản đồ vào URL như `#map=5/1/2`) để sử dụng `URLSearchParams` ở bên trong. Điều này cải thiện khả năng mở rộng cho các trường hợp sử dụng tùy chỉnh, nhưng có thể làm hỏng mã hiện có dựa vào cách triển khai trước đây. Nó cũng thay đổi cách một số trường hợp biên được phân tích cú pháp — ví dụ, các chuỗi như `#10%2F3.00%2F-1.00` giờ đây được chấp nhận, và các hash như `#foo` được chuẩn hóa thành `#foo=`. ([#7073](https://github.com/maplibre/maplibre-gl-js/pull/7073)) (by [@CommanderStorm](https://github.com/CommanderStorm))
- Expose hàm `getProjectionData` trong các object tham số của custom layer ([#7471](https://github.com/maplibre/maplibre-gl-js/pull/7471)) (by [@kubapelc](https://github.com/kubapelc))
- Đánh dấu `sideEffects` của package là chỉ dành cho CSS trong metadata của package, điều này có thể cải thiện tree-shaking và giảm kích thước bundle ở một số bundler ([#7258](https://github.com/maplibre/maplibre-gl-js/pull/7258)) (by [@CommanderStorm](https://github.com/CommanderStorm))

## 5.24.0

### ✨ Tính năng và cải tiến

- Tối ưu hóa hiệu năng GPU: Render halo và glyph trong một lượt duy nhất (giảm 40% thời gian) ([#7436](https://github.com/maplibre/maplibre-gl-js/pull/7436)) (by [@xavierjs](https://github.com/xavierjs))
- Tối ưu hóa các phép nghịch đảo ma trận (matrix inversions) và giảm hiện tượng treo GPU (GPU stalls) ([#7367](https://github.com/maplibre/maplibre-gl-js/pull/7367)) (by [@xavierjs](https://github.com/xavierjs))
- Thêm một ví dụ minh họa cách đo hiệu năng bản đồ bằng các sự kiện tích hợp sẵn (`load`, `idle`, `render`) ([#7077](https://github.com/maplibre/maplibre-gl-js/pull/7077)) (by [@CommanderStorm](https://github.com/CommanderStorm))

### 🐞 Sửa lỗi

- Sửa lỗi `Popup` không cập nhật vị trí khi chuyển đổi giữa các phép chiếu terrain/globe ([#7468](https://github.com/maplibre/maplibre-gl-js/pull/7468)) (by [@CommanderStorm](https://github.com/CommanderStorm))
- Bỏ qua việc tính toán sương mù (fog) khi độ mờ của sương mù bằng 0 ([#7476](https://github.com/maplibre/maplibre-gl-js/pull/7476)) (by [@CommanderStorm](https://github.com/CommanderStorm))

## 5.23.0

### ✨ Tính năng và cải tiến

- Thêm `touchZoomRotate.setZoomRate()` và `touchZoomRotate.setZoomThreshold()` để tùy chỉnh tốc độ thu phóng bằng cảm ứng và độ nhạy khi chụm ([#7271](https://github.com/maplibre/maplibre-gl-js/issues/7271)) (by [@itisyb](https://github.com/itisyb))
- Cải thiện khả năng giao tiếp với các script được import trong worker và sử dụng `makeRequest` trong worker luôn ([#7451](https://github.com/maplibre/maplibre-gl-js/issues/7451)) (by [@HarelM](https://github.com/HarelM))
- Cho phép `opacity` và `opacityWhenCovered` trong `Marker` và `MarkerOptions` nhận kiểu `number` ngoài kiểu `string`, và thêm class CSS `maplibregl-marker-covered` vào phần tử `Marker` khi bị che khuất bởi địa hình 3D hoặc globe ([#7433](https://github.com/maplibre/maplibre-gl-js/issues/7433)) (by [@YuChunTsao](https://github.com/YuChunTsao))
- perf: thêm một bài đo hiệu năng (bench) cho việc render địa hình và sửa lỗi tra cứu `_demMatrixCache` lãng phí chu kỳ (cycle) do chưa thực sự sử dụng cache ([#7400](https://github.com/maplibre/maplibre-gl-js/pull/7400)) (by [@CommanderStorm](https://github.com/CommanderStorm))

### 🐞 Sửa lỗi

- Sửa lỗi vị trí nhãn văn bản của đa giác bị trôi xa khỏi tâm đối với các đa giác lồi (convex polygon) ở mức zoom cao do làm tròn tọa độ trong geojson-vt ([#7380](https://github.com/maplibre/maplibre-gl-js/pull/7380)) (by [@CommanderStorm](https://github.com/CommanderStorm))
- Đảm bảo một phản hồi ArrayBuffer thành công từ một giao thức tùy chỉnh mà là null/undefined được đặt thành một ArrayBuffer rỗng ([#7427](https://github.com/maplibre/maplibre-gl-js/pull/7427)) (by [@neodescis](https://github.com/neodescis))
- Sửa lỗi trong `_contextRestored` khi bản đồ được khởi tạo mà không có style ([#7432](https://github.com/maplibre/maplibre-gl-js/issues/7432)) (by [@mvanhorn](https://github.com/mvanhorn))
- Sửa lỗi liên quan đến cache dùng cho tính năng zoomLevelsToOverscale ([#7450](https://github.com/maplibre/maplibre-gl-js/issues/7450)) (by [@HarelM](https://github.com/HarelM))
- Cập nhật stylelint và sửa các vấn đề cũ với CSS (chủ yếu là đổi rgb sang dùng dấu cách) ([#7365](https://github.com/maplibre/maplibre-gl-js/issues/7365)) (by [@HarelM](https://github.com/HarelM))

## 5.22.0

### ✨ Tính năng và cải tiến

- Làm cho `line-cap`, `line-miter-limit`, và `line-round-limit` trở thành các thuộc tính data-driven, cho phép có giá trị theo từng feature ([#7351](https://github.com/maplibre/maplibre-gl-js/pull/7351)) (by [@CommanderStorm](https://github.com/CommanderStorm))
- Tối ưu hóa hiệu năng GPU: loại bỏ sớm (early culling) các biểu tượng trong suốt trong vertex shader ([#7364](https://github.com/maplibre/maplibre-gl-js/pull/7364)) (by [@xavierjs](https://github.com/xavierjs))
- Thêm một ví dụ minh họa cách đo hiệu năng bản đồ bằng các sự kiện tích hợp sẵn (`load`, `idle`, `render`) ([#7077](https://github.com/maplibre/maplibre-gl-js/pull/7077)) (by [@CommanderStorm](https://github.com/CommanderStorm))
- UX: Làm rõ ngôn ngữ thông báo lỗi trong trường hợp các thuộc tính layout và paint bị nhầm lẫn trong `setPaintProperty` hoặc `setLayoutProperty` ([#6954](https://github.com/maplibre/maplibre-gl-js/pull/6954)) (by [@Willjfield](https://github.com/Willjfield) và [@CommanderStorm](https://github.com/CommanderStorm))

### 🐞 Sửa lỗi

- Sửa lỗi crash khi khởi động do một lần tải style bất đồng bộ cũ (stale) hoàn tất sau khi style đã bị xóa hoặc thay thế ([#7377](https://github.com/maplibre/maplibre-gl-js/issues/7377))
- Làm cho `fitBounds` và `fitScreenCoordinates` tôn trọng tùy chọn bản đồ `zoomSnap` bằng cách làm tròn (snap) mức zoom xuống để giữ cho toàn bộ ranh giới (bounds) vẫn hiển thị ([#7332](https://github.com/maplibre/maplibre-gl-js/issues/7332)) (by [@CommanderStorm](https://github.com/CommanderStorm))
- Làm cho `jumpTo`, `easeTo`, và `flyTo` tôn trọng tùy chọn bản đồ `zoomSnap` bằng cách làm tròn mức zoom về gia số (increment) hợp lệ gần nhất ([#7333](https://github.com/maplibre/maplibre-gl-js/issues/7333)) (by [@CommanderStorm](https://github.com/CommanderStorm))
- Sửa lỗi `setState` bị crash khi chuyển đổi style trong lúc phép chiếu globe đang được kích hoạt ([#7314](https://github.com/maplibre/maplibre-gl-js/issues/7314)) (by [@ashwinuae](https://github.com/ashwinuae))
- Ngăn hiện tượng crash khi gọi `map.remove()` ngay sau khi tạo bằng cách hủy các lần tải URL style đang diễn ra ([#7368](https://github.com/maplibre/maplibre-gl-js/pull/7368)) (by [@CommanderStorm](https://github.com/CommanderStorm))
- Sửa lỗi nhấp nháy khi va chạm biểu tượng (symbol collision) bằng cách thêm dung sai (tolerance) vào phép so sánh AABB của GridIndex ([#7360](https://github.com/maplibre/maplibre-gl-js/issues/7360)) (by [@kkokkoejong](https://github.com/kkokkojeong))
- Sửa lỗi `fitBounds` bỏ qua tùy chọn `maxZoom` trong phép chiếu `vertical-perspective` ([#7372](https://github.com/maplibre/maplibre-gl-js/issues/7372)) (by [@CommanderStorm](https://github.com/CommanderStorm))
- Ngăn các lần tải style bất đồng bộ cũ hoàn tất sau khi style bị xóa ([#7378](https://github.com/maplibre/maplibre-gl-js/pull/7378)) (by [@Lievesley](https://github.com/Lievesley))
- Sửa lỗi ví dụ bị hỏng cho `fill-pattern` ([#7326](https://github.com/maplibre/maplibre-gl-js/pull/7326)) (by [@k-yle](https://github.com/k-yle))

## 5.21.1

### 🐞 Sửa lỗi

- Thêm tham số `promoteId` bị thiếu vào geojson worker và tái cấu trúc object giao tiếp ([#7320](https://github.com/maplibre/maplibre-gl-js/issues/7320)) (by [@HarelM](https://github.com/HarelM))

## 5.21.0

### ✨ Tính năng và cải tiến

- Thêm khả năng tương thích với ES2020 ([#7283](https://github.com/maplibre/maplibre-gl-js/pull/7283)) (by [@claudiobgit](https://github.com/claudiobgit))
- Thêm tùy chọn `referrerPolicy` vào `RequestParameters` để cho phép kiểm soát chính sách referrer cho các yêu cầu tile ([#7278](https://github.com/maplibre/maplibre-gl-js/issues/7278)) (by [@Bingtagui404](https://github.com/Bingtagui404))
- Chờ GPU hoàn tất ngăn xếp lệnh gọi (callstack) cho các bài đo hiệu năng render ([#7285](https://github.com/maplibre/maplibre-gl-js/pull/7285)) (by [@xavierjs](https://github.com/xavierjs))
- Loại bỏ giải pháp phát hiện WebP cho Edge 18; luôn gửi header `Accept: image/webp` cho các yêu cầu hình ảnh ([#7293](https://github.com/maplibre/maplibre-gl-js/pull/7293)) (by [@johanrd](https://github.com/johanrd))
- Loại bỏ mã tương thích trình duyệt cũ nhắm đến IE11 và các trình duyệt trước 2016 ([#7294](https://github.com/maplibre/maplibre-gl-js/pull/7294)) (by [@johanrd](https://github.com/johanrd))
- Loại bỏ các wrapper cũ `DOM.remove()` và `DOM.mouseButton()`; sử dụng trực tiếp các API gốc (baseline 2015) ([#7295](https://github.com/maplibre/maplibre-gl-js/pull/7295)) (by [@johanrd](https://github.com/johanrd))
- Làm cho `setTransformRequest` chấp nhận một hàm bất đồng bộ (async) bên cạnh hàm đồng bộ. ([#7184](https://github.com/maplibre/maplibre-gl-js/issues/7184)) (by [@kikuomax](https://github.com/kikuomax))

### 🐞 Sửa lỗi

- Sửa lỗi vị trí popup không chính xác trong trường hợp có terrain và `jumpTo` ([#7267](https://github.com/maplibre/maplibre-gl-js/issues/7267)) (by [@HarelM](https://github.com/HarelM))
- Sửa lỗi rò rỉ bộ nhớ trong VideoSource: xóa listener sự kiện `playing` và tạm dừng video khi source bị xóa ([#7279](https://github.com/maplibre/maplibre-gl-js/pull/7279)) (by [@johanrd](https://github.com/johanrd))
- Sửa lỗi rò rỉ bộ nhớ khi các view typed array giữ lại buffer của StructArray sau khi đã tải lên GPU, ngăn cản việc thu gom rác (garbage collection) ([#7280](https://github.com/maplibre/maplibre-gl-js/pull/7280)) (by [@johanrd](https://github.com/johanrd))
- Sửa lỗi các raster DEM tile bị kẹt ở trạng thái `"reloading"` ([#7284](https://github.com/maplibre/maplibre-gl-js/pull/7284)) (by [@katemihalikova](https://github.com/katemihalikova))
- Sửa lỗi `GeolocateControl` rò rỉ một listener `movestart` trên bản đồ sau khi bị xóa, điều này cũng có thể gây crash nếu control đang ở trạng thái theo dõi (tracking) khi bị xóa ([#7286](https://github.com/maplibre/maplibre-gl-js/pull/7286)) (by [@johanrd](https://github.com/johanrd))
- Giới hạn pool tái sử dụng texture tile để ngăn VRAM tăng trưởng không giới hạn trong lúc zoom/pan nhanh ([#7289](https://github.com/maplibre/maplibre-gl-js/pull/7289)) (by [@johanrd](https://github.com/johanrd))
- Sửa lỗi listener `click` của Marker không bị xóa khi gọi `remove()`, gây rò rỉ handler được thêm trong #7028 ([#7287](https://github.com/maplibre/maplibre-gl-js/pull/7287)) (by [@johanrd](https://github.com/johanrd))
- Sửa lỗi rò rỉ tài nguyên GPU của Terrain: giải phóng FBO, texture, và mesh khi terrain bị vô hiệu hóa qua `setTerrain(null)` ([#7288](https://github.com/maplibre/maplibre-gl-js/pull/7288)) (by [@johanrd](https://github.com/johanrd))
- Sửa lỗi bảo vệ (guard) chống lại layout bị dở dang trong `PauseablePlacement` ([#7079](https://github.com/maplibre/maplibre-gl-js/pull/7079)) (by [@garethbowker](https://github.com/garethbowker))
- Sửa lỗi thiếu mã hóa tile cho MLT queryRenderedFeatures ([#7056](https://github.com/maplibre/maplibre-gl-js/pull/7056)) (by [@dannote](https://github.com/dannote) và [@ted-piotrowski](https://github.com/ted-piotrowski))
- Sửa lỗi ví dụ 3D Tiles ([#7275](https://github.com/maplibre/maplibre-gl-js/pull/7275)) (by [@hh-hang](https://github.com/hh-hang))

## 5.20.2

### 🐞 Sửa lỗi

- Sửa lỗi cập nhật GeoJSON khi sử dụng diff update bằng cách cập nhật package geojson-vt ([#7257](https://github.com/maplibre/maplibre-gl-js/issues/7257)) (by [@HarelM](https://github.com/HarelM))

## 5.20.1

### 🐞 Sửa lỗi

- Sửa lỗi "cannot read properties of undefined (reading 'range')" bằng cách cập nhật package geojson-vt ([#7245](https://github.com/maplibre/maplibre-gl-js/issues/7245)) (by [@HarelM](https://github.com/HarelM))
- Sửa lỗi `raster-resampling: nearest` không được áp dụng đúng như mong đợi ([#7247](https://github.com/maplibre/maplibre-gl-js/pull/7247)) (by [@yano-h](https://github.com/yano-h))

## 5.20.0

### ✨ Tính năng và cải tiến

- Thêm hỗ trợ Etag unmodified để tối ưu hóa việc tải lại vector tile ([#7074](https://github.com/maplibre/maplibre-gl-js/pull/7074)) (by [@rivkamatan](https://github.com/rivkamatan) và [@wayofthefuture](https://github.com/wayofthefuture))
- Thêm tùy chọn `boxZoom.boxZoomEnd` để tùy chỉnh hành động sau khi chọn vùng bằng Shift-kéo (box selection) ([#6397](https://github.com/maplibre/maplibre-gl-js/issues/6397)) (by [@itisyb](https://github.com/itisyb))
- Triển khai thuộc tính paint `resampling` cho các layer raster, hillshade, và color-relief ([#7194](https://github.com/maplibre/maplibre-gl-js/pull/7194)) (by [@larsmaxfield](https://github.com/larsmaxfield))
- Thêm hỗ trợ cập nhật cho GeoJSON-VT ([#7172](https://github.com/maplibre/maplibre-gl-js/issues/7172)) (by [@wayofthefuture](https://github.com/wayofthefuture) và [@HarelM](https://github.com/HarelM))
- Thêm ví dụ cho 3D Tiles sử dụng three.js ([#7198](https://github.com/maplibre/maplibre-gl-js/pull/7198)) (by [@hh-hang](https://github.com/hh-hang))

### 🐞 Sửa lỗi

- Sửa lỗi: Khoảng cách đến tile được tính toán không chính xác trong phép chiếu globe ở các góc pitch cao ([#7219](https://github.com/maplibre/maplibre-gl-js/issues/7219)) (by [@jtfedd](https://github.com/jtfedd))
- Sửa lỗi: Các tile không được xóa khi sử dụng `setUrl/setTiles` của vector tile source ([#7185](https://github.com/maplibre/maplibre-gl-js/issues/7185)) (by [@madoci](https://github.com/madoci))
- Sửa lỗi: Cho phép các origin không xác định ("null") trong việc lọc thông điệp của Actor ([#7047](https://github.com/maplibre/maplibre-gl-js/pull/7047)) (by [@pcardinal](https://github.com/pcardinal))

## 5.19.0

### ✨ Tính năng và cải tiến

- Thay đổi kiểu trả về của `LngLatBounds.toArray()` để sử dụng một kiểu chính xác hơn ([#7156](https://github.com/maplibre/maplibre-gl-js/pull/7156)) (by [@n4n5](https://github.com/Its-Just-Nans))
- Thêm tùy chọn bản đồ `anisotropicFilterPitch` để đặt mức pitch mà từ đó bộ lọc anisotropic được áp dụng cho tất cả các layer raster, giá trị mặc định là 20° ([#7134](https://github.com/maplibre/maplibre-gl-js/issues/7134)) (by [@larsmaxfield](https://github.com/larsmaxfield))
- Thêm source id vào thông báo lỗi ([#7107](https://github.com/maplibre/maplibre-gl-js/pull/7107)) (by [@HarelM](https://github.com/HarelM))

### 🐞 Sửa lỗi

- Sửa lỗi hiển thị SDF `icon-text-fit` bằng cách unpack đúng các giá trị shader đã đóng gói trong `symbol_sdf.vertex.glsl`, kèm theo độ bao phủ (coverage) của render-test ([#7141](https://github.com/maplibre/maplibre-gl-js/pull/7141), sửa [#6953](https://github.com/maplibre/maplibre-gl-js/issues/6953)) (by [@pcardinal](https://github.com/pcardinal))
- Sửa lỗi tính toán ranh giới (bounds) chính xác cho GeoJSON có độ cao (elevation) ([#6963](https://github.com/maplibre/maplibre-gl-js/pull/6963)) (by [@simonmnt](https://github.com/simonmnt))
- Sửa lỗi: hỗ trợ độ cao trong việc tính toán ranh giới ([#7135](https://github.com/maplibre/maplibre-gl-js/pull/7135)) (by [@simonmnt](https://github.com/simonmnt))
- Sửa lỗi cảnh báo "Alpha-premult deprecated for non-DOM uploads" trên Firefox ([#7128](https://github.com/maplibre/maplibre-gl-js/pull/7128)) (by [@birkskyum](https://github.com/birkskyum))
- Sửa lỗi các raster tile được render cùng nội dung atlas glyph/icon sau khi mất ngữ cảnh WebGL ([#7126](https://github.com/maplibre/maplibre-gl-js/pull/7126)) (by [@birkskyum](https://github.com/birkskyum))
- Sửa lỗi mũi nhọn (tip) của popup trên các trang RTL ([#7157](https://github.com/maplibre/maplibre-gl-js/pull/7157)) (by [@HarelM](https://github.com/HarelM))

## 5.18.0

### ✨ Tính năng và cải tiến

- Thêm hỗ trợ cho các sự kiện click trên Marker ([#7028](https://github.com/maplibre/maplibre-gl-js/pull/7028)) (by [@ganesh8068](https://github.com/ganesh8068))
- Đơn giản hóa và trừu tượng hóa GeoJSON Worker ([#7058](https://github.com/maplibre/maplibre-gl-js/pull/7058)) (by [@wayofthefuture](https://github.com/wayofthefuture))
- Thêm tùy chọn `pseudo` cho `FullscreenControl` để bắt buộc dùng chế độ toàn màn hình dựa trên CSS thay vì API toàn màn hình gốc. Người dùng có thể muốn điều này vì nó nhanh hơn trên một số thiết bị ([#7076](https://github.com/maplibre/maplibre-gl-js/pull/7076)) (by [@CommanderStorm](https://github.com/CommanderStorm))
- Di chuyển tài liệu API của chúng tôi sang zensical ([#7071](https://github.com/maplibre/maplibre-gl-js/pull/7071)) (by [@CommanderStorm](https://github.com/CommanderStorm))

### 🐞 Sửa lỗi

- Sửa lỗi mất ngữ cảnh WebGL khi style chưa được tải ([#7094](https://github.com/maplibre/maplibre-gl-js/pull/7094)) (by [@kaigritun](https://github.com/kaigritun))
- Sửa lỗi cập nhật các tile địa hình khi feature state thay đổi ([#6231](https://github.com/maplibre/maplibre-gl-js/issues/6231)) (by [@pstaszek](https://github.com/pstaszek))
- Sửa lỗi LngLatBounds.intersects đối với các ranh giới có chiều rộng bằng 0 ([#7055](https://github.com/maplibre/maplibre-gl-js/pull/7055)) (by [@lucaswoj](https://github.com/lucaswoj))
- Sửa lỗi `GlobeControl` không cập nhật khi `Map.setProjection()` được gọi theo cách lập trình (programmatically) ([#7005](https://github.com/maplibre/maplibre-gl-js/issues/7005), [#7075](https://github.com/maplibre/maplibre-gl-js/pull/7075)) (by [@CommanderStorm](https://github.com/CommanderStorm))
- Sửa lỗi `map.getProjection()` trả về `undefined` sau khi gọi `map.setProjection()` với phép chiếu mặc định `"mercator"` ([#7072](https://github.com/maplibre/maplibre-gl-js/pull/7072)) (by [@CommanderStorm](https://github.com/CommanderStorm))
- Sửa lỗi vị trí văn bản dọc theo đường không chính xác ở chế độ 3D ([#7039](https://github.com/maplibre/maplibre-gl-js/issues/7039)) (by [@russellporter](https://github.com/russellporter))
- Khi media query `prefers-reduced-motion` đang hoạt động, giờ đây chúng tôi không còn hiển thị animation nhấp nháy (pulsing) của GeoLocation nữa ([#7066](https://github.com/maplibre/maplibre-gl-js/pull/7066)) (by [@CommanderStorm](https://github.com/CommanderStorm))

## 5.17.0

### ✨ Tính năng và cải tiến

- Tái cấu trúc `_updateWorkerData` ([#6983](https://github.com/maplibre/maplibre-gl-js/pull/6983)) (by [@wayofthefuture](https://github.com/wayofthefuture))
- ⚠️ Thêm tùy chọn `zoomSnap` vào `Map` để cho phép làm tròn mức zoom theo một lưới khi zoom vào và ra; đồng bộ hành vi trên tất cả các mẫu hình giao diện người dùng (bàn phím, con lăn chuột, nút zoom trên màn hình, double-click, double-tap). Trước đây, nhấn +/- trên bàn phím sẽ zoom đến các số nguyên tròn, nhiều hơn hoặc ít hơn 1 mức zoom khi bắt đầu từ một mức zoom thập phân. Giờ đây bất kỳ số nào cũng có thể được chỉ định cho `zoomSnap`; giá trị 1.0 tạo ra hành vi số nguyên tròn trên tất cả các mẫu hình giao diện người dùng. ([#6941](https://github.com/maplibre/maplibre-gl-js/pull/6941)) (by [@mizmay](https://github.com/mizmay))
- Thêm hỗ trợ cho các phần tử container từ các cửa sổ (window) khác nhau (ví dụ popup hoặc iframe) ([#6969](https://github.com/maplibre/maplibre-gl-js/pull/6969)) (by [@Syncret](https://github.com/Syncret))
- Di chuyển sang @maplibre/geojson-vt ([#6995](https://github.com/maplibre/maplibre-gl-js/pull/6995)) (by [@HarelM](https://github.com/HarelM))

### 🐞 Sửa lỗi

- Sửa lỗi lựa chọn shader không chính xác cho các nhãn văn bản có hình ảnh nội tuyến (inline images) ([#6956](https://github.com/maplibre/maplibre-gl-js/pull/6956)) (by [@ciscorn](https://github.com/ciscorn))
- Sửa lỗi vị trí marker không cập nhật khi zoom hoặc pitch thay đổi sau một thay đổi trong các giới hạn (constraints) ([#6925](https://github.com/maplibre/maplibre-gl-js/issues/6925)) (by [@auspicus](https://github.com/auspicus))

## 5.16.0

### ✨ Tính năng và cải tiến

- Thêm tùy chọn `padding` vào class `Popup` để ngăn popup được định vị quá gần các cạnh của container bản đồ ([#5978](https://github.com/maplibre/maplibre-gl-js/issues/5978)) (by [@yuiseki](https://github.com/yuiseki) và [@lucaswoj](https://github.com/lucaswoj))
- Phát sự kiện `style.load` khi diff style ([#6880](https://github.com/maplibre/maplibre-gl-js/pull/6880)) (by [@lesbaa](https://github.com/lesbaa))

### 🐞 Sửa lỗi

- Sửa lỗi đặt hiển thị (visibility) trên custom layer ([#6883](https://github.com/maplibre/maplibre-gl-js/issues/6883)) (by [@melitele](https://github.com/melitele))
- Ẩn các ký tự điều khiển ở đầu và cuối trong các biểu thức `format` ([#6907](https://github.com/maplibre/maplibre-gl-js/pull/6907)) (by [@1ec5](https://github.com/1ec5))
- Sửa lỗi các image source bị cắt tại kinh độ -180 và 180 khi terrain được bật ([#4088](https://github.com/maplibre/maplibre-gl-js/issues/4088)) (by [@pstaszek](https://github.com/pstaszek))
- Sửa lỗi bản đồ không giới hạn (constrain) ngay lập tức về một mức zoom và tâm hợp lệ khi thay đổi phép chiếu ([#6892](https://github.com/maplibre/maplibre-gl-js/issues/6892)) (by [@larsmaxfield](https://github.com/larsmaxfield))
- Sửa lỗi bản đồ trắng khi một sự kiện resize được kích hoạt trước khi ngữ cảnh WebGL được khôi phục ([#6935](https://github.com/maplibre/maplibre-gl-js/pull/6935)) (by [@ToHold](https://github.com/ToHold))
- Các thay đổi đã diff khi json được truyền vào `setStyle` giờ đây phát ra sự kiện style.load. ([#2587](https://github.com/maplibre/maplibre-gl-js/issues/2587), [#4757](https://github.com/maplibre/maplibre-gl-js/issues/4757)) (by [@lesbaa](https://github.com/lesbaa))
- Sửa lỗi độ chính xác trong shader khí quyển (atmosphere) ở phép chiếu globe. ([#6916](https://github.com/maplibre/maplibre-gl-js/issues/6916)) (by [@tavimori](https://github.com/tavimori))

## 5.15.0

### ✨ Tính năng và cải tiến

- Hỗ trợ biểu thức global state cho khả năng hiển thị (visibility) của layer ([#6659](https://github.com/maplibre/maplibre-gl-js/pull/6659)) (by [@melitele](https://github.com/melitele))
- Cập nhật phiên bản Node.js lên 24.11 cho môi trường phát triển ([#6851](https://github.com/maplibre/maplibre-gl-js/pull/6851)) (by [@HarelM](https://github.com/HarelM))

### 🐞 Sửa lỗi

- Sửa lỗi `LngLatBounds#intersects` trả về `false` đối với các ranh giới trải dài 360° trở lên ([#6863](https://github.com/maplibre/maplibre-gl-js/pull/6863)) (by [@lucaswoj](https://github.com/lucaswoj))
- Sửa lỗi lấy đúng mức zoom cho getElevationForLngLat ([#6825](https://github.com/maplibre/maplibre-gl-js/pull/6825)) (by [@HarelM](https://github.com/HarelM))
- Sửa lỗi trạng thái transform cũ (stale) được áp dụng sau khi thay đổi `minZoom` hoặc `maxZoom` do các bản sao cũ từ `transformCameraUpdate` được ưu tiên hơn. `transformCameraUpdate` giờ đây được gọi từ `setMinZoom` và `setMaxZoom` để cho phép người dùng kiểm soát các thay đổi tiếp theo đối với `zoom` ([#6766](https://github.com/maplibre/maplibre-gl-js/issues/6766)) (by [@Auspicus](https://github.com/Auspicus))
- Sửa lỗi GeoJSON source phát sinh lỗi với các thuộc tính undefined ([#6730](https://github.com/maplibre/maplibre-gl-js/issues/6730)) (by [@wayofthefuture](https://github.com/wayofthefuture))

## 5.14.0

### ✨ Tính năng và cải tiến

- Ngăn việc lấp đầy lại viền (backfilling) DEM dư thừa bằng cách theo dõi trạng thái, di chuyển logic quản lý tile sang các file hỗ trợ ([#6756](https://github.com/maplibre/maplibre-gl-js/pull/6756)) (by [@HarelM](https://github.com/HarelM))
- Cải thiện hiệu năng của GeoJSON `updateData`, `setData`, và các tile bị overzoom ([#6738](https://github.com/maplibre/maplibre-gl-js/pull/6738), [#6772](https://github.com/maplibre/maplibre-gl-js/pull/6772)) (by [@lucaswoj](https://github.com/lucaswoj))

### 🐞 Sửa lỗi

- Xử lý các điểm trùng lặp liên tiếp trong offsetLine để tránh giá trị null trong đầu ra. ([#5431](https://github.com/maplibre/maplibre-gl-js/issues/5431)) (by [@mmc1718](https://github.com/mmc1718))
- ⚠️ Xử lý một cách nhẹ nhàng các AbortError nội bộ (ví dụ khi một URL TileJSON được cập nhật trong khi có yêu cầu đang diễn ra). Trước đây, các yêu cầu bị abort như vậy sẽ ném ra một AbortError trong một rejection không được xử lý, điều mà mã của người dùng khó có thể bắt được. Vì các yêu cầu bị abort đã được xử lý đầy đủ ở nội bộ, các rejection không được xử lý này là thừa và dẫn đến các lỗi phía client không hữu ích. ([#6747](https://github.com/maplibre/maplibre-gl-js/pull/6747)) (by [@andrewda](https://github.com/andrewda))
- Sửa lỗi các canvas source có kích thước lũy thừa của 2 render thành các ô vuông đen ([#6607](https://github.com/maplibre/maplibre-gl-js/issues/6607)) (by [@Omkarthipparthi](https://github.com/Omkarthipparthi))
- Sửa lỗi `queryTerrainElevation` để sử dụng các tile có mức zoom cao hơn khi có thể ([#6791](https://github.com/maplibre/maplibre-gl-js/pull/6791)) (by [@HarelM](https://github.com/HarelM))
- Sửa lỗi chuyển động không mong muốn khi di chuyển một bản đồ địa hình có pitch ở vĩ độ cao; sửa lỗi đóng băng khi di chuyển một bản đồ địa hình có pitch và xoay (rotated) ở mức zoom thấp ([#6775](https://github.com/maplibre/maplibre-gl-js/pull/6775)) (by [@larsmaxfield](https://github.com/larsmaxfield))
- Sửa lỗi liên quan đến bổ ngữ (modifier) `static` như một phần của package mlt ([#6796](https://github.com/maplibre/maplibre-gl-js/pull/6796)) (by [@HarelM](https://github.com/HarelM))
- Sửa lỗi tải lại tile của GeoJSONSource khi cập nhật dữ liệu ([#6800](https://github.com/maplibre/maplibre-gl-js/pull/6800)) (by [@HarelM](https://github.com/HarelM))
- `LngLatBounds#intersects` giờ đây trả về `true` khi các ranh giới chạm nhau dọc theo một cạnh hoặc tại một góc ([#6802](https://github.com/maplibre/maplibre-gl-js/pull/6802)) (by [@lucaswoj](https://github.com/lucaswoj))

## 5.13.0

### ✨ Tính năng và cải tiến

- Các nhãn văn bản giờ đây có thể bao gồm các ký tự Trung, Nhật, Hàn, và Việt tương đối hiếm gặp, cũng như các ký tự từ các hệ thống chữ viết lịch sử. Khi sử dụng font phía máy chủ (server-side fonts), bản đồ có thể yêu cầu các glyph PBF vượt quá U+FFFF từ máy chủ thay vì ném lỗi như trước đây. ([#6640](https://github.com/maplibre/maplibre-gl-js/pull/6640)) (by [@1ec5](https://github.com/1ec5))
- GeoJSON Source Diff: cải thiện, trừu tượng hóa, tái cấu trúc, tối ưu hóa, và sửa các hồi quy (regression). ([#6681](https://github.com/maplibre/maplibre-gl-js/pull/6681)) (by [@wayofthefuture](https://github.com/wayofthefuture))
- Tùy chọn waitForCompletion cho setData và updateData của GeoJSONSource ([#6688](https://github.com/maplibre/maplibre-gl-js/pull/6688)) (by [@wayofthefuture](https://github.com/wayofthefuture))
- Cải thiện hiệu năng của `GeoJSONSource#updateData` ([#6668](https://github.com/maplibre/maplibre-gl-js/pull/6668)) (by [@lucaswoj](https://github.com/lucaswoj))
- Tái cấu trúc GeoJSON Worker ([#6702](https://github.com/maplibre/maplibre-gl-js/pull/6702)) (by [@wayofthefuture](https://github.com/wayofthefuture))

### 🐞 Sửa lỗi

- Các bản sửa lỗi linh tinh liên quan đến `GeoJSONSource#updateData` ([#6689](https://github.com/maplibre/maplibre-gl-js/pull/6689), [#6690](https://github.com/maplibre/maplibre-gl-js/pull/6690), [#6704](https://github.com/maplibre/maplibre-gl-js/pull/6704)) (by [@lucaswoj](https://github.com/lucaswoj))

## 5.12.0

### ✨ Tính năng và cải tiến

- Thêm hỗ trợ cho MapLibre Tiles (MLT) bằng cách sử dụng `encoding: 'mlt'` trong định nghĩa vector source ([#6570](https://github.com/maplibre/maplibre-gl-js/pull/6570)) (by [@Salkin975](https://github.com/Salkin975) và [@HarelM](https://github.com/HarelM))
- Cắt lát (slice) các vector tile để cải thiện xử lý vector khi overscale ([#6521](https://github.com/maplibre/maplibre-gl-js/pull/6521)). Thêm cờ `experimentalZoomLevelsToOverscale` vào `MapOptions` để cho phép kiểm soát số mức zoom cần cắt lát và số mức cần scale. Nó dường như có hiệu năng tốt hơn ở các mức zoom cao. Nó có thể ngăn Safari bị crash trong một số trường hợp bằng cách đặt giá trị này về 4 hoặc thấp hơn. (by [@HarelM](https://github.com/HarelM))
- Thêm tùy chọn reduceMotion vào Map Options ([#6661](https://github.com/maplibre/maplibre-gl-js/pull/6661)) (by [@wayofthefuture](https://github.com/wayofthefuture))

### 🐞 Sửa lỗi

- Sửa lỗi thiếu setter `constrainOverride` trong `TransformHelper.apply` ([#6642](https://github.com/maplibre/maplibre-gl-js/pull/6642)) (by [@larsmaxfield](https://github.com/larsmaxfield))
- Sửa lỗi bản đồ trắng sau khi khôi phục ngữ cảnh WebGL ([#6242](https://github.com/maplibre/maplibre-gl-js/issues/6242)) (by [@ToHold](https://github.com/ToHold))

## 5.11.0

### ✨ Tính năng và cải tiến

- Cải thiện hiệu năng của `GeoJSONSource#updateData` khi được gọi với các diff nhỏ ([#6562](https://github.com/maplibre/maplibre-gl-js/pull/6562)) (by [@lucaswoj](https://github.com/lucaswoj))
- Nếu stylesheet không có thuộc tính `glyphs` ở cấp gốc, hãy diễn giải thuộc tính `text-font` như một danh sách font dự phòng theo tầng (cascading fallback) và render toàn bộ văn bản bằng font cục bộ hoặc font hệ thống. ([#4564](https://github.com/maplibre/maplibre-gl-js/pull/4564)) (by [@1ec5](https://github.com/1ec5))
- ⚠️ Tái cấu trúc SourceCache thành TileManager ([#6635](https://github.com/maplibre/maplibre-gl-js/pull/6635)) - đây không phải là một thay đổi phá vỡ tương thích vì SourceCache không nằm trong API công khai, nhưng nếu bạn có một plugin sử dụng các thành phần nội bộ, nó có thể bị hỏng... (by [@wayofthefuture](https://github.com/wayofthefuture))

### 🐞 Sửa lỗi

- Nếu một glyph PBF cần thiết không khả dụng hoặc nó thiếu một glyph cho một ký tự trong `text-field`, hãy thử render nó cục bộ thay vì bị crash. ([#4564](https://github.com/maplibre/maplibre-gl-js/pull/4564)) (by [@1ec5](https://github.com/1ec5))
- Export hàm `now()` trong API timeControl để hoàn thiện API và cho phép mã bên ngoài đọc thời gian được kiểm soát ([#6644](https://github.com/maplibre/maplibre-gl-js/pull/6644)) (by [@bjperson](https://github.com/bjperson))
- Kiểu dáng CSS của ScaleControl chứa `white-space: nowrap` để ngăn việc xuống dòng ([#6647](https://github.com/maplibre/maplibre-gl-js/pull/6647)) (by [@stroebjo](https://github.com/stroebjo))
- Sửa lỗi hiệu ứng mờ dần ở cạnh (edge fading) cho các tile chưa tải ([#6650](https://github.com/maplibre/maplibre-gl-js/pull/6650)) (by [@wayofthefuture](https://github.com/wayofthefuture))

## 5.10.0

### ✨ Tính năng và cải tiến

- Thêm API kiểm soát thời gian (`setNow`, `restoreNow`, `isTimeFrozen`) cho việc render tất định (deterministic), cho phép xuất video theo từng khung hình và kiểm thử tất định ([#6544](https://github.com/maplibre/maplibre-gl-js/pull/6544)) (by [@bjperson](https://github.com/bjperson))
- Sử dụng logic `isHidden` của style trong worker bằng cách thêm một tham số tùy chọn mới `roundMinZoom` ([#6547](https://github.com/maplibre/maplibre-gl-js/pull/6547)) (by [@HarelM](https://github.com/HarelM))
- Thêm callback `transformConstrain` vào các tùy chọn `Map` để ghi đè `constrain` của transform bằng kiểu mới `TransformConstrainFunction`; tái cấu trúc các tùy chọn constructor của transform thành một object `TransformOptions` ([#6484](https://github.com/maplibre/maplibre-gl-js/issues/6484)) (by [@larsmaxfield](https://github.com/larsmaxfield))
- Sử dụng timeControl.now() thay vì browser.now() ([#6573](https://github.com/maplibre/maplibre-gl-js/pull/6573)) (by [@bjperson](https://github.com/bjperson))

### 🐞 Sửa lỗi

- Các sự kiện Contextmenu không bị chặn bởi cuộn trang (scrolling) ([#5683](https://github.com/maplibre/maplibre-gl-js/issues/5683)) (by [@mmc1718](https://github.com/mmc1718))
- Các sự kiện Mousemove không bị chặn bởi cuộn trang ([#6302](https://github.com/maplibre/maplibre-gl-js/issues/6302)) (by [@mmc1718](https://github.com/mmc1718))
- Các đường nét đứt (dashed lines) có đầu bo tròn (rounded caps) bị mờ ([#6554](https://github.com/maplibre/maplibre-gl-js/pull/6554)) (by [@lucaswoj](https://github.com/lucaswoj))
- Giữ nguyên padding của flyTo khi prefers-reduced-motion được bật ([#6576](https://github.com/maplibre/maplibre-gl-js/issues/6576)) (by [@manuel-em](https://github.com/manuel-em))
- Sửa lỗi setClusterOptions không kích hoạt việc tái phân cụm (recluster) khi không có thay đổi dữ liệu nào đang chờ xử lý ([#6603](https://github.com/maplibre/maplibre-gl-js/pull/6603)) (by [@andrewda](https://github.com/andrewda))

## 5.9.0

### ✨ Tính năng và cải tiến

- Cải thiện hiệu ứng mờ dần (fading) - chuyển tiếp chéo (cross-fading) raster hai chiều động và tự mờ dần (self fading) ([#6469](https://github.com/maplibre/maplibre-gl-js/pull/6469)) (by [@wayofthefuture](https://github.com/wayofthefuture))
- Hỗ trợ sử dụng line-gradient cùng với line-dasharray ([#6487](https://github.com/maplibre/maplibre-gl-js/pull/6487)) (by [@Samarth1696](https://github.com/Samarth1696))

### 🐞 Sửa lỗi

- Thêm vai trò (role) `button` vào div của marker để sửa các vấn đề về khả năng truy cập (accessibility) với `aria-label` ([#6435](https://github.com/maplibre/maplibre-gl-js/issues/6435)) (by [@cmburcus](https://github.com/cmburcus))
- Sửa lỗi crash trên iOS khi có quá nhiều biểu tượng cần render ([#6526](https://github.com/maplibre/maplibre-gl-js/pull/6526)) (by [@HarelM](https://github.com/HarelM))

## 5.8.0

### ✨ Tính năng và cải tiến

- Bật các admonition (khung ghi chú) trong tài liệu ở Material for MkDocs. ([#6455](https://github.com/maplibre/maplibre-gl-js/issues/6455)) (by [@morehawes](https://github.com/morehawes))
- Chuyển MapEventType từ type sang interface để cho phép gộp khai báo (declaration merging) ([#6436](https://github.com/maplibre/maplibre-gl-js/pull/6436)) (by [@lhapaipai](https://github.com/lhapaipai))
- Triển khai hỗ trợ tạo kiểu data-driven cho `line-dasharray` ([#5812](https://github.com/maplibre/maplibre-gl-js/pull/5812)) (by [@lucaswoj](https://github.com/lucaswoj))

### 🐞 Sửa lỗi

- Sửa lỗi raster nhấp nháy khi sử dụng terrain 3D và tối ưu hóa logic terrain. ([#6446](https://github.com/maplibre/maplibre-gl-js/pull/6446)) (by [@wayofthefuture](https://github.com/wayofthefuture))
- Sửa lỗi các tile cha (parent tiles) bị giữ lại khi các tile con (descendant tiles) sâu hơn đã che phủ tile lý tưởng (ideal tile) bị thiếu. ([#6442](https://github.com/maplibre/maplibre-gl-js/pull/6442)) (by [@wayofthefuture](https://github.com/wayofthefuture))
- Sửa lỗi khi GeolocateControl phát sự kiện outofmaxbounds trong khi trackUserLocation bị tắt ([#6464](https://github.com/maplibre/maplibre-gl-js/pull/6464)) (by [@sorami](https://github.com/sorami))
- Sửa lỗi globe+terrain bị "zoom vào" khi kéo về phía các cực ([#6470](https://github.com/maplibre/maplibre-gl-js/pull/6470)) (by [@birkskyum](https://github.com/birkskyum))
- Sửa lỗi tràn số nguyên (integer overflow) trong việc đặt vị trí biểu tượng ([#6476](https://github.com/maplibre/maplibre-gl-js/pull/6476)) (by [@HarelM](https://github.com/HarelM))

## 5.7.3

### 🐞 Sửa lỗi

- Sửa lỗi trường hợp giữ lại (retain) các tile con đã tải không giữ lại các tile con cấp cao nhất (uppermost) đã tải ([#6399](https://github.com/maplibre/maplibre-gl-js/pull/6399)) (by [@wayofthefuture](https://github.com/wayofthefuture))
- Sửa lỗi liên quan đến toán tử spread gây ra vấn đề trong Angular và esbuild ([#6438](https://github.com/maplibre/maplibre-gl-js/pull/6438)) (by [@HarelM](https://github.com/HarelM))

## 5.7.2

### 🐞 Sửa lỗi

- Sửa lỗi `_updateRetainedTiles` kiểm tra các tile con khi độ dài các tile con là 1 tile con bị overscale ("child") ([#6388](https://github.com/maplibre/maplibre-gl-js/pull/6388)) (by [@NathanMOlson](https://github.com/NathanMOlson))
- Sửa lỗi đánh giá `global-state` cho các layer được thêm sau khi style đã tải ([#6361](https://github.com/maplibre/maplibre-gl-js/issues/6361)) (by [@melitele](https://github.com/melitele))
- Thay đổi cách thức truyền object `global-state` từ `Style` sang expression để sửa một giải pháp tạm (hack) được đưa ra trong các phiên bản trước ([#6366](https://github.com/maplibre/maplibre-gl-js/pull/6366)) (by [@melitele](https://github.com/melitele))
- Sửa lỗi kích hoạt các sự kiện `load` và `idle` khi TileJSON của source tải thất bại ([#5430](https://github.com/maplibre/maplibre-gl-js/issues/5430)) (by [@melitele](https://github.com/melitele))
- Sửa lỗi các sự kiện chuột trên các feature heatmap ([#714](https://github.com/maplibre/maplibre-gl-js/issues/714)) (by [@melitele](https://github.com/melitele))

## 5.7.1

### 🐞 Sửa lỗi

- Sửa lỗi vòng tròn độ chính xác (accuracy circle) trên control định vị người dùng (locate user control) ([#5432](https://github.com/maplibre/maplibre-gl-js/issues/5432)) (by [@geekdenz](https://github.com/geekdenz))
- Sửa lỗi đánh giá `global-state` trong các thuộc tính paint `...-pattern` ([#6301](https://github.com/maplibre/maplibre-gl-js/pull/6301)) (by [@melitele](https://github.com/melitele))
- Sửa lỗi thao tác kéo (pan) đi sai hướng khi bản đồ đang có pitch ([#6111](https://github.com/maplibre/maplibre-gl-js/issues/6111)) (by [@NathanMOlson](https://github.com/NathanMOlson))
- Sửa lỗi đánh giá `text-color` khi sử dụng `format` bên trong `step` ([#5833](https://github.com/maplibre/maplibre-gl-js/issues/5833)) (by [@sim51](https://github.com/sim51))
- Sửa lỗi hồi quy (regression) trong `mergeSourceDiffs`: xử lý add/remove/removeAll ([#6342](https://github.com/maplibre/maplibre-gl-js/pull/6342)) (by [@lhapaipai](https://github.com/lhapaipai))
- Sửa lỗi đánh giá `global-state` trong các thuộc tính layout `icon-size` và `text-size` ([#6308](https://github.com/maplibre/maplibre-gl-js/issues/6308)) (by [@melitele](https://github.com/melitele))

## 5.7.0

### ✨ Tính năng và cải tiến

- Truyền `lang` của tài liệu (document) tới Tiny-SDF để render các ký tự Trung Quốc Giản thể và Phồn thể ([#6223](https://github.com/maplibre/maplibre-gl-js/pull/6223)) (by [@mapmeld](https://github.com/mapmeld))
- Bật biểu thức `global-state` trong các thuộc tính layout ([#6209](https://github.com/maplibre/maplibre-gl-js/pull/6209)) (by [@melitele](https://github.com/melitele))
- Đồng bộ việc sinh kiểu typescript với việc sinh tài liệu và tránh export các kiểu không được export ([#6217](https://github.com/maplibre/maplibre-gl-js/pull/6217)) (by [@HarelM](https://github.com/HarelM))
- Thêm phương thức `coveringTiles` vào API công khai của object map ([#6292](https://github.com/maplibre/maplibre-gl-js/pull/6292)) (by [@HarelM](https://github.com/HarelM))

### 🐞 Sửa lỗi

- Ngăn JSON style đầu vào gốc bị thay đổi (mutated) bởi các phương thức `Style.set*` ([#6216](https://github.com/maplibre/maplibre-gl-js/pull/6216)) (by [@sruenwg](https://github.com/sruenwg))
- Sửa lỗi đánh giá `global-state` trong các thuộc tính paint có các biểu thức con khác ([#6048](https://github.com/maplibre/maplibre-gl-js/issues/6048)) (by [@melitele](https://github.com/melitele))
- Sửa lỗi bật terrain trong khi đang chuyển tiếp (transitioning) ([#6011](https://github.com/maplibre/maplibre-gl-js/issues/6011)) (by [@NathanMOlson](https://github.com/NathanMOlson))

## 5.6.2

### 🐞 Sửa lỗi

- Sửa lỗi các hiện tượng nhân tạo (artifact) màu trắng khi sử dụng độ cao khác 0 ([#6032](https://github.com/maplibre/maplibre-gl-js/pull/6032)) (by [@NathanMOlson](https://github.com/NathanMOlson))
- Sửa lỗi mất khóa (lock) của geolocate control khi resize cửa sổ và zoom ([#3504](https://github.com/maplibre/maplibre-gl-js/issues/3504)) (by [@tderflinger](https://github.com/tderflinger))
- Sửa lỗi rò rỉ bộ nhớ trong `GeoJSONSource` khi cập nhật dữ liệu nhanh chóng ([#6163](https://github.com/maplibre/maplibre-gl-js/pull/6163)) (by [@andrewda](https://github.com/andrewda))
- Sửa lỗi kiểu tham số của `Map.setTransformRequest` để bao gồm cả `null` ([#6179](https://github.com/maplibre/maplibre-gl-js/issues/6179)) (by [@madoci](https://github.com/madoci))
- Sửa lỗi chính tả `_rotatePitchHandler` trong file `navigation_control.ts` ([#6207](https://github.com/maplibre/maplibre-gl-js/issues/6207)) (by [@daandewaard](https://github.com/daandewaard))

## 5.6.1

### 🐞 Sửa lỗi

- Sửa lỗi sử dụng lệnh gọi `textureSize` trong shader color relief ([#5980](https://github.com/maplibre/maplibre-gl-js/pull/5980)) (by [@mwilsnd](https://github.com/mwilsnd))
- Sửa lỗi biến đổi trục Y trong projectFromLabelPlaneToClipSpace ([#6021](https://github.com/maplibre/maplibre-gl-js/pull/6021)) (by [@SinHongChen](https://github.com/SinHongChen))
- Sắp xếp theo thứ tự bảng chữ cái tất cả các ví dụ ([#6049](https://github.com/maplibre/maplibre-gl-js/pull/6049)) (by [@coliff](https://github.com/coliff))
- Đảm bảo độ mờ (opacity) được đặt lại cho các popup khi `locationOccludedOpacity` không còn được áp dụng ([#6088](https://github.com/maplibre/maplibre-gl-js/pull/6088)) (by [@jammie1903](https://github.com/jammie1903))

## 5.6.0

### ✨ Tính năng và cải tiến

- Thêm `setGlobalStateProperty()` và `getGlobalState()` vào API công khai của map ([#5613](https://github.com/maplibre/maplibre-gl-js/pull/5613)) (by [@zbigniewmatysek-tomtom](https://github.com/zbigniewmatysek-tomtom))
- Cải thiện việc loại bỏ (culling) frustum của tile cho globe, dẫn đến hiệu năng tốt hơn và thời gian tải nhanh hơn. ([#5865](https://github.com/maplibre/maplibre-gl-js/pull/5865)) (by [@kubapelc](https://github.com/kubapelc))
- Thêm loại layer mới `color-relief` để render sắc thái theo độ cao (hypsometric tint) từ các tile terrain-RGB. ([#5742](https://github.com/maplibre/maplibre-gl-js/pull/5742)) (by [@NathanMOlson](https://github.com/NathanMOlson))

### 🐞 Sửa lỗi

- Sửa lỗi hộp ranh giới (bounding box) của `queryRenderedFeatures` khi băng qua kinh tuyến đối cực trong chế độ xem globe. ([#5856](https://github.com/maplibre/maplibre-gl-js/pull/5856)) (by [@msbarry](https://github.com/msbarry))
- Sửa lỗi xử lý các kết quả đặt vị trí glyph không hợp lệ dọc theo các đường ([#5118](https://github.com/maplibre/maplibre-gl-js/pull/5118)) (by [@ragnarok56](https://github.com/ragnarok56))
- Sửa lỗi `refreshTiles()` cho vector tile ([#5875](https://github.com/maplibre/maplibre-gl-js/pull/5875)) (by [@NathanMOlson](https://github.com/NathanMOlson))
- Hoàn tác các thay đổi đối với việc phát hiện giao cắt đa giác (polygon intersection detection) ([#5590](https://github.com/maplibre/maplibre-gl-js/pull/5590) gây ra lỗi [5864](https://github.com/maplibre/maplibre-gl-js/issues/5864)) (by [@LostDragonist](https://github.com/LostDragonist))
- Sửa lỗi các cụm (clusters) bị hỏng khi cung cấp giá trị không phải số nguyên cho `clusterMaxZoom` (sẽ hiển thị cảnh báo) ([#5929](https://github.com/maplibre/maplibre-gl-js/issues/5929)) + làm rõ tài liệu API (by [@igalgh](https://github.com/igalgh))
- Sửa lỗi sử dụng câu lệnh GLSL dành riêng (reserved) `switch` trong shader hillshade ([#5972](https://github.com/maplibre/maplibre-gl-js/pull/5972)) (by [@mwilsnd](https://github.com/mwilsnd))

## 5.5.0

### ✨ Tính năng và cải tiến

- Thêm các phương thức hillshade bổ sung ([#5768](https://github.com/maplibre/maplibre-gl-js/pull/5768)) (by [@NathanMOlson](https://github.com/NathanMOlson))
- Thêm `refreshTiles()` vào API công khai của map ([#5806](https://github.com/maplibre/maplibre-gl-js/pull/5806)) (by [@NathanMOlson](https://github.com/NathanMOlson))
- Vô hiệu hóa nút geolocate control khi quyền truy cập bị từ chối và `trackUserLocation` đang tắt ([#5824](https://github.com/maplibre/maplibre-gl-js/pull/5824)) (by [@tsegarra](https://github.com/tsegarra))

### 🐞 Sửa lỗi

- Sửa lỗi mức zoom tối thiểu khi cuộn (scroll min zoom) trên chế độ xem globe ([#5775](https://github.com/maplibre/maplibre-gl-js/pull/5775)) (by [@msbarry](https://github.com/msbarry))
- ⚠️ Sửa lỗi hình thức hiển thị (appearance) của hillshade thay đổi giữa tile 256x256 và 512x512. Điều này sẽ thay đổi hình thức hiển thị của các layer hillshade sử dụng tile 512x512. ([#5768](https://github.com/maplibre/maplibre-gl-js/pull/5768)) (by [@NathanMOlson](https://github.com/NathanMOlson))
- Sửa lỗi logic hết hạn (expiry) tile cho các tile raster và raster-dem ([#5798](https://github.com/maplibre/maplibre-gl-js/pull/5798)) (by [@NathanMOlson](https://github.com/NathanMOlson))
- Sửa lỗi opacityWhenCovered không hoạt động để ẩn marker phía sau globe khi terrain được bật. ([#5838](https://github.com/maplibre/maplibre-gl-js/pull/5838)) (by [@acalcutt](https://github.com/acalcutt))
- Sửa lỗi các vector tile trong suốt đôi khi hiển thị hình học vượt ra ngoài ranh giới tile khi terrain đang hoạt động ([#5746](https://github.com/maplibre/maplibre-gl-js/pull/5746)) (by [@kubapelc](https://github.com/kubapelc))

## 5.4.0

### ✨ Tính năng và cải tiến

- Thêm khả năng kiểm soát mức độ chi tiết (LOD) của tile vào API công khai ([#5719](https://github.com/maplibre/maplibre-gl-js/pull/5719)) (by [@NathanMOlson](https://github.com/NathanMOlson))

### 🐞 Sửa lỗi

- Sửa lỗi `queryRenderedFeatures` trên chế độ xem globe khi băng qua đường đổi ngày quốc tế (international date line) ([#5765](https://github.com/maplibre/maplibre-gl-js/pull/5765)) (by [@msbarry](https://github.com/msbarry))
- Sửa lỗi `unproject` của globe để giới hạn các điểm về đường chân trời ([#5771](https://github.com/maplibre/maplibre-gl-js/pull/5771)) (by [@msbarry](https://github.com/msbarry))
- Sửa lỗi tọa độ kéo marker (marker drag) bị lệch kinh độ ±360° với Globe ([#5473](https://github.com/maplibre/maplibre-gl-js/issues/5473)) (by [@docentYT](https://github.com/docentYT))

## 5.3.1

### 🐞 Sửa lỗi

- Chỉ thêm `aria-label` vào phần tử của Marker nếu nó chưa có sẵn ([#5298](https://github.com/maplibre/maplibre-gl-js/pull/5298)) (by [@liorchamla](https://github.com/liorchamla))
- Trạng thái của `glPixelStore` giờ đây được dọn dẹp đúng cách sau khi cập nhật texture để tránh các lệnh gọi `glTexSubImage2D` trên cùng một ngữ cảnh (context) gl có hành vi khác nhau một cách ngẫu nhiên ([#5730](https://github.com/maplibre/maplibre-gl-js/pull/5730)) (by [@kubapelc](https://github.com/kubapelc))
- Sửa lỗi nút đóng popup không hoạt động ([#5754](https://github.com/maplibre/maplibre-gl-js/pull/5754)) (by [@HarelM](https://github.com/HarelM))

## 5.3.0

### ✨ Tính năng và cải tiến

- Thêm `getBounds` vào GeoJSON source để cho phép lấy ranh giới của dữ liệu bên trong nó ([#5575](https://github.com/maplibre/maplibre-gl-js/pull/5575)) (by [@HarelM](https://github.com/HarelM))
- Thêm một kiểm tra cho MouseEvent, để tránh lỗi khi bot đang thu thập dữ liệu (crawling) trên trang web sử dụng instance Event thay vì instance MouseEvent cho các kiểu như mouseover, mouseout v.v.. ([#5466](https://github.com/maplibre/maplibre-gl-js/pull/5466)). (by [@ToHold](https://github.com/ToHold))

### 🐞 Sửa lỗi

- Sửa lỗi phát hiện giao cắt (intersection) giữa MultiPolygon và Point ([#5590](https://github.com/maplibre/maplibre-gl-js/pull/5590)) (by [@LostDragonist](https://github.com/LostDragonist))
- Sửa lỗi hình ảnh chỉ được render một phần trên các tile terrain ([#1559](https://github.com/maplibre/maplibre-gl-js/issues/1559)). (by [@pstaszek](https://github.com/pstaszek))
- Sửa lỗi vùng bắt sự kiện (hitbox) của circle layer trong chế độ chiếu Globe ([#5599](https://github.com/maplibre/maplibre-gl-js/pull/5599)) (by [@lucaswoj](https://github.com/lucaswoj))
- Sửa lỗi attribution control render lại quá mức (excessive rerendering) ([#5673](https://github.com/maplibre/maplibre-gl-js/pull/5673)) (by [@viernullvier](https://github.com/viernullvier))

## 5.2.0

### ✨ Tính năng và cải tiến

- Cho phép đặt độ mờ (opacity) khi vị trí trở nên vô hình trong phép chiếu globe. ([#5532](https://github.com/maplibre/maplibre-gl-js/pull/5532)) (by [@geekdenz](https://github.com/geekdenz))

### 🐞 Sửa lỗi

- Sửa lỗi rò rỉ bộ nhớ của listener tín hiệu AbortController trong frameAsync và sendAsync. ([#5561](https://github.com/maplibre/maplibre-gl-js/pull/5561)) (by [@kamil-sienkiewicz-asi](https://github.com/kamil-sienkiewicz-asi))
- Loại bỏ listener sự kiện closeButton khi gọi popup.remove(). ([#5564](https://github.com/maplibre/maplibre-gl-js/pull/5564)) (by [@kamil-sienkiewicz-asi](https://github.com/kamil-sienkiewicz-asi))
- Thêm kiểu `GeoJSONFeature` còn thiếu vào phần export của thư viện vì nó được expose bởi `querySourceFeatures` ([#5567](https://github.com/maplibre/maplibre-gl-js/pull/5567)) (by [@HarelM](https://github.com/HarelM))

## 5.1.1

### ✨ Tính năng và cải tiến

- Tránh đặt độ mờ marker hai lần. ([#5441](https://github.com/maplibre/maplibre-gl-js/pull/5441)) (by [@erasta](https://github.com/erasta))

### 🐞 Sửa lỗi

- Sửa lỗi cách padding được áp dụng khi sử dụng flyTo() với Globe ([#5406](https://github.com/maplibre/maplibre-gl-js/pull/5406)) (by [@pjamessteven](https://github.com/pjamessteven))
- Sửa lỗi kiểm tra hợp lệ hash URL để hỗ trợ phạm vi bearing từ -180 đến 180 ([#5461](https://github.com/maplibre/maplibre-gl-js/issues/5461)) (by [@stanislawpuda-tomtom](https://github.com/stanislawpuda-tomtom))
- Sửa lỗi tính toán tile theo mức zoom biến đổi (variable zoom) khi có đặt padding ([#5486](https://github.com/maplibre/maplibre-gl-js/issues/5486)) (by [@NathanMOlson](https://github.com/NathanMOlson))
- Sửa lỗi render các ký hiệu tiếng Nhật bị bỏ qua một cách vô tình. ([#5421](https://github.com/maplibre/maplibre-gl-js/pull/5421)) (by [@Kanahiro](https://github.com/Kanahiro))

## 5.1.0

### ✨ Tính năng và cải tiến

- Thêm hỗ trợ cho `vertical-align` trong biểu thức `format` ([đặc tả](https://maplibre.org/maplibre-style-spec/expressions/#format))([#5043](https://github.com/maplibre/maplibre-gl-js/pull/5043)). (by [@stanislawpuda-tomtom](https://github.com/stanislawpuda-tomtom))

### 🐞 Sửa lỗi

- Đồng bộ lại khung hình render trong callback requestAnimationFrame ([#4535](https://github.com/maplibre/maplibre-gl-js/pull/4535)) (by [@xabbu42](https://github.com/xabbu42))

## 5.0.1

### ✨ Tính năng và cải tiến

- ⚠️ Hoàn tác các thay đổi được thực hiện trong `geometry-type` ([#5331](https://github.com/maplibre/maplibre-gl-js/pull/5331)). Thay đổi này đã gây ra vấn đề cho [một số lượng lớn các style](https://github.com/maplibre/maplibre-style-spec/issues/965) và do đó đã bị hoàn tác. (by [@HarelM](https://github.com/HarelM))

### 🐞 Sửa lỗi

- Bỏ qua hiệu ứng hover CSS của nút control trên các thiết bị cảm ứng ([#5285](https://github.com/maplibre/maplibre-gl-js/pull/5285)) (by [@digitaltom](https://github.com/digitaltom))

## 5.0.0

### ✨ Tính năng và cải tiến

- ~~⚠️ Thay đổi `geometry-type` để nhận diện các feature "Multi-" ([#4877](https://github.com/maplibre/maplibre-gl-js/pull/4877)). Sử dụng `$type` vốn không hỗ trợ "Multi-" hoặc sử dụng biểu thức `in` để có được hành vi trước đây.~~ (by [@HarelM](https://github.com/HarelM))
- ⚠️ Các tham số của phương thức `queryIntersectsFeature` của `StyleLayer` đã được chuyển sang `QueryIntersectsFeatureParams`. ([#5276](https://github.com/maplibre/maplibre-gl-js/pull/5276)) Bọc các tham số phương thức bằng `{}` để giải quyết vấn đề này (by [@HarelM](https://github.com/HarelM))
- ⚠️ Hỗ trợ đặt các tùy chọn ngữ cảnh (context) WebGL khi tạo bản đồ ([#5196](https://github.com/maplibre/maplibre-gl-js/pull/5196)). Các tùy chọn ngữ cảnh WebGL được hỗ trợ trước đây như `antialias`, `preserveDrawingBuffer` và `failIfMajorPerformanceCaveat` giờ đây phải được định nghĩa bên trong object `canvasContextAttributes` trên `MapOptions`. (by [@ibesora](https://github.com/ibesora))
- ⚠️ Thay đổi kiểu trả về của phương thức `on` để trả về một `Subscription`, cho phép hủy đăng ký (unsubscribe) dễ dàng ([#5080](https://github.com/maplibre/maplibre-gl-js/pull/5080)). `map.on('x').on('y')` => `map.on('x'); map.on('y');`. (by [@HarelM](https://github.com/HarelM))
- ⚠️ Thay đổi hành vi xoay khi kéo (drag rotate) để xoay quanh tâm màn hình ([#5074](https://github.com/maplibre/maplibre-gl-js/pull/5074)) (by [@HarelM](https://github.com/HarelM))
- ⚠️ Trả về độ cao thực từ queryTerrainElevation + Truyền các ma trận không bị dịch chuyển (non-translated) cho custom layer trên bản đồ mercator ([#3854](https://github.com/maplibre/maplibre-gl-js/pull/3854)) (by [@sbachinin](https://github.com/sbachinin))
- ⚠️ Loại bỏ bản build production chưa được minify ([#4906](https://github.com/maplibre/maplibre-gl-js/pull/4906)). Bạn sẽ cần sử dụng một bản build khác. (by [@birkskyum](https://github.com/birkskyum))
- Cho phép đặt phiên bản WebGL mong muốn để sử dụng ([#5236](https://github.com/maplibre/maplibre-gl-js/pull/5236)). Giờ đây bạn có thể dùng `contextType` bên trong `canvasContextAttributes` để chọn phiên bản WebGL cần sử dụng (by [@ibesora](https://github.com/ibesora))
- Runtime WebGL hai lớp (Dual-Stack) với cơ chế dự phòng (fallback) từ WebGL2 sang WebGL1 ([#5198](https://github.com/maplibre/maplibre-gl-js/pull/5198)) (by [@0xFA11](https://github.com/0xFA11))
- Thêm hỗ trợ cho biểu thức kiểu phép chiếu (projection type expression) như một phần của việc tái cấu trúc các class transform và projection ([#5139](https://github.com/maplibre/maplibre-gl-js/pull/5139)) (by [@HarelM](https://github.com/HarelM))
- Export class `Event` ([#5016](https://github.com/maplibre/maplibre-gl-js/pull/5016)) (by [@zdila](https://github.com/zdila))
- Hỗ trợ phép chiếu Vertical Perspective ([#5023](https://github.com/maplibre/maplibre-gl-js/pull/5023)) (by [@birkskyum](https://github.com/birkskyum))
- Khi phân cụm (clustering) các vòng tròn và promoteId được đặt thành một tham số nào đó, ID được promote sẽ được dùng cho các feature không thuộc cụm, và cluster_id được dùng cho các feature thuộc cụm. Trước đây ID là undefined đối với các feature không thuộc cụm ([#4899](https://github.com/maplibre/maplibre-gl-js/pull/4899)) (by [@popkinj](https://github.com/popkinj))
- Hỗ trợ Terrain trong phép chiếu Globe ([#4976](https://github.com/maplibre/maplibre-gl-js/pull/4976)) (by [@birkskyum](https://github.com/birkskyum))
- Cải thiện hiệu năng của hàm `coveringTiles` (loại bỏ tile) đối với globe ([#4937](https://github.com/maplibre/maplibre-gl-js/pull/4937)) (by [@kubapelc](https://github.com/kubapelc))
- Bắt các lỗi lấy dữ liệu từ mạng (network fetching errors) như CORS, DNS hoặc URL không hợp lệ dưới dạng `AJAXError` thực sự để expose chi tiết yêu cầu HTTP cho sự kiện `"error"` ([#4822](https://github.com/maplibre/maplibre-gl-js/pull/4822)) (by [@jonathanlurie](https://github.com/jonathanlurie))
- Thêm setVerticalFieldOfView() vào API công khai ([#4717](https://github.com/maplibre/maplibre-gl-js/issues/4717)) (by [@NathanMOlson](https://github.com/NathanMOlson))
- Vô hiệu hóa bầu trời (sky) khi sử dụng globe và hòa trộn (blend) nó vào khi chuyển sang mercator ([#4853](https://github.com/maplibre/maplibre-gl-js/issues/4853)) (by [@ibesora](https://github.com/ibesora))
- GlobeControl mới ([#4960](https://github.com/maplibre/maplibre-gl-js/pull/4960)) (by [@birkskyum](https://github.com/birkskyum))
- Thêm hỗ trợ cho pitch > 90 độ ([#4717](https://github.com/maplibre/maplibre-gl-js/issues/4717)) (by [@NathanMOlson](https://github.com/NathanMOlson))
- Thêm hỗ trợ cho góc roll của camera ([#4717](https://github.com/maplibre/maplibre-gl-js/issues/4717)) (by [@NathanMOlson](https://github.com/NathanMOlson))
- Cải thiện hiệu năng của `queryRenderedFeatures` bằng cách sử dụng `Set` của JavaScript để đánh giá thành viên layer (layer membership) ở nội bộ ([#4777](https://github.com/maplibre/maplibre-gl-js/pull/4777)) (by [@tomhicks](https://github.com/tomhicks))
- Hỗ trợ chế độ globe ([#3963](https://github.com/maplibre/maplibre-gl-js/pull/3963)) (by [@HarelM](https://github.com/HarelM))
- Gộp việc triển khai khí quyển (atmosphere) và bầu trời (sky) ([#3888](https://github.com/maplibre/maplibre-gl-js/issues/3888)) (by [@Pheonor](https://github.com/Pheonor))
- Thêm tùy chọn hiển thị một bầu khí quyển chân thực khi sử dụng phép chiếu Globe ([#3888](https://github.com/maplibre/maplibre-gl-js/issues/3888)) (by [@Pheonor](https://github.com/Pheonor))

### 🐞 Sửa lỗi

- ⚠️ Sửa lỗi mức độ chi tiết (level of detail) ở góc pitch cao bằng cách thay đổi các tile được tải ([#3983](https://github.com/maplibre/maplibre-gl-js/issues/3983)) (by [@NathanMOlson](https://github.com/NathanMOlson))
- Sửa lỗi các lỗ hổng ở các cực khi terrain được sử dụng cùng với globe ([#5232](https://github.com/maplibre/maplibre-gl-js/pull/5232)) (by [@kubapelc](https://github.com/kubapelc))
- Sửa lỗi các hiện tượng nhân tạo hình học khi terrain của globe bị thu nhỏ quá mức ([#5232](https://github.com/maplibre/maplibre-gl-js/pull/5232)) (by [@kubapelc](https://github.com/kubapelc))
- Sửa lỗi tâm bị giới hạn (constrained) không chính xác khi sử dụng globe ([#5186](https://github.com/maplibre/maplibre-gl-js/pull/5186)) (by [@ibesora](https://github.com/ibesora))
- Sửa lỗi khí quyển hòa trộn không đúng vào nền ([#5235](https://github.com/maplibre/maplibre-gl-js/pull/5235)) (by [@kubapelc](https://github.com/kubapelc))
- Sửa lỗi phân tích sai vị trí hash ([#5131](https://github.com/maplibre/maplibre-gl-js/issues/5131)) (by [@mattesCZ](https://github.com/mattesCZ))
- Sửa lỗi nuốt (swallowing) các lỗi ([#4532](https://github.com/maplibre/maplibre-gl-js/issues/4532)) (by [@ibesora](https://github.com/ibesora))
- Sửa lỗi các yêu cầu bị lỗi không được báo cáo trên handler `error` ([#4613](https://github.com/maplibre/maplibre-gl-js/issues/4613)) (by [@ibesora](https://github.com/ibesora))
- Sửa lỗi không giữ lại (retain) các tile con khi sử dụng globe ([#5271](https://github.com/maplibre/maplibre-gl-js/pull/5271)) (by [@ibesora](https://github.com/ibesora))
- Sửa lỗi kích thước biểu tượng tăng lên khi nhìn từ các cực ([#5275](https://github.com/maplibre/maplibre-gl-js/pull/5275)) (by [@ibesora](https://github.com/ibesora))
- Sửa lỗi các custom layer trên globe được cung cấp sai ma trận sau khi chuyển tiếp phép chiếu sang mercator ([#5150](https://github.com/maplibre/maplibre-gl-js/pull/5150)) (by [@kubapelc](https://github.com/kubapelc))
- Sửa lỗi các mô hình 3D tùy chỉnh biến mất trong quá trình chuyển tiếp phép chiếu ([#5150](https://github.com/maplibre/maplibre-gl-js/pull/5150)) (by [@kubapelc](https://github.com/kubapelc))
- Sửa lỗi hồi quy (regression) ở la bàn (compass) của NavigationControl trên các trình duyệt Firefox và Safari ([#5205](https://github.com/maplibre/maplibre-gl-js/pull/5205)) (by [@raboczi](https://github.com/raboczi))
- Sửa lỗi zoom mượt bằng con lăn chuột ([#5154](https://github.com/maplibre/maplibre-gl-js/pull/5154)) (by [@Al-4SW](https://github.com/Al-4SW))
- Thay đổi hành vi xoay khi kéo để bớt đột ngột hơn quanh tâm ([#5104](https://github.com/maplibre/maplibre-gl-js/pull/5104)) (by [@HarelM](https://github.com/HarelM))
- Sửa lỗi hồi quy ở tính năng render các bản sao thế giới (render world copies) ([#5101](https://github.com/maplibre/maplibre-gl-js/pull/5101)) (by [@HarelM](https://github.com/HarelM))
- Sửa lỗi roll không mong muốn khi chuyển động bị gián đoạn ([#5083](https://github.com/maplibre/maplibre-gl-js/issues/5083)) (by [@NathanMOlson](https://github.com/NathanMOlson))
- Sửa lỗi kết quả của biểu thức filter `geometry-type` ([#5132](https://github.com/maplibre/maplibre-gl-js/pull/5132)) (by [@HarelM](https://github.com/HarelM))
- Sửa lỗi easeTo không áp dụng padding trong phép chiếu globe ([#5134](https://github.com/maplibre/maplibre-gl-js/pull/5134)) (by [@kamil-sienkiewicz-asi](https://github.com/kamil-sienkiewicz-asi))
- Chuyển đổi các shader WebGL1 sang WebGL2 ([#5166](https://github.com/maplibre/maplibre-gl-js/pull/5166)) (by [@0xFA11](https://github.com/0xFA11))
- Sửa lỗi hiện tượng nhấp nháy đường (line flickering) ([#5094](https://github.com/maplibre/maplibre-gl-js/pull/5094)) (by [@ibesora](https://github.com/ibesora))
- Sửa lỗi hiệu năng kém trên Chrome liên quan đến việc truyền ma trận vào WebGL ([#5072](https://github.com/maplibre/maplibre-gl-js/pull/5072)) (by [@kubapelc](https://github.com/kubapelc))
- Sửa lỗi scale control cho globe khi thu nhỏ ([#4897](https://github.com/maplibre/maplibre-gl-js/pull/4897)) (by [@pcardinal](https://github.com/pcardinal))
- Sửa lỗi cooperative gestures hiển thị văn bản trợ giúp dành cho di động khi chiều rộng màn hình nhỏ hơn 480px trên các thiết bị không cảm ứng ([#5053](https://github.com/maplibre/maplibre-gl-js/pull/5053)) (by [@timsluis](https://github.com/timsluis))
- Sửa lỗi scale bán kính cụm (cluster radius) không chính xác trong `GeoJSONSource.setClusterOptions()` ([#5055](https://github.com/maplibre/maplibre-gl-js/pull/5055)) (by [@ciscorn](https://github.com/ciscorn))
- Cải thiện việc xử lý innerHTML trong mã nguồn ([#5057](https://github.com/maplibre/maplibre-gl-js/pull/5057)) (by [@HarelM](https://github.com/HarelM))
- Sửa lỗi hình học bị render vượt ra ngoài ranh giới tile ([#4868](https://github.com/maplibre/maplibre-gl-js/pull/4868)) (by [@kubapelc](https://github.com/kubapelc))
- Sửa lỗi các văn bản đặt dọc theo đường và căn theo pitch của bản đồ (map-pitch-aligned) bị quá lớn khi nhìn từ một số vĩ độ trên globe ([#4786](https://github.com/maplibre/maplibre-gl-js/issues/4786)) (by [@kubapelc](https://github.com/kubapelc))
- Vô hiệu hóa render Fog không được hỗ trợ, dành cho Terrain3D trên Globe ([#4963](https://github.com/maplibre/maplibre-gl-js/pull/4963)) (by [@birkskyum](https://github.com/birkskyum))
- Sửa lỗi raster tile source không fetch các cập nhật sau một lỗi yêu cầu ([#4890](https://github.com/maplibre/maplibre-gl-js/pull/4890)) (by [@wagewarbler](https://github.com/wagewarbler))
- Sửa lỗi các mô hình 3D trong custom layer không bị che khuất đúng cách bởi globe ([#4817](https://github.com/maplibre/maplibre-gl-js/issues/4817)) (by [@kubapelc](https://github.com/kubapelc))
- Sửa lỗi các raster tile không được render đúng khi sử dụng globe và terrain ([#4912](https://github.com/maplibre/maplibre-gl-js/pull/4912)) (by [@ibesora](https://github.com/ibesora))
- Sửa lỗi văn bản không bị ẩn phía sau globe khi chế độ overlap được đặt thành `always` ([#4802](https://github.com/maplibre/maplibre-gl-js/issues/4802)) (by [@kubapelc](https://github.com/kubapelc))
- Sửa lỗi một khung hình trắng đơn lẻ hiển thị khi bản đồ chuyển tiếp nội bộ từ phép chiếu mercator sang globe ([#4816](https://github.com/maplibre/maplibre-gl-js/issues/4816)) (by [@kubapelc](https://github.com/kubapelc))
- Sửa lỗi tải plugin RTL phiên bản 0.3.0 ([#4860](https://github.com/maplibre/maplibre-gl-js/pull/4860)) (by [@HarelM](https://github.com/HarelM))
- Sửa lỗi rò rỉ bộ nhớ do thiếu việc hủy đăng ký (removal) listener sự kiện ([#4824](https://github.com/maplibre/maplibre-gl-js/pull/4824)) (by [@HarelM](https://github.com/HarelM))
- Cải thiện hiệu năng va chạm biểu tượng (symbol collision) cho cả hai phép chiếu mercator và globe ([#4778](https://github.com/maplibre/maplibre-gl-js/pull/4778)) (by [@kubapelc](https://github.com/kubapelc))
- Sửa lỗi scale đường không đúng gần các cực trong phép chiếu globe ([#4778](https://github.com/maplibre/maplibre-gl-js/pull/4778)) (by [@kubapelc](https://github.com/kubapelc))
- Sửa lỗi globe tải quá nhiều tile ở một mức zoom cao không cần thiết khi camera đang pitch ([#4778](https://github.com/maplibre/maplibre-gl-js/pull/4778)) (by [@kubapelc](https://github.com/kubapelc))

## 5.0.0-pre.10

### ✨ Tính năng và cải tiến

- Thêm hỗ trợ cho biểu thức kiểu phép chiếu như một phần của việc tái cấu trúc các class transform và projection ([#5139](https://github.com/maplibre/maplibre-gl-js/pull/5139)) (by [@HarelM](https://github.com/HarelM))
- ⚠️ Hỗ trợ đặt các tùy chọn ngữ cảnh WebGL khi tạo bản đồ ([#5196](https://github.com/maplibre/maplibre-gl-js/pull/5196)). Các tùy chọn ngữ cảnh WebGL được hỗ trợ trước đây như `antialias`, `preserveDrawingBuffer` và `failIfMajorPerformanceCaveat` giờ đây phải được định nghĩa bên trong object `canvasContextAttributes` trên `MapOptions`. (by [@ibesora](https://github.com/ibesora))
- Runtime WebGL hai lớp với cơ chế dự phòng từ WebGL2 sang WebGL1 ([#5198](https://github.com/maplibre/maplibre-gl-js/pull/5198)) (by [@0xFA11](https://github.com/0xFA11))

### 🐞 Sửa lỗi

- Sửa lỗi các custom layer trên globe được cung cấp sai ma trận sau khi chuyển tiếp phép chiếu sang mercator ([#5150](https://github.com/maplibre/maplibre-gl-js/pull/5150)) (by [@kubapelc](https://github.com/kubapelc))
- Sửa lỗi các mô hình 3D tùy chỉnh biến mất trong quá trình chuyển tiếp phép chiếu ([#5150](https://github.com/maplibre/maplibre-gl-js/pull/5150)) (by [@kubapelc](https://github.com/kubapelc))
- Sửa lỗi hồi quy ở la bàn của NavigationControl trên các trình duyệt Firefox và Safari ([#5205](https://github.com/maplibre/maplibre-gl-js/pull/5205)) (by [@raboczi](https://github.com/raboczi))

## 5.0.0-pre.9

### 🐞 Sửa lỗi

- Sửa lỗi zoom mượt bằng con lăn chuột ([#5154](https://github.com/maplibre/maplibre-gl-js/pull/5154)) (by [@Al-4SW](https://github.com/Al-4SW))
- ⚠️ Thay đổi hành vi xoay khi kéo để bớt đột ngột hơn quanh tâm ([#5104](https://github.com/maplibre/maplibre-gl-js/pull/5104)) (by [@HarelM](https://github.com/HarelM))
- Sửa lỗi hồi quy ở tính năng render các bản sao thế giới ([#5101](https://github.com/maplibre/maplibre-gl-js/pull/5101)) (by [@HarelM](https://github.com/HarelM))
- Sửa lỗi roll không mong muốn khi chuyển động bị gián đoạn ([#5083](https://github.com/maplibre/maplibre-gl-js/issues/5083)) (by [@NathanMOlson](https://github.com/NathanMOlson))
- Sửa lỗi kết quả của biểu thức filter `geometry-type` ([#5132](https://github.com/maplibre/maplibre-gl-js/pull/5132)) (by [@HarelM](https://github.com/HarelM))
- Sửa lỗi easeTo không áp dụng padding trong phép chiếu globe ([#5134](https://github.com/maplibre/maplibre-gl-js/pull/5134)) (by [@kamil-sienkiewicz-asi](https://github.com/kamil-sienkiewicz-asi))
- Chuyển đổi các shader WebGL1 sang WebGL2 ([#5166](https://github.com/maplibre/maplibre-gl-js/pull/5166)) (by [@0xFA11](https://github.com/0xFA11))

## 5.0.0-pre.8

### ✨ Tính năng và cải tiến

- ⚠️ Thay đổi kiểu trả về của phương thức `on` để trả về một `Subscription`, cho phép hủy đăng ký dễ dàng ([#5080](https://github.com/maplibre/maplibre-gl-js/pull/5080)) (by [@HarelM](https://github.com/HarelM))

### 🐞 Sửa lỗi

- Sửa lỗi hiện tượng nhấp nháy đường ([#5094](https://github.com/maplibre/maplibre-gl-js/pull/5094)) (by [@ibesora](https://github.com/ibesora))
- Sửa lỗi hiệu năng kém trên Chrome liên quan đến việc truyền ma trận vào WebGL ([#5072](https://github.com/maplibre/maplibre-gl-js/pull/5072)) (by [@kubapelc](https://github.com/kubapelc))

## 5.0.0-pre.7

### ✨ Tính năng và cải tiến

- ⚠️ Thay đổi hành vi xoay khi kéo để xoay quanh tâm màn hình ([#5074](https://github.com/maplibre/maplibre-gl-js/pull/5074)) (by [@HarelM](https://github.com/HarelM))
- Export class `Event` ([#5016](https://github.com/maplibre/maplibre-gl-js/pull/5016)) (by [@zdila](https://github.com/zdila))
- Hỗ trợ phép chiếu Vertical Perspective ([#5023](https://github.com/maplibre/maplibre-gl-js/pull/5023)) (by [@birkskyum](https://github.com/birkskyum))

### 🐞 Sửa lỗi

- Sửa lỗi scale control cho globe khi thu nhỏ ([#4897](https://github.com/maplibre/maplibre-gl-js/pull/4897)) (by [@pcardinal](https://github.com/pcardinal))
- Sửa lỗi cooperative gestures hiển thị văn bản trợ giúp dành cho di động khi chiều rộng màn hình nhỏ hơn 480px trên các thiết bị không cảm ứng ([#5053](https://github.com/maplibre/maplibre-gl-js/pull/5053)) (by [@timsluis](https://github.com/timsluis))
- Sửa lỗi scale bán kính cụm không chính xác trong `GeoJSONSource.setClusterOptions()` ([#5055](https://github.com/maplibre/maplibre-gl-js/pull/5055)) (by [@ciscorn](https://github.com/ciscorn))
- Cải thiện việc xử lý innerHTML trong mã nguồn ([#5057](https://github.com/maplibre/maplibre-gl-js/pull/5057)) (by [@HarelM](https://github.com/HarelM))
- Sửa lỗi hình học bị render vượt ra ngoài ranh giới tile ([#4868](https://github.com/maplibre/maplibre-gl-js/pull/4868)) (by [@kubapelc](https://github.com/kubapelc))

## 5.0.0-pre.6

### ✨ Tính năng và cải tiến

- Khi phân cụm các vòng tròn và promoteId được đặt thành một tham số nào đó, ID được promote sẽ được dùng cho các feature không thuộc cụm, và cluster_id được dùng cho các feature thuộc cụm. Trước đây ID là undefined đối với các feature không thuộc cụm ([#4899](https://github.com/maplibre/maplibre-gl-js/pull/4899)) (by [@popkinj](https://github.com/popkinj))
- Hỗ trợ Terrain trong phép chiếu Globe ([#4976](https://github.com/maplibre/maplibre-gl-js/pull/4976)) (by [@birkskyum](https://github.com/birkskyum))
- Cải thiện hiệu năng của hàm `coveringTiles` (loại bỏ tile) đối với globe ([#4937](https://github.com/maplibre/maplibre-gl-js/pull/4937)) (by [@kubapelc](https://github.com/kubapelc))

### 🐞 Sửa lỗi

- ⚠️ Sửa lỗi mức độ chi tiết ở góc pitch cao bằng cách thay đổi các tile được tải ([#3983](https://github.com/maplibre/maplibre-gl-js/issues/3983)) (by [@NathanMOlson](https://github.com/NathanMOlson))
- ~~⚠️ Sửa lỗi phân tích URL trong `normalizeSpriteURL`, các URL sprite phải là tuyệt đối ([#4962](https://github.com/maplibre/maplibre-gl-js/pull/4962))~~ (by [@jcary741](https://github.com/jcary741))

## 5.0.0-pre.5

### ✨ Tính năng và cải tiến

- Bắt các lỗi lấy dữ liệu từ mạng như CORS, DNS hoặc URL không hợp lệ dưới dạng `AJAXError` thực sự để expose chi tiết yêu cầu HTTP cho sự kiện `"error"` ([#4822](https://github.com/maplibre/maplibre-gl-js/pull/4822)) (by [@jonathanlurie](https://github.com/jonathanlurie))
- Thêm setVerticalFieldOfView() vào API công khai ([#4717](https://github.com/maplibre/maplibre-gl-js/issues/4717)) (by [@NathanMOlson](https://github.com/NathanMOlson))
- ⚠️ Trả về độ cao thực từ queryTerrainElevation + Truyền các ma trận không bị dịch chuyển cho custom layer trên bản đồ mercator ([#3854](https://github.com/maplibre/maplibre-gl-js/pull/3854)) (by [@sbachinin](https://github.com/sbachinin))
- Vô hiệu hóa bầu trời khi sử dụng globe và hòa trộn nó vào khi chuyển sang mercator ([#4853](https://github.com/maplibre/maplibre-gl-js/issues/4853)) (by [@ibesora](https://github.com/ibesora))
- GlobeControl mới ([#4960](https://github.com/maplibre/maplibre-gl-js/pull/4960)) (by [@birkskyum](https://github.com/birkskyum))

### 🐞 Sửa lỗi

- Sửa lỗi các văn bản đặt dọc theo đường và căn theo pitch của bản đồ bị quá lớn khi nhìn từ một số vĩ độ trên globe ([#4786](https://github.com/maplibre/maplibre-gl-js/issues/4786)) (by [@kubapelc](https://github.com/kubapelc))
- Vô hiệu hóa render Fog không được hỗ trợ, dành cho Terrain3D trên Globe ([#4963](https://github.com/maplibre/maplibre-gl-js/pull/4963)) (by [@birkskyum](https://github.com/birkskyum))

## 5.0.0-pre.4

### ✨ Tính năng và cải tiến

- ⚠️ Thay đổi `geometry-type` để nhận diện các feature "Multi-" ([#4877](https://github.com/maplibre/maplibre-gl-js/pull/4877)) (by [@HarelM](https://github.com/HarelM))
- Thêm hỗ trợ cho pitch > 90 độ ([#4717](https://github.com/maplibre/maplibre-gl-js/issues/4717)) (by [@NathanMOlson](https://github.com/NathanMOlson))

### 🐞 Sửa lỗi

- ~~⚠️ Sửa lỗi thứ tự của normalizeSpriteURL và transformRequest trong loadSprite ([#3897](https://github.com/maplibre/maplibre-gl-js/issues/3897))~~ (by [@jcary741](https://github.com/jcary741))
- ⚠️ Loại bỏ bản build production chưa được minify ([#4906](https://github.com/maplibre/maplibre-gl-js/pull/4906)) (by [@birkskyum](https://github.com/birkskyum))
- Sửa lỗi raster tile source không fetch các cập nhật sau một lỗi yêu cầu ([#4890](https://github.com/maplibre/maplibre-gl-js/pull/4890)) (by [@wagewarbler](https://github.com/wagewarbler))
- Sửa lỗi các mô hình 3D trong custom layer không bị che khuất đúng cách bởi globe ([#4817](https://github.com/maplibre/maplibre-gl-js/issues/4817)) (by [@kubapelc](https://github.com/kubapelc))
- Sửa lỗi các raster tile không được render đúng khi sử dụng globe và terrain ([#4912](https://github.com/maplibre/maplibre-gl-js/pull/4912)) (by [@ibesora](https://github.com/ibesora))

## 5.0.0-pre.3

### ✨ Tính năng và cải tiến

- Thêm hỗ trợ cho góc roll của camera ([#4717](https://github.com/maplibre/maplibre-gl-js/issues/4717)) (by [@NathanMOlson](https://github.com/NathanMOlson))

### 🐞 Sửa lỗi

- Sửa lỗi văn bản không bị ẩn phía sau globe khi chế độ overlap được đặt thành `always` ([#4802](https://github.com/maplibre/maplibre-gl-js/issues/4802)) (by [@kubapelc](https://github.com/kubapelc))
- Sửa lỗi một khung hình trắng đơn lẻ hiển thị khi bản đồ chuyển tiếp nội bộ từ phép chiếu mercator sang globe ([#4816](https://github.com/maplibre/maplibre-gl-js/issues/4816)) (by [@kubapelc](https://github.com/kubapelc))
- Sửa lỗi tải plugin RTL phiên bản 0.3.0 ([#4860](https://github.com/maplibre/maplibre-gl-js/pull/4860)) (by [@HarelM](https://github.com/HarelM))

## 5.0.0-pre.2

### ✨ Tính năng và cải tiến

- Cải thiện hiệu năng của `queryRenderedFeatures` bằng cách sử dụng `Set` của JavaScript để đánh giá thành viên layer ở nội bộ ([#4777](https://github.com/maplibre/maplibre-gl-js/pull/4777)) (by [@tomhicks](https://github.com/tomhicks))

### 🐞 Sửa lỗi

- Sửa lỗi rò rỉ bộ nhớ do thiếu việc hủy đăng ký listener sự kiện ([#4824](https://github.com/maplibre/maplibre-gl-js/pull/4824)) (by [@HarelM](https://github.com/HarelM))
- Cải thiện hiệu năng va chạm biểu tượng cho cả hai phép chiếu mercator và globe ([#4778](https://github.com/maplibre/maplibre-gl-js/pull/4778)) (by [@kubapelc](https://github.com/kubapelc))
- Sửa lỗi scale đường không đúng gần các cực trong phép chiếu globe ([#4778](https://github.com/maplibre/maplibre-gl-js/pull/4778)) (by [@kubapelc](https://github.com/kubapelc))
- Sửa lỗi globe tải quá nhiều tile ở một mức zoom cao không cần thiết khi camera đang pitch ([#4778](https://github.com/maplibre/maplibre-gl-js/pull/4778)) (by [@kubapelc](https://github.com/kubapelc))

## 5.0.0-pre.1

### ✨ Tính năng và cải tiến

- Hỗ trợ chế độ globe ([#3963](https://github.com/maplibre/maplibre-gl-js/pull/3963)) (by [@HarelM](https://github.com/HarelM))
- Gộp việc triển khai khí quyển và bầu trời ([#3888](https://github.com/maplibre/maplibre-gl-js/issues/3888)) (by [@Pheonor](https://github.com/Pheonor))
- Thêm tùy chọn hiển thị một bầu khí quyển chân thực khi sử dụng phép chiếu Globe ([#3888](https://github.com/maplibre/maplibre-gl-js/issues/3888)) (by [@Pheonor](https://github.com/Pheonor))
## 4.7.1

### 🐞 Sửa lỗi

- Sửa lỗi circle không hiển thị (render) trên mesa 24.1 với GPU AMD ([#4062](https://github.com/maplibre/maplibre-gl-js/issues/4062)) (by [@cutephoton](https://github.com/cutephoton))
- Sửa hash router cho các url kết thúc bằng dấu hashtag ([#4730](https://github.com/maplibre/maplibre-gl-js/pull/4730)) (by [@birkskyum](https://github.com/birkskyum))
- Thay thế rollup-plugin-sourcemaps bằng rollup-plugin-sourcemaps2 ([#4740](https://github.com/maplibre/maplibre-gl-js/pull/4740)) (by [@birkskyum](https://github.com/birkskyum))

## 4.7.0

### ✨ Tính năng và cải tiến

- Hỗ trợ nhiều layer trong các phương thức `map.on`, `map.once` và `map.off` ([#4570](https://github.com/maplibre/maplibre-gl-js/pull/4570)) (by [@pstaszek](https://github.com/pstaszek))
- Đảm bảo các GeoJSON cluster source phát ra cảnh báo console nếu `maxzoom` nhỏ hơn hoặc bằng `clusterMaxZoom`, vì trong trường hợp này bạn có thể gặp kết quả không mong muốn. ([#4604](https://github.com/maplibre/maplibre-gl-js/pull/4604)) (by [@andrewharvey](https://github.com/andrewharvey))

### 🐞 Sửa lỗi

- Sửa lỗi Heatmap cho terrain 3D ([#4571](https://github.com/maplibre/maplibre-gl-js/pull/4571)) (by [@Samarth1696](https://github.com/Samarth1696))
- Sửa `Map#off` để không xóa listener có (các) layer đã đăng ký bằng `Map#once` ([#4592](https://github.com/maplibre/maplibre-gl-js/pull/4592)) (by [@pstaszek](https://github.com/pstaszek))
- Cải thiện một chút kiểu dữ liệu (types) cho `addSource` và `getSource` ([#4616](https://github.com/maplibre/maplibre-gl-js/pull/4616)) (by [@HarelM](https://github.com/HarelM))
- Sửa màu sắc gần đường chân trời khi bật terrain mà không có sky ([#4607](https://github.com/maplibre/maplibre-gl-js/pull/4607)) (by [@HarelM](https://github.com/HarelM))
- Sửa lỗi `fitBounds` và `cameraForBounds` không hiển thị đúng khi vượt qua kinh tuyến 180° (antimeridian) ([#4620](https://github.com/maplibre/maplibre-gl-js/pull/4620)) (by [@YoelRidgway](https://github.com/YoelRidgway))
- Sửa hiện tượng nhấp nháy trắng (white flickering) khi thay đổi kích thước bản đồ ([#4158](https://github.com/maplibre/maplibre-gl-js/issues/4158)) (by [@pstaszek](https://github.com/pstaszek))
- Sửa lỗi giảm hiệu năng (performance regression) liên quan đến việc đặt symbol (symbol placement) ([#4599](https://github.com/maplibre/maplibre-gl-js/pull/4599)) (by [@kubapelc](https://github.com/kubapelc))
- Sửa lỗi khi clone một instance `Transform` không bao gồm `lngRange`. Điều này gây ra lỗi khiến khi dùng `transformCameraUpdate` làm cho `maxBounds` ngừng hoạt động chỉ đối với giới hạn đông/tây. ([#4625](https://github.com/maplibre/maplibre-gl-js/pull/4625)) (by [@tomhicks](https://github.com/tomhicks))

## 4.6.0

### ✨ Tính năng và cải tiến

- Ưu tiên render glyph cục bộ (local glyph rendering) cho tất cả ký tự CJKV, không chỉ những ký tự thuộc các khối CJK Unified Ideographs, Hiragana, Katakana và Hangul Syllables. ([#4560](https://github.com/maplibre/maplibre-gl-js/pull/4560))) (by [@1ec5](https://github.com/1ec5))

### 🐞 Sửa lỗi

- Sửa bố cục phải-sang-trái (right-to-left) của nhãn (label) chứa ký tự thuộc khối mã Arabic Extended-B. ([#4536](https://github.com/maplibre/maplibre-gl-js/pull/4536)) (by [@1ec5](https://github.com/1ec5))
- Sửa lỗi bản đồ 3D bị đóng băng (freezing) khi camera bị điều chỉnh chạm giới hạn bản đồ. ([#4537](https://github.com/maplibre/maplibre-gl-js/issues/4537)) (by [@larsmaxfield](https://github.com/larsmaxfield))
- Sửa `getStyle()` để trả về một bản sao (clone) nhằm ngăn đối tượng bị thay đổi nội bộ ([#4488](https://github.com/maplibre/maplibre-gl-js/pull/4488)) (by [@gavinr-maps](https://github.com/gavinr-maps))
- Sửa các vấn đề khi đặt sky thành `undefined` ([#4587](https://github.com/maplibre/maplibre-gl-js/pull/4587))) (by [@HarelM](https://github.com/HarelM))

## 4.5.2

### ✨ Tính năng và cải tiến

- Phát ra sự kiện khi tùy chọn cooperative gestures đã ngăn một cử chỉ (gesture). ([#4470](https://github.com/maplibre/maplibre-gl-js/pull/4470)) (by [@tomhicks](https://github.com/tomhicks))
- Chỉ bật anisotropic filtering khi pitch lớn hơn 20 độ để giữ độ sắc nét hình ảnh trên bản đồ phẳng hoặc nghiêng nhẹ. ([#4525](https://github.com/maplibre/maplibre-gl-js/pull/4525)) (by [@e-k-m](https://github.com/e-k-m))

### 🐞 Sửa lỗi

- Sửa lỗi camera có thể di chuyển vào bên trong terrain 3D ([#1542](https://github.com/maplibre/maplibre-gl-js/issues/1542)) (by [@chrneumann](https://github.com/chrneumann))

## 4.5.1

### ✨ Tính năng và cải tiến

- Cho phép cử chỉ pinch trên trackpad vượt qua thiết lập `cooperativeGestures`, giúp hành vi này nhất quán với các bản đồ nhúng khác như Google Maps và Mapbox. ([#4465](https://github.com/maplibre/maplibre-gl-js/pull/4465)) (by [@tomhicks](https://github.com/tomhicks))
- Expose (công khai) các tham số ma trận chiếu (projection matrix) ([#3136](https://github.com/maplibre/maplibre-gl-js/pull/3136)) (by [@birkskyum](https://github.com/birkskyum))
- Thêm tùy chọn định vị marker tại tọa độ subpixel để ngăn marker bị giật (jumping) khi `moveend` ([#4458](https://github.com/maplibre/maplibre-gl-js/pull/4458)) (by [@JeroendeJong](https://github.com/JeroendeJong))

### 🐞 Sửa lỗi

- Sửa hiện tượng giật lag khi zoom bản đồ nhanh ([#4366](https://github.com/maplibre/maplibre-gl-js/pull/4366)) (by [@Codebreaker101](https://github.com/Codebreaker101))
- Sửa truy cập đọc không được bảo vệ (unguarded) tới đối tượng có thể là `undefined` ([#4431](https://github.com/maplibre/maplibre-gl-js/pull/4431)) (by [@birdofpreyru](https://github.com/birdofpreyru))
- Sửa việc xóa chuỗi hash khi bản đồ bị remove ([#4427](https://github.com/maplibre/maplibre-gl-js/pull/4427)) (by [@smellman](https://github.com/smellman))
- Sửa lỗi `GeolocateControl` có thể bị thêm hai lần khi gọi nhanh addControl/removeControl/addControl ([#4454](https://github.com/maplibre/maplibre-gl-js/pull/4454)) (by [@nkundu](https://github.com/nkundu))
- Sửa lỗi abort error của `style.loadURL` bị ghi log khi xóa style ([#4425](https://github.com/maplibre/maplibre-gl-js/pull/4425)) (by [@madoci](https://github.com/madoci))
- Sửa lỗi vector tile không tải được khi html được mở qua "resource://android" (tức thư mục assets) trong GeckoView trên Android ([#4451](https://github.com/maplibre/maplibre-gl-js/issues/4451)) (by [@jwoodwardtfx](https://github.com/jwoodwardtfx))

## 4.5.0

### ✨ Tính năng và cải tiến

- Thêm cài đặt (implementation) sky theo đúng spec ([#3645](https://github.com/maplibre/maplibre-gl-js/pull/3645)) (by [@prozessor13](https://github.com/prozessor13))

### 🐞 Sửa lỗi

- Sửa lỗi (de)serialization của các lớp kế thừa built-in (hiện tại chỉ có AjaxError) hoạt động không đúng trong web_worker_transfer. Đồng thời refactor code web_worker_transfer liên quan và thêm test ([#4024](https://github.com/maplibre/maplibre-gl-js/issues/4024)) (by [@oberhamsi](https://github.com/oberhamsi))

## 4.4.1

### 🐞 Sửa lỗi

- Sửa rò rỉ bộ nhớ (memory leak) của listener `terrain` khi thêm và xóa Marker ([#4284](https://github.com/maplibre/maplibre-gl-js/pull/4284)) (by [@rczobor](https://github.com/rczobor))

## 4.4.0

### ✨ Tính năng và cải tiến

- Cải thiện đường cong hoạt ảnh (animation curve) khi dùng easeTo và flyTo có ràng buộc (constraints) ([#3793](https://github.com/maplibre/maplibre-gl-js/pull/3793)) (by [@sbachinin](https://github.com/sbachinin))
- Đối với extrusion được tô (filled extrusions), tính độ cao (elevation) theo từng polygon ([#3313](https://github.com/maplibre/maplibre-gl-js/issues/3313)) (by [@antonmarsden](https://github.com/antonmarsden))
- Thêm sự kiện cho `GeolocateControl` để cho phép tương tác chi tiết hơn ([#3847](https://github.com/maplibre/maplibre-gl-js/pull/3847)) (by [@MeysamRT76](https://github.com/MeysamRT76))
- Đặt `MapOptions.style` thành tùy chọn (optional) để nhất quán với `Map.setStyle(null)` ([#4151](https://github.com/maplibre/maplibre-gl-js/pull/4151)) (by [@vicb](https://github.com/vicb))
- Dùng Autoprefixer để xử lý các tiền tố nhà cung cấp (vendor prefixes) trong CSS ([#4165](https://github.com/maplibre/maplibre-gl-js/pull/4165)) (by [@coliff](https://github.com/coliff))
- Cho phép cấu hình `aria-label` cho Map, Marker và Popup ([#4147](https://github.com/maplibre/maplibre-gl-js/pull/4147)) (by [@thom4parisot](https://github.com/thom4parisot))
- `<canvas>` của Map chỉ có thể focus khi ở chế độ tương tác (interactive) ([#4147](https://github.com/maplibre/maplibre-gl-js/pull/4147)) (by [@thom4parisot](https://github.com/thom4parisot))
- Header "Accept" được thiết lập trong Request Transformer sẽ không bị ghi đè ([#4210](https://github.com/maplibre/maplibre-gl-js/pull/4210)) (by [@CalRobert](https://github.com/CalRobert))
- ⚠️ Đổi tên `projMatrix` thành `modelViewProjectionMatrix`. Đồng thời đổi tên tương ứng `invProjMatrix`, `alignedProjMatrix` ([#4215](https://github.com/maplibre/maplibre-gl-js/pull/4215)) (by [@birkskyum](https://github.com/birkskyum))
- Phát hành một bản build production không minify (unminified) ([#4265](https://github.com/maplibre/maplibre-gl-js/pull/4265)) (by [@birkskyum](https://github.com/birkskyum))

### 🐞 Sửa lỗi

- ⚠️ Cho phép ngắt dòng trong nhãn (label) trước dấu ngoặc đơn mở ([#4138](https://github.com/maplibre/maplibre-gl-js/pull/4138)) (by [@candux](https://github.com/candux))
- ⚠️ Sửa lỗi bỏ qua ký tự ngắt dòng được nhúng (embedded line breaks) khi `symbol-placement` là `line` hoặc `line-center` ([#4124](https://github.com/maplibre/maplibre-gl-js/pull/4124)) (by [@LostDragonist](https://github.com/LostDragonist))
- Đảm bảo `loseContext` tồn tại trước khi gọi nó ([#4245](https://github.com/maplibre/maplibre-gl-js/pull/4245)) (by [@archmoj](https://github.com/archmoj))
- Cập nhật tiền tố `-ms-high-contrast` đã lỗi thời (deprecated) sang `(forced-colors: active)` và `(prefers-color-scheme: light)` cho phù hợp ([#4250](https://github.com/maplibre/maplibre-gl-js/pull/4250)) (by [@stacy-rendall](https://github.com/stacy-rendall))

## 4.3.2

### 🐞 Sửa lỗi

- Sửa lỗi mức zoom trong sự kiện `moveend` khác với mức zoom hiện tại thực tế ([#4132](https://github.com/maplibre/maplibre-gl-js/pull/4132)) (by [@HarelM](https://github.com/HarelM))

## 4.3.1

### 🐞 Sửa lỗi

- Sửa lỗi trôi (drift) mức zoom có thể xảy ra trong quá trình flyTo và easeTo do logic `freezeElevation`. ([#3878](https://github.com/maplibre/maplibre-gl-js/issues/3878)) (by [@olsen232](https://github.com/olsen232))

## 4.3.0

### ✨ Tính năng và cải tiến

- Thêm phương thức `getData` cho GeoJSON Source để có thể lấy tất cả feature của source ([#4082](https://github.com/maplibre/maplibre-gl-js/pull/4082)) (by [@smellyshovel](https://github.com/smellyshovel))
- Cho phép hiệu ứng chuyển mờ (cross-fading) giữa các lần cập nhật raster tile source ở cùng mức zoom ([#4072](https://github.com/maplibre/maplibre-gl-js/pull/4072)) (by [@wagewarbler](https://github.com/wagewarbler))

### 🐞 Sửa lỗi

- Sửa lỗi `normalizeSpriteURL` trước `transformRequest` ném ra Error với URL tương đối (relative URLs) ([#3897](https://github.com/maplibre/maplibre-gl-js/issues/3897)) (by [@jcary741](https://github.com/jcary741))
- Sửa kiểu trả về (return type) của `map.cameraForBounds` ([#3760](https://github.com/maplibre/maplibre-gl-js/issues/3760)) (by [@keichan34](https://github.com/keichan34))
- Sửa để chạy benchmark với biến môi trường MAPLIBRE_STYLES ([#2122](https://github.com/maplibre/maplibre-gl-js/issues/2122)) (by [@smellman](https://github.com/smellman))
- Sửa lỗi va chạm symbol (symbol collisions) sử dụng collision box không chính xác, đôi khi hoàn toàn sai, khi bản đồ bị nghiêng (pitched) hoặc xoay (rotated) ([#210](https://github.com/maplibre/maplibre-gl-js/issues/210)) (by [@kubapelc](https://github.com/kubapelc))
- Sửa `text-translate` và `icon-translate` hoạt động kỳ lạ và không nhất quán với các thuộc tính `-translate` khác ([#3456](https://github.com/maplibre/maplibre-gl-js/issues/3456)) (by [@kubapelc](https://github.com/kubapelc))
- Sửa chế độ xem debug va chạm symbol (`showCollisionBoxes`) không hiển thị đúng bounding box thực tế dùng cho va chạm và vùng click. Giờ đây các box hiển thị khớp chính xác với collision box thực tế ([#4071](https://github.com/maplibre/maplibre-gl-js/pull/4071)) (by [@kubapelc](https://github.com/kubapelc))
- Sửa collision box của symbol không chính xác đối với symbol có variable-anchor ([#4071](https://github.com/maplibre/maplibre-gl-js/pull/4071)) (by [@kubapelc](https://github.com/kubapelc))
- Sửa collision box của icon sử dụng thuộc tính `text-translate` để dịch chuyển thay vì `icon-translate` đúng ([#4071](https://github.com/maplibre/maplibre-gl-js/pull/4071)) (by [@kubapelc](https://github.com/kubapelc))

## 4.2.0

### ✨ Tính năng và cải tiến

- Cập nhật các phương thức `addClass` và `removeClass` của `Popup` để trả về một instance Popup ([#3975](https://github.com/maplibre/maplibre-gl-js/pull/3975)) (by [@ferdicus](https://github.com/ferdicus))
- Tùy chọn map mới để quyết định có hủy các tile đang chờ (pending) trước đó khi zoom in hay không ([#4051](https://github.com/maplibre/maplibre-gl-js/pull/4051)) (by [@DanielForniessoria-TomTom](https://github.com/DanielForniessoria-TomTom))
- Sprite giờ có thêm giá trị tùy chọn textFitHeight và textFitWidth ([#4019](https://github.com/maplibre/maplibre-gl-js/pull/4019)) (by [@DavidBuerer](https://github.com/DavidBuerer))
- Thêm hỗ trợ cho biểu thức (expression) `distance` ([#4076](https://github.com/maplibre/maplibre-gl-js/pull/4076)) (by [@HarelM](https://github.com/HarelM))

## 4.1.3

### ✨ Tính năng và cải tiến

- Thêm const enum cho actor message để cải thiện khả năng đọc và bảo trì. Trong tsconfig.json, cờ `isolatedModules` được đặt thành `false` để ưu tiên kích thước JS được sinh ra. ([#3879](https://github.com/maplibre/maplibre-gl-js/pull/3879)) (by [@zhangyiatmicrosoft](https://github.com/zhangyiatmicrosoft))

### 🐞 Sửa lỗi

- Sửa các thay đổi pan không mong muốn khác nhau xảy ra ở cuối chuyển động pan, xuất hiện trên màn hình lớn ([#3935](https://github.com/maplibre/maplibre-gl-js/issues/3935)) (by [@olsen232](https://github.com/olsen232))
- Sửa lỗi image source không được đánh dấu là đã tải (loaded) khi xảy ra lỗi ([#3981](https://github.com/maplibre/maplibre-gl-js/pull/3981)) (by [@tzetter](https://github.com/tzetter))
- Sửa các tùy chọn (options) của `ScaleControl` để chúng là optional. ([#4002](https://github.com/maplibre/maplibre-gl-js/pull/4002)) (by [@vicb](https://github.com/vicb))
- Sửa race condition trong `SourceCache` khiến unit test không ổn định. Loại bỏ sự kiện 'visibility' bị phát dư thừa từ class Style. ([#3992](https://github.com/maplibre/maplibre-gl-js/pull/3992)) (by [@zhangyiatmicrosoft](https://github.com/zhangyiatmicrosoft))
- Sửa thuộc tính paint không được cập nhật bởi `setPaintProperty` ([#2651](https://github.com/maplibre/maplibre-gl-js/issues/2651)) (by [@kumilange](https://github.com/kumilange))

## 4.1.2

### ✨ Tính năng và cải tiến

- Ẩn Popup khi Marker cha của nó bị khuất sau terrain ([#3865](https://github.com/maplibre/maplibre-gl-js/pull/3865)) (by [@sbachinin](https://github.com/sbachinin))

### 🐞 Sửa lỗi

- Sửa định nghĩa kiểu (type definition) của `localIdeographFontFamily` ([#3896](https://github.com/maplibre/maplibre-gl-js/pull/3896)) (by [@Kanahiro](https://github.com/Kanahiro))
- Sửa các thay đổi pan không mong muốn ở cuối chuyển động pan ([#3872](https://github.com/maplibre/maplibre-gl-js/issues/3872)) (by [@olsen232](https://github.com/olsen232))
- Sửa sự kiện `close` bị phát ra cho các popup chưa mở ([#3901](https://github.com/maplibre/maplibre-gl-js/pull/3901)) (by [@tzetter](https://github.com/tzetter))

## 4.1.1

### ✨ Tính năng và cải tiến

- Cải thiện đường cong hoạt ảnh khi easeTo và flyTo có ràng buộc ([#3793](https://github.com/maplibre/maplibre-gl-js/pull/3793)) (by [@sbachinin](https://github.com/sbachinin))

### 🐞 Sửa lỗi

- Sửa các thay đổi zoom không mong muốn ở cuối chuyển động pan ([#2094](https://github.com/maplibre/maplibre-gl-js/issues/2094)) (by [@olsen232](https://github.com/olsen232))

## 4.1.0

### ✨ Tính năng và cải tiến

- Thêm tùy chọn định vị popup tại tọa độ subpixel để cho phép hoạt ảnh mượt mà ([#3710](https://github.com/maplibre/maplibre-gl-js/pull/3710)) (by [@ericmagnuson](https://github.com/ericmagnuson))
- Giới hạn pan theo chiều ngang khi `renderWorldCopies` được đặt thành `false` ([#3738](https://github.com/maplibre/maplibre-gl-js/pull/3738)) (by [@sbachinin](https://github.com/sbachinin))

### 🐞 Sửa lỗi

- Sửa lỗi popup xuất hiện xa marker khi marker được di chuyển sang một bản sao (copy) khác của quả cầu (globe) ([#3712](https://github.com/maplibre/maplibre-gl-js/pull/3712)) (by [@sbachinin](https://github.com/sbachinin))
- Đặt màu chữ để đảm bảo độ tương phản trong attribution pill ([#3737](https://github.com/maplibre/maplibre-gl-js/pull/3737)) (by [@Fil](https://github.com/Fil))
- Sửa rò rỉ bộ nhớ trong Worker khi bản đồ bị remove ([#3734](https://github.com/maplibre/maplibre-gl-js/pull/3734)) (by [@pasieronen](https://github.com/pasieronen))
- Sửa lỗi `FullscreenControl` khi MapLibre nằm trong một [ShadowRoot](https://developer.mozilla.org/en-US/docs/Web/API/ShadowRoot) ([#3573](https://github.com/maplibre/maplibre-gl-js/pull/3573)) (by [@dschep](https://github.com/dschep))
- Sửa lỗi giảm hiệu năng của `setRTLTextPlugin` có thể khiến render thêm 1 hoặc 2 frame. ([#3728](https://github.com/maplibre/maplibre-gl-js/pull/3728)) (by [@zhangyiatmicrosoft](https://github.com/zhangyiatmicrosoft))

## 4.0.2

### 🐞 Sửa lỗi

- Sửa `Style.setState` bỏ qua cờ validate ([#3709](https://github.com/maplibre/maplibre-gl-js/issues/3709)) (by [@dsshep](https://github.com/dsshep))
- Sửa lỗi marker bay lệch khi ở gần đường chân trời ([#3704](https://github.com/maplibre/maplibre-gl-js/pull/3704)) (by [@sbachinin](https://github.com/sbachinin))

## 4.0.1

### ✨ Tính năng và cải tiến

- Thêm phương thức `setUrl` cho RasterTileSource để cập nhật động tài nguyên TileJSON hiện có. ([#3700](https://github.com/maplibre/maplibre-gl-js/pull/3700)) (by [@manuelroth](https://github.com/manuelroth))

### 🐞 Sửa lỗi

- Sửa lỗi Marker mất độ mờ (opacity) sau khi thay đổi kích thước cửa sổ (window resize) ([#3656](https://github.com/maplibre/maplibre-gl-js/pull/3656)) (by [@sbachinin](https://github.com/sbachinin))
- Sửa lỗi vector tile không tải được khi html được mở qua "file://" ([#3681](https://github.com/maplibre/maplibre-gl-js/pull/3681)) (by [@sbachinin](https://github.com/sbachinin))

## 4.0.0

### ✨ Tính năng và cải tiến

- ⚠️ Loại bỏ tất cả getter và setter toàn cục (global) khỏi `maplibregl`, nhằm tránh việc phải sử dụng một đối tượng toàn cục và cho phép named exports/imports ([#3601](https://github.com/maplibre/maplibre-gl-js/pull/3601)). Điều này có nghĩa là các phương thức sau đã thay đổi: (by [@HarelM](https://github.com/HarelM))
    - `maplibregl.version` => `getVersion()`
    - `maplibregl.workerCount` => `getWorkerCount()`, `setWorkerCount(...)`
    - `maplibregl.maxParallelImageRequests` => `getMaxParallelImageRequests()`, `setMaxParallelImageRequests(...)`
    - `maplibregl.workerUrl` => `getWorkerUrl()`, `setWorkerUrl(...)`

- ⚠️ Thay đổi để attribution được bật mặc định, thay đổi `MapOptions.attributionControl` thành kiểu mà control đó xử lý, loại bỏ `MapOptions.customAttribution` ([#3618](https://github.com/maplibre/maplibre-gl-js/pull/3618)). Lưu ý: việc hiển thị logo MapLibre không bắt buộc khi sử dụng MapLibre. (by [@HarelM](https://github.com/HarelM))
- ⚠️ Thay đổi cấu hình cooperative gesture và loại bỏ các chuỗi (strings) khỏi đó, ưu tiên sử dụng biến locale ([#3621](https://github.com/maplibre/maplibre-gl-js/pull/3621)) (by [@HarelM](https://github.com/HarelM))
- ⚠️ Thay đổi khóa (key) locale bật/tắt terrain để khớp với phong cách của các khóa khác, cập nhật typings để việc sử dụng locale dễ dàng hơn ([#3621](https://github.com/maplibre/maplibre-gl-js/pull/3621)) (by [@HarelM](https://github.com/HarelM))
- ⚠️ Thêm khả năng import một script trong worker thread và gọi `addProtocol` và `removeProtocol` tại đó ([#3459](https://github.com/maplibre/maplibre-gl-js/pull/3459)) - điều này cũng thay đổi cách `addSourceType` hoạt động, vì giờ bạn cần load script bằng `maplibregl.importScriptInWorkers`. (by [@HarelM](https://github.com/HarelM))
- ⚠️ Thay đổi `addProtocol` thành dựa trên promise (promise-based), không còn dùng callback và có thể hủy (cancelable) ([#3433](https://github.com/maplibre/maplibre-gl-js/pull/3433)) (by [@HarelM](https://github.com/HarelM))
- ⚠️ Di chuyển `addSourceType` thành một phần của đối tượng `maplibregl` toàn cục thay vì thuộc về từng đối tượng map riêng lẻ ([#3420](https://github.com/maplibre/maplibre-gl-js/pull/3420)) (by [@HarelM](https://github.com/HarelM))
- ⚠️ Loại bỏ việc sử dụng callback khỏi `map.loadImage`, tiếp nối thay đổi bên dưới ([#3422](https://github.com/maplibre/maplibre-gl-js/pull/3422)) (by [@HarelM](https://github.com/HarelM))
- ⚠️ Thay đổi các phương thức `getClusterExpansionZoom`, `getClusterChildren`, `getClusterLeaves` của `GeoJSONSource` để trả về `Promise` thay vì dùng callback ([#3421](https://github.com/maplibre/maplibre-gl-js/pull/3421)) (by [@HarelM](https://github.com/HarelM))
- ⚠️ Thay đổi hàm `setRTLTextPlugin` để trả về promise thay vì dùng callback ([#3418](https://github.com/maplibre/maplibre-gl-js/pull/3418)) điều này cũng thay đổi cách xử lý nội bộ code của RTL plugin bằng cách tách code main thread và worker thread. (by [@HarelM](https://github.com/HarelM))
- ⚠️ Loại bỏ các hàm `setCooperativeGestures` và `getCooperativeGestures`, thay bằng handler `cooperativeGestures` hiện có các phương thức `enabled()` hoặc `disabled()` ([#3430](https://github.com/maplibre/maplibre-gl-js/pull/3430)) (by [@HarelM](https://github.com/HarelM))
- ⚠️ Thay đổi cơ chế giao tiếp worker bên dưới từ callback sang promise. Điều này gây ảnh hưởng phá vỡ tương thích (breaking) đến việc triển khai `WorkerSource` tùy chỉnh (custom) và cách nó hoạt động ([#3233](https://github.com/maplibre/maplibre-gl-js/pull/3233)) (by [@HarelM](https://github.com/HarelM))
- ⚠️ Thay đổi interface `Source` để trả về promise thay vì callback ([#3233](https://github.com/maplibre/maplibre-gl-js/pull/3233)) (by [@HarelM](https://github.com/HarelM))
- ⚠️ Thay đổi tất cả các source để dựa trên promise (promise-based). ([#3233](https://github.com/maplibre/maplibre-gl-js/pull/3233)) (by [@HarelM](https://github.com/HarelM))
- ⚠️ Thay đổi phương thức `map.loadImage` để trả về `Promise` thay vì dùng callback ([#3233](https://github.com/maplibre/maplibre-gl-js/pull/3233)) (by [@HarelM](https://github.com/HarelM))
- Thêm tùy chọn "opacity" và phương thức `setOpacity` cho Marker ([#3620](https://github.com/maplibre/maplibre-gl-js/pull/3620)) (by [@sbachinin](https://github.com/sbachinin))
- Tạo một ví dụ mới minh họa cách đặt một scene threejs làm `CustomLayer` phía trên terrain 3D của maplibre ([#3429](https://github.com/maplibre/maplibre-gl-js/pull/3429)) (by [@MichaelLangbein](https://github.com/MichaelLangbein))
- Thay đổi `ImageRequest` để dựa trên `Promise` ([#3233](https://github.com/maplibre/maplibre-gl-js/pull/3233)) (by [@HarelM](https://github.com/HarelM))
- Cải thiện độ chính xác và thêm hiệu ứng chuyển mờ (fade transition) nhẹ nhàng cho các thay đổi opacity của marker ([#3431](https://github.com/maplibre/maplibre-gl-js/pull/3431)) (by [@SnailBones](https://github.com/SnailBones))
- Thêm hỗ trợ terrain trong `setStyle` với phương thức diff ([#3515](https://github.com/maplibre/maplibre-gl-js/pull/3515), [#3463](https://github.com/maplibre/maplibre-gl-js/pull/3463)) (by [@HarelM](https://github.com/HarelM))
- Nâng cấp lên sử dụng Node JS 20 và loại bỏ phụ thuộc vào package `gl` khỏi các test để việc thiết lập môi trường phát triển dễ dàng hơn. ([#3452](https://github.com/maplibre/maplibre-gl-js/pull/3452)) (by [@HarelM](https://github.com/HarelM))

### 🐞 Sửa lỗi

- Sửa zoom bằng con lăn chuột (wheel) để cùng hướng dù ở trên hay dưới đường chân trời ([#3398](https://github.com/maplibre/maplibre-gl-js/issues/3398)) (by [@Pheonor](https://github.com/Pheonor))
- Sửa `_cameraForBoxAndBearing` không fit bounds đúng khi sử dụng viewport camera bất đối xứng và bearing.([#3591](https://github.com/maplibre/maplibre-gl-js/pull/3591)) (by [@fcwheat](https://github.com/fcwheat))
- Sửa lỗi thiếu export kiểu `Map` trong file `d.ts` ([#3564](https://github.com/maplibre/maplibre-gl-js/pull/3564)) (by [@HarelM](https://github.com/HarelM))
- Sửa lỗi sự kiện chuột bị lệch (shifted) sau khi áp dụng css transform scale lên container của bản đồ ([#3437](https://github.com/maplibre/maplibre-gl-js/pull/3437)) (by [@HarelM](https://github.com/HarelM))
- Sửa lỗi marker vẫn trong suốt (transparent) khi tắt terrain ([#3431](https://github.com/maplibre/maplibre-gl-js/pull/3431)) (by [@SnailBones](https://github.com/SnailBones))
- Sửa lỗi nhãn (label) biến mất khi bật terrain ở mức zoom cao ([#3545](https://github.com/maplibre/maplibre-gl-js/pull/3545)) (by [@SnailBones](https://github.com/SnailBones))
- Sửa lỗi zoom ra ngoài quả cầu trung tâm (central globe) khi bật terrain 3D ([#3425](https://github.com/maplibre/maplibre-gl-js/pull/3425)) (by [@sbachinin](https://github.com/sbachinin))
- Sửa lỗi con trỏ chuột (cursor) hiển thị vô thời hạn dưới dạng pointer khi xóa một popup đang bật `trackPointer` ([#3434](https://github.com/maplibre/maplibre-gl-js/pull/3434)) (by [@simondriesen](https://github.com/simondriesen))
- Sửa lỗi hiển thị cooperative gestures khi scroll zoom bị tắt ([#2498](https://github.com/maplibre/maplibre-gl-js/issues/2498)) (by [@HarelM](https://github.com/HarelM))
- Xử lý việc tải các raster tile rỗng (204 No Content) ([#3428](https://github.com/maplibre/maplibre-gl-js/pull/3428)) (by [@petrsloup](https://github.com/petrsloup))
- Sửa một vấn đề bảo mật trong `Actor` liên quan đến tấn công XSS trong postMessage / onmessage ([#3239](https://github.com/maplibre/maplibre-gl-js/issues/3239)) (by [@HarelM](https://github.com/HarelM))

## 4.0.0-pre.6

### ✨ Tính năng và cải tiến

- ⚠️ Thay đổi để attribution được bật mặc định, thay đổi `MapOptions.attributionControl` thành kiểu mà control đó xử lý, loại bỏ `MapOptions.customAttribution` ([#3618](https://github.com/maplibre/maplibre-gl-js/pull/3618)). Lưu ý: việc hiển thị logo MapLibre không bắt buộc khi sử dụng MapLibre. (by [@HarelM](https://github.com/HarelM))
- ⚠️ Thay đổi cấu hình cooperative gesture và loại bỏ các chuỗi (strings) khỏi đó, ưu tiên sử dụng biến locale ([#3621](https://github.com/maplibre/maplibre-gl-js/pull/3621)) (by [@HarelM](https://github.com/HarelM))
- ⚠️ Thay đổi khóa (key) locale bật/tắt terrain để khớp với phong cách của các khóa khác, cập nhật typings để việc sử dụng locale dễ dàng hơn ([#3621](https://github.com/maplibre/maplibre-gl-js/pull/3621)) (by [@HarelM](https://github.com/HarelM))
- Thêm tùy chọn "opacity" và phương thức "setOpacity" cho Marker ([#3620](https://github.com/maplibre/maplibre-gl-js/pull/3620)) (by [@sbachinin](https://github.com/sbachinin))

## 4.0.0-pre.5

### ✨ Tính năng và cải tiến

- ⚠️ Loại bỏ tất cả getter và setter toàn cục (global) khỏi `maplibregl`, nhằm tránh việc phải sử dụng một đối tượng toàn cục và cho phép named exports/imports ([#3601](https://github.com/maplibre/maplibre-gl-js/pull/3601)). Điều này có nghĩa là các phương thức sau đã thay đổi: (by [@HarelM](https://github.com/HarelM))
    - `maplibregl.version` => `getVersion()`
    - `maplibregl.workerCount` => `getWorkerCount()`, `setWorkerCount(...)`
    - `maplibregl.maxParallelImageRequests` => `getMaxParallelImageRequests()`, `setMaxParallelImageRequests(...)`
    - `maplibregl.workerUrl` => `getWorkerUrl()`, `setWorkerUrl(...)`

### 🐞 Sửa lỗi

- Sửa zoom bằng con lăn chuột (wheel) để cùng hướng dù ở trên hay dưới đường chân trời ([#3398](https://github.com/maplibre/maplibre-gl-js/issues/3398)) (by [@Pheonor](https://github.com/Pheonor))
- Sửa `_cameraForBoxAndBearing` không fit bounds đúng khi sử dụng viewport camera bất đối xứng và bearing ([#3591](https://github.com/maplibre/maplibre-gl-js/pull/3591)) (by [@fcwheat](https://github.com/fcwheat))

## 4.0.0-pre.4

### 🐞 Sửa lỗi

- Sửa lỗi thiếu export kiểu `Map` trong file `d.ts` ([#3564](https://github.com/maplibre/maplibre-gl-js/pull/3564)) (by [@HarelM](https://github.com/HarelM))

## 4.0.0-pre.3

### ✨ Tính năng và cải tiến

- ⚠️ Thêm khả năng import một script trong worker thread và gọi `addProtocol` và `removeProtocol` tại đó ([#3459](https://github.com/maplibre/maplibre-gl-js/pull/3459)) - điều này cũng thay đổi cách `addSourceType` hoạt động, vì giờ bạn cần load script bằng `maplibregl.importScriptInWorkers`. (by [@HarelM](https://github.com/HarelM))
- Nâng cấp lên sử dụng Node JS 20 và loại bỏ phụ thuộc vào package `gl` khỏi các test để việc thiết lập môi trường phát triển dễ dàng hơn. ([#3452](https://github.com/maplibre/maplibre-gl-js/pull/3452)) (by [@HarelM](https://github.com/HarelM))
- Cải thiện độ chính xác và thêm hiệu ứng chuyển mờ (fade transition) nhẹ nhàng cho các thay đổi opacity của marker ([#3431](https://github.com/maplibre/maplibre-gl-js/pull/3431)) (by [@SnailBones](https://github.com/SnailBones))
- Thêm hỗ trợ terrain trong `setStyle` với phương thức diff ([#3515](https://github.com/maplibre/maplibre-gl-js/pull/3515), [#3463](https://github.com/maplibre/maplibre-gl-js/pull/3463)) (by [@HarelM](https://github.com/HarelM))

### 🐞 Sửa lỗi

- Sửa lỗi sự kiện chuột bị lệch (shifted) sau khi áp dụng css transform scale lên container của bản đồ ([#3437](https://github.com/maplibre/maplibre-gl-js/pull/3437)) (by [@HarelM](https://github.com/HarelM))
- Sửa lỗi marker vẫn trong suốt (transparent) khi tắt terrain ([#3431](https://github.com/maplibre/maplibre-gl-js/pull/3431)) (by [@SnailBones](https://github.com/SnailBones))
- Sửa lỗi nhãn (label) biến mất khi bật terrain ở mức zoom cao ([#3545](https://github.com/maplibre/maplibre-gl-js/pull/3545)) (by [@SnailBones](https://github.com/SnailBones))

## 4.0.0-pre.2

### ✨ Tính năng và cải tiến

- ⚠️ Thay đổi `addProtocol` thành dựa trên promise (promise-based), không còn dùng callback và có thể hủy (cancelable) ([#3433](https://github.com/maplibre/maplibre-gl-js/pull/3433)) (by [@HarelM](https://github.com/HarelM))
- ⚠️ Di chuyển `addSourceType` thành một phần của đối tượng `maplibregl` toàn cục thay vì thuộc về từng đối tượng map riêng lẻ ([#3420](https://github.com/maplibre/maplibre-gl-js/pull/3420)) (by [@HarelM](https://github.com/HarelM))
- ⚠️ Loại bỏ việc sử dụng callback khỏi `map.loadImage`, tiếp nối thay đổi bên dưới ([#3422](https://github.com/maplibre/maplibre-gl-js/pull/3422)) (by [@HarelM](https://github.com/HarelM))
- ⚠️ Thay đổi các phương thức `getClusterExpansionZoom`, `getClusterChildren`, `getClusterLeaves` của `GeoJSONSource` để trả về `Promise` thay vì dùng callback ([#3421](https://github.com/maplibre/maplibre-gl-js/pull/3421)) (by [@HarelM](https://github.com/HarelM))
- ⚠️ Thay đổi hàm `setRTLTextPlugin` để trả về promise thay vì dùng callback ([#3418](https://github.com/maplibre/maplibre-gl-js/pull/3418)) điều này cũng thay đổi cách xử lý nội bộ code của RTL plugin bằng cách tách code main thread và worker thread. (by [@HarelM](https://github.com/HarelM))
- ⚠️ Loại bỏ các hàm `setCooperativeGestures` và `getCooperativeGestures`, thay bằng handler `cooperativeGestures` hiện có các phương thức `enabled()` hoặc `disabled()` ([#3430](https://github.com/maplibre/maplibre-gl-js/pull/3430)) (by [@HarelM](https://github.com/HarelM))
- Tạo một ví dụ mới minh họa cách đặt một scene threejs làm `CustomLayer` phía trên terrain 3D của maplibre ([#3429](https://github.com/maplibre/maplibre-gl-js/pull/3429)) (by [@MichaelLangbein](https://github.com/MichaelLangbein))

### 🐞 Sửa lỗi

- Sửa lỗi zoom ra ngoài quả cầu trung tâm (central globe) khi bật terrain 3D ([#3425](https://github.com/maplibre/maplibre-gl-js/pull/3425)) (by [@sbachinin](https://github.com/sbachinin))
- Sửa lỗi con trỏ chuột (cursor) hiển thị vô thời hạn dưới dạng pointer khi xóa một popup đang bật `trackPointer` ([#3434](https://github.com/maplibre/maplibre-gl-js/pull/3434)) (by [@simondriesen](https://github.com/simondriesen))
- Sửa lỗi hiển thị cooperative gestures khi scroll zoom bị tắt ([#2498](https://github.com/maplibre/maplibre-gl-js/issues/2498)) (by [@HarelM](https://github.com/HarelM))
- Xử lý việc tải các raster tile rỗng (204 No Content) ([#3428](https://github.com/maplibre/maplibre-gl-js/pull/3428)) (by [@petrsloup](https://github.com/petrsloup))

## 4.0.0-pre.1

### ✨ Tính năng và cải tiến

- Thay đổi `ImageRequest` để dựa trên `Promise` ([#3233](https://github.com/maplibre/maplibre-gl-js/pull/3233)) (by [@HarelM](https://github.com/HarelM))
- ⚠️ Thay đổi cơ chế giao tiếp worker bên dưới từ callback sang promise. Điều này gây ảnh hưởng phá vỡ tương thích (breaking) đến việc triển khai `WorkerSource` tùy chỉnh (custom) và cách nó hoạt động ([#3233](https://github.com/maplibre/maplibre-gl-js/pull/3233)) (by [@HarelM](https://github.com/HarelM))
- ⚠️ Thay đổi interface `Source` để trả về promise thay vì callback ([#3233](https://github.com/maplibre/maplibre-gl-js/pull/3233)) (by [@HarelM](https://github.com/HarelM))
- ⚠️ Thay đổi tất cả các source để dựa trên promise (promise-based). ([#3233](https://github.com/maplibre/maplibre-gl-js/pull/3233)) (by [@HarelM](https://github.com/HarelM))
- ⚠️ Thay đổi phương thức `map.loadImage` để trả về `Promise` thay vì dùng callback ([#3233](https://github.com/maplibre/maplibre-gl-js/pull/3233)) (by [@HarelM](https://github.com/HarelM))

### 🐞 Sửa lỗi

- Sửa một vấn đề bảo mật trong `Actor` liên quan đến tấn công XSS trong postMessage / onmessage ([#3239](https://github.com/maplibre/maplibre-gl-js/issues/3239)) (by [@HarelM](https://github.com/HarelM))

## 3.6.2

### 🐞 Sửa lỗi

- Sửa ví dụ mapbox-gl-draw ([#2601](https://github.com/maplibre/maplibre-gl-js/issues/2601), [#3394](https://github.com/maplibre/maplibre-gl-js/pull/3394)) (by [@dBitech](https://github.com/dBitech))
- Sửa lỗi fill pattern đôi khi hoàn toàn không được render ([#3339](https://github.com/maplibre/maplibre-gl-js/pull/3339)) (by [@CraigglesO](https://github.com/CraigglesO))

## 3.6.1

### 🐞 Sửa lỗi

- Sửa lỗi gọi `_onEaseFrame` bị `undefined` trong `Camera._renderFrameCallback()` khi thực hiện `Camera.jumpTo` trong lúc đang `Camera.easeTo` ([#3332](https://github.com/maplibre/maplibre-gl-js/pull/3332)) (by [@ToHold](https://github.com/ToHold))

## 3.6.0

### ✨ Tính năng và cải tiến

- Thêm `getLayersOrder()` cho Map và Style ([#3279](https://github.com/maplibre/maplibre-gl-js/pull/3279)) (by [@neodescis](https://github.com/neodescis))
- Cập nhật mô tả cho ví dụ `fullscreen` ([#3311](https://github.com/maplibre/maplibre-gl-js/pull/3311)) (by [@jhemmje](https://github.com/jhemmje))

### 🐞 Sửa lỗi

- Sửa lỗi thuộc tính feature null trong resolve_tokens ([#3272](https://github.com/maplibre/maplibre-gl-js/pull/3272)) (by [@mattesCZ](https://github.com/mattesCZ))

## 3.5.2

### ✨ Tính năng và cải tiến

- Chuyển đổi sơ đồ plantuml sang mermaid ([#3217](https://github.com/maplibre/maplibre-gl-js/pull/3217)) (by [@msbarry](https://github.com/msbarry))
- Cải thiện việc chuyển buffer (buffer transfer) trong Safari sau khi Safari sửa một lỗi rò rỉ bộ nhớ ([#3225](https://github.com/maplibre/maplibre-gl-js/pull/3225)) (by [@HarelM](https://github.com/HarelM))
- Minify các export nội bộ để giảm kích thước bundle ([#3216](https://github.com/maplibre/maplibre-gl-js/pull/3216)) (by [@msbarry](https://github.com/msbarry))

### 🐞 Sửa lỗi

- Thêm thuộc tính terrain vào đối tượng style của map ([#3234](https://github.com/maplibre/maplibre-gl-js/pull/3234)) (by [@kumilange](https://github.com/kumilange))
- Sửa lỗi exception bị ném ra từ kiểm tra `isWebGL2` ([#3238](https://github.com/maplibre/maplibre-gl-js/pull/3238)) (by [@msbarry](https://github.com/msbarry))
- Sửa chế độ watch của rollup ([#3270](https://github.com/maplibre/maplibre-gl-js/pull/3270)) (by [@msbarry](https://github.com/msbarry))

## 3.5.1

### 🐞 Sửa lỗi

- Sửa lỗi regression được đưa vào trong 3.5.0, liên quan đến async/await ([#3228](https://github.com/maplibre/maplibre-gl-js/pull/3228)) (by [@birkskyum](https://github.com/birkskyum))

## 3.5.0

### ✨ Tính năng và cải tiến

- Thêm phương thức setTiles cho RasterTileSource để cập nhật động các tile source hiện có. ([#3208](https://github.com/maplibre/maplibre-gl-js/pull/3208)) (by [@wagewarbler](https://github.com/wagewarbler))

## 3.4.1

### ✨ Tính năng và cải tiến

- Glyph được render cục bộ (locally rendered) giờ có độ phân giải gấp đôi (48px), cải thiện đáng kể độ sắc nét của văn bản CJK. ([#2990](https://github.com/maplibre/maplibre-gl-js/issues/2990), [#3006](https://github.com/maplibre/maplibre-gl-js/pull/3006)) (by [@bdon](https://github.com/bdon))

### 🐞 Sửa lỗi

- Sửa lỗi setStyle->style.setState không reset \_serializedLayers ([#3133](https://github.com/maplibre/maplibre-gl-js/pull/3133)). (by [@CraigglesO](https://github.com/CraigglesO))
- Sửa lỗi giải mã (decoding) Raster DEM trong chế độ duyệt web riêng tư (private browsing) của Safari ([#3185](https://github.com/maplibre/maplibre-gl-js/pull/3185)) (by [@msbarry](https://github.com/msbarry))

## 3.4.0

### ✨ Tính năng và cải tiến

- Cải thiện thông báo lỗi khi một tile không thể tải được ([#3130](https://github.com/maplibre/maplibre-gl-js/pull/3130)) (by [@HarelM](https://github.com/HarelM))
- Hỗ trợ mã hóa (encoding) raster-dem tùy chỉnh ([#3087](https://github.com/maplibre/maplibre-gl-js/pull/3087)) (by [@ibesora](https://github.com/ibesora))

### 🐞 Sửa lỗi

- Sửa lỗi ngắt (interrupt) một thao tác scroll zoom khiến lần scroll zoom tiếp theo quay về mức zoom trước đó, bằng cách reset đúng trạng thái (state) của scroll handler ([#2709](https://github.com/maplibre/maplibre-gl-js/issues/2709), [#3051](https://github.com/maplibre/maplibre-gl-js/pull/305)) (by [@HarelM](https://github.com/HarelM))
- Sửa cảnh báo unit test về tên module bị trùng lặp ([#3049](https://github.com/maplibre/maplibre-gl-js/pull/3049)) (by [@miccou](https://github.com/miccou))
- Sửa vị trí marker khi chuyển đổi giữa chế độ xem 2D và 3D ([#2996](https://github.com/maplibre/maplibre-gl-js/pull/2996)) (by [@sebastianoscarlopez](https://github.com/sebastianoscarlopez))
- Sửa lỗi exception bị ném ra khi gỡ bỏ (unset) line-gradient ([#2683](https://github.com/maplibre/maplibre-gl-js/issues/2683)) (by [@tangerine-orange](https://github.com/tangerine-orange))
- Cập nhật các endpoint raster tile trong tài liệu ([#3105](https://github.com/maplibre/maplibre-gl-js/pull/3105)) (by [@RossThorn](https://github.com/RossThorn))
- Tránh hoạt ảnh quán tính (inertia animation) trên Mac khi chế độ reduced motion được bật ([#3068](https://github.com/maplibre/maplibre-gl-js/pull/3068)) (by [@sebastianoscarlopez](https://github.com/sebastianoscarlopez))
- Ví dụ 3d buildings không hoạt động như mong đợi ([#3165](https://github.com/maplibre/maplibre-gl-js/pull/3165)) (by [@sebastianoscarlopez](https://github.com/sebastianoscarlopez))

## 3.3.1

### ✨ Tính năng và cải tiến

- Sao chép LICENSE.txt vào thư mục dist để nó được đưa vào 3rdpartylicenses.txt bởi webpack ([#3021](https://github.com/maplibre/maplibre-gl-js/pull/3021)) (by [@miccou](https://github.com/miccou))

### 🐞 Sửa lỗi

- Sửa kiểu trả về khai báo của `Map.getLayer()` và `Style.getLayer()` thành `StyleLayer | undefined` để khớp với tài liệu ([#2969](https://github.com/maplibre/maplibre-gl-js/pull/2969)) (by [@RoystonS](https://github.com/RoystonS))
- Sửa kiểu của `Map.addLayer()` và `Style.addLayer()` để cho phép thêm một layer có source nhúng (embedded source), khớp với tài liệu ([#2966](https://github.com/maplibre/maplibre-gl-js/pull/2966)) (by [@neodescis](https://github.com/neodescis))
- Throttle việc resize map từ ResizeObserver để giảm hiện tượng nhấp nháy (flicker) ([#2986](https://github.com/maplibre/maplibre-gl-js/pull/2986)) (by [@neodescis](https://github.com/neodescis))
- Sửa hàm `Map.setTerrain(options: TerrainSpecification): Map` thành `Map.setTerrain(options: TerrainSpecification | null): Map` theo đúng API spec ([#2993](https://github.com/maplibre/maplibre-gl-js/pull/2993)) (by [@CraigglesO](https://github.com/CraigglesO))
- Sửa hàm `Map.getTerrain(): TerrainSpecification` thành `Map.getTerrain(): TerrainSpecification | null` để nhất quán với hàm setTerrain ([#3020](https://github.com/maplibre/maplibre-gl-js/pull/3020)) (by [@neodescis](https://github.com/neodescis))

## 3.3.0

### ✨ Tính năng và cải tiến

- Thêm hỗ trợ cho thuộc tính symbol style layer [`text-variable-anchor-offset`](https://maplibre.org/maplibre-style-spec/layers/#layout-symbol-text-variable-anchor-offset) ([#2914](https://github.com/maplibre/maplibre-gl-js/pull/2914)) (by [@drwestco](https://github.com/drwestco))

## 3.2.2

### ✨ Tính năng và cải tiến

- Thêm tham số `cache` vào [`RequestParameters`](https://maplibre.org/maplibre-gl-js/docs/API/types/maplibregl.RequestParameters/) ([#2910](https://github.com/maplibre/maplibre-gl-js/pull/2910)) (by [@marucjmar](https://github.com/marucjmar))
- Loại bỏ một số class khỏi tài liệu để định nghĩa rõ hơn public API ([#2945](https://github.com/maplibre/maplibre-gl-js/pull/2945)) (by [@HarelM](https://github.com/HarelM))

### 🐞 Sửa lỗi

- Kiểm tra `ImageBitmap` đúng cách ([#2942](https://github.com/maplibre/maplibre-gl-js/pull/2942), [#2940](https://github.com/maplibre/maplibre-gl-js/issues/2940)) (by [@HarelM](https://github.com/HarelM))
- `VectorTileWorkerSource`: sửa lỗi reload khi phân tích (parse) load ban đầu không truyền rawTileData và meta. ([#2941](https://github.com/maplibre/maplibre-gl-js/pull/2941)) (by [@ambientlight](https://github.com/ambientlight))

## 3.2.1

### ✨ Tính năng và cải tiến

- Loại bỏ màn hình cooperative gesture khỏi accessibility tree vì trình đọc màn hình (screenreader) không thể tương tác với bản đồ bằng cử chỉ ([#2857](https://github.com/maplibre/maplibre-gl-js/pull/2857)) (by [@manuelroth](https://github.com/manuelroth))
- Thêm ví dụ `cooperated gestures` vào tài liệu.([#2860](https://github.com/maplibre/maplibre-gl-js/pull/2860)) (by [@visitskyworld](https://github.com/visitskyworld))

### 🐞 Sửa lỗi

- Sửa lỗi tính toán khoảng cách trường nhìn (distance field of view) không chính xác đối với độ cao âm (negative elevation), bằng cách lưu độ cao tối thiểu của tile đang hiển thị ([#1655](https://github.com/maplibre/maplibre-gl-js/issues/1655), [#2858](https://github.com/maplibre/maplibre-gl-js/pull/2858)) (by [@HarelM](https://github.com/HarelM))
- Sửa lỗi reloadCallback không được gọi trong `VectorTileWorkerSource.reloadTile` ([#1874](https://github.com/maplibre/maplibre-gl-js/pull/1874)) (by [@ambientlight](https://github.com/ambientlight))
- Không vẽ các pixel halo bên dưới pixel chữ (text pixels) ([#2897](https://github.com/maplibre/maplibre-gl-js/pull/2897)) (by [@ChrisLoer](https://github.com/ChrisLoer))
- Sửa lỗi `RasterDEMTileSource` serialize các option không đúng ([#2895](https://github.com/maplibre/maplibre-gl-js/pull/2895)) (by [@neodescis](https://github.com/neodescis))
- Loại bỏ node và jest khỏi việc kiểm tra kiểu (type checking) của dist, sửa lỗi typing của map event và các vấn đề typing khác ([#2898](https://github.com/maplibre/maplibre-gl-js/pull/2898)) (by [@neodescis](https://github.com/neodescis))

## 3.2.0

### ✨ Tính năng và cải tiến

- Đổi tất cả export nội bộ thành named export([#2711](https://github.com/maplibre/maplibre-gl-js/pull/2711)) (by [@HarelM](https://github.com/HarelM))
- Việc sinh (generate) tài liệu giờ đã là một phần của repo này([#2733](https://github.com/maplibre/maplibre-gl-js/pull/2733)) (by [@HarelM](https://github.com/HarelM))
- Thêm tùy chọn `className` cho constructor của Marker ([#2729](https://github.com/maplibre/maplibre-gl-js/pull/2729)) (by [@marexandre](https://github.com/marexandre))
- Vẽ lại (redraw) bản đồ ngay lập tức sau khi đặt pixel ratio ([#2674](https://github.com/maplibre/maplibre-gl-js/pull/2674)) (by [@handymenny](https://github.com/handymenny))
- Thêm tùy chọn maxCanvasSize để giới hạn kích thước canvas. Điều này có thể ngăn việc chạm giới hạn GL và giảm tải cho thiết bị. Giá trị mặc định là [4096, 4096]. ([#2674](https://github.com/maplibre/maplibre-gl-js/pull/2674)) (by [@handymenny](https://github.com/handymenny))
- Giảm maxCanvasSize khi chạm giới hạn GL để tránh méo hình (distortions) ([#2674](https://github.com/maplibre/maplibre-gl-js/pull/2674)) (by [@handymenny](https://github.com/handymenny))
- Viết lại toàn bộ comment code theo TSDocs, giới thiệu hệ thống tài liệu mới và chuyển các ví dụ vào repo này để có tùy chọn debug tốt hơn ([#2756](https://github.com/maplibre/maplibre-gl-js/pull/2756)) (by [@HarelM](https://github.com/HarelM))
- ⚠️ Loại bỏ tham số constructor của `Marker` chưa được ghi trong tài liệu ([#2756](https://github.com/maplibre/maplibre-gl-js/pull/2756)) (by [@HarelM](https://github.com/HarelM))
- Cập nhật ví dụ `check-for-support` ([#2859](https://github.com/maplibre/maplibre-gl-js/pull/2859)) (by [@visitskyworld](https://github.com/visitskyworld))

### 🐞 Sửa lỗi

- Trả về undefined thay vì ném lỗi từ `Style.serialize()` khi style chưa được tải xong ([#2712](https://github.com/maplibre/maplibre-gl-js/pull/2712)) (by [@ChrisLoer](https://github.com/ChrisLoer))
- Không ném exception từ `checkMaxAngle` khi một nhãn (label) có độ dài 0 nằm ở đoạn cuối cùng của một đường (line) ([#2710](https://github.com/maplibre/maplibre-gl-js/pull/2710)) (by [@ChrisLoer](https://github.com/ChrisLoer))
- Sửa việc phát hiện cử chỉ zoom `tap then drag` để hủy khi hai lần tap cách xa nhau ([#2673](https://github.com/maplibre/maplibre-gl-js/pull/2673)) (by [@mz8i](https://github.com/mz8i))
- Sửa lỗi regression - cập nhật pixel ratio khi devicePixelRatio thay đổi, khôi phục lại hành vi của v1.x ([#2706](https://github.com/maplibre/maplibre-gl-js/pull/2706)) (by [@handymenny](https://github.com/handymenny))
- Sửa lỗi tính toán độ cao (elevation) không chính xác ([#2772](https://github.com/maplibre/maplibre-gl-js/pull/2772)) (by [@rotu](https://github.com/rotu))

## 3.1.0

### ✨ Tính năng và cải tiến

- Expose map options.maxTileCacheZoomLevels để kiểm soát tile cache tốt hơn ([#2581](https://github.com/maplibre/maplibre-gl-js/pull/2581)) (by [@pramilk](https://github.com/pramilk))

### 🐞 Sửa lỗi

- Sửa lỗi regression - Thêm cơ chế dự phòng (fallback) webgl1 để hỗ trợ người dùng không có webgl2 ([#2653](https://github.com/maplibre/maplibre-gl-js/issues/2653)) (by [@birkskyum](https://github.com/birkskyum))

## 3.0.1

### ✨ Tính năng và cải tiến

- Cập nhật shader lên GLSL ES 3.0 ([#2599](https://github.com/maplibre/maplibre-gl-js/pull/2599)) (by [@birkskyum](https://github.com/birkskyum))

### 🐞 Sửa lỗi

- Sửa kiểu `RequestTransformFunction` để trả về RequestParameters hoặc undefined ([#2586](https://github.com/maplibre/maplibre-gl-js/pull/2586)) (by [@nreese](https://github.com/nreese))
- Load extension WebGL2 `EXT_color_buffer_float` để sửa lỗi heatmap trên firefox ([#2595](https://github.com/maplibre/maplibre-gl-js/pull/2595)) (by [@birkskyum](https://github.com/birkskyum))

## 3.0.0

## Tính năng và cải tiến mới

- Thêm callback `transformCameraUpdate` vào tùy chọn `Map` ([#2535](https://github.com/maplibre/maplibre-gl-js/pull/2535)) (by [@Pessimistress](https://github.com/Pessimistress))
- Nâng cấp (bump) KDBush và supercluster để cải thiện hiệu quả sử dụng bộ nhớ ([#2522](https://github.com/maplibre/maplibre-gl-js/pull/2522)) (by [@birkskyum](https://github.com/birkskyum))
- Cải thiện hiệu năng bằng cách sử dụng HTMLImageElement để tải ảnh raster source khi refreshExpiredTiles là false ([#2126](https://github.com/maplibre/maplibre-gl-js/pull/2126)) (by [@pramilk](https://github.com/pramilk))
- Đặt fetchPriority cho HTMLImageElement để cải thiện các tình huống dùng nhiều raster ([#2459](https://github.com/maplibre/maplibre-gl-js/pull/2459)) (by [@pramilk](https://github.com/pramilk))
- Giảm số lần gọi render lúc tải ban đầu. Không cần thử render trước khi style được tải xong. ([#2464](https://github.com/maplibre/maplibre-gl-js/pull/2464)) (by [@pramilk](https://github.com/pramilk))
- Lazy load các thuộc tính style mặc định theo yêu cầu để cải thiện hiệu năng tải và giảm sử dụng bộ nhớ. ([#2476](https://github.com/maplibre/maplibre-gl-js/pull/2476)) (by [@pramilk](https://github.com/pramilk))
- Thêm queryTerrainElevation cho phép lấy độ cao terrain tính bằng mét tại một điểm cụ thể ([#2264](https://github.com/maplibre/maplibre-gl-js/pull/2264)) (by [@manhcuongincusar1](https://github.com/manhcuongincusar1))
- Cải thiện hiệu năng bằng cách gửi các style layer tới worker thread trước khi xử lý trên main thread để cho phép xử lý song song ([#2131](https://github.com/maplibre/maplibre-gl-js/pull/2131)) (by [@pramilk](https://github.com/pramilk))
- Thêm Map.getImage() để lấy lại các ảnh đã được tải trước đó. ([#2168](https://github.com/maplibre/maplibre-gl-js/pull/2168)) (by [@ZeLonewolf](https://github.com/ZeLonewolf))
- Thêm phương thức để bật/tắt cooperative gestures ([#2152](https://github.com/maplibre/maplibre-gl-js/pull/2152)) (by [@kevinschaul](https://github.com/kevinschaul))
- Cập nhật CONTRIBUTING.md với chi tiết về cách thiết lập trên Mac M1 ([#2196](https://github.com/maplibre/maplibre-gl-js/pull/2196)) (by [@llambanna](https://github.com/llambanna))
- Cập nhật kiểu mặc định của originalEvent trong MapLibreEvent thành `unknown` ([#2243](https://github.com/maplibre/maplibre-gl-js/pull/2243)) (by [@neodescis](https://github.com/neodescis))
- Cải thiện hiệu năng khi ép buộc đặt symbol đầy đủ (full symbol placement) bằng cách bỏ qua nhanh (short-circuit) các kiểm tra tạm dừng (pause checks) ([#2241](https://github.com/maplibre/maplibre-gl-js/pull/2241)) (by [@schlosna](https://github.com/schlosna))
- Thêm cảnh báo `warnonce` khi source của terrain và hillshade giống nhau ([#2298](https://github.com/maplibre/maplibre-gl-js/pull/2298)) (by [@tempranova](https://github.com/tempranova))
- Loại bỏ một cảnh báo deprecation bằng cách xóa một texture rỗng không còn được sử dụng trong codebase ([#2299](https://github.com/maplibre/maplibre-gl-js/pull/2299)) (by [@IvanSanchez](https://github.com/IvanSanchez))
- Cải thiện hiệu năng tải ban đầu bằng cách chỉ serialize layer khi cần thiết (lazy serializing). ([#2306](https://github.com/maplibre/maplibre-gl-js/pull/2306)) (by [@zhangyiatmicrosoft](https://github.com/zhangyiatmicrosoft))
- Thêm tùy chọn validateStyle cho Map để cho phép tắt việc validate style nhằm tăng hiệu năng trong môi trường production. ([#2390](https://github.com/maplibre/maplibre-gl-js/pull/2390)) (by [@pramilk](https://github.com/pramilk))
- Thêm `setClusterOptions` để cập nhật thuộc tính cluster của các source đã thêm: sửa các vấn đề ([#429](https://github.com/maplibre/maplibre-gl-js/issues/429)) và ([#1384](https://github.com/maplibre/maplibre-gl-js/issues/1384)) (by [@IhsenBen](https://github.com/IhsenBen))
- Thêm kiểu (types) cho `workerOptions` và `_options` trong `geojson_source.ts` ([#1998](https://github.com/maplibre/maplibre-gl-js/pull/1998)) (by [@IhsenBen](https://github.com/IhsenBen))
- Thêm sự kiện fullscreenstart, fullscreenend cho FullscreenControl ([#2128](https://github.com/maplibre/maplibre-gl-js/pull/2128)) (by [@kevinschaul](https://github.com/kevinschaul))
- Throttle hàng đợi (queue) request ảnh trong khi bản đồ đang di chuyển để cải thiện hiệu năng ([#2097](https://github.com/maplibre/maplibre-gl-js/pull/2097)) (by [@zhangyiatmicrosoft](https://github.com/zhangyiatmicrosoft))
- Thêm hỗ trợ khai báo nhiều `sprite` trong một file style ([#1805](https://github.com/maplibre/maplibre-gl-js/pull/1805)) (by [@smellyshovel](https://github.com/smellyshovel))
- Trích xuất ảnh sprite theo yêu cầu (on demand) để giảm sử dụng bộ nhớ và cải thiện hiệu năng bằng cách giảm số lần gọi getImageData ([#1809](https://github.com/maplibre/maplibre-gl-js/pull/1809)) (by [@pramilk](https://github.com/pramilk))
- Thêm kiểu `QueryRenderedFeaturesOptions` cho cả hai tham số trong queryRenderedFeatures ở map.ts ([#1900](https://github.com/maplibre/maplibre-gl-js/issues/1900)) (by [@beharguy](https://github.com/beharguy))
- NavigationControlOptions giờ là tùy chọn (optional) khi tạo một instance của NavigationControl ([#1754](https://github.com/maplibre/maplibre-gl-js/issues/1754)) (by [@guimochila](https://github.com/guimochila))
- Lắng nghe sự kiện webglcontextcreationerror và cung cấp thông tin debug chi tiết khi thất bại ([#1715](https://github.com/maplibre/maplibre-gl-js/pull/1715)) (by [@zhangyiatmicrosoft](https://github.com/zhangyiatmicrosoft))
- Đảm bảo overlay `cooperativeGestures` luôn nằm "trên cùng" (z-index) so với các feature của bản đồ ([#1753](https://github.com/maplibre/maplibre-gl-js/pull/1753)) (by [@blyme](https://github.com/blyme))
- Sử dụng gợi ý (hint) `willReadFrequently` để tối ưu việc sử dụng canvas 2D và loại bỏ cảnh báo ([#1808](https://github.com/maplibre/maplibre-gl-js/pull/1808)) (by [@kircher1](https://github.com/kircher1))
- Tăng tốc chỉ mục symbol xuyên tile (cross tile symbol index) trong một số trường hợp nhất định ([#1755](https://github.com/maplibre/maplibre-gl-js/pull/1755)) (by [@mfedderly](https://github.com/mfedderly))
- Cải thiện tốc độ render trong các cảnh có nhiều icon và nhãn biểu tượng (symbolic icons) va chạm nhau ([#1757](https://github.com/maplibre/maplibre-gl-js/pull/1757)) (by [@AdamS108](https://github.com/AdamS108))
- Cho phép hủy (cancelable) request của ImageSource ([#1802](https://github.com/maplibre/maplibre-gl-js/pull/1802)) (by [@blinkzz](https://github.com/blinkzz))
- Throttle hàng đợi (queue) request ảnh trong khi bản đồ đang di chuyển để cải thiện hiệu năng ([#2097](https://github.com/maplibre/maplibre-gl-js/pull/2097)) (by [@zhangyiatmicrosoft](https://github.com/zhangyiatmicrosoft))
- Trả về một promise từ phương thức `once` để dễ dàng sử dụng async/await hơn trong trường hợp này ([#1690](https://github.com/maplibre/maplibre-gl-js/pull/1690)) (by [@HarelM](https://github.com/HarelM))
- Thêm chế độ fullscreen giả (pseudo CSS fullscreen) làm phương án dự phòng cho iPhone ([#1678](https://github.com/maplibre/maplibre-gl-js/pull/1678)) (by [@caspg](https://github.com/caspg))
- Thêm `updateData` cho `GeoJSONSource` cho phép cập nhật dữ liệu từng phần (partial data updates) ([#1605](https://github.com/maplibre/maplibre-gl-js/pull/1605)) (by [@mfedderly](https://github.com/mfedderly))
- Thêm một RenderPool để render tile lên texture cho chế độ 3D ([#1671](https://github.com/maplibre/maplibre-gl-js/pull/1671)) (by [@prozessor13](https://github.com/prozessor13))
- Thêm map.getCameraTargetElevation() ([#1558](https://github.com/maplibre/maplibre-gl-js/pull/1558)) (by [@birkskyum](https://github.com/birkskyum))
- Thêm `freezeElevation` vào `AnimationOptions` để cho phép chuyển động camera mượt mà trong chế độ 3D ([#1514](https://github.com/maplibre/maplibre-gl-js/pull/1514), [#1492](https://github.com/maplibre/maplibre-gl-js/issues/1492)) (by [@prozessor13](https://github.com/prozessor13))
- Thêm tùy chọn transformStyle cho map.setStyle ([#1632](https://github.com/maplibre/maplibre-gl-js/pull/1632)) (by [@ambientlight](https://github.com/ambientlight))

## Các thay đổi có khả năng phá vỡ tương thích

Hầu hết các thay đổi này sẽ không ảnh hưởng đến code của bạn, nhưng hãy đọc kỹ danh sách để đánh giá xem có cần migrate hay không.

- ⚠️ Hủy các request tile chưa tải xong khi zoom in qua nhiều mức zoom. Trước đây các request này không bị hủy. ([#2377](https://github.com/maplibre/maplibre-gl-js/pull/2377)) (by [@pramilk](https://github.com/pramilk))
- ⚠️ Resize bản đồ khi phần tử container bị thay đổi kích thước. Các sự kiện liên quan tới "resize" giờ có dữ liệu đi kèm khác trước ([#2157](https://github.com/maplibre/maplibre-gl-js/pull/2157), [#2551](https://github.com/maplibre/maplibre-gl-js/issues/2551)). Trước đây trường originalEvent là nguyên nhân của thay đổi này, ví dụ nó có thể là một sự kiện `resize` từ trình duyệt. Giờ đây nó là `ResizeObserverEntry`, xem thêm [tại đây](https://developer.mozilla.org/en-US/docs/web/api/resizeobserverentry). (by [@HarelM](https://github.com/HarelM))
- ⚠️ Cải thiện việc render các khu vực dưới mực nước biển, và loại bỏ giải pháp tạm (workaround) elevationOffset ([#1578](https://github.com/maplibre/maplibre-gl-js/pull/1578)) (by [@birkskyum](https://github.com/birkskyum))
- ⚠️ Loại bỏ hỗ trợ màu css `hsl` ở định dạng không tuân theo đặc tả CSS Color. Các màu định nghĩa theo định dạng `hsl(110, 0.7, 0.055)` sẽ không còn hoạt động, thay vào đó nên dùng định dạng phần trăm `hsl(110, 70%, 5.5%)`. ([#2376](https://github.com/maplibre/maplibre-gl-js/pull/2376)) (by [@kajkal](https://github.com/kajkal))
- ⚠️ Di chuyển đối tượng terrain từ style.terrain sang map.terrain ([#1628](https://github.com/maplibre/maplibre-gl-js/pull/1628)) (by [@HarelM](https://github.com/HarelM))
- ⚠️ Loại bỏ các class css `mapboxgl-` đã lỗi thời (dùng `maplibregl-` thay thế) ([#1575](https://github.com/maplibre/maplibre-gl-js/pull/1575)) (by [@birkskyum](https://github.com/birkskyum))
- ⚠️ Chuyển đổi hoàn toàn từ WebGL1 sang WebGL2 ([hỗ trợ trình duyệt](https://caniuse.com/?search=webgl2)) ([#2512](https://github.com/maplibre/maplibre-gl-js/pull/2512), [#1891](https://github.com/maplibre/maplibre-gl-js/pull/1891)) (by [@birkskyum](https://github.com/birkskyum))
- ⚠️ `LngLat.toBounds()` được thay thế bằng phương thức tĩnh (static) `LngLatBounds.fromLngLat()` ([#2188](https://github.com/maplibre/maplibre-gl-js/pull/2188)) (by [@zhangyiatmicrosoft](https://github.com/zhangyiatmicrosoft))
- ⚠️ Đặt geojson data source thành trường bắt buộc (required) để khớp với tài liệu ([#1396](https://github.com/maplibre/maplibre-gl-js/issues/1396)) (by [@HarelM](https://github.com/HarelM))
- ⚠️ Cải thiện hiệu năng tải ban đầu của control bằng cách ép fadeDuration về 0 cho tới sự kiện idle đầu tiên ([#2447](https://github.com/maplibre/maplibre-gl-js/pull/2447)) (by [@pramilk](https://github.com/pramilk))
- ⚠️ Loại bỏ package "mapbox-gl-supported" khỏi API. Nếu cần, vui lòng tham chiếu trực tiếp đến nó thay vì thông qua MapLibre. ([#2451](https://github.com/maplibre/maplibre-gl-js/pull/2451)) (by [@zhangyiatmicrosoft](https://github.com/zhangyiatmicrosoft))
- ⚠️ Cải thiện hiệu năng control bằng cách giới hạn số lượng worker tối đa là 1, ngoại trừ trình duyệt Safari. ([#2354](https://github.com/maplibre/maplibre-gl-js/pull/2354)) (by [@pramilk](https://github.com/pramilk))

## Sửa lỗi

- Sửa lỗi nét đứt (dash) không chính xác trên các đường chéo (diagonal lines) với vector source ở một số mức zoom. ([#2479](https://github.com/maplibre/maplibre-gl-js/pull/2479)) (by [@newlinefu](https://github.com/newlinefu))
- Sửa event.isSourceLoaded để phản ánh đúng trạng thái tải của source cho sự kiện sourcedata ([#2543](https://github.com/maplibre/maplibre-gl-js/pull/2543)) (by [@ambientlight](https://github.com/ambientlight))
- Sửa lỗi chồng lấn (overlapping) các phần của tòa nhà 3D khi kích hoạt Terrain 3D ([#2513](https://github.com/maplibre/maplibre-gl-js/issues/2513)) (by [@zstadler](https://github.com/zstadler))
- Hiển thị các tòa nhà 3D nằm dưới mực nước biển khi kích hoạt Terrain 3D ([#2544](https://github.com/maplibre/maplibre-gl-js/issues/2544)) (by [@zstadler](https://github.com/zstadler))
- Sửa `LngLatBounds.extend()` để xử lý đúng tọa độ dạng `{ lng: number, lat: number }`. ([#2425](https://github.com/maplibre/maplibre-gl-js/pull/2425)) (by [@buffalom](https://github.com/buffalom))
- Sửa lỗi vòng tròn độ chính xác (accuracy-circle) trong geolocate control bị thay đổi kích thước ngẫu nhiên. ([#2450](https://github.com/maplibre/maplibre-gl-js/pull/2450)) (by [@Philip2809](https://github.com/Philip2809))
- Sửa kiểu của thuộc tính `features` trên `MapLayerMouseEvent` và `MapLayerTouchEvent` thành `MapGeoJSONFeature[]` thay vì `GeoJSON.Feature[]` ([#2244](https://github.com/maplibre/maplibre-gl-js/pull/2244)) (by [@parkerziegler](https://github.com/parkerziegler))
- Sửa lỗi GeolocateControl nếu bị xóa (remove) quá nhanh ([#2391](https://github.com/maplibre/maplibre-gl-js/pull/2391)) (by [@Pessimistress](https://github.com/Pessimistress))
- Sửa lỗi khi unload sprite sheet khi dùng `setStyle(style, {diff:true})` ([#2146](https://github.com/maplibre/maplibre-gl-js/pull/2146)) (by [@jcary741](https://github.com/jcary741))
- Sửa lỗi wrap tọa độ trong getTerrain khi fitBounds vượt qua đường đổi ngày (AM) ([#2155](https://github.com/maplibre/maplibre-gl-js/pull/2155)) (by [@llambanna](https://github.com/llambanna))
- Sửa kiểu trả về của phương thức toArray của LngLat thành [number,number] ([#2233](https://github.com/maplibre/maplibre-gl-js/issues/2233)) (by [@maxdacruz](https://github.com/maxdacruz))
- Sửa việc xử lý text-offset khi symbol-placement: line ([#2170](https://github.com/maplibre/maplibre-gl-js/issues/2170) và [#2171](https://github.com/maplibre/maplibre-gl-js/issues/2171)) (by [@ChrisLoer](https://github.com/ChrisLoer))
- Sửa lỗi kiểm tra quyền (permissions) của geolocate control thất bại trên web view iOS16 bằng cách dự phòng (fallback) sang window.navigator.geolocation ([#2359](https://github.com/maplibre/maplibre-gl-js/pull/2359)) (by [@HarelM](https://github.com/HarelM))
- Ngăn việc reload không cần thiết các raster source khi RTL Text Plugin được tải ([#2380](https://github.com/maplibre/maplibre-gl-js/issues/2380)) (by [@ChrisLoer](https://github.com/ChrisLoer))
- Sửa việc xử lý hàm callback AddProtocol khi trả về một HTMLImageElement ([#2393](https://github.com/maplibre/maplibre-gl-js/pull/2393)) (by [@pramilk](https://github.com/pramilk))
- Sửa lỗi raster tile bị giữ lại (retained) khi raster-fade-duration bằng 0 ([#2445](https://github.com/maplibre/maplibre-gl-js/issues/2445), [#2501](https://github.com/maplibre/maplibre-gl-js/issues/2501)) (by [@ibesora](https://github.com/ibesora))
- Sửa lỗi worker bị chấm dứt (terminated) khi đặt style mới ([#2123](https://github.com/maplibre/maplibre-gl-js/pull/2123)) (by [@pramilk](https://github.com/pramilk))
- Thay đổi cách phát hiện phím meta cho cooperative gestures ([#2152](https://github.com/maplibre/maplibre-gl-js/pull/2152)) (by [@kevinschaul](https://github.com/kevinschaul))
- Sửa lỗi worker bị chấm dứt (terminated) khi đặt style mới ([#2123](https://github.com/maplibre/maplibre-gl-js/pull/2123)) (by [@pramilk](https://github.com/pramilk))
- Sửa lỗi ([#1024](https://github.com/maplibre/maplibre-gl-js/issues/1024)) - tâm zoom (zoom center) không nằm dưới con trỏ chuột khi bật terrain (by [@HarelM](https://github.com/HarelM))
- Sửa lỗi khi chạy các script bin của style-spec và thêm phần trợ giúp (help) còn thiếu. Loại bỏ script không cần thiết 'gl-style-composite'. ([#1971](https://github.com/maplibre/maplibre-gl-js/pull/1971)) (by [@acalcutt](https://github.com/acalcutt))
- Sửa kiểu của biểu thức (expression) slice ([#1886](https://github.com/maplibre/maplibre-gl-js/issues/1886)) (by [@kevinschaul](https://github.com/kevinschaul))
- Loại bỏ phụ thuộc vào `@rollup/plugin-json`, vốn xung đột với `rollup-plugin-import-assert` ([#1894](https://github.com/maplibre/maplibre-gl-js/pull/1894)) (by [@rotu](https://github.com/rotu))
- Loại bỏ phụ thuộc vào `@mapbox/gazetteer` vốn gây ra một số cảnh báo build ([#1757](https://github.com/maplibre/maplibre-gl-js/pull/1757) [#1898](https://github.com/maplibre/maplibre-gl-js/pull/1898)) (by [@AdamS108](https://github.com/AdamS108))
- Sửa lỗi `getElevation()` gây ra lỗi không được bắt (uncaught error) ([#1650](https://github.com/maplibre/maplibre-gl-js/issues/1650)). (by [@zbigniewmatysek-tomtom](https://github.com/zbigniewmatysek-tomtom))
- Sửa việc chạy benchmark ở chế độ headless, đặc biệt trên máy ảo (VM) ([#1732](https://github.com/maplibre/maplibre-gl-js/pull/1732)) (by [@zhangyiatmicrosoft](https://github.com/zhangyiatmicrosoft))
- sửa lỗi [#860](https://github.com/maplibre/maplibre-gl-js/issues/860) fill-pattern với pixelRatio > 1 giờ được chuyển đổi đúng tại runtime. ([#1765](https://github.com/maplibre/maplibre-gl-js/pull/1765)) (by [@zhangyiatmicrosoft](https://github.com/zhangyiatmicrosoft))
- Sửa lỗi exception bị ném ra khi gọi map.setStyle với tùy chọn transformStyle trong khi map được khởi tạo mà không có style ban đầu. ([#1824](https://github.com/maplibre/maplibre-gl-js/pull/1824)) (by [@ambientlight](https://github.com/ambientlight))
- Sửa hành vi của nút la bàn (compass button) trên thiết bị cảm ứng. ([#1852](https://github.com/maplibre/maplibre-gl-js/pull/1852)) (by [@VehpuS](https://github.com/VehpuS))
- Sửa lỗi GeoJSONSource có vẻ như không bao giờ tải xong khi gọi phương thức setData ngay sau khi thêm nó vào Map, do không phát ra sự kiện data loại metadata ([#1693](https://github.com/maplibre/maplibre-gl-js/issues/1693)) (by [@vanilla-lake](https://github.com/vanilla-lake))
- Sửa khoảng hở (gap) giữa các tile được nâng cao (elevated) bởi terrain ([#1602](https://github.com/maplibre/maplibre-gl-js/issues/1602)) (by [@HarelM](https://github.com/HarelM))
- Sửa showTileBoundaries để hiển thị vector source đầu tiên ([#1395](https://github.com/maplibre/maplibre-gl-js/pull/1395)) (by [@jleedev](https://github.com/jleedev))
- Sửa kiểu của biểu thức match ([#1631](https://github.com/maplibre/maplibre-gl-js/pull/1631)) (by [@lukashass](https://github.com/lukashass))
- Sửa lỗi raster tile bị mờ (blurry) do request raster tile bị kẹt (stuck) trong hàng đợi ảnh (image queue). ([#2511](https://github.com/maplibre/maplibre-gl-js/pull/2511)) (by [@pramilk](https://github.com/pramilk))

## 3.0.0-pre.9

### 🐞 Sửa lỗi

- Sửa lỗi ResizeObserver phát ra một sự kiện 'resize' ban đầu (kể từ 3.0.0-pre.5) ([#2551](https://github.com/maplibre/maplibre-gl-js/issues/2551)) (by [@birkskyum](https://github.com/birkskyum))

## 3.0.0-pre.8

### ✨ Tính năng và cải tiến

- Thêm callback `transformCameraUpdate` vào tùy chọn `Map` ([#2535](https://github.com/maplibre/maplibre-gl-js/pull/2535)) (by [@Pessimistress](https://github.com/Pessimistress))

### 🐞 Sửa lỗi

- Chỉnh sửa lại bản sửa lỗi trước đó ([#2445](https://github.com/maplibre/maplibre-gl-js/issues/2445)) cho việc raster tile bị giữ lại khi raster-fade-duration bằng 0 ([#2501](https://github.com/maplibre/maplibre-gl-js/issues/2501)) (by [@ibesora](https://github.com/ibesora))

## 3.0.0-pre.7

### ✨ Tính năng và cải tiến

- ⚠️ Phá vỡ tương thích - Loại bỏ hỗ trợ WebGL1. Chuyển sang WebGL2 ([#2512](https://github.com/maplibre/maplibre-gl-js/pull/2512)) (by [@birkskyum](https://github.com/birkskyum))
- Nâng cấp KDBush và supercluster ([#2522](https://github.com/maplibre/maplibre-gl-js/pull/2522)) (by [@birkskyum](https://github.com/birkskyum))

## 3.0.0-pre.6

### ✨ Tính năng và cải tiến

- ⚠️ Phá vỡ tương thích - Cải thiện hiệu năng control bằng cách giới hạn số worker tối đa là 1, ngoại trừ trình duyệt Safari. ([#2354](https://github.com/maplibre/maplibre-gl-js/pull/2354)) (by [@pramilk](https://github.com/pramilk))
- Cải thiện hiệu năng bằng cách sử dụng HTMLImageElement để tải ảnh raster source khi refreshExpiredTiles là false ([#2126](https://github.com/maplibre/maplibre-gl-js/pull/2126)) (by [@pramilk](https://github.com/pramilk))
- ⚠️ Phá vỡ tương thích - Cải thiện hiệu năng tải ban đầu của control bằng cách ép fadeDuration về 0 cho tới sự kiện idle đầu tiên ([#2447](https://github.com/maplibre/maplibre-gl-js/pull/2447)) (by [@pramilk](https://github.com/pramilk))
- ⚠️ Phá vỡ tương thích - Loại bỏ package "mapbox-gl-supported" khỏi API. Nếu cần, vui lòng tham chiếu trực tiếp thay vì thông qua MapLibre. ([#2451](https://github.com/maplibre/maplibre-gl-js/pull/2451)) (by [@zhangyiatmicrosoft](https://github.com/zhangyiatmicrosoft))
- Đặt fetchPriority cho HTMLImageElement để cải thiện các tình huống dùng nhiều raster ([#2459](https://github.com/maplibre/maplibre-gl-js/pull/2459)) (by [@pramilk](https://github.com/pramilk))
- Giảm số lần gọi render lúc tải ban đầu. Không cần thử render trước khi style được tải xong. ([#2464](https://github.com/maplibre/maplibre-gl-js/pull/2464)) (by [@pramilk](https://github.com/pramilk))
- Lazy load các thuộc tính style mặc định theo yêu cầu để cải thiện hiệu năng tải và giảm sử dụng bộ nhớ. ([#2476](https://github.com/maplibre/maplibre-gl-js/pull/2476)) (by [@pramilk](https://github.com/pramilk))
- Hỗ trợ WebGL2 có điều kiện (Conditional WebGL2 support) ([#1891](https://github.com/maplibre/maplibre-gl-js/pull/1891)) (by [@rotu](https://github.com/rotu))

### 🐞 Sửa lỗi

- Sửa `LngLatBounds.extend()` để xử lý đúng tọa độ dạng `{ lng: number, lat: number }`. ([#2425](https://github.com/maplibre/maplibre-gl-js/pull/2425)) (by [@buffalom](https://github.com/buffalom))
- Sửa lỗi vòng tròn độ chính xác (accuracy-circle) trong geolocate control bị thay đổi kích thước ngẫu nhiên. ([#2450](https://github.com/maplibre/maplibre-gl-js/pull/2450)) (by [@Philip2809](https://github.com/Philip2809))

## 3.0.0-pre.5

### ✨ Tính năng và cải tiến

- Thêm queryTerrainElevation cho phép lấy độ cao terrain tính bằng mét tại một điểm cụ thể ([#2264](https://github.com/maplibre/maplibre-gl-js/pull/2264)) (by [@manhcuongincusar1](https://github.com/manhcuongincusar1))
- Cải thiện hiệu năng bằng cách gửi các style layer tới worker thread trước khi xử lý trên main thread để cho phép xử lý song song ([#2131](https://github.com/maplibre/maplibre-gl-js/pull/2131)) (by [@pramilk](https://github.com/pramilk))
- ⚠️ Phá vỡ tương thích - Resize bản đồ khi phần tử container bị thay đổi kích thước. Các sự kiện liên quan tới resize giờ có dữ liệu đi kèm khác trước ([#2157](https://github.com/maplibre/maplibre-gl-js/pull/2157)). Trước đây trường originalEvent là nguyên nhân của thay đổi này, ví dụ nó có thể là một sự kiện `resize` từ trình duyệt. Giờ đây nó là `ResizeObserverEntry`, xem thêm [tại đây](https://developer.mozilla.org/en-US/docs/web/api/resizeobserverentry). (by [@HarelM](https://github.com/HarelM))
- Thêm Map.getImage() để lấy lại các ảnh đã được tải trước đó. ([#2168](https://github.com/maplibre/maplibre-gl-js/pull/2168)) (by [@ZeLonewolf](https://github.com/ZeLonewolf))
- Thêm phương thức để bật/tắt cooperative gestures ([#2152](https://github.com/maplibre/maplibre-gl-js/pull/2152)) (by [@kevinschaul](https://github.com/kevinschaul))
- ⚠️ Phá vỡ tương thích - `LngLat.toBounds()` được thay thế bằng phương thức tĩnh `LngLatBounds.fromLngLat()` ([#2188](https://github.com/maplibre/maplibre-gl-js/pull/2188)) (by [@zhangyiatmicrosoft](https://github.com/zhangyiatmicrosoft))
- Cập nhật CONTRIBUTING.md với chi tiết về cách thiết lập trên Mac M1 ([#2196](https://github.com/maplibre/maplibre-gl-js/pull/2196)) (by [@llambanna](https://github.com/llambanna))
- Cập nhật kiểu mặc định của originalEvent trong MapLibreEvent thành `unknown` ([#2243](https://github.com/maplibre/maplibre-gl-js/pull/2243)) (by [@neodescis](https://github.com/neodescis))
- Cải thiện hiệu năng khi ép buộc đặt symbol đầy đủ bằng cách bỏ qua nhanh các kiểm tra tạm dừng ([#2241](https://github.com/maplibre/maplibre-gl-js/pull/2241)) (by [@schlosna](https://github.com/schlosna))
- Thêm cảnh báo `warnonce` khi source của terrain và hillshade giống nhau ([#2298](https://github.com/maplibre/maplibre-gl-js/pull/2298)) (by [@tempranova](https://github.com/tempranova))
- Loại bỏ một cảnh báo deprecation bằng cách xóa một texture rỗng không còn được sử dụng trong codebase ([#2299](https://github.com/maplibre/maplibre-gl-js/pull/2299)) (by [@IvanSanchez](https://github.com/IvanSanchez))
- Cải thiện hiệu năng tải ban đầu bằng cách chỉ serialize layer khi cần thiết (lazy serializing). ([#2306](https://github.com/maplibre/maplibre-gl-js/pull/2306)) (by [@zhangyiatmicrosoft](https://github.com/zhangyiatmicrosoft))
- ⚠️ Phá vỡ tương thích - Hủy request tile chưa tải xong khi zoom in qua nhiều mức zoom. Trước đây các request này không bị hủy. ([#2377](https://github.com/maplibre/maplibre-gl-js/pull/2377)) (by [@pramilk](https://github.com/pramilk))
- Thêm tùy chọn validateStyle cho Map để cho phép tắt việc validate style nhằm tăng hiệu năng trong môi trường production. ([#2390](https://github.com/maplibre/maplibre-gl-js/pull/2390)) (by [@pramilk](https://github.com/pramilk))
- ⚠️ Phá vỡ tương thích - Loại bỏ hỗ trợ màu css `hsl` ở định dạng không tuân theo đặc tả CSS Color. Các màu định nghĩa theo định dạng `hsl(110, 0.7, 0.055)` sẽ không còn hoạt động, thay vào đó nên dùng định dạng phần trăm `hsl(110, 70%, 5.5%)`. ([#2376](https://github.com/maplibre/maplibre-gl-js/pull/2376)) (by [@kajkal](https://github.com/kajkal))

### 🐞 Sửa lỗi

- Sửa kiểu của thuộc tính `features` trên `MapLayerMouseEvent` và `MapLayerTouchEvent` thành `MapGeoJSONFeature[]` thay vì `GeoJSON.Feature[]` ([#2244](https://github.com/maplibre/maplibre-gl-js/pull/2244)) (by [@parkerziegler](https://github.com/parkerziegler))
- Sửa lỗi GeolocateControl nếu bị xóa quá nhanh ([#2391](https://github.com/maplibre/maplibre-gl-js/pull/2391)) (by [@Pessimistress](https://github.com/Pessimistress))
- Sửa lỗi khi unload sprite sheet khi dùng `setStyle(style, {diff:true})` ([#2146](https://github.com/maplibre/maplibre-gl-js/pull/2146)) (by [@jcary741](https://github.com/jcary741))
- Sửa lỗi wrap tọa độ trong getTerrain khi fitBounds vượt qua đường đổi ngày (AM) ([#2155](https://github.com/maplibre/maplibre-gl-js/pull/2155)) (by [@llambanna](https://github.com/llambanna))
- Sửa kiểu trả về của phương thức toArray của LngLat thành [number,number] ([#2233](https://github.com/maplibre/maplibre-gl-js/issues/2233)) (by [@maxdacruz](https://github.com/maxdacruz))
- Sửa việc xử lý text-offset khi symbol-placement: line ([#2170](https://github.com/maplibre/maplibre-gl-js/issues/2170) và [#2171](https://github.com/maplibre/maplibre-gl-js/issues/2171)) (by [@ChrisLoer](https://github.com/ChrisLoer))
- Sửa lỗi kiểm tra quyền của geolocate control thất bại trên web view iOS16 bằng cách dự phòng sang window.navigator.geolocation ([#2359](https://github.com/maplibre/maplibre-gl-js/pull/2359)) (by [@HarelM](https://github.com/HarelM))
- Ngăn việc reload không cần thiết các raster source khi RTL Text Plugin được tải ([#2380](https://github.com/maplibre/maplibre-gl-js/issues/2380)) (by [@ChrisLoer](https://github.com/ChrisLoer))
- Sửa việc xử lý hàm callback AddProtocol khi trả về một HTMLImageElement ([#2393](https://github.com/maplibre/maplibre-gl-js/pull/2393)) (by [@pramilk](https://github.com/pramilk))
- Sửa lỗi raster tile bị giữ lại khi raster-fade-duration bằng 0 ([#2445](https://github.com/maplibre/maplibre-gl-js/issues/2445)) (by [@ibesora](https://github.com/ibesora))

## 3.0.0-pre.4

### ✨ Tính năng và cải tiến

- Thêm `setClusterOptions` để cập nhật thuộc tính cluster của các source đã thêm: sửa các vấn đề ([#429](https://github.com/maplibre/maplibre-gl-js/issues/429)) và ([#1384](https://github.com/maplibre/maplibre-gl-js/issues/1384)) (by [@IhsenBen](https://github.com/IhsenBen))
- Thêm kiểu (types) cho `workerOptions` và `_options` trong `geojson_source.ts` ([#1998](https://github.com/maplibre/maplibre-gl-js/pull/1998)) (by [@IhsenBen](https://github.com/IhsenBen))
- Thêm sự kiện fullscreenstart, fullscreenend cho FullscreenControl ([#2128](https://github.com/maplibre/maplibre-gl-js/pull/2128)) (by [@kevinschaul](https://github.com/kevinschaul))
- Throttle hàng đợi request ảnh trong khi bản đồ đang di chuyển để cải thiện hiệu năng ([#2097](https://github.com/maplibre/maplibre-gl-js/pull/2097)) (by [@zhangyiatmicrosoft](https://github.com/zhangyiatmicrosoft))

### 🐞 Sửa lỗi

- Sửa lỗi worker bị chấm dứt khi đặt style mới ([#2123](https://github.com/maplibre/maplibre-gl-js/pull/2123)) (by [@pramilk](https://github.com/pramilk))
- Thay đổi cách phát hiện phím meta cho cooperative gestures ([#2152](https://github.com/maplibre/maplibre-gl-js/pull/2152)) (by [@kevinschaul](https://github.com/kevinschaul))
- Sửa lỗi worker bị chấm dứt khi đặt style mới ([#2123](https://github.com/maplibre/maplibre-gl-js/pull/2123)) (by [@pramilk](https://github.com/pramilk))

## 3.0.0-pre.3

### ✨ Tính năng và cải tiến

- Thêm hỗ trợ khai báo nhiều `sprite` trong một file style ([#1805](https://github.com/maplibre/maplibre-gl-js/pull/1805)) (by [@smellyshovel](https://github.com/smellyshovel))
- Trích xuất ảnh sprite theo yêu cầu để giảm sử dụng bộ nhớ và cải thiện hiệu năng bằng cách giảm số lần gọi getImageData ([#1809](https://github.com/maplibre/maplibre-gl-js/pull/1809)) (by [@pramilk](https://github.com/pramilk))

### 🐞 Sửa lỗi

- Sửa lỗi ([#1024](https://github.com/maplibre/maplibre-gl-js/issues/1024)) - tâm zoom không nằm dưới con trỏ chuột khi bật terrain (by [@HarelM](https://github.com/HarelM))
- Sửa lỗi khi chạy các script bin của style-spec và thêm phần trợ giúp còn thiếu. Loại bỏ script không cần thiết 'gl-style-composite'. ([#1971](https://github.com/maplibre/maplibre-gl-js/pull/1971)) (by [@acalcutt](https://github.com/acalcutt))
- Sửa kiểu của biểu thức slice ([#1886](https://github.com/maplibre/maplibre-gl-js/issues/1886)) (by [@kevinschaul](https://github.com/kevinschaul))

## 3.0.0-pre.2

### ✨ Tính năng và cải tiến

- Thêm kiểu `QueryRenderedFeaturesOptions` cho cả hai tham số trong queryRenderedFeatures ở map.ts ([#1900](https://github.com/maplibre/maplibre-gl-js/issues/1900)) (by [@beharguy](https://github.com/beharguy))
- NavigationControlOptions giờ là tùy chọn khi tạo một instance của NavigationControl ([#1754](https://github.com/maplibre/maplibre-gl-js/issues/1754)) (by [@guimochila](https://github.com/guimochila))
- Lắng nghe sự kiện webglcontextcreationerror và cung cấp thông tin debug chi tiết khi thất bại ([#1715](https://github.com/maplibre/maplibre-gl-js/pull/1715)) (by [@zhangyiatmicrosoft](https://github.com/zhangyiatmicrosoft))
- Đảm bảo overlay `cooperativeGestures` luôn nằm "trên cùng" (z-index) so với các feature của bản đồ ([#1753](https://github.com/maplibre/maplibre-gl-js/pull/1753)) (by [@blyme](https://github.com/blyme))
- Sử dụng gợi ý `willReadFrequently` để tối ưu việc sử dụng canvas 2D và loại bỏ cảnh báo ([#1808](https://github.com/maplibre/maplibre-gl-js/pull/1808)) (by [@kircher1](https://github.com/kircher1))
- Tăng tốc chỉ mục symbol xuyên tile trong một số trường hợp nhất định ([#1755](https://github.com/maplibre/maplibre-gl-js/pull/1755)) (by [@mfedderly](https://github.com/mfedderly))
- Cải thiện tốc độ render trong các cảnh có nhiều icon và nhãn biểu tượng va chạm nhau ([#1757](https://github.com/maplibre/maplibre-gl-js/pull/1757)) (by [@AdamS108](https://github.com/AdamS108))
- Cho phép hủy (cancelable) request của ImageSource ([#1802](https://github.com/maplibre/maplibre-gl-js/pull/1802)) (by [@blinkzz](https://github.com/blinkzz))
- Throttle hàng đợi request ảnh trong khi bản đồ đang di chuyển để cải thiện hiệu năng ([#2097](https://github.com/maplibre/maplibre-gl-js/pull/2097)) (by [@zhangyiatmicrosoft](https://github.com/zhangyiatmicrosoft))

### 🐞 Sửa lỗi

- Loại bỏ phụ thuộc vào `@rollup/plugin-json`, vốn xung đột với `rollup-plugin-import-assert` ([#1894](https://github.com/maplibre/maplibre-gl-js/pull/1894)) (by [@rotu](https://github.com/rotu))
- Loại bỏ phụ thuộc vào `@mapbox/gazetteer` vốn gây ra một số cảnh báo build ([#1757](https://github.com/maplibre/maplibre-gl-js/pull/1757) [#1898](https://github.com/maplibre/maplibre-gl-js/pull/1898)) (by [@AdamS108](https://github.com/AdamS108))
- Sửa lỗi `getElevation()` gây ra lỗi không được bắt ([#1650](https://github.com/maplibre/maplibre-gl-js/issues/1650)). (by [@zbigniewmatysek-tomtom](https://github.com/zbigniewmatysek-tomtom))
- Sửa việc chạy benchmark ở chế độ headless, đặc biệt trên máy ảo ([#1732](https://github.com/maplibre/maplibre-gl-js/pull/1732)) (by [@zhangyiatmicrosoft](https://github.com/zhangyiatmicrosoft))
- sửa lỗi [#860](https://github.com/maplibre/maplibre-gl-js/issues/860) fill-pattern với pixelRatio > 1 giờ được chuyển đổi đúng tại runtime. ([#1765](https://github.com/maplibre/maplibre-gl-js/pull/1765)) (by [@zhangyiatmicrosoft](https://github.com/zhangyiatmicrosoft))
- Sửa lỗi exception bị ném ra khi gọi map.setStyle với tùy chọn transformStyle trong khi map được khởi tạo mà không có style ban đầu. ([#1824](https://github.com/maplibre/maplibre-gl-js/pull/1824)) (by [@ambientlight](https://github.com/ambientlight))
- Sửa hành vi của nút la bàn trên thiết bị cảm ứng. ([#1852](https://github.com/maplibre/maplibre-gl-js/pull/1852)) (by [@VehpuS](https://github.com/VehpuS))

## 3.0.0-pre.1

### ✨ Tính năng và cải tiến

- Trả về một promise từ phương thức `once` để dễ dàng sử dụng async/await hơn trong trường hợp này ([#1690](https://github.com/maplibre/maplibre-gl-js/pull/1690)) (by [@HarelM](https://github.com/HarelM))
- Thêm chế độ fullscreen giả (pseudo CSS fullscreen) làm phương án dự phòng cho iPhone ([#1678](https://github.com/maplibre/maplibre-gl-js/pull/1678)) (by [@caspg](https://github.com/caspg))
- Thêm `updateData` cho `GeoJSONSource` cho phép cập nhật dữ liệu từng phần ([#1605](https://github.com/maplibre/maplibre-gl-js/pull/1605)) (by [@mfedderly](https://github.com/mfedderly))

### 🐞 Sửa lỗi

- Sửa lỗi `GeoJSONSource` có vẻ như không bao giờ tải xong khi gọi phương thức setData ngay sau khi thêm nó vào Map, do không phát ra sự kiện data loại metadata ([#1693](https://github.com/maplibre/maplibre-gl-js/issues/1693)) (by [@vanilla-lake](https://github.com/vanilla-lake))
- Sửa khoảng hở giữa các tile được nâng cao bởi terrain ([#1602](https://github.com/maplibre/maplibre-gl-js/issues/1602)) (by [@HarelM](https://github.com/HarelM))

## 3.0.0-pre.0

### ✨ Tính năng và cải tiến

- Thêm một RenderPool để render tile lên texture cho chế độ 3D ([#1671](https://github.com/maplibre/maplibre-gl-js/pull/1671)) (by [@prozessor13](https://github.com/prozessor13))
- Thêm map.getCameraTargetElevation() ([#1558](https://github.com/maplibre/maplibre-gl-js/pull/1558)) (by [@birkskyum](https://github.com/birkskyum))
- Thêm `freezeElevation` vào `AnimationOptions` để cho phép chuyển động camera mượt mà trong chế độ 3D ([#1514](https://github.com/maplibre/maplibre-gl-js/pull/1514), [#1492](https://github.com/maplibre/maplibre-gl-js/issues/1492)) (by [@prozessor13](https://github.com/prozessor13))
- ⚠️ Phá vỡ tương thích - Loại bỏ các class css `mapboxgl-` đã lỗi thời ([#1575](https://github.com/maplibre/maplibre-gl-js/pull/1575)) (by [@birkskyum](https://github.com/birkskyum))
- Thêm tùy chọn transformStyle cho map.setStyle ([#1632](https://github.com/maplibre/maplibre-gl-js/pull/1632)) (by [@ambientlight](https://github.com/ambientlight))
- ⚠️ Phá vỡ tương thích - Cải thiện việc render các khu vực dưới mực nước biển, và loại bỏ giải pháp tạm elevationOffset ([#1578](https://github.com/maplibre/maplibre-gl-js/pull/1578)) (by [@birkskyum](https://github.com/birkskyum))
- ⚠️ Phá vỡ tương thích - Di chuyển đối tượng terrain từ style.terrain sang map.terrain ([#1628](https://github.com/maplibre/maplibre-gl-js/pull/1628)) (by [@HarelM](https://github.com/HarelM))

### 🐞 Sửa lỗi

- ⚠️ Phá vỡ tương thích - Đặt geojson data source thành trường bắt buộc để khớp với tài liệu ([#1396](https://github.com/maplibre/maplibre-gl-js/issues/1396)) (by [@HarelM](https://github.com/HarelM))
- Sửa showTileBoundaries để hiển thị vector source đầu tiên ([#1395](https://github.com/maplibre/maplibre-gl-js/pull/1395)) (by [@jleedev](https://github.com/jleedev))
- Sửa kiểu của biểu thức match ([#1631](https://github.com/maplibre/maplibre-gl-js/pull/1631)) (by [@lukashass](https://github.com/lukashass))

## 2.4.0

### ✨ Tính năng và cải tiến

- Thêm calculateCameraOptionsFromTo cho camera ([#1427](https://github.com/maplibre/maplibre-gl-js/pull/1427)) (by [@BAschl](https://github.com/BAschl))
- Cải thiện các kiểu expression ([#1510](https://github.com/maplibre/maplibre-gl-js/pull/1510)) (by [@cns-solutions-admin](https://github.com/cns-solutions-admin))
- Cải thiện hiệu năng cho việc chọn kích thước primitive ([#1508](https://github.com/maplibre/maplibre-gl-js/pull/1508)) (by [@kircher1](https://github.com/kircher1))
- Nâng cấp target biên dịch từ ES2017 lên ES2019 ([#1499](https://github.com/maplibre/maplibre-gl-js/pull/1499)) (by [@birkskyum](https://github.com/birkskyum))
- Cải thiện xử lý lỗi ([#1485](https://github.com/maplibre/maplibre-gl-js/pull/1485)) (by [@birkskyum](https://github.com/birkskyum))
- Loại bỏ trường `_interpolationType` không sử dụng ([#264](https://github.com/maplibre/maplibre-gl-js/issues/264)) (by [@HarelM](https://github.com/HarelM))

### 🐞 Sửa lỗi

- Sửa lỗi attribution không được hiển thị cho terrain ([#1516](https://github.com/maplibre/maplibre-gl-js/pull/1516)) (by [@acalcutt](https://github.com/acalcutt))
- Không kích hoạt contextmenu sau khi rotate, pitch, v.v. kể cả trên Windows ([#1537](https://github.com/maplibre/maplibre-gl-js/pull/1537)) (by [@cns-solutions-admin](https://github.com/cns-solutions-admin))

## 2.3.1-pre.2

### ✨ Tính năng và cải tiến

- Cải thiện các kiểu expression ([#1510](https://github.com/maplibre/maplibre-gl-js/pull/1510)) (by [@cns-solutions-admin](https://github.com/cns-solutions-admin))
- Cải thiện hiệu năng cho việc chọn kích thước primitive ([#1508](https://github.com/maplibre/maplibre-gl-js/pull/1508)) (by [@kircher1](https://github.com/kircher1))
- Nâng cấp target biên dịch từ ES2017 lên ES2019 ([#1499](https://github.com/maplibre/maplibre-gl-js/pull/1499)) (by [@birkskyum](https://github.com/birkskyum))

## 2.3.1-pre.1

### ✨ Tính năng và cải tiến

- Cải thiện xử lý lỗi ([#1485](https://github.com/maplibre/maplibre-gl-js/pull/1485)) (by [@birkskyum](https://github.com/birkskyum))

## 2.3.0

### ✨ Tính năng và cải tiến

- Bật lại phương thức lấy phiên bản thư viện. Có thể dùng `import {version} from 'maplibre-gl'`, hoặc trên instance Map bằng `map.version`. ([#1471](https://github.com/maplibre/maplibre-gl-js/pull/1471)) (by [@birkskyum](https://github.com/birkskyum))

## 2.2.1

### 🐞 Sửa lỗi

- Sửa việc sinh (generate) types và đảm bảo chúng chạy như một phần của CI ([#1462](https://github.com/maplibre/maplibre-gl-js/issues/1462), [#1465](https://github.com/maplibre/maplibre-gl-js/pull/1465)) (by [@HarelM](https://github.com/HarelM))

## 2.2.0

Tất cả từ bốn bản pre-release trước đó:

### ✨ Tính năng và cải tiến

- Cập nhật thuộc tính layout symbol `icon-padding` để hỗ trợ padding bất đối xứng (asymmetric) ([#1289](https://github.com/maplibre/maplibre-gl-js/pull/1289)) (by [@drwestco](https://github.com/drwestco))
- Thêm tùy chọn `cooperativeGestures` khi khởi tạo map để ngăn việc scroll/pan ngoài ý muốn khi duyệt trang có bản đồ được nhúng inline ([#234](https://github.com/maplibre/maplibre-gl-js/issues/234)) (by [@ewagstaff](https://github.com/ewagstaff))
- Cải thiện typings của đặc tả filter ([#1390](https://github.com/maplibre/maplibre-gl-js/pull/1390)) (by [@HarelM](https://github.com/HarelM))
- Thêm khả năng terrain 3D ([#165](https://github.com/maplibre/maplibre-gl-js/pull/165), [#1022](https://github.com/maplibre/maplibre-gl-js/pull/1022)) (by [@prozessor13](https://github.com/prozessor13))
- Hủy các request GeoJSON đang chờ (pending) khi `GeoJSONSource.setData()` được gọi, thay vì đợi request đang chờ hoàn tất trước khi gửi request cho URL mới ([#1102](https://github.com/maplibre/maplibre-gl-js/pull/1102)) (by [@vanilla-lake](https://github.com/vanilla-lake))

### 🐞 Sửa lỗi

- Sửa kiểu (style) compact attribution khi dùng CSS toàn cục đặt `box-sizing: border-box;` ([#1250](https://github.com/maplibre/maplibre-gl-js/pull/1250)) (by [@lukashass](https://github.com/lukashass))
- Xử lý `maxBounds` vượt qua kinh tuyến tại longitude ±180° ([#1299](https://github.com/maplibre/maplibre-gl-js/pull/1299)) (by [@burleight](https://github.com/burleight))
- Ẩn mũi tên hiển thị trong style `summary` mặc định trên attribution control ([#1258](https://github.com/maplibre/maplibre-gl-js/pull/1258)) (by [@pjsier](https://github.com/pjsier))
- Sửa mức sử dụng bộ nhớ trong terrain 3D ([#1291](https://github.com/maplibre/maplibre-gl-js/issues/1291), [#1302](https://github.com/maplibre/maplibre-gl-js/pull/1302)) (by [@prozessor13](https://github.com/prozessor13))
- Sửa lỗi biến mất của các tile gần nhất khi bật terrain 3D ([#1241](https://github.com/maplibre/maplibre-gl-js/issues/1241), [#1300](https://github.com/maplibre/maplibre-gl-js/pull/1300)) (by [@prozessor13](https://github.com/prozessor13))

## 2.2.0-pre.4

### ✨ Tính năng và cải tiến

- Cập nhật thuộc tính layout symbol `icon-padding` để hỗ trợ padding bất đối xứng ([#1289](https://github.com/maplibre/maplibre-gl-js/pull/1289)) (by [@drwestco](https://github.com/drwestco))
- Thêm tùy chọn `cooperativeGestures` khi khởi tạo map để ngăn việc scroll/pan ngoài ý muốn khi duyệt trang có bản đồ được nhúng inline ([#234](https://github.com/maplibre/maplibre-gl-js/issues/234)) (by [@ewagstaff](https://github.com/ewagstaff))
- Cải thiện typings của đặc tả filter ([#1390](https://github.com/maplibre/maplibre-gl-js/pull/1390)) (by [@HarelM](https://github.com/HarelM))

### 🐞 Sửa lỗi

- Sửa kiểu compact attribution khi dùng CSS toàn cục đặt `box-sizing: border-box;` ([#1250](https://github.com/maplibre/maplibre-gl-js/pull/1250)) (by [@lukashass](https://github.com/lukashass))

## 2.2.0-pre.3

### 🐞 Sửa lỗi

- Xử lý `maxBounds` vượt qua kinh tuyến tại longitude ±180° ([#1299](https://github.com/maplibre/maplibre-gl-js/pull/1299)) (by [@burleight](https://github.com/burleight))
- Ẩn mũi tên hiển thị trong style `summary` mặc định trên attribution control ([#1258](https://github.com/maplibre/maplibre-gl-js/pull/1258)) (by [@pjsier](https://github.com/pjsier))
- Sửa mức sử dụng bộ nhớ trong terrain 3D ([#1291](https://github.com/maplibre/maplibre-gl-js/issues/1291), [#1302](https://github.com/maplibre/maplibre-gl-js/pull/1302)) (by [@prozessor13](https://github.com/prozessor13))
- Sửa lỗi biến mất của các tile gần nhất khi bật terrain 3D ([#1241](https://github.com/maplibre/maplibre-gl-js/issues/1241), [#1300](https://github.com/maplibre/maplibre-gl-js/pull/1300)) (by [@prozessor13](https://github.com/prozessor13))

## 2.2.0-pre.2

### ✨ Tính năng và cải tiến

- Thêm khả năng terrain 3D ([#165](https://github.com/maplibre/maplibre-gl-js/pull/165), [#1022](https://github.com/maplibre/maplibre-gl-js/pull/1022)) (by [@prozessor13](https://github.com/prozessor13))

## 2.2.0-pre.1

### ✨ Tính năng và cải tiến

- Hủy các request GeoJSON đang chờ khi `GeoJSONSource.setData()` được gọi, thay vì đợi request đang chờ hoàn tất trước khi gửi request cho URL mới ([#1102](https://github.com/maplibre/maplibre-gl-js/pull/1102)) (by [@vanilla-lake](https://github.com/vanilla-lake))

## 2.1.9

### 🐞 Sửa lỗi

- Thêm lại typescript typings vào dependencies thay vì devDependencies ([#1178](https://github.com/maplibre/maplibre-gl-js/pull/1178)) (by [@HarelM](https://github.com/HarelM))

## 2.1.8

### ✨ Tính năng và cải tiến

- Thay đổi logic hiển thị logo MapLibre. Logo MapLibre giờ được hiển thị bằng cách đặt tùy chọn map 'maplibreLogo' thành true hoặc thêm nó vào map bằng addControl. TileJSON không còn kiểm soát việc hiển thị logo nữa. ([#786](https://github.com/maplibre/maplibre-gl-js/pull/786)) (by [@acalcutt](https://github.com/acalcutt))

### 🐞 Sửa lỗi

- Sửa lỗi thiếu `touchmove` trong `MapTouchEvent["type"]` ([#1131](https://github.com/maplibre/maplibre-gl-js/pull/1131)) (by [@smellyshovel](https://github.com/smellyshovel))
- Đặt kiểu cho `CustomLayerInterface` với `renderingMode`, `onRemove`, `onAdd`, và `prerender` là tùy chọn (optional) ([#1122](https://github.com/maplibre/maplibre-gl-js/pull/1122)) (by [@nreese](https://github.com/nreese))

## 2.1.8-pre.3

### 🐞 Sửa lỗi

- Dùng đúng vị trí (location) cho sự kiện chuột của line layer có line-offset ([#1108](https://github.com/maplibre/maplibre-gl-js/issues/1108)). (by [@jkoelewijn](https://github.com/jkoelewijn))
- Thay đổi kiểu `GeoJSONFeature.properties` từ `{}` thành `{ [name: string]: any; }` ([#1115](https://github.com/maplibre/maplibre-gl-js/pull/1115)). (by [@nreese](https://github.com/nreese))
- Sửa lỗi `error TS2503: Cannot find namespace 'GeoJSON'` ([#1096](https://github.com/maplibre/maplibre-gl-js/issues/1096)). (by [@wipfli](https://github.com/wipfli))

## 2.1.8-pre.2

### ✨ Tính năng và cải tiến

- Loại bỏ target build production không minify (unminified), vì vậy `npm run build-prod` sẽ là lệnh build chính từ nay về sau.

### 🐞 Sửa lỗi

- Giải phóng (dispose) tài nguyên source khi style của map bị xóa, điều này cũng sửa lỗi `cannot read properties of undefined (reading 'sourceCaches')` ([#1099](https://github.com/maplibre/maplibre-gl-js/pull/1099)). (by [@khmm12](https://github.com/khmm12))
- Thêm kiểu `MapGeoJSONFeature` thay thế cho `MapboxGeoJSONFeature`. Kiểu `MapGeoJSONFeature` mở rộng (extends) kiểu `GeoJSONFeature` với các thuộc tính layer, source, sourceLayer, và state ([#1104](https://github.com/maplibre/maplibre-gl-js/pull/1104)). (by [@nreese](https://github.com/nreese))
- Sửa việc tự động làm mới (refresh) các raster tile đã hết hạn ([#1106](https://github.com/maplibre/maplibre-gl-js/pull/1106)) (by [@westinrm](https://github.com/westinrm))
- Sửa mất độ chính xác (precision loss) trong một số phép tính ma trận ([#1105](https://github.com/maplibre/maplibre-gl-js/issues/1105)) (by [@timokorkalainen](https://github.com/timokorkalainen))

## 2.1.8-pre.1

### ✨ Tính năng và cải tiến

- Thêm tùy chọn `viewport-glyph` cho `text-rotation-alignment`, đặt các glyph dọc theo một linestring và xoay chúng theo trục x của viewport ([#716](https://github.com/maplibre/maplibre-gl-js/pull/716)). (by [@wipfli](https://github.com/wipfli))

### 🐞 Sửa lỗi

- Thay đổi kiểu `GeoJSONFeature.id` từ `number | string | void` thành `number | string | undefined` ([#1093](https://github.com/maplibre/maplibre-gl-js/pull/1093)) (by [@nreese](https://github.com/nreese))
- Thêm kiểu `FeatureIdentifier` để định nghĩa tham số feature trong các phương thức setFeatureState, removeFeatureState, và getFeatureState. Thay đổi `FeatureIdentifier.id` từ `id: string | number;` thành `id?: string | number | undefined;` ([#1095](https://github.com/maplibre/maplibre-gl-js/pull/1095)) (by [@nreese](https://github.com/nreese))
- Thay đổi tham số kiểu của map.on, map.off, và map.once từ "type: MapEvent" thành "type: MapEvent | string" ([#1094](https://github.com/maplibre/maplibre-gl-js/pull/1094)) (by [@nreese](https://github.com/nreese))

## 2.1.7

### 🐞 Sửa lỗi

- Thêm điều chỉnh cho việc render glyph, chủ yếu ảnh hưởng tới font CJK ([#1002](https://github.com/maplibre/maplibre-gl-js/issues/1002)). (by [@Kanahiro](https://github.com/Kanahiro))
- Cải thiện typings để sửa lỗi thất bại ở chế độ strict mode của Angular ([#790](https://github.com/maplibre/maplibre-gl-js/issues/790), [#970](https://github.com/maplibre/maplibre-gl-js/issues/970), [#934](https://github.com/maplibre/maplibre-gl-js/issues/934)) (by [@HarelM](https://github.com/HarelM))
- Sửa lỗi `SourceCache.loaded()` luôn trả về `true` sau khi xảy ra lỗi tải ([#1025](https://github.com/maplibre/maplibre-gl-js/issues/1025)) (by [@vanilla-lake](https://github.com/vanilla-lake))
- Thêm lại bản build csp và dev vào npm package ([#1042](https://github.com/maplibre/maplibre-gl-js/issues/1042)) (by [@HarelM](https://github.com/HarelM))

## 2.1.6

### 🐞 Sửa lỗi

- Publish `dist/package.json` ([#998](https://github.com/maplibre/maplibre-gl-js/pull/998)). (by [@wipfli](https://github.com/wipfli))

## 2.1.6-pre.1

### 🐞 Sửa lỗi

- Publish `dist/package.json` ([#998](https://github.com/maplibre/maplibre-gl-js/pull/998)). (by [@wipfli](https://github.com/wipfli))

## 2.1.5

### 🐞 Sửa lỗi

- Publish file `postinstall.js` rỗng. Tiếp nối ([#990](https://github.com/maplibre/maplibre-gl-js/issues/990)) (by [@wipfli](https://github.com/wipfli))

## 2.1.5-pre.1

### 🐞 Sửa lỗi

- Publish file `postinstall.js` rỗng. Tiếp nối ([#990](https://github.com/maplibre/maplibre-gl-js/issues/990)) (by [@wipfli](https://github.com/wipfli))

## 2.1.4

### 🐞 Sửa lỗi

- Sửa lỗi thiếu file `postinstall.js` khi publish npm. Tiếp nối ([#990](https://github.com/maplibre/maplibre-gl-js/issues/990)) (by [@wipfli](https://github.com/wipfli))

## 2.1.3

### 🐞 Sửa lỗi

- Sửa lỗi `ts-node` ở bước postinstall khi cài đặt không phải môi trường dev (non-dev installs) ([#900](https://github.com/maplibre/maplibre-gl-js/pull/900)) (by [@birkskyum](https://github.com/birkskyum))

## 2.1.2

### Tính năng và cải tiến

- Đặt compact attribution mặc định ở trạng thái mở để tuân thủ Hướng dẫn Attribution của OpenStreetMap ([#795](https://github.com/maplibre/maplibre-gl-js/pull/795)) (by [@acalcutt](https://github.com/acalcutt))
- Export khai báo các class `Source` (`GeoJSONSource`, v.v.). ([#801](https://github.com/maplibre/maplibre-gl-js/issues/801)) (by [@sebisteiner](https://github.com/sebisteiner))
- Đặt `AJAXError` công khai (public) để phản hồi lỗi HTTP có thể được xử lý khác với các lỗi khác. ([#941](https://github.com/maplibre/maplibre-gl-js/pull/941)) (by [@vanilla-lake](https://github.com/vanilla-lake))

### 🐞 Sửa lỗi

- Sửa lỗi nút compact attribution hiển thị khi attribution trống ([#795](https://github.com/maplibre/maplibre-gl-js/pull/795)) (by [@acalcutt](https://github.com/acalcutt))
- Sửa lỗi kích thước ảnh không khớp (mismatched) đối với ký tự CJK ([#718](https://github.com/maplibre/maplibre-gl-js/issues/718)) (by [@HarelM](https://github.com/HarelM))
- Phát ra sự kiện `dataabort` và `sourcedataabort` khi một request tile bị hủy (aborted) ([#794](https://github.com/maplibre/maplibre-gl-js/issues/794)) (by [@vanilla-lake](https://github.com/vanilla-lake))
- Sửa lỗi `performance` bị undefined trên NextJs ([#768](https://github.com/maplibre/maplibre-gl-js/issues/768)) (by [@HarelM](https://github.com/HarelM))

## 2.1.1

### 🐞 Sửa lỗi

- Sửa lỗi tile cũ (stale) bị hiển thị khi gọi VectorTileSource#setTiles trong lúc bản đồ đang di chuyển. ([#913](https://github.com/maplibre/maplibre-gl-js/pull/913)) (by [@vanilla-lake](https://github.com/vanilla-lake))

## 2.1.0

### ✨ Tính năng và cải tiến

- Thêm các thuộc tính layout symbol `icon-overlap` và `text-overlap` ([#347](https://github.com/maplibre/maplibre-gl-js/pull/347)) (by [@drwestco](https://github.com/drwestco))
- Đánh dấu lỗi thời (deprecate) các thuộc tính layout symbol `icon-allow-overlap` và `text-allow-overlap`. `icon-overlap` và `text-overlap` là các thuộc tính thay thế. ([#347](https://github.com/maplibre/maplibre-gl-js/pull/347)) (by [@drwestco](https://github.com/drwestco))
- Loại bỏ package node chalk khỏi devDependencies ([#789](https://github.com/maplibre/maplibre-gl-js/pull/789)). (by [@astridx](https://github.com/astridx))
- Cho phép đặt pixel ratio tùy chỉnh bằng cách thêm thuộc tính `MapOptions#pixelRatio` và phương thức `Map#setPixelRatio`. Vì giá trị `devicePixelRatio` cao có thể dẫn đến các vấn đề về hiệu năng và hiển thị, việc này được thực hiện với rủi ro do người dùng tự chịu. ([#769](https://github.com/maplibre/maplibre-gl-js/issues/769)) (by [@vanilla-lake](https://github.com/vanilla-lake))

## 2.0.5

### 🐞 Sửa lỗi

- Loại bỏ danh sách các phiên bản node được phép cài đặt package.

## 2.0.4

### 🐞 Sửa lỗi

- Thiếu file package.json trong bản dist phiên bản 2.0.3 trên npm ([#811](https://github.com/maplibre/maplibre-gl-js/issues/811)) - điều này khiến webpack thất bại (by [@HarelM](https://github.com/HarelM))

## 2.0.3

### Tính năng và cải tiến

- Loại bỏ package node chalk khỏi devDependencies ([#789](https://github.com/maplibre/maplibre-gl-js/pull/789)). (by [@astridx](https://github.com/astridx))
- Loại bỏ khai báo module vector-tile và quay lại dùng point từ [@mapbox/point-geometry](https://github.com/mapbox/point-geometry) ([#788](https://github.com/maplibre/maplibre-gl-js/issues/788), [#800](https://github.com/maplibre/maplibre-gl-js/pull/800)) (by [@HarelM](https://github.com/HarelM))
- Chuyển môi trường phát triển sang sử dụng NodeJs 16 ([#781](https://github.com/maplibre/maplibre-gl-js/pull/781), [#806](https://github.com/maplibre/maplibre-gl-js/pull/806)) (by [@birkskyum](https://github.com/birkskyum))

### 🐞 Sửa lỗi

- Sửa mức zoom cluster tối đa (max cluster zoom) trong geojson source ([#61](https://github.com/maplibre/maplibre-gl-js/issues/61)) (by [@HarelM](https://github.com/HarelM))

## 2.0.2

### 🐞 Sửa lỗi

- Sửa file được sinh (generated) bởi typescript ([#776](https://github.com/maplibre/maplibre-gl-js/issues/776)). (by [@wipfli](https://github.com/wipfli))

## 2.0.1

### 🐞 Sửa lỗi

- Sửa tài liệu của `addProtocol` và `removeProtocol`. ([#779](https://github.com/maplibre/maplibre-gl-js/pull/779)) (by [@wipfli](https://github.com/wipfli))

## 2.0.0

### Tính năng và cải tiến

- Migrate code production sang typescript ([#209](https://github.com/maplibre/maplibre-gl-js/pull/209)) (by [@HarelM](https://github.com/HarelM))
- ** Thay đổi phá vỡ tương thích ** loại bỏ `version` khỏi public API
- ** Thay đổi phá vỡ tương thích ** ngừng hỗ trợ IE (Internet Explorer)
- ** Thay đổi phá vỡ tương thích ** ngừng hỗ trợ Chrome 49-65. Yêu cầu Chrome 66 trở lên. Để hỗ trợ Chrome 49-65, sử dụng phiên bản 1.15.2.
- ** Thay đổi phá vỡ tương thích ** loại bỏ toàn bộ code liên quan đến `accessToken` và các url đặc thù của Mapbox bắt đầu bằng `mapbox://`. Code telemetry và tracking đã bị loại bỏ.
- ** Thay đổi phá vỡ tương thích ** loại bỏ `baseApiUrl` vì nó chỉ được dùng cho các url liên quan đến Mapbox
- ** Thay đổi phá vỡ tương thích ** typings typescript đã thay đổi:
    - `Style` => `StyleSpecification`
    - `AnyLayer` => `LayerSpecification`
    - `AnySourceData` => `SourceSpecification`
    - `MapboxEvent` => `MapLibreEvent`
    - `MapboxOptions` => `MapOptions`
    - `MapBoxZoomEvent` => `MapLibreZoomEvent`
    - `*SourceRaw` + `*SourceOptions` => `*SourceSpecification`
    - `*Source` (định nghĩa cài đặt source) đã bị loại bỏ
    - `*Layer` => `*LayerSpecification`
    - `*Paint` => `*LayerSpecification['paint']`
    - `*Layout` => `*LayerSpecification['layout']`
    - `MapboxGeoJSONFeature` => `GeoJSONFeature`
- Thêm hàm `redraw` cho map ([#206](https://github.com/maplibre/maplibre-gl-js/issues/206)) (by [@fredj](https://github.com/fredj))
- Cải thiện khả năng truy cập (accessibility) của attribution control. Xem ([#359](https://github.com/maplibre/maplibre-gl-js/issues/359)) (by [@astridx](https://github.com/astridx))
- Cho phép giá trị `maxPitch` lên tới 85, sử dụng giá trị lớn hơn 60 với rủi ro tự chịu ([#574](https://github.com/maplibre/maplibre-gl-js/pull/574)) (by [@kibala145](https://github.com/kibala145))
- `getImage` sử dụng createImageBitmap khi được hỗ trợ ([#650](https://github.com/maplibre/maplibre-gl-js/pull/650)) (by [@clementgayvallet](https://github.com/clementgayvallet))

### 🐞 Sửa lỗi

- Sửa cảnh báo do so sánh chặt (strict comparison) thuộc tính SDF trong image sprite ([#303](https://github.com/maplibre/maplibre-gl-js/issues/303)) (by [@drwestco](https://github.com/drwestco))
- Sửa việc thay thế placeholder của tile để cho phép placeholder xuất hiện nhiều hơn một lần trong URL. ([#348](https://github.com/maplibre/maplibre-gl-js/pull/348)) (by [@rbrundritt](https://github.com/rbrundritt))
- Sửa kiểm tra kiểu (type check) cho môi trường không có DOM. ([#334](https://github.com/maplibre/maplibre-gl-js/issues/334)) (by [@lhapaipai](https://github.com/lhapaipai))
- Sửa vấn đề độ chính xác trong pattern khi overzoom trên thiết bị OpenGL ES. ([#416](https://github.com/maplibre/maplibre-gl-js/pull/416)) (by [@andreadapisa](https://github.com/andreadapisa))
- Sửa padding-top của popup để cải thiện khả năng đọc văn bản trong popup ([#354](https://github.com/maplibre/maplibre-gl-js/pull/354)). (by [@naogify](https://github.com/naogify))
- Sửa lỗi `GeoJSONSource#loaded` đôi khi trả về true trong khi vẫn còn các lần tải đang chờ (pending) ([#669](https://github.com/maplibre/maplibre-gl-js/issues/669)) (by [@vanilla-lake](https://github.com/vanilla-lake))
- Sửa lỗi `MapDataEvent#isSourceLoaded` là true trong các handler sự kiện "dataloading" của GeoJSONSource ([#694](https://github.com/maplibre/maplibre-gl-js/issues/694)) (by [@vanilla-lake](https://github.com/vanilla-lake))
- Sửa lỗi sự kiện vẫn bị phát ra sau khi Map#remove đã được gọi, khi WebGL context bị mất và được khôi phục ([#726](https://github.com/maplibre/maplibre-gl-js/issues/726)) (by [@vanilla-lake](https://github.com/vanilla-lake))
- Sửa định nghĩa kiểu (types definition) cho các expression lồng nhau (nested) ([#757](https://github.com/maplibre/maplibre-gl-js/pull/757)) (by [@j8seangel](https://github.com/j8seangel))

## 1.15.2

### 🐞 Sửa lỗi

- Sửa các thay đổi phá vỡ tương thích được đưa vào từ v1.15.0 bằng cách áp dụng cơ chế đặt tên kép (dual naming scheme) cho tên class CSS ([#203](https://github.com/maplibre/maplibre-gl-js/pull/203)) (by [@p-j](https://github.com/p-j))

## 1.15.1

### 🐞 Sửa lỗi

- Thêm kiểu trả về `void` cho một số khai báo phương thức để khớp với chế độ TS strict mode ([#194](https://github.com/maplibre/maplibre-gl-js/pull/194)) (by [@ArthurMetzger](https://github.com/ArthurMetzger))
- Sửa các phần CSS còn sót lại (leftovers) ([#83](https://github.com/maplibre/maplibre-gl-js/issues/83)) (by [@HarelM](https://github.com/HarelM))

## 1.15.0

### Tính năng và cải tiến

- ** Thay đổi phá vỡ tương thích: ** Đổi tên các class CSS ([#83](https://github.com/maplibre/maplibre-gl-js/issues/83)) (by [@HarelM](https://github.com/HarelM))
- Thêm hỗ trợ custom protocol để cho phép ghi đè (override) các lệnh gọi ajax ([#29](https://github.com/maplibre/maplibre-gl-js/issues/29)) (by [@HarelM](https://github.com/HarelM))
- Thêm `setTransformRequest` cho map ([#159](https://github.com/maplibre/maplibre-gl-js/pull/159)) (by [@thaddmt](https://github.com/thaddmt))
- Publish @maplibre/maplibre-gl-style-spec v14.0.0 lên NPM ([#149](https://github.com/maplibre/maplibre-gl-js/pull/149)) (by [@wipfli](https://github.com/wipfli))
- Thay thế link tới mapbox trên LogoControl bằng link tới maplibre ([#151](https://github.com/maplibre/maplibre-gl-js/pull/151)) (by [@habi](https://github.com/habi))
- Migrate các file style spec từ mapbox sang maplibre ([#147](https://github.com/maplibre/maplibre-gl-js/pull/147)) (by [@wipfli](https://github.com/wipfli))
- Publish MapLibre style spec lên NPM ([#140](https://github.com/maplibre/maplibre-gl-js/pull/140)) (by [@wipfli](https://github.com/wipfli))
- Thay thế mapboxgl bằng maplibregl trong các ví dụ inline của JSDocs ([#134](https://github.com/maplibre/maplibre-gl-js/pull/134)) (by [@wipfli](https://github.com/wipfli))
- Đưa vào file định nghĩa typescript (typescript definitions file) ([#24](https://github.com/maplibre/maplibre-gl-js/issues/24)) (by [@HarelM](https://github.com/HarelM))
- Cập nhật link ví dụ trỏ tới https://maplibre.org/maplibre-gl-js-docs/ ([#131](https://github.com/maplibre/maplibre-gl-js/pull/131)) (by [@wipfli](https://github.com/wipfli))
- Cải thiện hiệu năng của layer có `*-sort-key` không đổi (constant) ([#78](https://github.com/maplibre/maplibre-gl-js/pull/78)) (by [@ghost](https://github.com/ghost))

### 🐞 Sửa lỗi

- Ngăn nút attribution submit form ([#178](https://github.com/maplibre/maplibre-gl-js/issues/178)) (by [@BartInTheField](https://github.com/BartInTheField))

## 1.14.0

### Tính năng và cải tiến

- Đổi thương hiệu (rebrand) thành MapLibre
- Logo mới

### 🐞 Sửa lỗi

- Đổi tên các SVG mapboxgl-ctrl-\*.svg thành maplibregl ([#85](https://github.com/maplibre/maplibre-gl-js/pull/85)) (by [@nyurik](https://github.com/nyurik))
- sửa lỗi ImageSource không hoạt động trên FF/Safari ([#87](https://github.com/maplibre/maplibre-gl-js/pull/87)) (by [@lseelenbinder](https://github.com/lseelenbinder))
- Cập nhật các file HTML debug để dùng MapLibre trong tiêu đề (titles) ([#84](https://github.com/maplibre/maplibre-gl-js/pull/84)) (by [@nyurik](https://github.com/nyurik))
- sửa job checksize của CI để dùng tên maplibre ([#86](https://github.com/maplibre/maplibre-gl-js/pull/86)) (by [@nyurik](https://github.com/nyurik))
- Di chuyển các file output từ mapbox._ sang maplibre._ ([#75](https://github.com/maplibre/maplibre-gl-js/pull/75)) (by [@Joxit](https://github.com/Joxit))
- Loại bỏ các phần đặc thù của mapbox và thương hiệu (branding) khỏi .github ([#64](https://github.com/maplibre/maplibre-gl-js/pull/64)) (by [@marcelnormann](https://github.com/marcelnormann))
- Sửa một vấn đề khi mapbox-gl-js không còn được cấp phép mã nguồn mở nữa, tuy nhiên chúng tôi vô cùng biết ơn Mapbox vì đã phát hành toàn bộ code ban đầu của họ cho cộng đồng theo giấy phép BSD-3.

## 1.13.0

### ✨ Tính năng và cải tiến

- Cải thiện khả năng truy cập (accessibility) bằng cách sửa các vấn đề được báo cáo bởi WCAG 2.1. [#9991](https://github.com/mapbox/mapbox-gl-js/pull/9991)
- Cải thiện khả năng truy cập khi mở popup bằng cách focus ngay vào nội dung. [#9774](https://github.com/mapbox/mapbox-gl-js/pull/9774) (by [@watofundefined](https://github.com/watofundefined)))
- Cải thiện hiệu năng render của symbol có `symbol-sort-key`. [#9751](https://github.com/mapbox/mapbox-gl-js/pull/9751) (by [@osvodef](https://github.com/osvodef)))
- Thêm tùy chọn `clickTolerance` cho `Marker`. [#9640](https://github.com/mapbox/mapbox-gl-js/pull/9640) (by [@ChristopherChudzicki](https://github.com/ChristopherChudzicki)))
- Thêm phương thức `hasControl` cho `Map`. [#10035](https://github.com/mapbox/mapbox-gl-js/pull/10035)
- Thêm phương thức `setOffset` cho `Popup`. [#9946](https://github.com/mapbox/mapbox-gl-js/pull/9946) (by [@jutaz](https://github.com/jutaz)))
- Thêm các phương thức `disableRotation` và `enableRotation` cho `KeyboardHandler`. [#10072](https://github.com/mapbox/mapbox-gl-js/pull/10072) (by [@jmbott](https://github.com/jmbott)))

### 🐞 Sửa lỗi

- Sửa lỗi `queryRenderedFeatures` không expose đúng các giá trị paint nếu chúng là data-driven. [#10074](https://github.com/mapbox/mapbox-gl-js/pull/10074) (by [@osvodef](https://github.com/osvodef)))
- Sửa lỗi attribution không cập nhật khi độ hiển thị (visibility) của layer thay đổi trong lúc zoom. [#9943](https://github.com/mapbox/mapbox-gl-js/pull/9943)
- Sửa lỗi hash control xung đột với việc thao tác history bên ngoài (ví dụ trong single-page app). [#9960](https://github.com/mapbox/mapbox-gl-js/pull/9960) (by [@raegen](https://github.com/raegen)))
- Sửa lỗi `fitBounds` cho kết quả không mong đợi khi bearing khác 0 và padding không đều (uneven). [#9821](https://github.com/mapbox/mapbox-gl-js/pull/9821) (by [@allison-strandberg](https://github.com/allison-strandberg)))
- Sửa hỗ trợ HTTP khi chạy GL JS với [Mapbox Atlas](https://www.mapbox.com/atlas). [#10090](https://github.com/mapbox/mapbox-gl-js/pull/10090)
- Sửa lỗi biểu thức `within` không hoạt động trong `querySourceFeatures`. [#9933](https://github.com/mapbox/mapbox-gl-js/pull/9933)
- Sửa lỗi phần tử HTML nội dung của `Popup` bị xóa khi gọi `setDOMContent`. [#10036](https://github.com/mapbox/mapbox-gl-js/pull/10036)
- Sửa lỗi tương thích khi `icon-image` được dùng như một hàm categorical kiểu cũ (legacy). [#10060](https://github.com/mapbox/mapbox-gl-js/pull/10060)
- Giảm tốc độ tăng bộ nhớ nhanh trên Safari bằng cách đảm bảo dataURI của `Image` được giải phóng. [#10118](https://github.com/mapbox/mapbox-gl-js/pull/10118)

### ⚠️ Lưu ý về IE11

Chúng tôi dự định loại bỏ hỗ trợ Internet Explorer 11 trong một bản phát hành GL JS trong tương lai vào cuối năm nay.

## 1.12.0

### ✨ Tính năng và cải tiến

- Thêm các phương thức để thay đổi động vector tile source (ví dụ `setTiles`, `setUrl`). [#8048](https://github.com/mapbox/mapbox-gl-js/pull/8048) (by [@stepankuzmin](https://github.com/stepankuzmin))
- Thêm tùy chọn `filter` cho GeoJSON source để lọc bỏ feature trước khi xử lý (ví dụ trước khi cluster). [#9864](https://github.com/mapbox/mapbox-gl-js/pull/9864)
- Tăng đáng kể độ chính xác của `line-gradient` đối với các đường dài. [#9694](https://github.com/mapbox/mapbox-gl-js/pull/9694)
- Cải thiện `raster-dem` source để hỗ trợ đúng tùy chọn `maxzoom` và overzoom. [#9789](https://github.com/mapbox/mapbox-gl-js/pull/9789) (by [@brendan-ward](@brendanhttps://github.com/ward))

### 🐞 Sửa lỗi

- Sửa lỗi bearing snap gây ảnh hưởng đến hoạt ảnh `easeTo` và `flyTo`, khiến bản đồ bị đóng băng. [#9884](https://github.com/mapbox/mapbox-gl-js/pull/9884) (by [@andycalder](https://github.com/andycalder))
- Sửa lỗi ảnh dự phòng (fallback image) không được sử dụng nếu nó được thêm qua `addImage`. [#9911](https://github.com/mapbox/mapbox-gl-js/pull/9911) (by [@francois2metz](https://github.com/francois2metz))
- Sửa lỗi tùy chọn `promoteId` thất bại đối với fill extrusion có feature id được định nghĩa sẵn. [#9863](https://github.com/mapbox/mapbox-gl-js/pull/9863)

### 🛠️ Quy trình làm việc

- Đổi tên nhánh phát triển mặc định từ `master` thành `main`.

## 1.11.1

### 🐞 Sửa lỗi

- Sửa lỗi khiến `map.loaded()` trả về sai `false` sau một sự kiện click. ([#9825](https://github.com/mapbox/mapbox-gl-js/pull/9825))

## 1.11.0

### ✨ Tính năng và cải tiến

- Thêm tùy chọn để scale icon `Marker` mặc định.([#9414](https://github.com/mapbox/mapbox-gl-js/pull/9414)) (by [@adrianababakanian](https://github.com/adrianababakanian))
- Cải thiện tốc độ biên dịch shader bằng cách lấy thủ công (manually) các attribute và uniform tại runtime.([#9497](https://github.com/mapbox/mapbox-gl-js/pull/9497))
- Thêm tùy chọn `clusterMinPoints` cho GeoJSON source có cluster, định nghĩa số điểm tối thiểu để tạo thành một cluster.([#9748](https://github.com/mapbox/mapbox-gl-js/pull/9748))

### 🐞 Sửa lỗi

- Sửa lỗi bản đồ bị kẹt (stuck) trong tương tác DragRotate nếu sự kiện mouseup xảy ra bên ngoài cửa sổ trình duyệt hoặc iframe.([#9512](https://github.com/mapbox/mapbox-gl-js/pull/9512))
- Sửa lỗi hồi quy hiển thị (visual regression) tiềm ẩn đối với các thuộc tính `*-pattern` trên card đồ họa AMD.([#9681](https://github.com/mapbox/mapbox-gl-js/pull/9681))
- Sửa lỗi zoom bằng double tap trên iOS Safari 13.([#9757](https://github.com/mapbox/mapbox-gl-js/pull/9757))
- Loại bỏ cảnh báo gây hiểu lầm `geometry exceeds allowed extent` khi sử dụng vector tile Mapbox Streets.([#9753](https://github.com/mapbox/mapbox-gl-js/pull/9753))
- Sửa lỗi reference error khi require bundle trình duyệt (browser bundle) trong Node. ([#9749](https://github.com/mapbox/mapbox-gl-js/pull/9749))

## 1.10.2

### 🐞 Sửa lỗi

- Sửa lỗi zoom bằng double tap trên iOS Safari 13.([#9757](https://github.com/mapbox/mapbox-gl-js/pull/9757))

## 1.10.1

### 🐞 Sửa lỗi

- Sửa lỗi marker làm gián đoạn cử chỉ chạm (touch gestures) ([#9675](https://github.com/mapbox/mapbox-gl-js/issues/9675), được sửa bởi [#9683](https://github.com/mapbox/mapbox-gl-js/pull/9683))
- Sửa lỗi `map.isMoving()` trả về `true` trong khi bản đồ không di chuyển ([#9647](https://github.com/mapbox/mapbox-gl-js/issues/9647), được sửa bởi [#9679](https://github.com/mapbox/mapbox-gl-js/pull/9679))
- Sửa lỗi regression khiến sự kiện `touchmove` không được phát ra trong lúc thực hiện cử chỉ ([#9676](https://github.com/mapbox/mapbox-gl-js/issues/9676), được sửa bởi [#9685](https://github.com/mapbox/mapbox-gl-js/pull/9685))
- Sửa việc đánh giá (evaluation) biểu thức `image` bị lỗi trong một số điều kiện nhất định ([#9630](https://github.com/mapbox/mapbox-gl-js/issues/9630), được sửa bởi [#9685](https://github.com/mapbox/mapbox-gl-js/pull/9668))
- Sửa các biểu thức `within` lồng nhau trong filter đánh giá không đúng ([#9605](https://github.com/mapbox/mapbox-gl-js/issues/9605), được sửa bởi [#9611](https://github.com/mapbox/mapbox-gl-js/pull/9611))
- Sửa biến paint có thể bị `undefined` trong `StyleLayer` ([#9688](https://github.com/mapbox/mapbox-gl-js/pull/9688)) (by [mannnick24](https://github.com/mannnick24))

## 1.10.0

### ✨ Tính năng

- Thêm các phương thức `mapboxgl.prewarm()` và `mapboxgl.clearPrewarmedResources()` để cho phép nhà phát triển tối ưu thời gian tải cho bản đồ của họ ([#9391](https://github.com/mapbox/mapbox-gl-js/pull/9391))
- Thêm các biểu thức `index-of` và `slice` để tìm kiếm trong mảng và chuỗi vị trí xuất hiện đầu tiên của một giá trị xác định, và trả về một đoạn của mảng hoặc chuỗi gốc ([#9450](https://github.com/mapbox/mapbox-gl-js/pull/9450)) (by [lbutler](https://github.com/lbutler))
- Đặt đúng trạng thái RTL text plugin nếu URL của plugin không thể tải được. Điều này cho phép nhà phát triển thêm logic thử lại (retry) khi gặp lỗi mạng lúc tải plugin ([#9489](https://github.com/mapbox/mapbox-gl-js/pull/9489))

### 🍏 Cử chỉ (Gestures)

Bản phát hành này refactor và cải thiện đáng kể việc xử lý cử chỉ (gesture handling) trên desktop và mobile. Ba cử chỉ chạm mới đã được thêm vào: `two-finger swipe` để điều chỉnh pitch, `two-finger double tap` để zoom out, và `tap then drag` để điều chỉnh zoom bằng một ngón tay ([#9365](https://github.com/mapbox/mapbox-gl-js/pull/9365)). Ngoài ra, bản phát hành này còn mang lại các thay đổi và sửa lỗi sau:

- Giờ đây có thể tương tác với nhiều bản đồ trên cùng một trang cùng lúc ([#9365](https://github.com/mapbox/mapbox-gl-js/pull/9365))
- Sửa lỗi bản đồ bị giật (jump) khi thả một ngón tay sau khi pinch zoom ([#9136](https://github.com/mapbox/mapbox-gl-js/issues/9136))
- Ngăn `mousedown` và `touchstart` làm gián đoạn hoạt ảnh `easeTo` khi các interaction handler bị tắt ([#8725](https://github.com/mapbox/mapbox-gl-js/issues/8725))
- Ngăn con lăn chuột (mouse wheel) làm gián đoạn hoạt ảnh khi `map.scrollZoom` bị tắt ([#9230](https://github.com/mapbox/mapbox-gl-js/issues/9230))
- Việc thay đổi camera không còn có thể bị ngăn lại bằng cách tắt interaction handler bên trong sự kiện thay đổi camera. Hãy ngăn các thay đổi camera một cách có chọn lọc bằng cách lắng nghe sự kiện `mousedown` hoặc `touchstart` của map và gọi [.preventDefault()](https://docs.mapbox.com/mapbox-gl-js/api/#mapmouseevent#preventdefault) ([#9365](https://github.com/mapbox/mapbox-gl-js/pull/9365))
- Các thuộc tính chưa được ghi trong tài liệu (undocumented) trên sự kiện thay đổi camera được phát ra bởi handler doubleClickZoom đã bị loại bỏ ([#9365](https://github.com/mapbox/mapbox-gl-js/pull/9365))

### 🐞 Cải tiến và sửa lỗi

- Nhãn trên đường (line labels) giờ có cơ chế phát hiện va chạm (collision detection) được cải thiện, với độ chính xác vị trí cao hơn, giảm dung lượng bộ nhớ sử dụng (memory footprint), và định vị tốt hơn khi camera bị nghiêng (pitched) ([#9219](https://github.com/mapbox/mapbox-gl-js/pull/9219))
- Sửa lỗi `GlyphManager` liên tục gửi lại request cho các dải glyph (glyph ranges) còn thiếu ([#8027](https://github.com/mapbox/mapbox-gl-js/issues/8027), được sửa bởi [#9375](https://github.com/mapbox/mapbox-gl-js/pull/9375)) (by [oterral](https://github.com/oterral))
- Tránh ném lỗi khi gọi một số phương thức popup trước khi phần tử popup được tạo ([#9433](https://github.com/mapbox/mapbox-gl-js/pull/9433))
- Sửa lỗi các feature fill-extrusion có điểm thẳng hàng (colinear points) không được trả về bởi `map.queryRenderedFeatures(...)` ([#9454](https://github.com/mapbox/mapbox-gl-js/pull/9454))
- Sửa lỗi sử dụng feature state trên đầu vào lớn có thể gây ra lỗi tràn stack (stack overflow) ([#9463](https://github.com/mapbox/mapbox-gl-js/pull/9463))
- Sửa lỗi exception khi sử dụng `background-pattern` với biểu thức data-driven ([#9518](https://github.com/mapbox/mapbox-gl-js/issues/9518), được sửa bởi [#9520](https://github.com/mapbox/mapbox-gl-js/pull/9520))
- Sửa lỗi UI popup có khả năng làm rò rỉ (leaking) event listener ([#9498](https://github.com/mapbox/mapbox-gl-js/pull/9498)) (by [mbell697](https://github.com/mbell697))
- Sửa lỗi biểu thức `within` trả về giá trị không nhất quán đối với các điểm nằm trên ranh giới tile (tile boundaries) ([#9411](https://github.com/mapbox/mapbox-gl-js/issues/9411), [#9428](https://github.com/mapbox/mapbox-gl-js/pull/9428))
- Sửa lỗi biểu thức `within` đánh giá không đúng đối với geometry vượt qua đường đổi ngày (antimeridian) ([#9440](https://github.com/mapbox/mapbox-gl-js/pull/9440))
- Sửa lỗi exception có thể xảy ra do biến paint của style layer bị `undefined` ([#9437](https://github.com/mapbox/mapbox-gl-js/pull/9437)) (by [mannnick24](https://github.com/mannnick24))
- Nâng cấp minimist lên ^1.2.5 để nhận bản sửa lỗi cho vấn đề bảo mật [CVE-2020-7598](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-7598) từ upstream ([#9425](https://github.com/mapbox/mapbox-gl-js/issues/9431), được sửa bởi [#9425](https://github.com/mapbox/mapbox-gl-js/pull/9425)) (by [watson](https://github.com/watson))

## 1.9.1

### 🐞 Sửa lỗi

- Sửa lỗi [#9477](https://github.com/mapbox/mapbox-gl-js/issues/9477) trong `Map#fitBounds(..)` khiến `padding` được truyền vào options bị áp dụng hai lần.
- Sửa lỗi render [#9479](https://github.com/mapbox/mapbox-gl-js/issues/9479) xảy ra khi các thuộc tính `*-pattern` data-driven tham chiếu đến ảnh được thêm bằng `Map#addImage(..)`.
- Sửa lỗi [#9468](https://github.com/mapbox/mapbox-gl-js/issues/9468) khiến một exception bị ném ra khi cập nhật thuộc tính paint của symbol layer bằng `setPaintProperty`.
## 1.9.0

Với bản phát hành này, chúng tôi bổ sung [một chính sách changelog mới](./CONTRIBUTING.md#changelog-conventions) vào hướng dẫn đóng góp của mình.

Bản phát hành này cũng sửa một số lỗi tồn tại lâu ngày và hành vi render không mong muốn với `line-pattern`. Các bản sửa lỗi đi kèm với một thay đổi trực quan về cách các pattern được thêm bằng `line-pattern` được scale (thu phóng). Trước đây, các pattern lớn hơn đường line sẽ bị cắt (clip), đôi khi làm biến dạng pattern, đặc biệt trên thiết bị di động và màn hình retina. Giờ đây pattern sẽ được scale để vừa khít trong mọi trường hợp. [#9266](https://github.com/mapbox/mapbox-gl-js/pull/9266) trình bày các ví dụ về sự khác biệt trực quan này. Để biết thêm thông tin và góp ý về thay đổi này, xem [#9394](https://github.com/mapbox/mapbox-gl-js/pull/9394).

### ✨ Tính năng

- Thêm biểu thức `within` để kiểm tra xem một feature đã được đánh giá có nằm trong một đối tượng GeoJSON cho trước hay không ([#9352](https://github.com/mapbox/mapbox-gl-js/pull/9352)). - Chúng tôi biết về một trường hợp biên trong đó các điểm có tọa độ bị wrap (ví dụ kinh độ -185) không được đánh giá đúng. Xem ([#9442](https://github.com/mapbox/mapbox-gl-js/issues/9442)) để biết thêm thông tin. - Một ví dụ về biểu thức `within`:<br> `"icon-opacity": ["case", ["==", ["within", "some-polygon"], true], 1,
["==", ["within", "some-polygon"], false], 0]`
- Các hàm API Map như `easeTo` và `flyTo` giờ đây hỗ trợ `padding: PaddingOptions` cho phép nhà phát triển dịch chuyển tâm phối cảnh của bản đồ khi xây dựng sidebar nổi ([#8638](https://github.com/mapbox/mapbox-gl-js/pull/8638))

### 🍏 Cải tiến

- Kết quả từ `queryRenderedFeatures` giờ đây có các giá trị thuộc tính đã được đánh giá thay vì các biểu thức thô ([#9198](https://github.com/mapbox/mapbox-gl-js/pull/9198))
- Cải thiện việc scale các pattern dùng trong `line-pattern` trên mọi độ phân giải thiết bị và tỷ lệ pixel ([#9266](https://github.com/mapbox/mapbox-gl-js/pull/9266))
- Cải thiện nhẹ mức sử dụng bộ nhớ GPU ([#9377](https://github.com/mapbox/mapbox-gl-js/pull/9377))
- `LngLatBounds.extend` linh hoạt hơn vì giờ nó chấp nhận cả object có thuộc tính `lat` và `lon` cũng như mảng tọa độ ([#9293](https://github.com/mapbox/mapbox-gl-js/pull/9293))
- Giảm kích thước bundle và cải thiện chất lượng trực quan của text debug `showTileBoundaries` ([#9267](https://github.com/mapbox/mapbox-gl-js/pull/9267))

### 🐞 Sửa lỗi

- Điều chỉnh đúng các pattern được thêm bằng `addImage(id, image, pixelRatio)` theo tỷ lệ pixel của asset, không phải tỷ lệ pixel của thiết bị ([#9372](https://github.com/mapbox/mapbox-gl-js/pull/9372))
- Cho phép tham số needle của biểu thức `in` là false ([#9295](https://github.com/mapbox/mapbox-gl-js/pull/9295))
- Sửa lỗi ngoại lệ (exception) khi cố gắng đặt `feature-state` cho một layer đã bị xóa, sửa [#8634](https://github.com/mapbox/mapbox-gl-js/issues/8634) ([#9305](https://github.com/mapbox/mapbox-gl-js/pull/9305))
- Sửa lỗi bản đồ không hiển thị bên trong các phần tử có `dir=rtl` ([#9332](https://github.com/mapbox/mapbox-gl-js/pull/9332))
- Sửa lỗi render đối với các phiên bản Chrome rất cũ (khoảng 2016) khiến chữ hiển thị lớn hơn nhiều so với dự định ([#9349](https://github.com/mapbox/mapbox-gl-js/pull/9349))
- Ngăn ngoại lệ phát sinh từ `line-dash-array` có độ dài rỗng ([#9385](https://github.com/mapbox/mapbox-gl-js/pull/9385))
- Sửa lỗi biểu thức `icon-image` khi được đánh giá thành chuỗi rỗng (`''`) sẽ tạo ra cảnh báo ([#9380](https://github.com/mapbox/mapbox-gl-js/pull/9380))
- Sửa lỗi một số phương thức `popup` ném ra lỗi khi truy cập phần tử container trước khi nó được tạo, sửa [#9429](https://github.com/mapbox/mapbox-gl-js/issues/9429)([#9433](https://github.com/mapbox/mapbox-gl-js/pull/9433))

## 1.8.1

- Đã sửa lỗi tất cả các nhãn hiển thị theo một đường chéo trên Windows khi dùng GPU Intel tích hợp thế hệ Haswell ([#9327](https://github.com/mapbox/mapbox-gl-js/issues/9327), sửa bằng cách revert [#9229](https://github.com/mapbox/mapbox-gl-js/pull/9229))

## 1.8.0

### ✨ Tính năng và cải tiến

- Giảm kích thước line atlas bằng cách loại bỏ các kênh không sử dụng ([#9232](https://github.com/mapbox/mapbox-gl-js/pull/9232))
- Ngăn tạo các buffer rỗng cho dữ liệu debug khi không sử dụng ([#9237](https://github.com/mapbox/mapbox-gl-js/pull/9237))
- Thêm khoảng trắng giữa khoảng cách và đơn vị trong scale control ([#9276](https://github.com/mapbox/mapbox-gl-js/pull/9276)) (bởi [gely](https://api.github.com/users/gely)) và ([#9284](https://github.com/mapbox/mapbox-gl-js/pull/9284)) (bởi [pakastin](https://api.github.com/users/pakastin))
- Thêm tùy chọn `showAccuracyCircle` cho GeolocateControl để hiển thị độ chính xác của vị trí người dùng dưới dạng hình tròn trong suốt. Mapbox GL JS sẽ hiển thị hình tròn này theo mặc định. ([#9253](https://github.com/mapbox/mapbox-gl-js/pull/9253)) (bởi [Meekohi](https://api.github.com/users/Meekohi))
- Triển khai một thuật toán tile coverage mới để hỗ trợ level-of-detail trong bản phát hành tương lai ([#8975](https://github.com/mapbox/mapbox-gl-js/pull/8975))

### 🐞 Sửa lỗi

- `line-dasharray` giờ đây được bỏ qua đúng cách khi `line-pattern` được thiết lập ([#9189](https://github.com/mapbox/mapbox-gl-js/pull/9189))
- Sửa lỗi line distances làm hỏng gradient qua ranh giới tile ([#9220](https://github.com/mapbox/mapbox-gl-js/pull/9220))
- Sửa lỗi các đường line có điểm cuối trùng nhau có thể biến mất ở zoom 18+ ([#9218](https://github.com/mapbox/mapbox-gl-js/pull/9218))
- Sửa lỗi Ctrl-click để kéo xoay bản đồ bị vô hiệu hóa nếu phím Alt, Cmd hoặc Windows cũng được nhấn ([#9203](https://github.com/mapbox/mapbox-gl-js/pull/9203))
- Truyền lỗi vào callback của `getClusterExpansionZoom`, `getClusterChildren`, và `getClusterLeaves` ([#9251](https://github.com/mapbox/mapbox-gl-js/pull/9251))
- Sửa hồi quy (regression) về hiệu năng render ([#9261](https://github.com/mapbox/mapbox-gl-js/pull/9261))
- Sửa lỗi hiển thị (artifact) trực quan cho `line-dasharray` ([#9246](https://github.com/mapbox/mapbox-gl-js/pull/9246))
- Đã sửa lỗi trong GeolocateControl dẫn đến lỗi khi `trackUserLocation` là `false` và control bị xóa trước khi Geolocation API trả về vị trí ([#9291](https://github.com/mapbox/mapbox-gl-js/pull/9291))
- Sửa `promoteId` cho các layer line ([#9210](https://github.com/mapbox/mapbox-gl-js/pull/9210))
- Cải thiện độ chính xác của các phép tính khoảng cách ([#9202](https://github.com/mapbox/mapbox-gl-js/pull/9202)) (bởi [Meekohi](https://api.github.com/users/Meekohi))

## 1.7.0

### ✨ Tính năng

- Thêm tùy chọn `promoteId` để dùng một thuộc tính feature làm ID cho feature state ([#8987](https://github.com/mapbox/mapbox-gl-js/pull/8987))
- Thêm tùy chọn constructor mới cho `mapboxgl.Popup`, `closeOnMove`, giúp đóng popup khi vị trí bản đồ thay đổi ([#9163](https://github.com/mapbox/mapbox-gl-js/pull/9163))
- Cho phép tạo bản đồ không cần style (một style rỗng sẽ được tự động tạo) (bởi [@stepankuzmin](https://github.com/stepankuzmin)) ([#8924](https://github.com/mapbox/mapbox-gl-js/pull/8924))
- `map.once()` giờ đây cho phép chỉ định layer id làm tham số thứ ba, nhất quán với `map.on()` ([#8875](https://github.com/mapbox/mapbox-gl-js/pull/8875))

### 🍏 Cải tiến

- Cải thiện hiệu năng của các layer raster trên màn hình lớn ([#9050](https://github.com/mapbox/mapbox-gl-js/pull/9050))
- Cải thiện hiệu năng cho hillshade và raster layer bằng cách triển khai cải tiến tiệm tiến sử dụng `ImageBitmap` và `OffscreenCanvas` ([#8845](https://github.com/mapbox/mapbox-gl-js/pull/8845))
- Cải thiện hiệu năng render tile raster bằng cách dùng stencil buffer ([#9012](https://github.com/mapbox/mapbox-gl-js/pull/9012))
- Cập nhật tài liệu `symbol-avoid-edges` để công nhận sự tồn tại của global collision detection ([#9157](https://github.com/mapbox/mapbox-gl-js/pull/9157))
- Loại bỏ tham chiếu đến hàm `in` đã được thay thế bằng biểu thức `in` ([#9102](https://github.com/mapbox/mapbox-gl-js/pull/9102))

### 🐞 Sửa lỗi

- Đổi kiểu của khóa tile id thành string để tránh xung đột hash ([#8979](https://github.com/mapbox/mapbox-gl-js/pull/8979))
- Ngăn việc thay đổi bearing qua URL hash khi rotation bị vô hiệu hóa ([#9156](https://github.com/mapbox/mapbox-gl-js/pull/9156))
- Sửa lỗi URL hash không có bearing khiến bản đồ tải thất bại ([#9170](https://github.com/mapbox/mapbox-gl-js/pull/9170))
- Sửa lỗi trong `GeolocateControl` khi có nhiều instance của control trên một trang có thể khiến vị trí người dùng không được cập nhật ([#9092](https://github.com/mapbox/mapbox-gl-js/pull/9092))
- Sửa lỗi truy vấn `fill-extrusions` được tạo từ các polygon có điểm trùng nhau và polygon có ít hơn bốn điểm ([#9138](https://github.com/mapbox/mapbox-gl-js/pull/9138))
- Sửa lỗi `symbol-sort-key` không được dùng cho các va chạm (collision) xảy ra qua ranh giới tile ([#9054](https://github.com/mapbox/mapbox-gl-js/pull/9054))
- Sửa lỗi trong `DragRotateHandler._onMouseUp` bị kẹt trong trạng thái kéo/xoay ([#9137](https://github.com/mapbox/mapbox-gl-js/pull/9137))
- Sửa "Click on Compass" trên một số thiết bị di động (thêm `clickTolerance` vào `DragRotateHandler`) ([#9015](https://github.com/mapbox/mapbox-gl-js/pull/9015)) (bởi [Yanonix](https://github.com/Yanonix))

## 1.6.1

### 🐞 Sửa lỗi

- Sửa lỗi thông báo lỗi xác thực style không hiển thị ([#9073](https://github.com/mapbox/mapbox-gl-js/pull/9073))
- Sửa lỗi tải trễ (deferred loading) của rtl-text-plugin không hoạt động với các nhãn được tạo từ nguồn GeoJSON ([#9091](https://github.com/mapbox/mapbox-gl-js/pull/9091))
- Sửa lỗi text RTL không được render bằng rtl-text-plugin trên các trang không cho phép `script-src: blob:` trong CSP của họ.([#9122](https://github.com/mapbox/mapbox-gl-js/pull/9122))

## 1.6.0

### ✨ Tính năng

- Thêm khả năng chèn hình ảnh vào nhãn text bằng biểu thức `image` bên trong biểu thức `format`: `"text-field": ["format", "Some text", ["image", "my-image"], "some more text"]` ([#8904](https://github.com/mapbox/mapbox-gl-js/pull/8904))
- Thêm hỗ trợ cho ảnh có thể co giãn (stretchable images, còn gọi là nine-part hoặc nine-patch images). Các ảnh có thể co giãn có thể dùng với `icon-text-fit` để vẽ ảnh được resize với các góc và viền không bị kéo giãn. ([#8997](https://github.com/mapbox/mapbox-gl-js/pull/8997))
- Thêm biểu thức `in`. Nó có thể kiểm tra một giá trị có nằm trong mảng (`["in", value, array]`) hoặc một chuỗi con có nằm trong chuỗi (`["in", substring, string]`) ([#8876](https://github.com/mapbox/mapbox-gl-js/pull/8876))
- Thêm tùy chọn map `minPitch` và `maxPitch` ([#8834](https://github.com/mapbox/mapbox-gl-js/pull/8834))
- Thêm tùy chọn `rotation`, `rotationAlignment` và `pitchAlignment` cho marker ([#8836](https://github.com/mapbox/mapbox-gl-js/pull/8836)) (bởi [@dburnsii](https://github.com/dburnsii))
- Thêm các phương thức cho Popup để thao tác tên class của container ([#8759](https://github.com/mapbox/mapbox-gl-js/pull/8759)) (bởi [Ashot-KR](https://github.com/Ashot-KR))
- Thêm cài đặt inertia (quán tính) có thể cấu hình cho panning (bởi [@aMoniker](https://github.com/aMoniker))) ([#8887](https://github.com/mapbox/mapbox-gl-js/pull/8887))
- Thêm khả năng bản địa hóa (localize) các UI control ([#8095](https://github.com/mapbox/mapbox-gl-js/pull/8095)) (bởi [@dmytro-gokun](https://github.com/dmytro-gokun))
- Thêm phương thức LatLngBounds.contains() ([#7512](https://github.com/mapbox/mapbox-gl-js/issues/7512), sửa bằng [#8200](https://github.com/mapbox/mapbox-gl-js/pull/8200))
- Thêm tùy chọn tải rtl-text-plugin theo kiểu lazy (trễ khi cần) ([#8865](https://github.com/mapbox/mapbox-gl-js/pull/8865))
- Thêm tham số `essential` vào AnimationOptions có thể ghi đè `prefers-reduced-motion: reduce` ([#8743](https://github.com/mapbox/mapbox-gl-js/issues/8743), sửa bằng [#8883](https://github.com/mapbox/mapbox-gl-js/pull/8883))

### 🍏 Cải tiến

- Cho phép render toàn bộ world nhỏ hơn 512px. Để khôi phục giới hạn trước đó, gọi `map.setMinZoom(0)` ([#9028](https://github.com/mapbox/mapbox-gl-js/pull/9028))
- Thêm bản build es modules cho mapbox-gl-style-spec trong dist/ ([#8247](https://github.com/mapbox/mapbox-gl-js/pull/8247)) (bởi [@ahocevar](https://github.com/ahocevar))
- Thêm header accept 'image/webp,_/_' vào các request fetch/ajax ảnh khi webp được hỗ trợ ([#8262](https://github.com/mapbox/mapbox-gl-js/pull/8262))
- Cải thiện tài liệu cho setStyle, getStyle, và isStyleLoaded ([#8807](https://github.com/mapbox/mapbox-gl-js/pull/8807))

### 🐞 Sửa lỗi

- Sửa lỗi render bản đồ sau khi addImage và removeImage được dùng để thay đổi một ảnh đang được sử dụng ([#9016](https://github.com/mapbox/mapbox-gl-js/pull/9016))
- Sửa lỗi hiển thị của control trong chế độ High Contrast trên IE ([#8874](https://github.com/mapbox/mapbox-gl-js/pull/8874))
- Sửa lỗi customizable url hash string trên IE 11 ([#8990](https://github.com/mapbox/mapbox-gl-js/pull/8990)) (bởi [pakastin](https://github.com/pakastin))
- Cho phép expression stops lên đến zoom 24 thay vì 22 ([#8908](https://github.com/mapbox/mapbox-gl-js/pull/8908)) (bởi [nicholas-l](https://github.com/nicholas-l))
- Sửa lỗi căn chỉnh (alignment) của các line trong các tile bị overscale nặng ([#9024](https://github.com/mapbox/mapbox-gl-js/pull/9024))
- Sửa lỗi `Failed to execute 'shaderSource' on 'WebGLRenderingContext'` ([#9017](https://github.com/mapbox/mapbox-gl-js/pull/9017))
- Khiến việc xác thực biểu thức thất bại khi gặp NaN ([#8615](https://github.com/mapbox/mapbox-gl-js/pull/8615))
- Sửa lỗi setLayerZoomRange khiến tile bị yêu cầu lại ([#7865](https://github.com/mapbox/mapbox-gl-js/issues/7865), sửa bằng [#8854](https://github.com/mapbox/mapbox-gl-js/pull/8854))
- Sửa lỗi render `map.showTileBoundaries` ([#7314](https://github.com/mapbox/mapbox-gl-js/pull/7314))
- Sửa lỗi khi dùng `generateId` kết hợp với `cluster` trong GeoJSONSource ([#8223](https://github.com/mapbox/mapbox-gl-js/issues/8223), sửa bằng [#8945](https://github.com/mapbox/mapbox-gl-js/pull/8945))
- Sửa lỗi mở popup trên marker từ bàn phím ([#6835](https://github.com/mapbox/mapbox-gl-js/pull/6835))
- Sửa lỗi khi request bị hủy (aborted) ([#7614](https://github.com/mapbox/mapbox-gl-js/issues/7614), sửa bằng [#9021](https://github.com/mapbox/mapbox-gl-js/pull/9021))
- Sửa lỗi attribution control khi liên tục xóa và thêm lại ([#9052](https://github.com/mapbox/mapbox-gl-js/pull/9052))

## 1.5.1

Bản vá này giới thiệu hai giải pháp tạm thời (workaround) giải quyết các vấn đề tồn tại lâu dài liên quan đến tăng trưởng bộ nhớ không giới hạn trên Safari, bao gồm [#8771](https://github.com/mapbox/mapbox-gl-js/issues/8771) và [#4695](https://github.com/mapbox/mapbox-gl-js/issues/4695). Chúng tôi đã xác định hai rò rỉ bộ nhớ trên Safari: một trong API [CacheStorage](https://developer.mozilla.org/en-US/docs/Web/API/CacheStorage), được giải quyết bởi [#8956](https://github.com/mapbox/mapbox-gl-js/pull/8956), và một trong việc truyền dữ liệu giữa các web worker thông qua [Transferables](https://developer.mozilla.org/en-US/docs/Web/API/Transferable), được giải quyết bởi [#9003](https://github.com/mapbox/mapbox-gl-js/pull/9003).

### 🍏 Cải tiến

- Triển khai giải pháp tạm thời cho rò rỉ bộ nhớ trên Safari khi dùng API `CacheStorage`. ([#8856](https://github.com/mapbox/mapbox-gl-js/pull/8956))
- Triển khai giải pháp tạm thời cho rò rỉ bộ nhớ trên Safari khi dùng đối tượng `Transferable` để truyền `ArrayBuffers` đến WebWorker. Nếu GL-JS phát hiện đang chạy trên Safari, việc dùng `Transferables` để truyền dữ liệu đến WebWorker sẽ bị vô hiệu hóa. ([#9003](https://github.com/mapbox/mapbox-gl-js/pull/9003))
- Cải thiện hiệu năng animation khi dùng `map.setData`. ([#8913](https://github.com/mapbox/mapbox-gl-js/pull/8913)) (bởi [msbarry](https://github.com/msbarry))

## 1.5.0

### ✨ Tính năng

- Thêm icon vô hiệu hóa (disabled) cho GeolocateControl nếu người dùng từ chối quyền geolocation. [#8871](https://github.com/mapbox/mapbox-gl-js/pull/8871))
- Thêm sự kiện `outofmaxbounds` cho GeolocateControl, được phát ra khi người dùng nằm ngoài `map.maxBounds` ([#8756](https://github.com/mapbox/mapbox-gl-js/pull/8756)) (bởi [MoradiDavijani](https://github.com/MoradiDavijani))
- Thêm `mapboxgl.getRTLTextPluginStatus()` để truy vấn trạng thái hiện tại của `rtl-text-plugin`, giúp việc xóa plugin khi cần dễ dàng hơn. (tham chiếu [#7869](https://github.com/mapbox/mapbox-gl-js/issues/7869)) ([#8864](https://github.com/mapbox/mapbox-gl-js/pull/8864))
- Cho phép tùy chọn Map `hash` được đặt dưới dạng chuỗi, giúp đặt hash bản đồ trong url thành một query parameter tùy chỉnh. ([#8603](https://github.com/mapbox/mapbox-gl-js/pull/8603)) (bởi [SebCorbin](https://github.com/SebCorbin))

### 🍏 Cải tiến

- Mờ dần (fade) symbol nhanh hơn khi zoom out nhanh, giảm chồng chéo. ([#8628](https://github.com/mapbox/mapbox-gl-js/pull/8628))
- Giảm mức sử dụng bộ nhớ cho vector tile chứa chuỗi dài trong thuộc tính feature. ([#8863](https://github.com/mapbox/mapbox-gl-js/pull/8863))

### 🐞 Sửa lỗi

- Sửa lỗi `text-variable-anchor` không thử nhiều vị trí đặt (placement) khi va chạm với icon lúc `icon-text-fit` được bật. ([#8803](https://github.com/mapbox/mapbox-gl-js/pull/8803))
- Sửa lỗi `icon-text-fit` không tôn trọng đúng nhãn theo chiều dọc. ([#8835](https://github.com/mapbox/mapbox-gl-js/pull/8835))
- Sửa lỗi nội suy opacity cho các biểu thức tổng hợp (composition expressions). ([#8818](https://github.com/mapbox/mapbox-gl-js/pull/8818))
- Sửa lỗi sự kiện rotate và pitch được phát ra cùng lúc. ([#8872](https://github.com/mapbox/mapbox-gl-js/pull/8872))
- Sửa các rò rỉ bộ nhớ xảy ra trong quá trình tải tile và gỡ bản đồ.([#8813](https://github.com/mapbox/mapbox-gl-js/pull/8813) và [#8850](https://github.com/mapbox/mapbox-gl-js/pull/8850))
- Sửa lỗi truyền `ArrayBuffers` qua web-worker trong các môi trường mà `instanceof ArrayBuffer` thất bại (ví dụ `cypress`) ([#8868](https://github.com/mapbox/mapbox-gl-js/pull/8868))

## 1.4.1

### 🐞 Sửa lỗi

- Sửa cách `coalesce` xử lý toán tử `image` để các ảnh khả dụng được render đúng cách ([#8839](https://github.com/mapbox/mapbox-gl-js/pull/8839))
- Không phát sự kiện `styleimagemissing` với giá trị chuỗi rỗng ([#8840](https://github.com/mapbox/mapbox-gl-js/pull/8840))
- Sửa lỗi serialize kiểu `ResolvedImage` để các thuộc tính `*-pattern` hoạt động đúng ([#8833](https://github.com/mapbox/mapbox-gl-js/pull/8833))

## 1.4.0

### ✨ Tính năng

- Thêm toán tử biểu thức `image` để xác định tình trạng khả dụng của ảnh ([#8684](https://github.com/mapbox/mapbox-gl-js/pull/8684))
- Bật `text-offset` với vị trí đặt nhãn linh động (variable label placement) ([#8642](https://github.com/mapbox/mapbox-gl-js/pull/8642))

### 🍏 Cải tiến

- Tải nhanh hơn và giao diện đẹp hơn cho raster terrain ([#8694](https://github.com/mapbox/mapbox-gl-js/pull/8694))
- Cải thiện tài liệu code xung quanh việc resize và {get/set}RenderedWorldCopies và hơn thế ([#8748](https://github.com/mapbox/mapbox-gl-js/pull/8748), [#8754](https://github.com/mapbox/mapbox-gl-js/pull/8754))
- Cải thiện tương tác zoom & pan đơn chạm so với đa chạm ([#7196](https://github.com/mapbox/mapbox-gl-js/issues/7196)) ([#8100](https://github.com/mapbox/mapbox-gl-js/pull/8100))

### 🐞 Sửa lỗi

- Sửa lỗi render `collisionBox` khi `text-translate` hoặc `icon-translate` được bật ([#8659](https://github.com/mapbox/mapbox-gl-js/pull/8659))
- Sửa lỗi `TypeError` khi reload một source và ngay lập tức xóa bản đồ ([#8711](https://github.com/mapbox/mapbox-gl-js/pull/8711))
- Thêm tooltip vào nút geolocation control ([#8735](https://github.com/mapbox/mapbox-gl-js/pull/8735)) (bởi [BAByrne](https://github.com/BAByrne))
- Thêm thuộc tính `originalEvent` vào các sự kiện NavigationControl ([#8693](https://github.com/mapbox/mapbox-gl-js/pull/8693)) (bởi [stepankuzmin](https://github.com/stepankuzmin))
- Không hủy chế độ follow trong GeolocateControl khi resize bản đồ hoặc xoay màn hình ([#8736](https://github.com/mapbox/mapbox-gl-js/pull/8736))
- Sửa lỗi khi gọi `Popup#trackPointer` trước khi thiết lập nội dung hoặc vị trí ([#8757](https://github.com/mapbox/mapbox-gl-js/pull/8757)) (bởi [zxwandrew](https://github.com/zxwandrew))
- Tôn trọng ký tự xuống dòng khi text-max-width được đặt bằng 0 ([#8706](https://github.com/mapbox/mapbox-gl-js/pull/8706))
- Cập nhật earcut lên v2.2.0 để sửa các lỗi tessellation polygon ([#8772](https://github.com/mapbox/mapbox-gl-js/pull/8772))
- Sửa icon-fit với variable label placement ([#8755](https://github.com/mapbox/mapbox-gl-js/pull/8755))
- Các icon được co giãn bằng `icon-text-fit` giờ đây được định kích thước đúng ([#8741](https://github.com/mapbox/mapbox-gl-js/pull/8741))
- Collision detection cho icon với `icon-text-fit` giờ đây hoạt động đúng ([#8741](https://github.com/mapbox/mapbox-gl-js/pull/8741))

## 1.3.2

- Sửa lỗi SecurityError trên Firefox >= 69 khi truy cập cache [#8780](https://github.com/mapbox/mapbox-gl-js/pull/8780)

## 1.3.1

### 🐞 Sửa lỗi

- Sửa một race condition tạo ra lỗi khi bản đồ bị xóa trong lúc đang reload một source. [#8711](https://github.com/mapbox/mapbox-gl-js/pull/8711)
- Sửa một race condition khiến sự kiện `render` đôi khi không được phát sau sự kiện `load` trên IE11. [#8708](https://github.com/mapbox/mapbox-gl-js/pull/8708)

## 1.3.0

### 🍏 Tính năng

- Giới thiệu thuộc tính symbol layer `text-writing-mode` cho phép đặt nhãn điểm theo chiều dọc. [#8399](https://github.com/mapbox/mapbox-gl-js/pull/8399)
- Mở rộng variable text placement để hoạt động khi `text/icon-allow-overlap` được đặt là `true`. [#8620](https://github.com/mapbox/mapbox-gl-js/pull/8620)
- Cho phép dùng `text-color` trong các biểu thức định dạng (formatted expressions) để có thể vẽ các phần khác nhau của một nhãn bằng các màu khác nhau. [#8068](https://github.com/mapbox/mapbox-gl-js/pull/8068)

### ✨ Cải tiến

- Cải thiện logic tải tile để hủy request quyết liệt hơn, cải thiện hiệu năng khi zoom hoặc pan nhanh. [#8633](https://github.com/mapbox/mapbox-gl-js/pull/8633)
- Hiển thị viền (outline) trên các nút control khi được focus (ví dụ bằng phím tab) để cải thiện khả năng tiếp cận (accessibility). [#8520](https://github.com/mapbox/mapbox-gl-js/pull/8520)
- Cải thiện hình dạng của các round join của line. [#8275](https://github.com/mapbox/mapbox-gl-js/pull/8275)
- Cải thiện hiệu năng xử lý line layer. [#8303](https://github.com/mapbox/mapbox-gl-js/pull/8303)
- Cải thiện độ rõ ràng của thông tin hiển thị với `map.showTileBoundaries = true`. [#8380](https://github.com/mapbox/mapbox-gl-js/pull/8380) (bởi [@andrewharvey](https://github.com/andrewharvey))
- Thêm phương thức `MercatorCoordinate.meterInMercatorCoordinateUnits` để dễ dàng chuyển đổi từ đơn vị mét sang giá trị tọa độ dùng trong custom layer. [#8524](https://github.com/mapbox/mapbox-gl-js/pull/8524) (bởi [@andrewharvey](https://github.com/andrewharvey))
- Cải thiện việc chuyển đổi các filter kiểu cũ (legacy) có giá trị trùng lặp. [#8542](https://github.com/mapbox/mapbox-gl-js/pull/8542)
- Chuyển mã nguồn website tài liệu & ví dụ sang một repo `mapbox-gl-js-docs` riêng biệt. [#8582](https://github.com/mapbox/mapbox-gl-js/pull/8582)

### 🐞 Sửa lỗi

- Sửa lỗi các font CJK cục bộ (local) sẽ chuyển sang font do server tạo trong các tile bị overzoom. [#8657](https://github.com/mapbox/mapbox-gl-js/pull/8657)
- Sửa các vấn đề về độ chính xác trong các custom layer dùng [deck.gl](https://deck.gl). [#8502](https://github.com/mapbox/mapbox-gl-js/pull/8502)
- Sửa lỗi fill và line layer không render đúng khi nằm trên fill extrusion đến từ cùng một source. [#8661](https://github.com/mapbox/mapbox-gl-js/pull/8661)
- Sửa lỗi tải bản đồ cho các document được tải từ Blob URLs. [#8612](https://github.com/mapbox/mapbox-gl-js/pull/8612)
- Sửa lỗi phân loại các URL file:// tương đối khi ở trong document được tải từ file URL. [#8612](https://github.com/mapbox/mapbox-gl-js/pull/8612)
- Loại bỏ `esm` khỏi `dependencies` của package (để nó không được cài khi chạy `npm install mapbox-gl`). [#8586](https://github.com/mapbox/mapbox-gl-js/pull/8586) (bởi [@DatGreekChick](https://github.com/DatGreekChick))

## 1.2.1

### 🐞 Sửa lỗi

- Sửa lỗi trong nút compass của `NavigationControl` khiến nó không xoay theo bản đồ ([#8605](https://github.com/mapbox/mapbox-gl-js/pull/8605))

## 1.2.0

### Tính năng và cải tiến

- Thêm thuộc tính layout `*-sort-key` cho các layer circle, fill, và line, để quy định feature nào xuất hiện phía trên feature khác trong cùng một layer([#8467](https://github.com/mapbox/mapbox-gl-js/pull/8467))
- Thêm khả năng khởi tạo bản đồ với access token cụ thể ([#8364](https://github.com/mapbox/mapbox-gl-js/pull/8364))
- Đáp ứng cài đặt `prefers-reduced-motion` của trình duyệt ([#8494](https://github.com/mapbox/mapbox-gl-js/pull/8494))
- Thêm tùy chọn Map `visualizePitch` làm nghiêng la bàn (compass) theo pitch của bản đồ ([#8208](https://github.com/mapbox/mapbox-gl-js/issues/8208), sửa bằng [#8296](https://github.com/mapbox/mapbox-gl-js/pull/8296)) (bởi [pakastin](https://github.com/pakastin))
- Cho phép tùy chọn source được ưu tiên hơn TileJSON ([#8232](https://github.com/mapbox/mapbox-gl-js/pull/8232)) (bởi [jingsam](https://github.com/jingsam))
- Làm cho yêu cầu về thuộc tính text offset chính xác hơn ([#8418](https://github.com/mapbox/mapbox-gl-js/pull/8418))
- Expose API `convertFilter` trong style specification ([#8493](https://github.com/mapbox/mapbox-gl-js/pull/8493)

### Sửa lỗi

- Sửa các thay đổi đối với `text-variable-anchor`, sao cho vị trí anchor trước đó chỉ được ưu tiên nếu chúng có mặt trong mảng đã cập nhật (được coi là sửa lỗi, nhưng về mặt kỹ thuật là một thay đổi phá vỡ tương thích so với hành vi trước đó) ([#8473](https://github.com/mapbox/mapbox-gl-js/pull/8473))
- Sửa lỗi render các layer thuộc opaque pass đè lên các layer heatmap và fill-extrusion ([#8440](https://github.com/mapbox/mapbox-gl-js/pull/8440))
- Sửa lỗi render đường thẳng đứng thừa (extraneous) trong vector tile ([#8477](https://github.com/mapbox/mapbox-gl-js/issues/8477), sửa bằng [#8479](https://github.com/mapbox/mapbox-gl-js/pull/8479))
- Tắt các listener sự kiện 'move' khi xóa một marker ([#8465](https://github.com/mapbox/mapbox-gl-js/pull/8465))
- Sửa lỗi toggle class trên navigation control trên IE ([#8495](https://github.com/mapbox/mapbox-gl-js/pull/8495)) (bởi [@cs09g](https://github.com/cs09g))
- Sửa lỗi background bị xoay khi hover trên geolocate control ([#8367](https://github.com/mapbox/mapbox-gl-js/pull/8367)) (bởi [GuillaumeGomez](https://github.com/GuillaumeGomez))
- Sửa lỗi trong các sự kiện click trên marker khi `startPos` không được định nghĩa ([#8462](https://github.com/mapbox/mapbox-gl-js/pull/8462)) (bởi [@msbarry](https://github.com/msbarry))
- Sửa lỗi url bị sai định dạng khi dùng `baseAPIURL` tùy chỉnh có dạng nhất định ([#8466](https://github.com/mapbox/mapbox-gl-js/pull/8466))

## 1.1.1

### 🐞 Sửa lỗi

- Sửa lỗi tăng trưởng bộ nhớ không giới hạn do không hủy được các request đến cache ([#8472](https://github.com/mapbox/mapbox-gl-js/pull/8472))
- Sửa lỗi tăng trưởng bộ nhớ không giới hạn do không hủy được request trên IE ([#8481](https://github.com/mapbox/mapbox-gl-js/issues/8481))
- Sửa hiệu năng lấy tile từ cache ([#8489](https://github.com/mapbox/mapbox-gl-js/pull/8449))

## 1.1.0

### ✨ Tính năng và cải tiến nhỏ

- Cải thiện hiệu năng render line bằng cách dùng layout thuộc tính line nhỏ gọn hơn ([#8306](https://github.com/mapbox/mapbox-gl-js/pull/8306))
- Cải thiện hiệu năng render các symbol layer theo kiểu data-driven ([#8295](https://github.com/mapbox/mapbox-gl-js/pull/8295))
- Thêm khả năng vô hiệu hóa xác thực (validation) trong các lệnh gọi `queryRenderedFeatures` và `querySourceFeatures`, như một tối ưu hóa hiệu năng ([#8211](https://github.com/mapbox/mapbox-gl-js/pull/8211)) (bởi [gorshkov-leonid](https://github.com/gorshkov-leonid))
- Cải thiện hiệu năng `setFilter` bằng cách cache các key trong routine `groupByLayout` ([#8122](https://github.com/mapbox/mapbox-gl-js/pull/8122)) (bởi [vallendm](https://github.com/vallendm))
- Cải thiện render các symbol layer với `symbol-z-order: viewport-y`, khi icon được phép chồng lấn nhưng text thì không ([#8180](https://github.com/mapbox/mapbox-gl-js/pull/8180))
- Ưu tiên ngắt dòng tại khoảng trắng độ rộng bằng 0 (zero width space) để đưa ra gợi ý điểm ngắt tốt hơn cho nhãn tiếng Nhật ([#8255](https://github.com/mapbox/mapbox-gl-js/pull/8255))
- Thêm tham số `WebGLRenderingContext` vào hàm `onRemove` của `CustomLayerInterface`, để cho phép dọn dẹp trực tiếp context liên quan ([#8156](https://github.com/mapbox/mapbox-gl-js/pull/8156)) (bởi [ogiermaitre](https://github.com/ogiermaitre))
- Cho phép tùy chỉnh tốc độ zoom bằng cách thêm phương thức `setZoomRate` và `setWheelZoomRate` vào `ScrollZoomHandler` ([#7863](https://github.com/mapbox/mapbox-gl-js/pull/7863)) (bởi [sf31](https://github.com/sf31))
- Thêm phương thức `trackPointer` vào API `Popup` để liên tục định vị lại popup theo con trỏ chuột khi con trỏ nằm trong bản đồ ([#7786](https://github.com/mapbox/mapbox-gl-js/pull/7786))
- Thêm phương thức `getElement` vào `Popup` để lấy phần tử HTML của popup ([#8123](https://github.com/mapbox/mapbox-gl-js/pull/8123)) (bởi [@bravecow](https://github.com/bravecow))
- Thêm ví dụ `fill-pattern` vào tài liệu ([#8022](https://github.com/mapbox/mapbox-gl-js/pull/8022)) (bởi [@flawyte](https://github.com/flawyte))
- Cập nhật phát hiện script cho Unicode 12.1 ([#8158](https://github.com/mapbox/mapbox-gl-js/pull/8158))
- Thêm `nofollow` vào các liên kết logo Mapbox & "Improve this map" ([#8106](https://github.com/mapbox/mapbox-gl-js/pull/8106)) (bởi [viniciuskneves](https://github.com/viniciuskneves))
- Đưa tên source vào thông báo lỗi GeoJSON không hợp lệ ([#8113](https://github.com/mapbox/mapbox-gl-js/pull/8113)) (bởi [Zirak](https://github.com/Zirak))

### 🐞 Sửa lỗi

- Sửa lỗi `updateImage` không hoạt động như mong đợi trên Chrome ([#8199](https://github.com/mapbox/mapbox-gl-js/pull/8199))
- Sửa các vấn đề với double-tap zoom trên thiết bị cảm ứng ([#8086](https://github.com/mapbox/mapbox-gl-js/pull/8086))
- Sửa lỗi trùng lặp sự kiện `movestart` khi zoom ([#8259](https://github.com/mapbox/mapbox-gl-js/pull/8259)) (bởi [@bambielli-flex](https://github.com/bambielli-flex))
- Sửa lỗi xác thực biểu thức `"format"` thất bại khi có tùy chọn được cung cấp ([#8339](https://github.com/mapbox/mapbox-gl-js/pull/8339))
- Sửa lỗi `setPaintProperty` không hoạt động trên thuộc tính `line-pattern` ([#8289](https://github.com/mapbox/mapbox-gl-js/pull/8289))
- Sửa lỗi GL context bị để lại ở trạng thái không thể đoán trước khi dùng custom layer ([#8132](https://github.com/mapbox/mapbox-gl-js/pull/8132))
- Sửa các cập nhật không cần thiết cho chuỗi attribution control ([#8082](https://github.com/mapbox/mapbox-gl-js/pull/8082)) (bởi [poletani](https://github.com/poletani))
- Sửa các lỗi trong thuật toán `findStopLessThanOrEqualTo` ([#8134](https://github.com/mapbox/mapbox-gl-js/pull/8134)) (bởi [Mike96Angelo](https://github.com/Mike96Angelo))
- Sửa lỗi bản đồ không hiển thị đúng khi nằm trong phần tử có `text-align: center` ([#8227](https://github.com/mapbox/mapbox-gl-js/pull/8227)) (bởi [mc100s](https://github.com/mc100s))
- Làm rõ trong tài liệu rằng `Popup#maxWidth` chấp nhận mọi giá trị CSS `max-width` ([#8312](https://github.com/mapbox/mapbox-gl-js/pull/8312)) (bởi [viniciuskneves](https://github.com/viniciuskneves))
- Sửa lỗi bóng của chấm vị trí (location dot) không hiển thị ([#8119](https://github.com/mapbox/mapbox-gl-js/pull/8119)) (bởi [@bravecow](https://github.com/bravecow))
- Sửa lỗi các dev dependency của docs bị cài nhầm thành package dependency ([#8121](https://github.com/mapbox/mapbox-gl-js/pull/8121)) (bởi [@bravecow](https://github.com/bravecow))
- Sửa nhiều lỗi chính tả ([#8230](https://github.com/mapbox/mapbox-gl-js/pull/8230), cảm ơn [@erictheise](https://github.com/erictheise)) ([#8236](https://github.com/mapbox/mapbox-gl-js/pull/8236), cảm ơn [@fredj](https://github.com/fredj))
- Sửa CSS của nút geolocate ([#8367](https://github.com/mapbox/mapbox-gl-js/pull/8367), cảm ơn [GuillaumeGomez](https://github.com/GuillaumeGomez))
- Sửa lỗi caching cho tile Mapbox ([#8389](https://github.com/mapbox/mapbox-gl-js/pull/8389))

## 1.0.0

### ⚠️ Thay đổi phá vỡ tương thích

Bản phát hành này thay thế mô hình giá "map views" hiện tại bằng mô hình "map load". Tìm hiểu thêm trong [một bài blog gần đây về các thay đổi này](https://blog.mapbox.com/new-pricing-46b7c26166e7).

**Bằng việc nâng cấp lên bản phát hành này, bạn đang chấp nhận (opt in) mô hình giá map loads mới.**

**Tại sao có thay đổi này?**

Thay đổi này cho phép chúng tôi triển khai một phương pháp tính phí sử dụng GL JS chuẩn hóa và dễ dự đoán hơn. Bạn sẽ bị tính phí mỗi khi website hoặc ứng dụng web của bạn tải bản đồ, chứ không phải theo số lần người dùng pan và zoom quanh bản đồ, khuyến khích các nhà phát triển tạo ra các trải nghiệm bản đồ tương tác cao. Cấu trúc giá mới cũng tạo ra một gói miễn phí (free tier) lớn hơn đáng kể để giúp các nhà phát triển bắt đầu xây dựng ứng dụng với các công cụ của Mapbox, trong khi giá trả theo mức sử dụng (pay-as-you-go) và chiết khấu khối lượng tự động giúp ứng dụng của bạn mở rộng quy mô cùng Mapbox. Việc tính phí theo phiên (session billing) cũng giúp hóa đơn khớp với các chỉ số mà nhà phát triển web đã theo dõi sẵn và giúp việc so sánh mức sử dụng với các nhà cung cấp bản đồ khác dễ dàng hơn.

**Điều gì đang thay đổi?**

- Thêm SKU token vào các request đến Mapbox API [#8276](https://github.com/mapbox/mapbox-gl-js/pull/8276)

Khi (và chỉ khi) tải tile từ Mapbox API với một Mapbox access token được thiết lập (`mapboxgl.accessToken`), một query parameter tên `sku` sẽ được thêm vào tất cả các request cho tile vector, raster và raster-dem. Mỗi instance bản đồ dùng một giá trị `sku` duy nhất, được làm mới sau mỗi 12 giờ. Bản thân token bao gồm phiên bản token (luôn là "1"), một sku ID (luôn là "01") và một số base-62 gồm 10 chữ số ngẫu nhiên. Mục đích của token là cho phép đo lường (metering) các phiên bản đồ ở phía server. Một phiên kéo dài từ khi khởi tạo bản đồ mới cho đến khi bản đồ bị hủy hoặc sau 12 giờ, tùy điều kiện nào đến trước.

Để biết thêm thông tin về các thay đổi giá, bạn có thể đọc [bài blog](https://blog.mapbox.com/new-pricing-46b7c26166e7) của chúng tôi và xem [trang giá](https://www.mapbox.com/pricing) mới, có công cụ tính giá. Như thường lệ, bạn cũng có thể liên hệ đội ngũ của chúng tôi tại [https://support.mapbox.com](https://support.mapbox.com).

## 0.54.1

### Sửa lỗi

- Sửa lỗi tăng trưởng bộ nhớ không giới hạn do không hủy được request trên IE ([#8481](https://github.com/mapbox/mapbox-gl-js/issues/8481))

## 0.54.0

### Thay đổi phá vỡ tương thích

- Bật tùy chọn map `localIdeographFontFamily` theo mặc định. Điều này có thể thay đổi cách nhãn CJK được render, nhưng cải thiện đáng kể hiệu năng của các bản đồ CJK (vì trình duyệt không còn cần tải một lượng lớn dữ liệu font từ server). Thêm `localIdeographFontFamily: false` để tắt tính năng này. [#8008](https://github.com/mapbox/mapbox-gl-js/pull/8008)
- Thêm tùy chọn `maxWidth` cho `Popup`, mặc định là `"240px"`. [#7906](https://github.com/mapbox/mapbox-gl-js/pull/7906)

### Tính năng lớn

- Thêm hỗ trợ cập nhật và animate các ảnh style. [#7999](https://github.com/mapbox/mapbox-gl-js/pull/7999)
- Thêm hỗ trợ tạo ảnh style động (ví dụ để vẽ icon dựa trên thuộc tính feature). [#7987](https://github.com/mapbox/mapbox-gl-js/pull/7987)
- Thêm hỗ trợ antialiasing cho custom layer. [#7821](https://github.com/mapbox/mapbox-gl-js/pull/7821)
- Thêm một bundle `mapbox-gl-csp.js` mới cho các môi trường CSP nghiêm ngặt nơi `worker-src: blob` không được phép. [#8044](https://github.com/mapbox/mapbox-gl-js/pull/8044)

### Tính năng và cải tiến nhỏ

- Cải thiện hiệu năng của fill extrusion. [#7821](https://github.com/mapbox/mapbox-gl-js/pull/7821)
- Cải thiện hiệu năng của symbol layer. [#7967](https://github.com/mapbox/mapbox-gl-js/pull/7967)
- Cải thiện nhẹ hiệu năng render nói chung. [#7969](https://github.com/mapbox/mapbox-gl-js/pull/7969)
- Cải thiện nhẹ hiệu năng của HTML marker. [#8018](https://github.com/mapbox/mapbox-gl-js/pull/8018)
- Cải thiện việc diff các style với `"visibility": "visible"`. [#8005](https://github.com/mapbox/mapbox-gl-js/pull/8005)
- Cải thiện các nút zoom để chuyển màu xám khi đạt min/max zoom. [#8023](https://github.com/mapbox/mapbox-gl-js/pull/8023)
- Thêm title cho nút fullscreen control. [#8012](https://github.com/mapbox/mapbox-gl-js/pull/8012)
- Thêm thuộc tính `rel="noopener"` vào các liên kết dẫn đến website bên ngoài (như logo Mapbox và liên kết edit OpenStreetMap) để cải thiện bảo mật. [#7914](https://github.com/mapbox/mapbox-gl-js/pull/7914)
- Thêm thông tin kích thước tile khi `map.showTileBoundaries` được bật. [#7963](https://github.com/mapbox/mapbox-gl-js/pull/7963)
- Cải thiện đáng kể thời gian tải của bộ benchmark. [#8066](https://github.com/mapbox/mapbox-gl-js/pull/8066)
- Cải thiện hành vi của `canvasSource.pause` để đáng tin cậy hơn và có thể render một frame duy nhất. [#8130](https://github.com/mapbox/mapbox-gl-js/pull/8130)

### Sửa lỗi

- Đã sửa lỗi trên Mac Safari 12+ khi các control biến mất cho đến khi bạn tương tác với bản đồ. [#8193](https://github.com/mapbox/mapbox-gl-js/pull/8193)
- Đã sửa rò rỉ bộ nhớ khi gọi `source.setData(url)` nhiều lần. [#8035](https://github.com/mapbox/mapbox-gl-js/pull/8035)
- Đã sửa lỗi marker mất focus khi kéo. [#7799](https://github.com/mapbox/mapbox-gl-js/pull/7799)
- Đã sửa lỗi `map.getCenter()` trả về tham chiếu đến đối tượng `LngLat` nội bộ thay vì clone nó, dẫn đến khả năng gặp lỗi do tính mutable. [#7922](https://github.com/mapbox/mapbox-gl-js/pull/7922)
- Đã sửa lỗi vị trí mặc định của HTML marker bị lệch nhẹ. [#8074](https://github.com/mapbox/mapbox-gl-js/pull/8074)
- Đã sửa lỗi khi thêm fill extrusion layer cho các layer không phải polygon dẫn đến hiện tượng hiển thị bất thường (visual artifact). [#7685](https://github.com/mapbox/mapbox-gl-js/pull/7685)
- Đã sửa lỗi Flow bị thất bại ngắt quãng trên CI. [#8061](https://github.com/mapbox/mapbox-gl-js/pull/8061)
- Đã sửa lỗi khi gọi `Map#removeFeatureState` không xóa state khỏi một số zoom của tile [#8087](https://github.com/mapbox/mapbox-gl-js/pull/8087)
- Đã sửa lỗi `removeFeatureState` không hoạt động với feature có `id` bằng `0`. [#8150](https://github.com/mapbox/mapbox-gl-js/pull/8150) (bởi [jutaz](https://github.com/jutaz))

## 0.53.1

### Sửa lỗi

- Tắt telemetry cho Mapbox Atlas ([#7945](https://github.com/mapbox/mapbox-gl-js/pull/7945))
- Sửa thứ tự các feature 3D trong kết quả truy vấn (sửa [#7883](https://github.com/mapbox/mapbox-gl-js/issues/7883)) ([#7953](https://github.com/mapbox/mapbox-gl-js/pull/7953))
- Sửa các benchmark RemovePaintState ([#7930](https://github.com/mapbox/mapbox-gl-js/pull/7930))

## 0.53.0

### Tính năng và cải tiến

- Bật truy vấn `fill-extrusion` bằng ray picking ([#7499](https://github.com/mapbox/mapbox-gl-js/pull/7499))
- Thêm tùy chọn `clusterProperties` cho các thuộc tính cluster tổng hợp ([#2412](https://github.com/mapbox/mapbox-gl-js/issues/2412), sửa bằng [#7584](https://github.com/mapbox/mapbox-gl-js/pull/7584))
- Cho phép điều chỉnh bounds ban đầu của bản đồ bằng tùy chọn `fitBounds`. ([#7681](https://github.com/mapbox/mapbox-gl-js/pull/7681)) (bởi [@elyobo](https://github.com/elyobo))
- Xóa popup khi `Map#remove` ([#7749](https://github.com/mapbox/mapbox-gl-js/pull/7749)) (bởi [@andycalder](https://github.com/andycalder))
- Thêm `Map#removeFeatureState` ([#7761](https://github.com/mapbox/mapbox-gl-js/pull/7761))
- Thêm biểu thức `number-format` ([#7626](https://github.com/mapbox/mapbox-gl-js/pull/7626))
- Thêm thuộc tính style `symbol-sort-key` ([#7678](https://github.com/mapbox/mapbox-gl-js/pull/7678))

### Sửa lỗi

- Nâng cấp Earcut để sửa một lỗi hiếm gặp khi render polygon chứa chuỗi lỗ (holes) trùng nhau ([#7806](https://github.com/mapbox/mapbox-gl-js/issues/7806), sửa bằng [#7878](https://github.com/mapbox/mapbox-gl-js/pull/7878))
- Cho phép giao thức `file://` trong các request XHR cho Cordova/Ionic/v.v. ([#7818](https://github.com/mapbox/mapbox-gl-js/pull/7818))
- Xử lý đúng ảnh WebP trên Edge 18 ([#7687](https://github.com/mapbox/mapbox-gl-js/pull/7687))
- Sửa lỗi vô tình yêu cầu ảnh WebP trên các trình duyệt không hỗ trợ WebP ([#7817](https://github.com/mapbox/mapbox-gl-js/pull/7817)) ([#7819](https://github.com/mapbox/mapbox-gl-js/pull/7819))
- Sửa lỗi ảnh không bị hủy khi bị dequeue ([#7655](https://github.com/mapbox/mapbox-gl-js/pull/7655))
- Sửa rò rỉ bộ nhớ của layer DEM ([#7690](https://github.com/mapbox/mapbox-gl-js/issues/7690), sửa bằng [#7691](https://github.com/mapbox/mapbox-gl-js/pull/7691))
- Thiết lập đúng trạng thái màu trước khi render custom layer ([#7711](https://github.com/mapbox/mapbox-gl-js/pull/7711))
- Đặt bán kính mặc định của `LngLat.toBounds()` là 0 ([#7722](https://github.com/mapbox/mapbox-gl-js/issues/7722), sửa bằng [#7723](https://github.com/mapbox/mapbox-gl-js/pull/7723)) (bởi [@cherniavskii](https://github.com/cherniavskii))
- Sửa race condition trong các layer phụ thuộc `feature-state` ([#7523](https://github.com/mapbox/mapbox-gl-js/issues/7523), sửa bằng [#7790](https://github.com/mapbox/mapbox-gl-js/pull/7790))
- Ngăn `map.repaint` vô tình bật chế độ repaint liên tục ([#7667](https://github.com/mapbox/mapbox-gl-js/pull/7667))
- Ngăn bản đồ bị rung khi zoom in trên tile raster ([#7426](https://github.com/mapbox/mapbox-gl-js/pull/7426))
- Sửa việc chuyển đổi điểm truy vấn (query point) cho hình học đa điểm (multi-point) ([#6833](https://github.com/mapbox/mapbox-gl-js/issues/6833), sửa bằng [#7581](https://github.com/mapbox/mapbox-gl-js/pull/7581))

## 0.52.0

### Thay đổi phá vỡ tương thích

- Chuẩn hóa (canonicalize) các url tile thành url `mapbox://` để chúng có thể được biến đổi bằng `config.API_URL` ([#7594](https://github.com/mapbox/mapbox-gl-js/pull/7594))

### Tính năng và cải tiến

- Thêm getter và setter cho `config.API_URL` ([#7594](https://github.com/mapbox/mapbox-gl-js/pull/7594))
- Cho phép người dùng định nghĩa phần tử khác ngoài container bản đồ cho full screen control ([#7548](https://github.com/mapbox/mapbox-gl-js/pull/7548))
- Thêm tùy chọn validation vào các setter style ([#7604](https://github.com/mapbox/mapbox-gl-js/pull/7604))
- Thêm sự kiện 'idle': được phát khi không còn hoạt động render nào được kỳ vọng nếu không có tương tác thêm. ([#7625](https://github.com/mapbox/mapbox-gl-js/pull/7625))

### Sửa lỗi

- Phát lỗi khi map.getLayoutProperty tham chiếu đến layer bị thiếu ([#7537](https://github.com/mapbox/mapbox-gl-js/issues/7537), sửa bằng [#7539](https://github.com/mapbox/mapbox-gl-js/pull/7539))
- Sửa hiện tượng sprite bị rung khi zoom kèm cuộn (scrolling) ([#7558](https://github.com/mapbox/mapbox-gl-js/pull/7558))
- Sửa các vấn đề bố cục (layout) trong attribution control ([#7608](https://github.com/mapbox/mapbox-gl-js/pull/7608)) (bởi [lucaswoj](https://github.com/lucaswoj))
- Sửa việc pitch bản đồ bị reset về 0 nếu bounds ban đầu được thiết lập ([#7617](https://github.com/mapbox/mapbox-gl-js/pull/7617)) (bởi [stepankuzmin](https://github.com/stepankuzmin))
- Sửa lỗi thỉnh thoảng không tải được ảnh sau nhiều lần request ảnh bị hủy [#7641](https://github.com/mapbox/mapbox-gl-js/pull/7641)
- Cập nhật url repo về đúng địa chỉ ([#7486](https://github.com/mapbox/mapbox-gl-js/pull/7486)) (bởi [nicholas-l](https://github.com/nicholas-l))
- Sửa lỗi symbol đôi khi không được render ngay lập tức ([#7610](https://github.com/mapbox/mapbox-gl-js/pull/7610))
- Sửa lỗi cameraForBounds trả về CameraOptions không chính xác khi padding/offset không đối xứng ([#7517](https://github.com/mapbox/mapbox-gl-js/issues/7517), sửa bằng [#7518](https://github.com/mapbox/mapbox-gl-js/pull/7518)) (bởi [mike-marcacci](https://github.com/mike-marcacci))
- Dùng phương pháp diff+patch cho map.setStyle khi tham số là một URL ([#4025](https://github.com/mapbox/mapbox-gl-js/issues/4025), sửa bằng [#7562](https://github.com/mapbox/mapbox-gl-js/pull/7562))
- Bắt đầu touch zoom ngay lập tức khi rotation bị vô hiệu hóa ([#7582](https://github.com/mapbox/mapbox-gl-js/pull/7582)) (bởi [msbarry](https://github.com/msbarry))
- Sửa lỗi render symbol bên dưới các opaque fill layer ([#7612](https://github.com/mapbox/mapbox-gl-js/pull/7612))
- Sửa hiện tượng rung bằng cách căn chỉnh raster source theo pixel grid chỉ khi bản đồ ở trạng thái idle ([#7426](https://github.com/mapbox/mapbox-gl-js/pull/7426))
- Sửa lỗi raster layer trên Edge 18 bằng cách vô hiệu hóa hỗ trợ WebP chưa hoàn chỉnh của nó ([#7687](https://github.com/mapbox/mapbox-gl-js/pull/7687))
- Sửa rò rỉ bộ nhớ trong hillshade layer ([#7691](https://github.com/mapbox/mapbox-gl-js/pull/7691))
- Sửa lỗi custom layer bị biến mất ([#7711](https://github.com/mapbox/mapbox-gl-js/pull/7711))

## 0.51.0

7 tháng 11, 2018

### ✨ Tính năng và cải tiến

- Thêm bounds ban đầu làm tùy chọn map constructor ([#5518](https://github.com/mapbox/mapbox-gl-js/pull/5518)) (bởi [stepankuzmin](https://github.com/stepankuzmin))
- Cải thiện hiệu năng trên các máy có > 8 lõi ([#7407](https://github.com/mapbox/mapbox-gl-js/issues/7407), sửa bằng [#7430](https://github.com/mapbox/mapbox-gl-js/pull/7430))
- Thêm kiểu `MercatorCoordinate` ([#7488](https://github.com/mapbox/mapbox-gl-js/pull/7488))
- Cho phép bật `contextmenu` gốc của trình duyệt ([#2301](https://github.com/mapbox/mapbox-gl-js/issues/2301), sửa bằng [#7369](https://github.com/mapbox/mapbox-gl-js/pull/7369))
- Thêm bản build production chưa minify vào NPM package ([#7403](https://github.com/mapbox/mapbox-gl-js/pull/7403))
- Thêm hỗ trợ chuyển đổi `LngLat` từ `{lat, lon}` ([#7507](https://github.com/mapbox/mapbox-gl-js/pull/7507)) (bởi [@bfrengley](https://github.com/bfrengley))
- Thêm tooltip cho navigation control ([#7373](https://github.com/mapbox/mapbox-gl-js/pull/7373))
- Chỉ hiển thị attribution cho các source đang được sử dụng ([#7384](https://github.com/mapbox/mapbox-gl-js/pull/7384))
- Thêm sự kiện telemetry để ghi log các lần tải bản đồ ([#7431](https://github.com/mapbox/mapbox-gl-js/pull/7431))
- **Thắt chặt xác thực style**
    - Không cho phép biểu thức làm giá trị stop ([#7396](https://github.com/mapbox/mapbox-gl-js/pull/7396))
    - Không cho phép biểu thức `feature-state` trong filter ([#7366](https://github.com/mapbox/mapbox-gl-js/pull/7366))

### 🐛 Sửa lỗi

- Sửa lỗi các geometry GeoJSON không hoạt động khi trùng với ranh giới tile([#7436](https://github.com/mapbox/mapbox-gl-js/issues/7436), sửa bằng [#7448](https://github.com/mapbox/mapbox-gl-js/pull/7448))
- Sửa các vấn đề render liên quan đến depth buffer trên một số thiết bị Android. ([#7471](https://github.com/mapbox/mapbox-gl-js/pull/7471))
- Sửa vị trí của chuỗi attribution dạng compact (rút gọn) ([#7444](https://github.com/mapbox/mapbox-gl-js/pull/7444), [#7445](https://github.com/mapbox/mapbox-gl-js/pull/7445), và [#7391](https://github.com/mapbox/mapbox-gl-js/pull/7391))
- Sửa lỗi khi xóa marker trong callback sự kiện chuột ([#7442](https://github.com/mapbox/mapbox-gl-js/pull/7442)) (bởi [vbud](https://github.com/vbud))
- Xóa các control trước khi hủy bản đồ ([#7479](https://github.com/mapbox/mapbox-gl-js/pull/7479))
- Sửa việc hiển thị giá trị Scale control < 1 ([#7469](https://github.com/mapbox/mapbox-gl-js/pull/7469)) (bởi [MichaelHedman](https://github.com/MichaelHedman))
- Sửa lỗi khi dùng location `hash` trong iframe trên IE11 ([#7411](https://github.com/mapbox/mapbox-gl-js/pull/7411))
- Sửa việc sử dụng depth mode trong custom layer ([#7432](https://github.com/mapbox/mapbox-gl-js/pull/7432)) (bởi [markusjohnsson](https://github.com/markusjohnsson))
- Sửa lỗi ảnh sprite bị rung khi scroll zoom ([#7558](https://github.com/mapbox/mapbox-gl-js/pull/7558))

## 0.50.0

10 tháng 10, 2018

### ✨ Tính năng và cải tiến

- 🎉 Thêm Custom Layer có thể render bằng mã WebGL do người dùng cung cấp ([#7039](https://github.com/mapbox/mapbox-gl-js/pull/7039))
- Thêm WebGL face culling để tăng hiệu năng ([#7178](https://github.com/mapbox/mapbox-gl-js/pull/7178))
- Cải thiện tốc độ đánh giá biểu thức ([#7334](https://github.com/mapbox/mapbox-gl-js/pull/7334))
- Tự động chuyển đổi (coerce) sang string cho biểu thức `concat` và thuộc tính `text-field` ([#6190](https://github.com/mapbox/mapbox-gl-js/issues/6190), sửa bằng [#7280](https://github.com/mapbox/mapbox-gl-js/pull/7280))
- Thêm thuộc tính `fill-extrusion-vertical-gradient` để kiểm soát bóng đổ (shading) của fill extrusion ([#5768](https://github.com/mapbox/mapbox-gl-js/issues/5768), sửa bằng [#6841](https://github.com/mapbox/mapbox-gl-js/pull/6841))
- Thêm chức năng cập nhật cho ảnh được cung cấp qua `ImageSource` ([#4050](https://github.com/mapbox/mapbox-gl-js/issues/4050), sửa bằng [#7342](https://github.com/mapbox/mapbox-gl-js/pull/7342)) (bởi [@dcervelli](https://github.com/dcervelli))

### 🐛 Sửa lỗi

- **Biểu thức (Expressions)**
    - Sửa các biểu thức dùng `log2` và `log10` trên IE11 ([#7318](https://github.com/mapbox/mapbox-gl-js/issues/7318), sửa bằng [#7320](https://github.com/mapbox/mapbox-gl-js/pull/7320))
    - Sửa biểu thức `let` làm mất kiểu (type) mong đợi trong quá trình parse ([#7300](https://github.com/mapbox/mapbox-gl-js/issues/7300), sửa bằng [#7301](https://github.com/mapbox/mapbox-gl-js/pull/7301))
    - Sửa việc bọc (wrapping) thừa các literal trong biểu thức `literal` ([#7336](https://github.com/mapbox/mapbox-gl-js/issues/7336), sửa bằng [#7337](https://github.com/mapbox/mapbox-gl-js/pull/7337))
    - Cho phép gọi `to-color` trên các giá trị đã thuộc kiểu `Color` ([#7260](https://github.com/mapbox/mapbox-gl-js/pull/7260))
    - Sửa `to-array` cho mảng rỗng (([#7261](https://github.com/mapbox/mapbox-gl-js/pull/7261)))
    - Sửa identity function cho `text-field` khi dùng formatted text ([#7351](https://github.com/mapbox/mapbox-gl-js/pull/7351))
    - Sửa việc chuyển đổi `null` thành `0` trong biểu thức `to-number` ([#7083](https://github.com/mapbox/mapbox-gl-js/issues/7083), sửa bằng [#7274](https://github.com/mapbox/mapbox-gl-js/pull/7274))
- **Canvas source**
    - Sửa lỗi thiếu các bản lặp lại (repeats) của `CanvasSource` khi nó băng qua đường đối tuyến (antimeridian) ([#7273](https://github.com/mapbox/mapbox-gl-js/pull/7273))
    - Sửa `CanvasSource` không tôn trọng giá trị alpha đặt trên phần tử `canvas` ([#7302](https://github.com/mapbox/mapbox-gl-js/issues/7302), sửa bằng [#7309](https://github.com/mapbox/mapbox-gl-js/pull/7309))
- **Render**
    - Sửa việc render fill extrusion có độ cao rất lớn ([#7292](https://github.com/mapbox/mapbox-gl-js/pull/7292))
    - Sửa lỗi trạng thái bản đồ không quay về `loaded` sau một số thay đổi runtime styling khi có tile bị lỗi trong viewport ([#7355](https://github.com/mapbox/mapbox-gl-js/pull/7355))
    - Sửa lỗi khi render symbol layer không có symbol ([#7241](https://github.com/mapbox/mapbox-gl-js/issues/7241), sửa bằng [#7253](https://github.com/mapbox/mapbox-gl-js/pull/7253))
    - Không fade in các symbol có `*-allow-overlap: true` khi pan vào viewport ([#7172](https://github.com/mapbox/mapbox-gl-js/issues/7172), sửa bằng[#7244](https://github.com/mapbox/mapbox-gl-js/pull/7244))
- **Thư viện**
    - Sửa việc phân biệt (disambiguation) cho sự kiện `mouseover` ([#7295](https://github.com/mapbox/mapbox-gl-js/issues/7295), sửa bằng [#7299](https://github.com/mapbox/mapbox-gl-js/pull/7299))
    - Sửa lỗi im lặng (silent failure) của `getImage` nếu một SVG được yêu cầu ([#7312](https://github.com/mapbox/mapbox-gl-js/issues/7312), sửa bằng [#7313](https://github.com/mapbox/mapbox-gl-js/pull/7313))
    - Sửa box shadow rỗng của control group ([#7303](https://github.com/mapbox/mapbox-gl-js/issues/7303), sửa bằng [#7304](https://github.com/mapbox/mapbox-gl-js/pull/7304)) (bởi [Duder-onomy](https://github.com/Duder-onomy))
    - Đã sửa lỗi timestamp sai được gửi cho sự kiện turnstile của Mapbox ([#7381](https://github.com/mapbox/mapbox-gl-js/pull/7381))
    - Đã sửa lỗi khiến attribution không hiển thị đúng trên Internet Explorer ([#3945](https://github.com/mapbox/mapbox-gl-js/issues/3945), sửa bằng [#7391](https://github.com/mapbox/mapbox-gl-js/pull/7391))

## 0.49.0

6 tháng 9, 2018

### ⚠️ Thay đổi phá vỡ tương thích

- Dùng `client{Height/Width}` thay vì `offset{Height/Width}` để định kích thước canvas bản đồ ([#6848](https://github.com/mapbox/mapbox-gl-js/issues/6848), sửa bằng [#7128](https://github.com/mapbox/mapbox-gl-js/pull/7128))

### 🐛 Sửa lỗi

- Sửa [danh sách Top Issues](https://mapbox.github.io/top-issues/#!mapbox/mapbox-gl-js) cho mapbox-gl-js ([#7108](https://github.com/mapbox/mapbox-gl-js/issues/7108), sửa bằng [#7112](https://github.com/mapbox/mapbox-gl-js/pull/7112))
- Sửa lỗi symbol với `icon-allow-overlap: true, text-allow-overlap: true, text-optional: false` sẽ hiển thị icon dù không nên ([#7041](https://github.com/mapbox/mapbox-gl-js/pull/7041))
- Sửa lỗi bản đồ không dừng đúng ở zoom level được yêu cầu bởi Map#FlyTo ([#7222](https://github.com/mapbox/mapbox-gl-js/issues/7222)) ([#7223](https://github.com/mapbox/mapbox-gl-js/pull/7223)) (bởi [@benoitbzl](https://github.com/benoitbzl))
- Giữ bản đồ căn giữa tại điểm trung tâm của cử chỉ đa chạm (multi-touch gesture) khi zoom ([#6722](https://github.com/mapbox/mapbox-gl-js/issues/6722)) ([#7191](https://github.com/mapbox/mapbox-gl-js/pull/7191)) (bởi [pakastin](https://github.com/pakastin))
- Cập nhật script `gl-style-migrate` cũ của style-spec để bao gồm việc chuyển đổi các function và filter kiểu cũ sang biểu thức tương đương ([#6927](https://github.com/mapbox/mapbox-gl-js/issues/6927), sửa bằng [#7095](https://github.com/mapbox/mapbox-gl-js/pull/7095))
- Sửa `icon-size` cho các giá trị data-driven nhỏ ([#7125](https://github.com/mapbox/mapbox-gl-js/pull/7125))
- Sửa lỗi trong cách các request AJAX tải file cục bộ trên iOS web view ([#6610](https://github.com/mapbox/mapbox-gl-js/pull/6610)) (bởi [oscarfonts](https://github.com/oscarfonts))
- Sửa lỗi các canvas source không render trong các tile bị world-wrap ở cạnh viewport ([#7271]https://github.com/mapbox/mapbox-gl-js/issues/7271), sửa bằng [#7273](https://github.com/mapbox/mapbox-gl-js/pull/7273))

### ✨ Tính năng và cải tiến

- Các cập nhật về hiệu năng:
    - Cải thiện thời gian render đầu tiên bằng cách cập nhật cách các feature ID map được truyền đến main thread ([#7110](https://github.com/mapbox/mapbox-gl-js/issues/7110), sửa bằng [#7132](https://github.com/mapbox/mapbox-gl-js/pull/7132))
    - Giảm kích thước JSON truyền từ worker thread đến main thread ([#7124](https://github.com/mapbox/mapbox-gl-js/pull/7124))
    - Cải thiện thuật toán đóng gói (packing) image/glyph atlas ([#7171](https://github.com/mapbox/mapbox-gl-js/pull/7171))
    - Dùng murmur hash cho các khóa symbol instance để giảm chi phí truyền dữ liệu qua worker ([#7127](https://github.com/mapbox/mapbox-gl-js/pull/7127))
- Thêm quản lý trạng thái GL cho uniform ([#6018](https://github.com/mapbox/mapbox-gl-js/pull/6018))
- Thêm thuộc tính layout symbol `symbol-z-order` vào style spec ([#7219](https://github.com/mapbox/mapbox-gl-js/pull/7219))
- Triển khai hỗ trợ data-driven styling cho các thuộc tính `*-pattern` ([#6289](https://github.com/mapbox/mapbox-gl-js/pull/6289))
- Thêm `Map#fitScreenCoordinates` để khớp viewport với hai điểm, tương tự `Map#fitBounds` nhưng dùng tọa độ màn hình và hỗ trợ map bearing khác 0 ([#6894](https://github.com/mapbox/mapbox-gl-js/pull/6894))
- Triển khai lại nội suy không gian màu LAB/HSL cho biểu thức ([#5326](https://github.com/mapbox/mapbox-gl-js/issues/5326), sửa bằng [#7123](https://github.com/mapbox/mapbox-gl-js/pull/7123))
- Bật kiểm thử benchmark cho các style Mapbox ([#7047](https://github.com/mapbox/mapbox-gl-js/pull/7047))
- Cho phép `Map#setFeatureState` và `Map#getFeatureState` chấp nhận ID dạng số ([#7106](https://github.com/mapbox/mapbox-gl-js/pull/7106)) (bởi [@bfrengley](https://github.com/bfrengley))

## 0.48.0

16 tháng 8, 2018

### ⚠️ Thay đổi phá vỡ tương thích

- Xử lý các tile bị lỗi với status 404 như các tile trống có thể render để ngăn việc render các feature trùng lặp trong một số tileset thưa (sparse) ([#6803](https://github.com/mapbox/mapbox-gl-js/pull/6803))

### 🐛 Sửa lỗi

- Sửa lỗi thuộc tính `text-max-angle` bị tính toán sai nội bộ, gây ra lỗi render tiềm ẩn khi `"symbol-placement": line`
- Yêu cầu `feature.id` khi dùng `Map#setFeatureState` ([#6974](https://github.com/mapbox/mapbox-gl-js/pull/6974))
- Sửa lỗi khi xóa `GeolocateControl` trong lúc vị trí người dùng đang được sử dụng ([#6977](https://github.com/mapbox/mapbox-gl-js/pull/6977)) (bởi [sergei-zelinsky](https://github.com/sergei-zelinsky))
- Sửa rò rỉ bộ nhớ do không xóa hết các control đã thêm vào bản đồ ([#7042](https://github.com/mapbox/mapbox-gl-js/pull/7042))
- Sửa lỗi build thất bại khi dùng mapbox-gl với webpack 2 và UglifyJSPlugin ([#4359](https://github.com/mapbox/mapbox-gl-js/issues/4359), sửa bằng [#6956](https://api.github.com/repos/mapbox/mapbox-gl-js/pulls/6956))
- Sửa lỗi fitBounds được gọi với tọa độ nằm ngoài giới hạn của Web Mercator dẫn đến lỗi không được bắt (uncaught error) ([#6906](https://github.com/mapbox/mapbox-gl-js/issues/6906), sửa bằng [#6918](https://api.github.com/repos/mapbox/mapbox-gl-js/pulls/6918))
- Sửa lỗi `Map#querySourceFeatures` trả về kết quả sai ở các zoom > maxZoom ([#7061](https://github.com/mapbox/mapbox-gl-js/pull/7061))
- Nới lỏng typing cho các biểu thức so sánh bằng và thứ tự ([#6459](https://github.com/mapbox/mapbox-gl-js/issues/6459), sửa bằng [#6961](https://api.github.com/repos/mapbox/mapbox-gl-js/pulls/6961))
- Sửa lỗi `queryPadding` cho tất cả layer trong một source bị đặt bởi layer đầu tiên, gây ra truy vấn sai trên các layer khác và, trong một số trường hợp, phát sai sự kiện liên quan đến từng layer riêng lẻ ([#6909](https://github.com/mapbox/mapbox-gl-js/pull/6909))

### ✨ Tính năng và cải tiến

- Cải thiện hiệu năng:
    - Dừng việc serialize không cần thiết các feature của symbol source. ([#7013](https://github.com/mapbox/mapbox-gl-js/pull/7013))
    - Tối ưu phép tính lấy tọa độ tile hiển thị (visible tile coordinates) ([#6998](https://github.com/mapbox/mapbox-gl-js/pull/6998))
    - Cải thiện hiệu năng tạo `{Glyph/Image}Atlas` ([#7091](https://github.com/mapbox/mapbox-gl-js/pull/7091))
    - Tối ưu và đơn giản hóa logic giữ (retention) tile ([#6995](https://github.com/mapbox/mapbox-gl-js/pull/6995))
- Thêm sự kiện turnstile người dùng cho người dùng truy cập Mapbox API ([#6980](https://github.com/mapbox/mapbox-gl-js/pull/6980))
- Thêm hỗ trợ tự động tạo feature id cho GeoJSON source để dễ dàng dùng với API `Map#setFeatureState` hơn ([#7043](https://www.github.com/mapbox/mapbox-gl-js/pull/7043))) ([#7091](https://github.com/mapbox/mapbox-gl-js/pull/7091))
- Thêm khả năng style nhãn symbol layer bằng nhiều font và kích thước text thông qua biểu thức `"format"` ([#6994](https://www.github.com/mapbox/mapbox-gl-js/pull/6994))
- Thêm tùy chọn customAttribution cho AttributionControl ([#7033](https://github.com/mapbox/mapbox-gl-js/pull/7033)) (bởi [mklopets](https://github.com/mklopets))
- Phát hành các định nghĩa kiểu Flow cùng với bundle đã biên dịch ([#7079](https://api.github.com/repos/mapbox/mapbox-gl-js/pulls/7079))
- Giới thiệu symbol cross fading khi vượt qua các zoom level nguyên để ngăn nhãn biến mất trước khi nhãn của tile mới tải xong có thể được render ([#6951](https://github.com/mapbox/mapbox-gl-js/pull/6951))
- Cải tiến trong việc phát hiện va chạm nhãn (label collision detection) ([#6925](https://api.github.com/repos/mapbox/mapbox-gl-js/pulls/6925)))

## 0.47.0

### ✨ Tính năng và cải tiến

- Thêm ngưỡng drag pan có thể cấu hình ([#6809](https://github.com/mapbox/mapbox-gl-js/pull/6809)) (bởi [msbarry](https://github.com/msbarry))
- Thêm thuộc tính paint `raster-resampling` ([#6411](https://github.com/mapbox/mapbox-gl-js/pull/6411)) (bởi [@andrewharvey](https://github.com/andrewharvey))
- Thêm `symbol-placement: line-center` ([#6821](https://github.com/mapbox/mapbox-gl-js/pull/6821))
- Thêm các phương thức để kiểm tra (inspect) cluster GeoJSON ([#3318](https://github.com/mapbox/mapbox-gl-js/issues/3318), sửa bằng [#6829](https://github.com/mapbox/mapbox-gl-js/pull/6829))
- Thêm cảnh báo cho geolocate control khi không được hỗ trợ ([#6923](https://github.com/mapbox/mapbox-gl-js/pull/6923)) (bởi [@aendrew](https://github.com/aendrew))
- Nâng cấp geojson-vt lên 3.1.4 ([#6942](https://github.com/mapbox/mapbox-gl-js/pull/6942))
- Thêm liên kết đến giấy phép trong bundle đã biên dịch ([#6975](https://github.com/mapbox/mapbox-gl-js/pull/6975))

### 🐛 Sửa lỗi

- Dùng updateData thay vì tạo lại buffer cho các paint array được điền lại ([#6853](https://github.com/mapbox/mapbox-gl-js/pull/6853))
- Sửa lỗi ScrollZoom handler đặt tr.zoom = NaN ([#6924](https://github.com/mapbox/mapbox-gl-js/pull/6924))
    - Lỗi không nghịch đảo được ma trận (Failed to invert matrix error) ([#6486](https://github.com/mapbox/mapbox-gl-js/issues/6486), sửa bằng [#6924](https://github.com/mapbox/mapbox-gl-js/pull/6924))
    - Sửa các lỗi ma trận ([#6782](https://github.com/mapbox/mapbox-gl-js/issues/6782), sửa bằng [#6924](https://github.com/mapbox/mapbox-gl-js/pull/6924))
- Sửa lỗi tile heatmap bị cắt (clipping) khi các layer được xếp phía trên nó ([#6806](https://github.com/mapbox/mapbox-gl-js/issues/6806), sửa bằng [#6807](https://github.com/mapbox/mapbox-gl-js/pull/6807))
- Sửa video source trên safari (macOS và iOS) ([#6443](https://github.com/mapbox/mapbox-gl-js/issues/6443), sửa bằng [#6811](https://github.com/mapbox/mapbox-gl-js/pull/6811))
- Không reload các tile bị lỗi ([#6813](https://github.com/mapbox/mapbox-gl-js/pull/6813))
- Sửa lỗi timing gửi / xóa trong Dispatcher ([#6756](https://github.com/mapbox/mapbox-gl-js/pull/6756), sửa bằng [#6826](https://github.com/mapbox/mapbox-gl-js/pull/6826))
- Sửa lỗi flyTo không zoom đến đúng zoom được yêu cầu ([#6828](https://github.com/mapbox/mapbox-gl-js/pull/6828))
- Không dừng animation khi resize bản đồ ([#6636](https://github.com/mapbox/mapbox-gl-js/pull/6636))
- Sửa map.getBounds() với bản đồ bị xoay (rotated) ([#6875](https://github.com/mapbox/mapbox-gl-js/pull/6875)) (bởi [zoltan-mihalyi](https://github.com/zoltan-mihalyi))
- Hỗ trợ collator trong các biểu thức filter feature. ([#6929](https://github.com/mapbox/mapbox-gl-js/pull/6929))
- Sửa khả năng tương thích với chế độ production của Webpack ([#6981](https://github.com/mapbox/mapbox-gl-js/pull/6981))

## 0.46.0

### ⚠️ Thay đổi phá vỡ tương thích

- Đồng bộ hành vi ép kiểu ngầm định (implicit type casting) của biểu thức `match` với `case/==` ([#6684](https://github.com/mapbox/mapbox-gl-js/pull/6684))

### ✨ Tính năng và cải tiến

- :tada: Thêm `Map#setFeatureState` và biểu thức `feature-state` để hỗ trợ styling tương tác ([#6263](https://github.com/mapbox/mapbox-gl-js/pull/6263))
- Tạo `Marker` có thể kéo (draggable) bằng `setDraggable` ([#6687](https://github.com/mapbox/mapbox-gl-js/pull/6687))
- Thêm `Map#listImages` để liệt kê tất cả sprite/ảnh đang hoạt động ([#6381](https://github.com/mapbox/mapbox-gl-js/issues/6381))
- Thêm tùy chọn "crossSourceCollisions" để vô hiệu hóa phát hiện va chạm giữa các source (cross-source collision detection) ([#6566](https://github.com/mapbox/mapbox-gl-js/pull/6566))
- Xử lý `text/icon-rotate` cho symbol với `symbol-placement: point` ([#6075](https://github.com/mapbox/mapbox-gl-js/issues/6075))
- Tự động thu gọn (compact) wordmark Mapbox trên bản đồ hẹp. ([#4282](https://github.com/mapbox/mapbox-gl-js/issues/4282)) (bởi [@andrewharvey](https://github.com/andrewharvey))
- Chỉ hiển thị AttributionControl dạng thu gọn trên các màn hình tương tác ([#6506](https://github.com/mapbox/mapbox-gl-js/pull/6506)) (bởi [@andrewharvey](https://github.com/andrewharvey))
- Dùng postcss để nhúng file svg vào css, giảm kích thước mapbox-gl.css ([#6513](https://github.com/mapbox/mapbox-gl-js/pull/6513)) (bởi [@andrewharvey](https://github.com/andrewharvey))
- Thêm hỗ trợ attribution GeoJSON ([#6364](https://github.com/mapbox/mapbox-gl-js/pull/6364)) (bởi [@andrewharvey](https://github.com/andrewharvey))
- Thêm hướng dẫn chạy các unit test và render test riêng lẻ ([#6686](https://github.com/mapbox/mapbox-gl-js/pull/6686))
- Khiến Map constructor thất bại nếu khởi tạo WebGL thất bại. ([#6744](https://github.com/mapbox/mapbox-gl-js/pull/6744)) (bởi [uforic](https://github.com/uforic))
- Thêm mã dự phòng (fallback) trình duyệt cho `collectResourceTiming: true` trong web worker ([#6721](https://github.com/mapbox/mapbox-gl-js/pull/6721))
- Loại bỏ việc dùng gl.lineWidth không còn được sử dụng ([#5541](https://github.com/mapbox/mapbox-gl-js/pull/5541))
- Tách phần tính toán bounds mới ra khỏi fitBounds thành một phương thức mới ([#6683](https://github.com/mapbox/mapbox-gl-js/pull/6683))
- Cho phép các integration test được tổ chức trong cấu trúc thư mục sâu tùy ý ([#3920](https://github.com/mapbox/mapbox-gl-js/issues/3920))
- Biến "Missing Mapbox GL JS CSS" thành cảnh báo console ([#5786](https://github.com/mapbox/mapbox-gl-js/issues/5786))
- Thêm rel="noopener" vào liên kết attribution Mapbox. ([#6729](https://github.com/mapbox/mapbox-gl-js/pull/6729)) (bởi [gorbypark](https://github.com/gorbypark))
- Cập nhật kiểm tra deep equality trong mã ví dụ ([#6599](https://github.com/mapbox/mapbox-gl-js/pull/6599)) (bởi [jonsadka](https://github.com/jonsadka))
- Nâng cấp!
    - Nâng cấp dependency ESM lên ^3.0.39 ([#6750](https://github.com/mapbox/mapbox-gl-js/pull/6750))
    - Bỏ bản fork gl-matrix để dùng package gốc ([#6751](https://github.com/mapbox/mapbox-gl-js/pull/6751))
    - Cập nhật lên sinon mới nhất ([#6771](https://github.com/mapbox/mapbox-gl-js/pull/6771))
    - Nâng cấp lên Flow 0.69 ([#6594](https://github.com/mapbox/mapbox-gl-js/pull/6594))
    - Cập nhật lên mapbox-gl-supported 1.4.0 ([#6773](https://github.com/mapbox/mapbox-gl-js/pull/6773))

### 🐛 Sửa lỗi

- `collectResourceTiming: true` gây lỗi trên iOS9 Safari, IE 11 ([#6690](https://github.com/mapbox/mapbox-gl-js/issues/6690))
- Sửa khai báo kiểu Flow của PopupOptions ([#6670](https://github.com/mapbox/mapbox-gl-js/pull/6670)) (bởi [TimPetricola](https://github.com/TimPetricola))
- Thêm tùy chọn className vào Popup constructor ([#6502](https://github.com/mapbox/mapbox-gl-js/pull/6502)) (bởi [Ashot-KR](https://github.com/Ashot-KR))
- GeoJSON MultiLineStrings với `lineMetrics=true` chỉ render dòng đầu tiên ([#6649](https://github.com/mapbox/mapbox-gl-js/issues/6649))
- Cung cấp thuộc tính target cho sự kiện mouseenter/over/leave/out ([#6623](https://github.com/mapbox/mapbox-gl-js/issues/6623))
- Không bị lỗi với các source có tên chứa "." ([#6660](https://github.com/mapbox/mapbox-gl-js/issues/6660))
- Rotate và pitch với navigationControl bị hỏng ở v0.45 ([#6650](https://github.com/mapbox/mapbox-gl-js/issues/6650))
- Các line có độ rộng bằng 0 vẫn hiển thị ([#6769](https://github.com/mapbox/mapbox-gl-js/pull/6769))
- Heatmap bị cắt sai tại ranh giới tile ([#6806](https://github.com/mapbox/mapbox-gl-js/issues/6806))
- Dùng named export cho entrypoint module style-spec ([#6601](https://github.com/mapbox/mapbox-gl-js/issues/6601)
- Không phát sự kiện click nếu default bị ngăn (prevented) trên mousedown cho một sự kiện kéo ([#6697](https://github.com/mapbox/mapbox-gl-js/pull/6697), sửa [#6642](https://github.com/mapbox/mapbox-gl-js/issues/6642))
- Double click để zoom in làm hỏng việc kéo/pan bản đồ trên Edge ([#6740](https://github.com/mapbox/mapbox-gl-js/issues/6740)) (bởi [GUI](https://github.com/GUI))
- Không thể đặt các thuộc tính \*-transition bằng setPaintProperty() ([#6706](https://github.com/mapbox/mapbox-gl-js/issues/6706))
- Marker với phần tử `a` không mở url khi được click ([#6730](https://github.com/mapbox/mapbox-gl-js/issues/6730))
- `setRTLTextPlugin` lỗi với URL tương đối ([#6719](https://github.com/mapbox/mapbox-gl-js/issues/6719))
- Phát hiện va chạm (collision detection) không chính xác cho các symbol layer dùng chung thuộc tính layout ([#6548](https://github.com/mapbox/mapbox-gl-js/pull/6548))
- Sửa khả năng crash khi gọi queryRenderedFeatures sau querySourceFeatures ([#6559](https://github.com/mapbox/mapbox-gl-js/pull/6559))
- Sửa vấn đề phát hiện va chạm khiến nhãn tạm thời được đặt quá dày đặc trong lúc pan nhanh ([#5654](https://github.com/mapbox/mapbox-gl-js/issues/5654))

## 0.45.0

### ⚠️ Thay đổi phá vỡ tương thích

- `Evented#fire` và `Evented#listens` giờ được đánh dấu là private. Mặc dù `Evented` vẫn được export, và `fire` cùng `listens` vẫn hoạt động, chúng tôi khuyến khích bạn tìm giải pháp thay thế; một phiên bản tương lai có thể loại bỏ khả năng truy cập API này hoặc thay đổi hành vi của nó. Nếu bạn đang viết một class cần chức năng phát sự kiện, hãy cân nhắc dùng [`EventEmitter`](https://nodejs.org/api/events.html#events_class_eventemitter) hoặc các thư viện tương tự.
- Toán tử biểu thức `"to-string"` giờ chuyển đổi `null` thành chuỗi rỗng thay vì thành `"null"`. [#6534](https://github.com/mapbox/mapbox-gl-js/pull/6534)

### ✨ Tính năng và cải tiến

- :rainbow: Thêm thuộc tính `line-gradient` [#6303](https://github.com/mapbox/mapbox-gl-js/pull/6303)
- Thêm toán tử biểu thức `abs`, `round`, `floor`, và `ceil` [#6496](https://github.com/mapbox/mapbox-gl-js/pull/6496)
- Thêm biểu thức `collator` để kiểm soát độ nhạy chữ hoa/thường và dấu (diacritic) khi so sánh chuỗi [#6270](https://github.com/mapbox/mapbox-gl-js/pull/6270)
    - Đổi tên biểu thức `caseSensitive` và `diacriticSensitive` thành `case-sensitive` và `diacritic-sensitive` để nhất quán [#6598](https://github.com/mapbox/mapbox-gl-js/pull/6598)
    - Ngăn các biểu thức `collator` được đánh giá như hằng số (constant) để tính đến khả năng khác biệt tùy môi trường trong việc đánh giá biểu thức [#6596](https://github.com/mapbox/mapbox-gl-js/pull/6596)
- Thêm CSS linting vào bộ test (bởi [@jasonbarry](https://github.com/jasonbarry))) [#6071](https://github.com/mapbox/mapbox-gl-js/pull/6071)
- Thêm hỗ trợ maxzoom có thể cấu hình trong tileset `raster-dem` [#6103](https://github.com/mapbox/mapbox-gl-js/pull/6103)
- Thêm phương thức `Map#isZooming` và `Map#isRotating` [#6128](https://github.com/mapbox/mapbox-gl-js/pull/6128), [#6183](https://github.com/mapbox/mapbox-gl-js/pull/6183)
- Thêm hỗ trợ tile Mapzen Terrarium trong các source `raster-dem` [#6110](https://github.com/mapbox/mapbox-gl-js/pull/6110)
- Thêm phương thức `preventDefault` trên sự kiện `mousedown`, `touchstart`, và `dblclick` [#6218](https://github.com/mapbox/mapbox-gl-js/pull/6218)
- Thêm thuộc tính `originalEvent` trên `zoomend` và `moveend` cho các sự kiện scroll do người dùng khởi tạo (bởi [@stepankuzmin](https://github.com/stepankuzmin))) [#6175](https://github.com/mapbox/mapbox-gl-js/pull/6175)
- Chấp nhận tham số kiểu `value` trong [biểu thức `"length"`](https://www.mapbox.com/mapbox-gl-js/style-spec/#expressions-length) [#6244](https://github.com/mapbox/mapbox-gl-js/pull/6244)
- Giới thiệu `MapWheelEvent`[#6237](https://github.com/mapbox/mapbox-gl-js/pull/6237)
- Thêm setter cho đơn vị `ScaleControl` (bởi [@ryanhamley](https://github.com/ryanhamley))) [#6138](https://github.com/mapbox/mapbox-gl-js/pull/6138), [#6274](https://github.com/mapbox/mapbox-gl-js/pull/6274)
- Thêm sự kiện `open` cho `Popup` [#6311](https://github.com/mapbox/mapbox-gl-js/pull/6311)
- Không còn yêu cầu assertion kiểu `"object"` rõ ràng khi dùng biểu thức [#6235](https://github.com/mapbox/mapbox-gl-js/pull/6235)
- Thêm tùy chọn `anchor` cho `Marker` [#6350](https://github.com/mapbox/mapbox-gl-js/pull/6350)
- `HTMLElement` giờ được truyền vào `Marker` như một phần của object `options`, nhưng chữ ký hàm cũ vẫn được hỗ trợ để tương thích ngược [#6356](https://github.com/mapbox/mapbox-gl-js/pull/6356)
- Thêm hỗ trợ màu tùy chỉnh khi dùng phần tử SVG `Marker` mặc định (bởi [@andrewharvey](https://github.com/andrewharvey))) [#6416](https://github.com/mapbox/mapbox-gl-js/pull/6416)
- Cho phép khởi tạo `CanvasSource` từ `HTMLElement` [#6424](https://github.com/mapbox/mapbox-gl-js/pull/6424)
- Thêm biểu thức `is-supported-script` [#6260](https://github.com/mapbox/mapbox-gl-js/pull/6260)

### 🐛 Sửa lỗi

- Căn chỉnh tile `raster-dem` theo pixel grid để loại bỏ hiện tượng render mờ trên một số thiết bị [#6059](https://github.com/mapbox/mapbox-gl-js/pull/6059)
- Sửa lỗi vẽ debug collision circle của nhãn trên các tile bị overzoom [#6073](https://github.com/mapbox/mapbox-gl-js/pull/6073)
- Cải thiện báo cáo lỗi cho một số request thất bại [#6126](https://github.com/mapbox/mapbox-gl-js/pull/6126), [#6032](https://github.com/mapbox/mapbox-gl-js/pull/6032)
- Sửa một số lỗi của `Map#queryRenderedFeatures`:
    - tính đến `{text, icon}-offset` khi truy vấn[#6135](https://github.com/mapbox/mapbox-gl-js/pull/6135)
    - truy vấn đúng các feature trải dài qua ranh giới tile [#5756](https://github.com/mapbox/mapbox-gl-js/pull/6283)
    - sửa việc truy vấn các feature layer `circle` với `-pitch-scaling: 'viewport'` hoặc `-pitch-alignment: 'map'` [#6036](https://github.com/mapbox/mapbox-gl-js/pull/6036)
    - loại bỏ hiệu ứng nhấp nháy (flicker) khi dùng kết quả truy vấn để đặt hiệu ứng hover bằng cách chuyển từ truy vấn symbol theo tile sang theo viewport [#6497](https://github.com/mapbox/mapbox-gl-js/pull/6497)
- Giữ nguyên trạng thái lịch sử trình duyệt khi cập nhật hash của `Map` [#6140](https://github.com/mapbox/mapbox-gl-js/pull/6140)
- Sửa hành vi không xác định khi `Map#addLayer` được gọi với `id` của một layer đã tồn tại [#6147](https://github.com/mapbox/mapbox-gl-js/pull/6147)
- Sửa lỗi `icon-image` không được render nếu `text-field` là chuỗi rỗng [#6164](https://github.com/mapbox/mapbox-gl-js/pull/6164)
- Đảm bảo tất cả phương thức camera phát sự kiện `rotatestart` và `rotateend` [#6187](https://github.com/mapbox/mapbox-gl-js/pull/6187)
- Luôn ẩn các nhãn trùng lặp [#6166](https://github.com/mapbox/mapbox-gl-js/pull/6166)
- Sửa lỗi `DragHandler` khi click chuột trái kết thúc drag rotate bằng chuột phải, và một cử chỉ kéo không kết thúc nếu phím control được giữ khi `mouseup` [#6193](https://github.com/mapbox/mapbox-gl-js/pull/6193)
- Thêm hỗ trợ gọi `{DragPanHandler, DragRotateHandler}#disable` trong lúc một cử chỉ đang diễn ra [#6232](https://github.com/mapbox/mapbox-gl-js/pull/6232)
- Sửa kích thước chấm vị trí người dùng của `GeolocateControl` khi `<div>` của `Map` kế thừa `box-sizing: border-box;` (bởi [@andrewharvey](https://github.com/andrewharvey))) [#6227](https://github.com/mapbox/mapbox-gl-js/pull/6232)
- Sửa lỗi lệch một đơn vị (off-by-one) trong thông báo lỗi biểu thức `array` (bởi [@drewbo](https://github.com/drewbo))) [#6269](https://github.com/mapbox/mapbox-gl-js/pull/6269)
- Cải thiện thông báo lỗi khi access token không hợp lệ gây ra lỗi 401 [#6283](https://github.com/mapbox/mapbox-gl-js/pull/6283)
- Sửa lỗi các line có `line-width` lớn hơn chiều cao sprite của thuộc tính `line-pattern` sẽ render nhầm các ảnh sprite khác [#6246](https://github.com/mapbox/mapbox-gl-js/pull/6246)
- Sửa các sự kiện touch bị hỏng cho `DragPanHandler` trên di động dùng Edge (lưu ý các handler zoom/rotate/pitch vẫn chưa hỗ trợ sự kiện touch trên Edge [#1928](https://github.com/mapbox/mapbox-gl-js/pull/1928)) [#6325](https://github.com/mapbox/mapbox-gl-js/pull/6325)
- Sửa race condition trong `VectorTileWorkerSource#reloadTile` gây timeout khi render [#6308](https://github.com/mapbox/mapbox-gl-js/issues/6308)
- Sửa lỗi gây ra các lệnh gọi `gl.stencilFunc` thừa do kiểm tra trạng thái không đúng (bởi [@yangdonglai](https://github.com/yangdonglai))) [#6330](https://github.com/mapbox/mapbox-gl-js/pull/6330)
- Sửa lỗi `mousedown` hoặc `touchstart` hủy animation camera trong bản đồ không tương tác (non-interactive) [#6338](https://github.com/mapbox/mapbox-gl-js/pull/6338)
- Sửa lỗi gây nhấp nháy toàn màn hình khi bản đồ bị pitch và symbol layer dùng `text-translate` khác 0 [#6365](https://github.com/mapbox/mapbox-gl-js/issues/6365)
- Sửa lỗi chia cho 0 trong biểu thức `to-rgba` [#6388](https://github.com/mapbox/mapbox-gl-js/pull/6388)
- Sửa lỗi cross-fading cho các thuộc tính `*-pattern` với zoom stop không nguyên [#6430](https://github.com/mapbox/mapbox-gl-js/pull/6430)
- Sửa lỗi gọi `Map#remove` trên bản đồ có tùy chọn constructor `hash: true` ném ra lỗi (bởi [@allthesignals](https://github.com/allthesignals))) [#6490](https://github.com/mapbox/mapbox-gl-js/pull/6497)
- Sửa lỗi nhấp nháy khi pan qua đường đối tuyến (anti-meridian) [#6438](https://github.com/mapbox/mapbox-gl-js/pull/6438)
- Sửa lỗi khi dùng tile có kích thước không phải lũy thừa của 2 [#6444](https://github.com/mapbox/mapbox-gl-js/pull/6444)
- Sửa lỗi `Map#moveLayer(layerId, beforeId)` xóa layer khi `layerId === beforeId` [#6542](https://github.com/mapbox/mapbox-gl-js/pull/6542)

* Sửa bản build Rollup cho module style-spec [#6575](https://github.com/mapbox/mapbox-gl-js/pull/6575)
* Sửa lỗi `Map#querySourceFeatures` ném ra `Uncaught TypeError`(https://github.com/mapbox/mapbox-gl-js/pull/6555)
* Sửa vấn đề phát hiện va chạm nhãn không chính xác cho một số symbol layer dùng chung thuộc tính layout với layer khác [#6558](https://github.com/mapbox/mapbox-gl-js/pull/6558)
* Khôi phục thuộc tính `target` cho các sự kiện `mouse{enter,over,leave,out}` [#6623](https://github.com/mapbox/mapbox-gl-js/pull/6623)

## 0.44.2

### 🐛 Sửa lỗi

- Giải pháp tạm thời cho một thay đổi phá vỡ tương thích (breaking change) trên Safari khiến trang bị cuộn/zoom để phản hồi các thao tác của người dùng vốn nhằm pan/zoom bản đồ [#6095](https://github.com/mapbox/mapbox-gl-js/issues/6095). (Lưu ý, không nên nhầm với giải pháp tạm thời từ tháng 4/2017 xử lý cùng một breaking change trên Chrome [#4259](https://github.com/mapbox/mapbox-gl-js/issues/6095). Xem thêm https://github.com/WICG/interventions/issues/18, https://bugs.webkit.org/show_bug.cgi?id=182521, https://bugs.chromium.org/p/chromium/issues/detail?id=639227 .)

## 0.44.1

### 🐛 Sửa lỗi

- Sửa lỗi các feature từ symbol layer bị bỏ sót khỏi `map.queryRenderedFeatures()` [#6074](https://github.com/mapbox/mapbox-gl-js/issues/6074)
- Sửa lỗi phát sinh khi scroll-zoom và drag-pan cùng lúc. [#6106](https://github.com/mapbox/mapbox-gl-js/issues/6106)
- Sửa lỗi drag-pan không tiếp tục sau một khoảng dừng ngắn [#6063](https://github.com/mapbox/mapbox-gl-js/issues/6063)

## 0.44.0

### ✨ Tính năng và cải tiến

- Chính sách CSP của trang dùng mapbox-gl-js không còn cần bao gồm `script-src 'unsafe-eval'` [#559](https://github.com/mapbox/mapbox-gl-js/issues/559)
- Thêm phương thức `LngLatBounds#isEmpty()` [#5917](https://github.com/mapbox/mapbox-gl-js/pull/5917)
- Cập nhật lên flow 0.62.0 [#5923](https://github.com/mapbox/mapbox-gl-js/issues/5923)
- Cho phép tùy chọn ẩn compass và zoom control ([#5348](https://github.com/mapbox/mapbox-gl-js/pull/5348)) (bởi [@matijs](https://github.com/matijs)))
- Thêm tùy chọn `collectResourceTiming` để bật thu thập dữ liệu [Resource Timing](https://developer.mozilla.org/en-US/docs/Web/API/Resource_Timing_API/Using_the_Resource_Timing_API) cho các request được thực hiện từ Web Worker. ([#5948](https://github.com/mapbox/mapbox-gl-js/issues/5948))
- Cải thiện giao diện chấm vị trí người dùng trên các trình duyệt ([#5498](https://github.com/mapbox/mapbox-gl-js/pull/5498)) (bởi [@jasonbarry](https://github.com/jasonbarry)))

### 🐛 Sửa lỗi

- Sửa lỗi phát sinh bởi biểu thức `==` và `!=` [#5947](https://github.com/mapbox/mapbox-gl-js/issues/5947)
- Image source tôn trọng `renderWorldCopies` [#5932](https://github.com/mapbox/mapbox-gl-js/pull/5932)
- Sửa transition về fill-outline-color mặc định [#5953](https://github.com/mapbox/mapbox-gl-js/issues/5953)
- Sửa transition cho các thuộc tính light [#5982](https://github.com/mapbox/mapbox-gl-js/issues/5982)
- Sửa va chạm symbol nhỏ trên bản đồ bị pitch [#5913](https://github.com/mapbox/mapbox-gl-js/pull/5913)
- Sửa rò rỉ bộ nhớ sau `Map#remove()` [#5943](https://github.com/mapbox/mapbox-gl-js/pull/5943), [#5951](https://github.com/mapbox/mapbox-gl-js/pull/5951)
- Sửa lỗi `GeoJSONSource#setData()` khiến nhãn mờ đi rồi hiện lại ([#6002](https://github.com/mapbox/mapbox-gl-js/issues/6002))
- Sửa lỗi có thể gây va chạm sai cho các nhãn đặt rất gần nhau ở zoom level thấp ([#5993](https://github.com/mapbox/mapbox-gl-js/issues/5993))
- Sửa lỗi sự kiện `move` được phát không đồng bộ với chuyển động thực tế của bản đồ ([#6005](https://github.com/mapbox/mapbox-gl-js/pull/6005))
- Sửa lỗi `Map` không phát sự kiện `mouseover` ([#6000](https://github.com/mapbox/mapbox-gl-js/pull/6000)] (bởi [@jay-manday](https://github.com/jay-manday)))
- Sửa lỗi render mờ của tile raster ([#4552](https://github.com/mapbox/mapbox-gl-js/issues/4552))
- Sửa rò rỉ bộ nhớ tiềm ẩn do xóa layer ([#5995](https://github.com/mapbox/mapbox-gl-js/issues/5995))
- Sửa lỗi icon attribution hiển thị sai trong bản đồ dạng compact không dùng dữ liệu Mapbox ([#6042](https://github.com/mapbox/mapbox-gl-js/pull/6042))
- Sửa vị trí của phần tử marker mặc định ([#6012](https://github.com/mapbox/mapbox-gl-js/pull/6012)) (bởi [@andrewharvey](https://github.com/andrewharvey)))

## 0.43.0 (21 tháng 12, 2017)

### ⚠️ Thay đổi phá vỡ tương thích

- Giờ đây sẽ báo lỗi khi cố gắng xóa một source đang được sử dụng [#5562](https://github.com/mapbox/mapbox-gl-js/pull/5562)
- Giờ đây sẽ báo lỗi nếu layer được chỉ định bởi tham số `before` cho `moveLayer` không tồn tại [#5679](https://github.com/mapbox/mapbox-gl-js/pull/5679)
- `"colorSpace": "hcl"` giờ dùng nội suy đường ngắn nhất (shortest-path interpolation) cho hue [#5811](https://github.com/mapbox/mapbox-gl-js/issues/5811)

### ✨ Tính năng và cải tiến

- Giới thiệu hillshading phía client với loại source `raster-dem` và loại layer `hillshade` [#5286](https://github.com/mapbox/mapbox-gl-js/pull/5286)
- Các source GeoJSON dùng ít hơn 2 lần bộ nhớ và tạo tile nhanh hơn 20%–100% [#5799](https://github.com/mapbox/mapbox-gl-js/pull/5799)
- Bật giá trị data-driven cho text-font [#5698](https://github.com/mapbox/mapbox-gl-js/pull/5698)
- Bật giá trị data-driven cho heatmap-radius [#5898](https://github.com/mapbox/mapbox-gl-js/pull/5898)
- Thêm getter và setter cho offset trên marker [#5759](https://github.com/mapbox/mapbox-gl-js/pull/5759)
- Thêm `Map#hasImage` [#5775](https://github.com/mapbox/mapbox-gl-js/pull/5775)
- Cải thiện typing cho biểu thức `==` và `!=` [#5840](https://github.com/mapbox/mapbox-gl-js/pull/5840)
- Biểu thức `coalesce` hữu ích hơn [#5755](https://github.com/mapbox/mapbox-gl-js/issues/5755)
- Bật assertion kiểu ngầm định cho các kiểu mảng [#5738](https://github.com/mapbox/mapbox-gl-js/pull/5738)
- Cải thiện độ chính xác của hash control [#5767](https://github.com/mapbox/mapbox-gl-js/pull/5767)
- `supported()` giờ trả về false trên các phiên bản IE 11 cũ không hỗ trợ Web Worker blob URL [#5801](https://github.com/mapbox/mapbox-gl-js/pull/5801)
- Loại bỏ flow global TileJSON và Transferable [#5668](https://github.com/mapbox/mapbox-gl-js/pull/5668)
- Cải thiện hiệu năng của image, video, và canvas source [#5845](https://github.com/mapbox/mapbox-gl-js/pull/5845)

### 🐛 Sửa lỗi

- Sửa lỗi popup và marker bị trễ (lag) khi animation pan [#4670](https://github.com/mapbox/mapbox-gl-js/issues/4670)
- Sửa lỗi mờ dần symbol layer gây ra bởi setData [#5716](https://github.com/mapbox/mapbox-gl-js/issues/5716)
- Sửa hành vi của biểu thức `to-rgba` và `rgba` [#5778](https://github.com/mapbox/mapbox-gl-js/pull/5778), [#5866](https://github.com/mapbox/mapbox-gl-js/pull/5866)
- Sửa cross-fading của `*-pattern` và `line-dasharray` [#5791](https://github.com/mapbox/mapbox-gl-js/pull/5791)
- Sửa thuộc tính function `colorSpace` [#5843](https://github.com/mapbox/mapbox-gl-js/pull/5843)
- Sửa việc diff style khi thay đổi thuộc tính source GeoJSON [#5731](https://github.com/mapbox/mapbox-gl-js/issues/5731)
- Sửa lỗi mất nhãn khi zoom out từ tile bị overzoom [#5827](https://github.com/mapbox/mapbox-gl-js/issues/5827)
- Sửa lỗi mất nhãn khi zoom out và dùng setData nhanh [#5837](https://github.com/mapbox/mapbox-gl-js/issues/5837)
- Xử lý NaN như đầu vào cho biểu thức step và interpolate [#5757](https://github.com/mapbox/mapbox-gl-js/pull/5757)
- Clone giá trị thuộc tính ở đầu vào và đầu ra [#5806](https://github.com/mapbox/mapbox-gl-js/pull/5806)
- Cập nhật dependency geojson-rewind [#5769](https://github.com/mapbox/mapbox-gl-js/pull/5769)
- Cho phép đặt popup của Marker trước LngLat [#5893](https://github.com/mapbox/mapbox-gl-js/pull/5893)

## 0.42.2 (21 tháng 11, 2017)

### 🐛 Sửa lỗi

- Thêm box-sizing vào class "mapboxgl-ctrl-scale" [#5715](https://github.com/mapbox/mapbox-gl-js/pull/5715)
- Sửa lỗi render trên Safari [#5712](https://github.com/mapbox/mapbox-gl-js/issues/5712)
- Sửa lỗi "Cannot read property 'hasTransition' of undefined" [#5714](https://github.com/mapbox/mapbox-gl-js/issues/5714)
- Sửa lỗi tile raster bị đặt sai vị trí [#5713](https://github.com/mapbox/mapbox-gl-js/issues/5713)
- Sửa lỗi fading tile raster [#5722](https://github.com/mapbox/mapbox-gl-js/issues/5722)
- Đảm bảo filter chưa được đặt là undefined thay vì null [#5727](https://github.com/mapbox/mapbox-gl-js/pull/5727)
- Khôi phục pitch-with-rotate cho nav control [#5725](https://github.com/mapbox/mapbox-gl-js/pull/5725)
- Xác thực tùy chọn container trong map constructor [#5695](https://github.com/mapbox/mapbox-gl-js/pull/5695)
- Sửa hành vi queryRenderedFeatures cho các feature hiển thị trong nhiều layer [#5172](https://github.com/mapbox/mapbox-gl-js/issues/5172)

## 0.42.1 (17 tháng 11, 2017)

### 🐛 Sửa lỗi

- Giải pháp tạm thời cho lỗi bản đồ nhấp nháy trên Chrome 62+ với card đồ họa Intel Iris Graphics 6100 [#5704](https://github.com/mapbox/mapbox-gl-js/pull/5704)
- Render lại bản đồ khi `map.showCollisionBoxes` được đặt là `false` [#5673](https://github.com/mapbox/mapbox-gl-js/pull/5673)
- Sửa transition từ giá trị thuộc tính mặc định [#5682](https://github.com/mapbox/mapbox-gl-js/pull/5682)
- Sửa việc cập nhật runtime cho `heatmap-color` [#5682](https://github.com/mapbox/mapbox-gl-js/pull/5682)
- Sửa lỗi `history.replaceState` trên mobile Safari [#5613](https://github.com/mapbox/mapbox-gl-js/pull/5613)

### ✨ Tính năng và cải tiến

- Cung cấp phần tử mặc định cho class Marker [#5661](https://github.com/mapbox/mapbox-gl-js/pull/5661)

## 0.42.0 (10 tháng 11, 2017)

### ⚠️ Thay đổi phá vỡ tương thích

- Yêu cầu `heatmap-color` dùng biểu thức thay vì stop function [#5624](https://github.com/mapbox/mapbox-gl-js/issues/5624)
- Loại bỏ hỗ trợ xác thực và di trú (migrating) style v6
- Loại bỏ hỗ trợ xác thực style v7 [#5604](https://github.com/mapbox/mapbox-gl-js/pull/5604)
- Loại bỏ hỗ trợ dùng `{tokens}` trong biểu thức cho `text-field` và `icon-image` [#5599](https://github.com/mapbox/mapbox-gl-js/issues/5599)
- Tách biểu thức `curve` thành biểu thức `step` và `interpolate` [#5542](https://github.com/mapbox/mapbox-gl-js/pull/5542)
- Không cho phép nội suy trong biểu thức cho `line-dasharray` [#5519](https://github.com/mapbox/mapbox-gl-js/pull/5519)

### ✨ Tính năng và cải tiến

- Cải thiện phát hiện va chạm nhãn [#5150](https://github.com/mapbox/mapbox-gl-js/pull/5150)
    - Nhãn từ các source khác nhau giờ sẽ va chạm lẫn nhau
    - Va chạm gây ra bởi rotation và pitch giờ được chuyển tiếp mượt mà bằng hiệu ứng fade
    - Thuật toán cải tiến giúp giảm va chạm sai, đặt nhãn dày đặc hơn, và ổn định nhãn tốt hơn khi xoay
- Thêm biểu thức `sqrt` [#5493](https://github.com/mapbox/mapbox-gl-js/pull/5493)

### 🐛 Sửa lỗi và cải thiện báo cáo lỗi

- Sửa các phép tính viewport cho `fitBounds` khi cả zoom và padding cùng thay đổi [#4846](https://github.com/mapbox/mapbox-gl-js/issues/4846)
- Sửa lỗi WebGL "range out of bounds for buffer" gây ra bởi symbol layer đã sắp xếp (sorted) [#5620](https://github.com/mapbox/mapbox-gl-js/issues/5620)
- Sửa lỗi fading symbol qua các lần reload tile [#5491](https://github.com/mapbox/mapbox-gl-js/issues/5491)
- Thay đổi thứ tự render tile để khớp hơn với GL Native [#5601](https://github.com/mapbox/mapbox-gl-js/pull/5601)
- Đảm bảo không có lỗi nào phát sinh khi gọi `queryRenderedFeatures` trên một heatmap layer [#5594](https://github.com/mapbox/mapbox-gl-js/pull/5594)
- Sửa lỗi `queryRenderedSymbols` trả về kết quả từ các source khác nhau [#5554](https://github.com/mapbox/mapbox-gl-js/issues/5554)
- Sửa các vấn đề render CJK [#5544](https://github.com/mapbox/mapbox-gl-js/issues/5544), [#5546](https://github.com/mapbox/mapbox-gl-js/issues/5546)
- Tính đến `circle-stroke-width` trong `queryRenderedFeatures` [#5514](https://github.com/mapbox/mapbox-gl-js/pull/5514)
- Sửa việc render fill layer nằm trên raster layer [#5513](https://github.com/mapbox/mapbox-gl-js/pull/5513)
- Sửa việc render circle layer với `circle-stroke-opacity` bằng 0 [#5496](https://github.com/mapbox/mapbox-gl-js/issues/5496)
- Sửa rò rỉ bộ nhớ gây ra bởi các actor callback [#5443](https://github.com/mapbox/mapbox-gl-js/issues/5443)
- Sửa kích thước source cache cho các raster source có tile size khác 512px [#4313](https://github.com/mapbox/mapbox-gl-js/issues/4313)
- Xác thực rằng biểu thức zoom chỉ xuất hiện ở cấp cao nhất của một biểu thức [#5609](https://github.com/mapbox/mapbox-gl-js/issues/5609)
- Xác thực rằng biểu thức step và interpolate không có stop trùng lặp [#5605](https://github.com/mapbox/mapbox-gl-js/issues/5605)
- Sửa việc render `icon-text-fit` với `text-size` kiểu data-driven [#5632](https://github.com/mapbox/mapbox-gl-js/pull/5632)
- Cải thiện xác thực để bắt các trường hợp dùng cú pháp function đã lỗi thời [#5667](https://github.com/mapbox/mapbox-gl-js/pull/5667)
- Cho phép tọa độ độ cao (altitude) trong trường `position` của GeoJSON [#5608](https://github.com/mapbox/mapbox-gl-js/pull/5608)

## 0.41.0 (11 tháng 10, 2017)

### :warning: Thay đổi phá vỡ tương thích

- Loại bỏ hỗ trợ paint class [#3643](https://github.com/mapbox/mapbox-gl-js/pull/3643). Thay vào đó, hãy dùng API runtime styling hoặc `Map#setStyle`.
- Hoàn tác tùy chọn `contextType` của canvas source được thêm ở 0.40.0 [#5449](https://github.com/mapbox/mapbox-gl-js/pull/5449)

### :bug: Sửa lỗi

- Cắt (clip) tile raster để tránh chồng lấn tile [#5105](https://github.com/mapbox/mapbox-gl-js/pull/5105)
- Bảo vệ khỏi trường hợp biên (edgecase) về offset trong flyTo [#5331](https://github.com/mapbox/mapbox-gl-js/pull/5331)
- Đảm bảo bản đồ được cập nhật sau khi sprite tải xong [#5367](https://github.com/mapbox/mapbox-gl-js/pull/5367)
- Giới hạn thời lượng animation trên flyTo bằng tùy chọn maxDuration [#5349](https://github.com/mapbox/mapbox-gl-js/pull/5349)
- Khiến double-tap zoom in với hệ số 2 trên iOS [#5274](https://github.com/mapbox/mapbox-gl-js/pull/5274)
- Sửa lỗi render với tile raster trong suốt (translucent) [#5380](https://github.com/mapbox/mapbox-gl-js/pull/5380)
- Báo lỗi nếu tham số 'before' không hợp lệ được truyền vào Map#addLayer [#5401](https://github.com/mapbox/mapbox-gl-js/pull/5401)
- Hoàn tác bản sửa lỗi buffer ảnh trung gian của CanvasSource [#5449](https://github.com/mapbox/mapbox-gl-js/pull/5449)

### :sparkles: Tính năng và cải tiến

- Dùng thao tác setData khi diff các source geojson [#5332](https://github.com/mapbox/mapbox-gl-js/pull/5332)
- Trả về sớm (return early) từ các lệnh gọi draw trên các layer có opacity=0 [#5429](https://github.com/mapbox/mapbox-gl-js/pull/5429)
- Loại layer [heatmap](https://www.mapbox.com/mapbox-gl-js/example/heatmap-layer/) giờ đây khả dụng. Loại layer này cho phép bạn trực quan hóa và khám phá các bộ dữ liệu điểm khổng lồ, phản ánh tốt hình dạng và mật độ dữ liệu đồng thời trông rất đẹp mắt. Xem [bài blog](https://blog.mapbox.com/sneak-peek-at-heatmaps-in-mapbox-gl-73b41d4b16ae) để biết thêm chi tiết.
  ![heatmap screenshot](https://cdn-images-1.medium.com/max/1600/1*Dme5MAgdA3pYdTRHUQzvLw.png)
- Giá trị của một thuộc tính style hoặc filter giờ đây có thể là một [biểu thức (expression)](https://www.mapbox.com/mapbox-gl-js/style-spec/#expressions). Biểu thức là cách thực hiện styling theo dữ liệu (data-driven) và theo zoom (zoom-driven) mang lại sự linh hoạt và kiểm soát tốt hơn, đồng thời hợp nhất cú pháp thuộc tính và filter.

    Trước đây, styling theo dữ liệu và theo zoom dựa vào stop function: bạn chỉ định một thuộc tính feature và một tập cặp input-output về cơ bản định nghĩa một "thang đo" (scale) cho cách tính toán style dựa trên thuộc tính feature. Ví dụ, đoạn sau sẽ đặt màu circle theo thang từ xanh sang đỏ dựa trên giá trị của `feature.properties.population`:

    ```
    "circle-color": {
      "property": "population",
      "stops": [
        [0, "green"],
        [1000000, "red"]
      ]
    }
    ```

    Cách tiếp cận này mạnh mẽ, nhưng chúng tôi đã thấy nhiều trường hợp sử dụng mà stop function không thể đáp ứng. Biểu thức mang lại sự linh hoạt để giải quyết các trường hợp như sau:

    **Nhiều thuộc tính feature**
    Dùng nhiều hơn một thuộc tính feature để tính toán một thuộc tính style cho trước. Ví dụ: định màu polygon đất dựa trên cả `feature.properties.land_use_category` và `feature.properties.elevation`.

    **Số học**
    Với một số trường hợp sử dụng, cần thực hiện tính toán số học trên dữ liệu đầu vào. Một ví dụ là định kích thước circle để biểu diễn dữ liệu định lượng. Vì kích thước hiển thị của circle trên màn hình thực chất là diện tích của nó (và A=πr^2), cách đúng để scale `circle-radius` là `square_root(feature.properties.input_data_value)`. Một ví dụ khác là chuyển đổi đơn vị: dữ liệu feature có thể chứa các thuộc tính theo một đơn vị cụ thể nào đó. Để hiển thị dữ liệu như vậy theo đơn vị phù hợp với, chẳng hạn, sở thích hoặc vị trí của người dùng, cần có khả năng thực hiện các phép toán đơn giản (nhân, chia) trên bất kỳ giá trị nào có trong dữ liệu.

    **Logic điều kiện**
    Đây là một trường hợp lớn: logic if-then cơ bản, ví dụ để quyết định chính xác văn bản nào sẽ hiển thị cho một nhãn dựa trên các thuộc tính có sẵn trong feature hoặc thậm chí độ dài của tên. Một ví dụ điển hình là hỗ trợ đúng cho nhãn song ngữ, khi chúng ta phải quyết định hiển thị địa phương + tiếng Anh, chỉ địa phương, hay chỉ tiếng Anh, dựa trên dữ liệu có sẵn cho mỗi feature.

    **Thao tác chuỗi**
    Kiểm soát động hơn với văn bản nhãn bằng các thao tác như chuyển đổi chữ hoa/chữ thường/viết hoa chữ cái đầu, định dạng số theo địa phương, v.v. Nếu không có chức năng này, việc tạo và lặp lại nội dung nhãn sẽ đòi hỏi khối lượng chuẩn bị dữ liệu lớn.

    **Filter**
    Các filter style layer có những hạn chế tương tự. Hơn nữa, chúng dùng cú pháp khác, mặc dù công việc của chúng rất giống với các hàm styling theo dữ liệu: filter nói rằng "đây là cách nhìn vào một feature và quyết định có vẽ nó hay không", còn các hàm style theo dữ liệu nói rằng "đây là cách nhìn vào một feature và quyết định cách định kích thước/màu sắc/vị trí cho nó". Biểu thức cung cấp một cú pháp thống nhất để định nghĩa các phần của style cần được tính toán động từ dữ liệu feature.

    Để biết thông tin về cú pháp và hành vi của biểu thức, vui lòng xem [tài liệu](https://www.mapbox.com/mapbox-gl-js/style-spec/#expressions).

### :wrench: Cải tiến quy trình phát triển

- Làm cho công cụ chạy benchmark hiệu năng thông tin hơn và đáng tin cậy hơn về mặt thống kê

## 0.40.1 (18 tháng 9, 2017)

### :bug: Sửa lỗi

- Sửa lỗi nhấp nháy khi zoom in trên tile bị overzoom [#5295](https://github.com/mapbox/mapbox-gl-js/pull/5295)
- Loại bỏ lệnh gọi thừa đến Tile#redoPlacement cho các thay đổi camera chỉ zoom hoặc pitch thấp [#5284](https://github.com/mapbox/mapbox-gl-js/pull/5284)
- Sửa lỗi tọa độ `CanvasSource` bị lật và cải thiện hiệu năng cho các `CanvasSource` không animate [#5303](https://github.com/mapbox/mapbox-gl-js/pull/5303)
- Sửa lỗi bản đồ không render trong một số trường hợp trên Internet Explorer 11 [#5321](https://github.com/mapbox/mapbox-gl-js/pull/5321)
- Loại bỏ giới hạn trên của thuộc tính `fill-extrusion-height` [#5320](https://github.com/mapbox/mapbox-gl-js/pull/5320)

## 0.40.0 (13 tháng 9, 2017)

### :warning: Thay đổi phá vỡ tương thích

- `Map#addImage` giờ yêu cầu ảnh dưới dạng `HTMLImageElement`, `ImageData`, hoặc object có thuộc tính `width`, `height`, và
  `data` theo cùng định dạng với `ImageData`. Nó không còn chấp nhận `ArrayBufferView` thô trong tham số thứ hai
  và tùy chọn `width`, `height` trong tham số thứ ba.
- Các source `canvas` giờ yêu cầu tùy chọn `contextType` chỉ định drawing context liên kết với canvas source. [#5155](https://github.com/mapbox/mapbox-gl-js/pull/5155)

### :sparkles: Tính năng và cải tiến

- Sửa việc render đúng cho nhiều layer `fill-extrusion` trên cùng một bản đồ [#5101](https://github.com/mapbox/mapbox-gl-js/pull/5101)
- Thêm thuộc tính `icon-anchor` cho symbol layer [#5183](https://github.com/mapbox/mapbox-gl-js/pull/5183)
- Thêm tùy chọn `transformRequest` theo từng map, cho phép người dùng cung cấp callback biến đổi URL request tài nguyên [#5021](https://github.com/mapbox/mapbox-gl-js/pull/5021)
- Thêm hỗ trợ data-driven styling cho
    - `text-max-width` [#5067](https://github.com/mapbox/mapbox-gl-js/pull/5067)
    - `text-letter-spacing` [#5071](https://github.com/mapbox/mapbox-gl-js/pull/5071)
    - `line-join` [#5020](https://github.com/mapbox/mapbox-gl-js/pull/5020)
- Thêm hỗ trợ SDF icon trong `Map#addImage()` [#5181](https://github.com/mapbox/mapbox-gl-js/pull/5181)
- Thêm đơn vị hải lý (nautical miles) vào ScaleControl [#5238](https://github.com/mapbox/mapbox-gl-js/pull/5238) (bởi [@fmairesse](https://github.com/fmairesse)))
- Loại bỏ giới hạn toàn bản đồ về số lượng glyph và sprite có thể dùng trong một style [#141](https://github.com/mapbox/mapbox-gl-js/issues/141). (Sửa bằng [#5190](https://github.com/mapbox/mapbox-gl-js/pull/5190), xem thêm [mapbox-gl-native[#9213](https://github.com/mapbox/mapbox-gl-js/issues/9213)](https://github.com/mapbox/mapbox-gl-native/pull/9213)
- Nhiều tối ưu hóa hiệu năng (bao gồm [#5108](https://github.com/mapbox/mapbox-gl-js/pull/5108) cảm ơn [@pirxpilot](https://github.com/pirxpilot)))

### :bug: Sửa lỗi

- Thêm tài liệu còn thiếu cho các sự kiện mouseenter, mouseover, mouseleave [#4772](https://github.com/mapbox/mapbox-gl-js/issues/4772)
- Thêm tài liệu còn thiếu cho phương thức `Marker#getElement()` [#5242](https://github.com/mapbox/mapbox-gl-js/pull/5242)
- Sửa lỗi khi xóa canvas source với animate=true khiến bản đồ kẹt trong vòng lặp render [#5097](https://github.com/mapbox/mapbox-gl-js/issues/5097)
- Sửa việc phát hiện fullscreen trên Firefox [#5272](https://github.com/mapbox/mapbox-gl-js/pull/5272)
- Sửa hiện tượng z-fighting trên các fill chồng lấn trong cùng một layer [#3320](https://github.com/mapbox/mapbox-gl-js/issues/3320)
- Sửa việc xử lý giá trị thập phân (fractional) cho `layer.minzoom` [#2929](https://github.com/mapbox/mapbox-gl-js/issues/2929)
- Làm rõ thứ tự tọa độ trong tài liệu cho tùy chọn `center` [#5042](https://github.com/mapbox/mapbox-gl-js/pull/5042) (bởi [@karthikb351](https://github.com/karthikb351)))
- Sửa đầu ra của stop function khi hai stop có cùng giá trị input [#5020](https://github.com/mapbox/mapbox-gl-js/pull/5020) (bởi [@edpop](https://github.com/edpop))
- Sửa lỗi khi dùng `Map#addLayer()` với một inline source làm thay đổi (mutate) input của nó [#4040](https://github.com/mapbox/mapbox-gl-js/issues/4040)
- Sửa selector css keyframes không hợp lệ [#5075](https://github.com/mapbox/mapbox-gl-js/pull/5075) (bởi [@aar0nr](https://github.com/aar0nr)))
- Sửa lỗi đặc thù GPU khiến canvas source gây lỗi [#4262](https://github.com/mapbox/mapbox-gl-js/issues/4262)
- Sửa race condition trong xử lý symbol layer gây ra lỗi không được bắt ngẫu nhiên [#5185](https://github.com/mapbox/mapbox-gl-js/pull/5185)
- Sửa lỗi nhãn line render sai trên tile bị overzoom [#5120](https://github.com/mapbox/mapbox-gl-js/pull/5120)
- Sửa lỗi `NavigationControl` kích hoạt sự kiện chuột không mong muốn [#5148](https://github.com/mapbox/mapbox-gl-js/issues/5148)
- Sửa lỗi click vào compass của `NavigationControl` gây lỗi trên IE 11 [#4784](https://github.com/mapbox/mapbox-gl-js/issues/4784)
- Loại bỏ dependency vào module `fast-stable-stringify` (giấy phép GPL-3) [#5152](https://github.com/mapbox/mapbox-gl-js/issues/5152)
- Sửa lỗi event listener riêng của layer gây lỗi sau khi layer mục tiêu bị xóa khỏi bản đồ [#5145](https://github.com/mapbox/mapbox-gl-js/issues/5145)
- Sửa `Marker#togglePopup()` không trả về instance marker [#5116](https://github.com/mapbox/mapbox-gl-js/issues/5116)
- Sửa lỗi vị trí marker không thích ứng khi kích thước phần tử marker thay đổi [#5133](https://github.com/mapbox/mapbox-gl-js/issues/5133)
- Sửa lỗi render ảnh hưởng đến GPU Broadcom [#5073](https://github.com/mapbox/mapbox-gl-js/pull/5073)

### :wrench: Cải tiến quy trình phát triển

- Thêm (và giờ yêu cầu) chú thích kiểu Flow trong phần lớn codebase.
- Chuyển sang CircleCI 2.0 [#4939](https://github.com/mapbox/mapbox-gl-js/pull/4939)

## 0.39.1 (24 tháng 7, 2017)

### :bug: Sửa lỗi

- Sửa lỗi đóng gói (packaging) trong 0.39.0 [#5025](https://github.com/mapbox/mapbox-gl-js/issues/5025)
- Đánh giá đúng các identity function dựa trên enum [#5023](https://github.com/mapbox/mapbox-gl-js/issues/5023)

## 0.39.0 (21 tháng 7, 2017)

### :warning: Thay đổi phá vỡ tương thích

- Các thay đổi phá vỡ tương thích của `GeolocateControl` [#4479](https://github.com/mapbox/mapbox-gl-js/pull/4479)
    - Tùy chọn `watchPosition` đã được thay thế bằng `trackUserLocation`
    - Thao tác camera đã thay đổi từ `jumpTo` (không animate) sang `fitBounds` (có animate). Một hệ quả là pitch bản đồ không còn bị reset, mặc dù bearing vẫn được reset về 0.
    - Độ chính xác của geolocation do thiết bị cung cấp được dùng để thiết lập view (trước đây được cố định ở zoom level 17). `maxZoom` giờ có thể kiểm soát qua tùy chọn `fitBoundsOptions` mới (mặc định là 15).
- Neo (anchor) `Marker` ở tâm theo mặc định [#5019](https://github.com/mapbox/mapbox-gl-js/issues/5019) [@andrewharvey](https://github.com/andrewharvey)
- Tăng `significantRotateThreshold` cho `TouchZoomRotateHandler` [#4971](https://github.com/mapbox/mapbox-gl-js/pull/4971), [@dagjomar](https://github.com/dagjomar)

### :sparkles: Tính năng và cải tiến

- Cải thiện hiệu năng cập nhật các source GeoJSON [#4069](https://github.com/mapbox/mapbox-gl-js/pull/4069), [@ezheidtmann](https://github.com/ezheidtmann)
- Cải thiện tốc độ render các layer extrusion [#4818](https://github.com/mapbox/mapbox-gl-js/pull/4818)
- Cải thiện độ rõ ràng của nhãn line trong các view bị pitch [#4781](https://github.com/mapbox/mapbox-gl-js/pull/4781)
- Cải thiện độ rõ ràng của nhãn line trên các đường cong [#4853](https://github.com/mapbox/mapbox-gl-js/pull/4853)
- Thêm khả năng theo dõi vị trí người dùng cho `GeolocateControl` [#4479](https://github.com/mapbox/mapbox-gl-js/pull/4479), [@andrewharvey](https://github.com/andrewharvey)
    - Tùy chọn mới `showUserLocation` để vẽ một "chấm" (dot) làm `Marker` trên bản đồ tại vị trí người dùng
    - Trạng thái khóa hoạt động (active lock) và nền (background) được giới thiệu với `trackUserLocation`. Khi ở khóa hoạt động, camera sẽ cập nhật để theo vị trí người dùng, tuy nhiên nếu camera bị thay đổi bởi API hoặc UI thì control sẽ chuyển sang trạng thái nền, nơi nó sẽ không cập nhật camera để theo vị trí người dùng nữa.
    - Tùy chọn mới `fitBoundsOptions` để kiểm soát thao tác camera
    - Sự kiện mới `trackuserlocationstart` và `trackuserlocationend`
    - Phương thức mới `LngLat.toBounds` để mở rộng một vị trí điểm theo bán kính cho trước thành một object `LngLatBounds`
- Đưa file CSS chính vào `package.json` [#4809](https://github.com/mapbox/mapbox-gl-js/pull/4809), [@tomscholz](https://github.com/tomscholz)
- Thêm hỗ trợ property function (data-driven styling) cho `line-width` [#4773](https://github.com/mapbox/mapbox-gl-js/pull/4773)
- Thêm hỗ trợ property function (data-driven styling) cho `text-anchor` [#4997](https://github.com/mapbox/mapbox-gl-js/pull/4997)
- Thêm hỗ trợ property function (data-driven styling) cho `text-justify` [#5000](https://github.com/mapbox/mapbox-gl-js/pull/5000)
- Thêm tùy chọn `maxTileCacheSize` [#4778](https://github.com/mapbox/mapbox-gl-js/pull/4778), [@jczaplew](https://github.com/jczaplew)
- Thêm thuộc tính mới `icon-pitch-alignment` và `circle-pitch-alignment` [#4869](https://github.com/mapbox/mapbox-gl-js/pull/4869) [#4871](https://github.com/mapbox/mapbox-gl-js/pull/4871)
- Thêm phương thức `Map#getMaxBounds` [#4890](https://github.com/mapbox/mapbox-gl-js/pull/4890), [@andrewharvey](https://github.com/andrewharvey) [@lamuertepeluda](https://github.com/lamuertepeluda)
- Thêm tùy chọn (`localIdeographFontFamily`) để dùng TinySDF nhằm tránh tải các glyph CJK tốn kém [#4895](https://github.com/mapbox/mapbox-gl-js/pull/4895)
- Nếu `config.API_URL` chứa một path, thêm nó vào trước URL request [#4995](https://github.com/mapbox/mapbox-gl-js/pull/4995)
- Nâng phiên bản `supercluster` để expose thuộc tính `cluster_id` trên các source đã cluster [#5002](https://github.com/mapbox/mapbox-gl-js/pull/5002)

### :bug: Sửa lỗi

- Không hiển thị `FullscreenControl` trên các thiết bị không được hỗ trợ [#4838](https://github.com/mapbox/mapbox-gl-js/pull/4838), [@stepankuzmin](https://github.com/stepankuzmin)
- Sửa lỗi build yarn trên máy Windows [#4887](https://github.com/mapbox/mapbox-gl-js/pull/4887)
- Ngăn rò rỉ bộ nhớ tiềm ẩn bằng cách luôn gửi `loadData` đến cùng một worker [#4877](https://github.com/mapbox/mapbox-gl-js/pull/4877)
- Sửa lỗi ngăn rtlTextPlugin tải trước sự kiện `load` style ban đầu [#4870](https://github.com/mapbox/mapbox-gl-js/pull/4870)
- Sửa lỗi khiến runtime-styling không có hiệu lực trong một số trường hợp [#4893](https://github.com/mapbox/mapbox-gl-js/pull/4893)
- Ngăn yêu cầu glyph dọc (vertical) cho các nhãn không thể được xoay dọc (verticalize) [#4720](https://github.com/mapbox/mapbox-gl-js/issues/4720)
- Sửa việc phát hiện ký tự cho Zanabazar Square [#4940](https://github.com/mapbox/mapbox-gl-js/pull/4940)
- Sửa logic `LogoControl` cập nhật đúng cách, và ẩn `<div>` thay vì xóa nó khỏi DOM khi không cần thiết [#4842](https://github.com/mapbox/mapbox-gl-js/pull/4842)
- Sửa `GeoJSONSource#serialize` để bao gồm tất cả tùy chọn
- Sửa xử lý lỗi trong `GlyphSource#getSimpleGlyphs`[#4992](https://github.com/mapbox/mapbox-gl-js/pull/4992)
- Sửa lỗi `setStyle` reload tile raster [#4852](https://github.com/mapbox/mapbox-gl-js/pull/4852)
- Sửa lỗi symbol layer không render trên thiết bị có device pixel ratio không nguyên [#4989](https://github.com/mapbox/mapbox-gl-js/pull/4989)
- Sửa lỗi `Map#queryRenderedFeatures` bị lỗi khi trả về không có kết quả [#4993](https://github.com/mapbox/mapbox-gl-js/pull/4993)
- Sửa lỗi `Map#areTilesLoaded` luôn là false trên các sự kiện `sourcedata` khi reload tile [#4987](https://github.com/mapbox/mapbox-gl-js/pull/4987)
- Sửa lỗi các property function dạng categorical gây lỗi với stop không theo thứ tự tăng dần [#4996](https://github.com/mapbox/mapbox-gl-js/pull/4996)

### :hammer_and_wrench: Thay đổi quy trình phát triển

- Dùng flow để định kiểu phần lớn codebase [#4629](https://github.com/mapbox/mapbox-gl-js/pull/4629) [#4903](https://github.com/mapbox/mapbox-gl-js/pull/4903) [#4909](https://github.com/mapbox/mapbox-gl-js/pull/4909) [#4910](https://github.com/mapbox/mapbox-gl-js/pull/4910) [#4911](https://github.com/mapbox/mapbox-gl-js/pull/4911) [#4913](https://github.com/mapbox/mapbox-gl-js/pull/4913) [#4915](https://github.com/mapbox/mapbox-gl-js/pull/4915) [#4918](https://github.com/mapbox/mapbox-gl-js/pull/4918) [#4932](https://github.com/mapbox/mapbox-gl-js/pull/4932) [#4933](https://github.com/mapbox/mapbox-gl-js/pull/4933) [#4948](https://github.com/mapbox/mapbox-gl-js/pull/4948) [#4949](https://github.com/mapbox/mapbox-gl-js/pull/4949) [#4955](https://github.com/mapbox/mapbox-gl-js/pull/4955) [#4966](https://github.com/mapbox/mapbox-gl-js/pull/4966) [#4967](https://github.com/mapbox/mapbox-gl-js/pull/4967) [#4973](https://github.com/mapbox/mapbox-gl-js/pull/4973) :muscle: [@jfirebaugh](https://github.com/jfirebaugh) [@vicapow](https://github.com/vicapow)
- Dùng style specification để tạo kiểu flow [#4958](https://github.com/mapbox/mapbox-gl-js/pull/4958)
- Liệt kê rõ ràng các file cần publish trong `package.json` [#4819](https://github.com/mapbox/mapbox-gl-js/pull/4819) [@tomscholz](https://github.com/tomscholz)
- Chuyển các render test ignore sang một file riêng [#4977](https://github.com/mapbox/mapbox-gl-js/pull/4977)
- Thêm code of conduct [#5015](https://github.com/mapbox/mapbox-gl-js/pull/5015) :sparkling_heart:

## 0.38.0 (9 tháng 6, 2017)

#### Tính năng mới :sparkles:

- Làm giảm scale kích thước nhãn theo khoảng cách, cải thiện khả năng đọc trên bản đồ bị pitch [#4547](https://github.com/mapbox/mapbox-gl-js/pull/4547)

#### Sửa lỗi :beetle:

- Bỏ qua render cho các patterned layer khi pattern bị thiếu [#4687](https://github.com/mapbox/mapbox-gl-js/pull/4687)
- Sửa lỗi bản đồ không render lại sau sự kiện `webglcontextlost` [#4725](https://github.com/mapbox/mapbox-gl-js/pull/4725) [@cdawi](https://github.com/cdawi)
- Giới hạn (clamp) zoom level trong `flyTo` trong khoảng min- và maxzoom được chỉ định của bản đồ để ngăn hành vi không xác định [#4726](https://github.com/mapbox/mapbox-gl-js/pull/4726) [@](https://github.com/) IvanSanchez
- Sửa việc render wordmark trên IE [#4741](https://github.com/mapbox/mapbox-gl-js/pull/4741)
- Sửa các lỗi render symbol theo từng pixel nhỏ gây ra bởi tính toán sprite sai [#4737](https://github.com/mapbox/mapbox-gl-js/pull/4737)
- Ngăn các ngoại lệ phát sinh bởi một số lệnh gọi `flyTo` [#4761](https://github.com/mapbox/mapbox-gl-js/pull/4761)
- Sửa liên kết "Improve this map" [#4685](https://github.com/mapbox/mapbox-gl-js/pull/4685)
- Điều chỉnh logic `queryRenderedSymbols` để tính đến pitch scaling tốt hơn [#4792](https://github.com/mapbox/mapbox-gl-js/pull/4792)
- Sửa lỗi symbol layer đôi khi không render, thường gặp nhất trên Safari [#4795](https://github.com/mapbox/mapbox-gl-js/pull/4795)
- Áp dụng `text-keep-upright` sau `text-offset` để giữ nhãn thẳng đứng khi cần [#4779](https://github.com/mapbox/mapbox-gl-js/pull/4779) **[Có thể phá vỡ tương thích :warning: nhưng được xem là bugfix]**
- Ngăn ngoại lệ phát sinh bởi các tile GeoJSON rỗng [#4803](https://github.com/mapbox/mapbox-gl-js/pull/4803)

#### Cải thiện khả năng tiếp cận (Accessibility) :sound:

- Thêm `aria-label` vào nút đóng popup [#4799](https://github.com/mapbox/mapbox-gl-js/pull/4799) [@andrewharvey](https://github.com/andrewharvey)

#### Cải tiến quy trình phát triển + kiểm thử :wrench:

- Sửa lỗi equality assertion trong test [#4731](https://github.com/mapbox/mapbox-gl-js/pull/4731) [@IvanSanchez](https://github.com/IvanSanchez)
- Cải thiện trang kết quả benchmark [#4746](https://github.com/mapbox/mapbox-gl-js/pull/4746)
- Yêu cầu node phiên bản >=6.4.0, cho phép dùng nhiều tính năng ES6 hơn [#4752](https://github.com/mapbox/mapbox-gl-js/pull/4752)
- Bổ sung tài liệu còn thiếu cho tùy chọn `pitchWithRotate` [#4800](https://github.com/mapbox/mapbox-gl-js/pull/4800) [@simast](https://github.com/simast)
- Chuyển các file Markdown đặc thù Github vào một thư mục con [#4806](https://github.com/mapbox/mapbox-gl-js/pull/4806) [@tomscholz](https://github.com/tomscholz)

## 0.37.0 (2 tháng 5, 2017)

#### :warning: Thay đổi phá vỡ tương thích

- Đã loại bỏ `LngLat#wrapToBestWorld`

#### Tính năng mới :rocket:

- Cải thiện việc định vị popup/marker [#4577](https://github.com/mapbox/mapbox-gl-js/pull/4577)
- Thêm sự kiện `Map#isStyleLoaded` và `Map#areTilesLoaded` [#4321](https://github.com/mapbox/mapbox-gl-js/pull/4321)
- Hỗ trợ sprite offline dùng giao thức `file:` [#4649](https://github.com/mapbox/mapbox-gl-js/pull/4649) [@oscarfonts](https://github.com/oscarfonts)

#### Sửa lỗi :bug:

- Sửa fullscreen control trên Firefox [#4666](https://github.com/mapbox/mapbox-gl-js/pull/4666)
- Sửa các lỗi hiển thị (artifact) khiến ranh giới tile bị lộ trong một số trường hợp [#4636](https://github.com/mapbox/mapbox-gl-js/pull/4636)
- Sửa phép tính mặc định cho các categorical zoom-and-property function [#4657](https://github.com/mapbox/mapbox-gl-js/pull/4657)
- Sửa việc scale ảnh trên màn hình retina [#4645](https://github.com/mapbox/mapbox-gl-js/pull/4645)
- Lỗi render khi một ảnh trong suốt được thêm qua `Map#addImage` [#4644](https://github.com/mapbox/mapbox-gl-js/pull/4644)
- Sửa vấn đề render các line có điểm trùng lặp [#4634](https://github.com/mapbox/mapbox-gl-js/pull/4634)
- Sửa lỗi khi chuyển từ style data-driven sang giá trị paint không đổi (constant) [#4611](https://github.com/mapbox/mapbox-gl-js/pull/4611)
- Thêm kiểm tra để đảm bảo bounds không hợp lệ trên tilejson không gây lỗi [#4641](https://github.com/mapbox/mapbox-gl-js/pull/4641)

#### Cải tiến quy trình phát triển :computer:

- Thêm interface và định nghĩa flowtype [@vicapow](https://github.com/vicapow)
- Thêm stylelinting để đảm bảo tiền tố `mapboxgl-` trên tất cả các class [#4584](https://github.com/mapbox/mapbox-gl-js/pull/4584) [@asantos3026](https://github.com/asantos3026)

## 0.36.0 (19 tháng 4, 2017)

#### Tính năng mới :sparkles:

- Thay logo LogoControl bằng logo Mapbox mới [#4598](https://github.com/mapbox/mapbox-gl-js/pull/4598)

#### Sửa lỗi :bug:

- Sửa lỗi trong BoxZoomHandler khiến nó bị chập chờn (glitchy) nếu được bật sau DragPanHandler [#4528](https://github.com/mapbox/mapbox-gl-js/pull/4528)
- Sửa hành vi không xác định trong shader `fill_outline` [#4600](https://github.com/mapbox/mapbox-gl-js/pull/4600)
- Sửa nội suy `Camera#easeTo` trên bản đồ bị pitch [#4540](https://github.com/mapbox/mapbox-gl-js/pull/4540)
- Chọn phương pháp nội suy của property function theo kiểu dữ liệu của `property` [#4614](https://github.com/mapbox/mapbox-gl-js/pull/4614)

#### Cải tiến quy trình phát triển :nerd_face:

- Sửa lỗi crash khi thiếu `style.json` trong integration test
- `gl-style-composite` giờ đây có thể thực thi (executable) giống các công cụ khác [@andrewharvey](https://github.com/andrewharvey) [#4595](https://github.com/mapbox/mapbox-gl-js/pull/4595)
- Tiện ích `gl-style-composite` giờ báo lỗi nếu xảy ra xung đột tên giữa các layer [@andrewharvey](https://github.com/andrewharvey) [#4595](https://github.com/mapbox/mapbox-gl-js/pull/4595)

## 0.35.1 (12 tháng 4, 2017)

#### Sửa lỗi :bug:

- Thêm đuôi `.json` vào các câu lệnh `require` của style-spec để tương thích với webpack [#4563](https://github.com/mapbox/mapbox-gl-js/pull/4563) [@orangemug](https://github.com/orangemug)
- Sửa kiểu tài liệu cho `Map#fitBounde` [#4569](https://github.com/mapbox/mapbox-gl-js/pull/4569) [@andrewharvey](https://github.com/andrewharvey)
- Sửa lỗi khiến {Image,Video,Canvas}Source ném ngoại lệ nếu vĩ độ nằm ngoài +/-85.05113 [#4574](https://github.com/mapbox/mapbox-gl-js/pull/4574)
- Sửa lỗi tile raster bị overzoom biến mất khỏi bản đồ [#4567](https://github.com/mapbox/mapbox-gl-js/pull/4567)
- Sửa lỗi queryRenderedFeatures crash trên các feature polygon có trường `id` [#4581](https://github.com/mapbox/mapbox-gl-js/pull/4581)

## 0.35.0 (7 tháng 4, 2017)

#### Tính năng mới :rocket:

- Dùng anisotropic filtering để cải thiện việc render tile raster trên bản đồ bị pitch [#1064](https://github.com/mapbox/mapbox-gl-js/issues/1064)
- Thêm sự kiện `pitchstart` và `pitchend` [#2449](https://github.com/mapbox/mapbox-gl-js/issues/2449)
- Thêm tham số `layers` tùy chọn vào `Map#on` [#1002](https://github.com/mapbox/mapbox-gl-js/issues/1002)
- Thêm hỗ trợ data-driven styling cho `text-offset` [#4495](https://github.com/mapbox/mapbox-gl-js/pull/4495)
- Thêm hỗ trợ data-driven styling cho `text-rotate` [#3516](https://github.com/mapbox/mapbox-gl-js/issues/3516)
- Thêm hỗ trợ data-driven styling cho `icon-image` [#4304](https://github.com/mapbox/mapbox-gl-js/issues/4304)
- Thêm hỗ trợ data-driven styling cho `{text,icon}-size` [#4455](https://github.com/mapbox/mapbox-gl-js/pull/4455)

#### Sửa lỗi :bug:

- Ẩn thông báo lỗi trong console JS do tile bị thiếu [#1800](https://github.com/mapbox/mapbox-gl-js/issues/1800)
- Sửa lỗi `GeoJSONSource#setData()` có thể gây ra các cập nhật DOM không cần thiết [#4447](https://github.com/mapbox/mapbox-gl-js/issues/4447)
- Sửa lỗi `Map#flyTo` không tôn trọng cài đặt `renderWorldCopies` [#4449](https://github.com/mapbox/mapbox-gl-js/issues/4449)
- Sửa hồi quy (regression) trong hỗ trợ browserify # 4453
- Sửa lỗi hành vi sự kiện touch kém trên thiết bị di động [#4259](https://github.com/mapbox/mapbox-gl-js/issues/4259)
- Sửa lỗi stop trùng lặp trong property function có thể gây vòng lặp vô hạn [#4498](https://github.com/mapbox/mapbox-gl-js/issues/4498)
- Tôn trọng chiều cao/rộng ảnh trong api `addImage` [#4531](https://github.com/mapbox/mapbox-gl-js/pull/4531)
- Sửa lỗi ngăn hành vi đúng của `shift+zoom` [#3334](https://github.com/mapbox/mapbox-gl-js/issues/3334)
- Sửa lỗi ngăn image source render khi vùng tọa độ quá lớn [#4550](https://github.com/mapbox/mapbox-gl-js/issues/4550)
- Hiển thị image source trên các world bị wrap theo chiều ngang [#4555](https://github.com/mapbox/mapbox-gl-js/pull/4555)
- Sửa lỗi xử lý tùy chọn `refreshedExpiredTiles` [#4549](https://github.com/mapbox/mapbox-gl-js/pull/4549)
- Hỗ trợ thuộc tính `bounds` của TileJSON [#1775](https://github.com/mapbox/mapbox-gl-js/issues/1775)

#### Cải tiến quy trình phát triển :computer:

- Nâng cấp flow lên 0.42.0 ([#4500](https://github.com/mapbox/mapbox-gl-js/pull/4500))

## 0.34.0 (17 tháng 3, 2017)

#### Tính năng mới :rocket:

- Thêm API `Map#addImage` và `Map#removeImage` để cho phép thêm icon image lúc runtime [#4404](https://github.com/mapbox/mapbox-gl-js/pull/4404)
- Đơn giản hóa việc dùng bundler không phải browserify bằng cách biến bản build distribution thành entrypoint chính [#4423](https://github.com/mapbox/mapbox-gl-js/pull/4423)

#### Sửa lỗi :bug:

- Sửa lỗi các điểm đầu/cuối trùng nhau của LineString bị render sai thành đã nối (joined) [#4413](https://github.com/mapbox/mapbox-gl-js/pull/4413)
- Sửa lỗi `queryRenderedFeatures` thất bại trong trường hợp có cả nhiều source và thuộc tính paint data-driven cùng tồn tại [#4417](https://github.com/mapbox/mapbox-gl-js/issues/4417)
- Sửa lỗi request tile bị lỗi khiến `map.loaded()` trả về sai `false` [#4425](https://github.com/mapbox/mapbox-gl-js/issues/4425)

#### Cải tiến kiểm thử :white_check_mark:

- Cải thiện độ bao phủ (coverage) test trên nhiều module lõi [#4432](https://github.com/mapbox/mapbox-gl-js/pull/4432) [#4431](https://github.com/mapbox/mapbox-gl-js/pull/4431) [#4422](https://github.com/mapbox/mapbox-gl-js/pull/4422) [#4244](https://github.com/mapbox/mapbox-gl-js/pull/4244) :bowing_man:
## 0.33.1 (March 10, 2017)

#### Bug fixes :bug:

- Ngăn logo Mapbox bị thêm vào bản đồ nhiều hơn một lần [#4386](https://github.com/mapbox/mapbox-gl-js/pull/4386)
- Thêm `type='button'` vào `FullscreenControl` để ngăn nút hoạt động như nút submit của form [#4397](https://github.com/mapbox/mapbox-gl-js/pull/4397)
- Sửa lỗi bản đồ tiếp tục xoay nếu phím `Ctrl` được nhả ra trước khi click trong quá trình sự kiện `DragRotate` [#4389](https://github.com/mapbox/mapbox-gl-js/pull/4389)
- Xóa mô tả `options.easing` bị trùng lặp trong tài liệu `Map#fitBounds` [#4402](https://github.com/mapbox/mapbox-gl-js/pull/4402)

## 0.33.0 (March 8, 2017)

#### :warning: Thay đổi phá vỡ tương thích

- Tự động thêm wordmark Mapbox khi được yêu cầu bởi Điều khoản dịch vụ (TOS) của Mapbox [#3933](https://github.com/mapbox/mapbox-gl-js/pull/3933)
- Tăng `maxZoom` mặc định từ 20 lên 22 [#4333](https://github.com/mapbox/mapbox-gl-js/pull/4333)
- Loại bỏ dần (deprecate) các sự kiện `tiledata` và `tiledataloading` để chuyển sang dùng `sourcedata` và `sourcedataloading`. [#4347](https://github.com/mapbox/mapbox-gl-js/pull/4347)
- `mapboxgl.util` không còn được export nữa [#1408](https://github.com/mapbox/mapbox-gl-js/issues/1408)
- `"type": "categorical"` giờ đây là bắt buộc đối với tất cả các hàm phân loại (categorical). Trước đây, một số dạng hàm "ngầm định" là categorical hoạt động được, còn một số khác thì không. [#3717](https://github.com/mapbox/mapbox-gl-js/issues/3717)

#### :white_check_mark: Tính năng mới

- Thêm hỗ trợ property function cho hầu hết các thuộc tính paint của symbol [#4074](https://github.com/mapbox/mapbox-gl-js/pull/4074), [#4186](https://github.com/mapbox/mapbox-gl-js/pull/4186), [#4226](https://github.com/mapbox/mapbox-gl-js/pull/4226)
- Thêm khả năng chỉ định giá trị thuộc tính mặc định cho các giá trị thuộc tính không xác định hoặc không hợp lệ được dùng trong property function. [#4175](https://github.com/mapbox/mapbox-gl-js/pull/4175)
- Cải tiến `Map#fitBounds` để chấp nhận các giá trị `padding` khác nhau cho top, bottom, left và right [#3890](https://github.com/mapbox/mapbox-gl-js/pull/3890)
- Thêm `FullscreenControl` để hiển thị bản đồ toàn màn hình [#3977](https://github.com/mapbox/mapbox-gl-js/pull/3977)

#### :beetle: Sửa lỗi

- Sửa lỗi validation trên hàm categorical kết hợp zoom-và-property [#4220](https://github.com/mapbox/mapbox-gl-js/pull/4220)
- Sửa lỗi khiến các tài nguyên đã hết hạn bị yêu cầu lại gây ra vòng lặp vô hạn [#4255](https://github.com/mapbox/mapbox-gl-js/pull/4255)
- Sửa lỗi khiến `MapDataEvent#isSourceLoaded` luôn trả về false [#4254](https://github.com/mapbox/mapbox-gl-js/pull/4254)
- Khắc phục vấn đề tile trong source cache bị xóa quá sớm, dẫn đến tile bị nhấp nháy khi phóng to/thu nhỏ [#4311](https://github.com/mapbox/mapbox-gl-js/pull/4311)
- Đảm bảo `MapEventData` được truyền qua khi gọi `Map#flyTo` [#4342](https://github.com/mapbox/mapbox-gl-js/pull/4342)
- Sửa giá trị trả về không chính xác của `Map#isMoving` [#4350](https://github.com/mapbox/mapbox-gl-js/pull/4350)
- Sửa lỗi hàm categorical không cho phép giá trị stop domain kiểu boolean [#4195](https://github.com/mapbox/mapbox-gl-js/pull/4195)
- Sửa lỗi hàm piecewise-constant để cho phép các mức zoom không phải số nguyên. [#4196](https://github.com/mapbox/mapbox-gl-js/pull/4196)
- Sửa các vấn đề với `$id` trong filter [#4236](https://github.com/mapbox/mapbox-gl-js/pull/4236) [#4237](https://github.com/mapbox/mapbox-gl-js/pull/4237)
- Sửa lỗi race condition trong thuật toán tính centroid của polygon gây ra tile không tải được trong một số trường hợp. [#4273](https://github.com/mapbox/mapbox-gl-js/pull/4273)
- Ném ra lỗi có ý nghĩa khi truyền tham số `layers` không phải mảng cho `queryRenderedFeatures` [#4331](https://github.com/mapbox/mapbox-gl-js/pull/4331)
- Ném ra lỗi có ý nghĩa khi cung cấp giá trị `minZoom` và `maxZoom` không hợp lệ [#4324](https://github.com/mapbox/mapbox-gl-js/pull/4324)
- Sửa rò rỉ bộ nhớ khi sử dụng plugin RTL Text [#4248](https://github.com/mapbox/mapbox-gl-js/pull/4248)

#### Thay đổi trong quy trình phát triển

- Đã hợp nhất repo [đặc tả style Mapbox GL](https://github.com/mapbox/mapbox-gl-style-spec) vào repo này (nay nằm dưới `src/style-spec` và `test/unit/style-spec`).

## 0.32.1 (Jan 26, 2017)

#### Sửa lỗi

- Sửa lỗi khiến [plugin `mapbox-gl-rtl-text`](https://github.com/mapbox/mapbox-gl-rtl-text) không hoạt động [#4055](https://github.com/mapbox/mapbox-gl-js/pull/4055)

## 0.32.0 (Jan 26, 2017)

#### Thông báo loại bỏ dần (Deprecation)

- [Style classes](https://www.mapbox.com/mapbox-gl-style-spec/#layer-paint.*) đã bị loại bỏ dần và sẽ được gỡ bỏ trong một phiên bản sắp tới của Mapbox GL JS.

#### Tính năng mới

- Thêm phương thức `Map#isSourceLoaded` [#4033](https://github.com/mapbox/mapbox-gl-js/pull/4033)
- Tự động tải lại tile dựa trên header HTTP `Expires` và `Cache-Control` của chúng [#3944](https://github.com/mapbox/mapbox-gl-js/pull/3944)
- Thêm tùy chọn `around=center` cho các trình xử lý tương tác `scrollZoom` và `touchZoomRotate` [#3876](https://github.com/mapbox/mapbox-gl-js/pull/3876)
- Thêm hỗ trợ [plugin `mapbox-gl-rtl-text`](https://github.com/mapbox/mapbox-gl-rtl-text) để hỗ trợ các văn bản viết từ phải sang trái [#3758](https://github.com/mapbox/mapbox-gl-js/pull/3758)
- Thêm loại source `canvas` [#3765](https://github.com/mapbox/mapbox-gl-js/pull/3765)
- Thêm phương thức `Map#isMoving` [#2792](https://github.com/mapbox/mapbox-gl-js/issues/2792)

#### Sửa lỗi

- Sửa lỗi khiến văn bản bị méo (garbled) khi zoom [#3962](https://github.com/mapbox/mapbox-gl-js/pull/3962)
- Sửa lỗi khiến trình duyệt bị crash trên Firefox và Mobile Safari khi hiển thị bản đồ lớn [#4037](https://github.com/mapbox/mapbox-gl-js/pull/4037)
- Sửa lỗi khiến tile raster bị nhấp nháy khi zoom [#2467](https://github.com/mapbox/mapbox-gl-js/issues/2467)
- Sửa lỗi ngoại lệ khi unset rồi set lại fill-outline-color [#3657](https://github.com/mapbox/mapbox-gl-js/issues/3657)
- Sửa rò rỉ bộ nhớ khi gỡ bỏ các raster source [#3951](https://github.com/mapbox/mapbox-gl-js/issues/3951)
- Sửa lỗi ngoại lệ khi zoom vào/ra trên tile GeoJSON rỗng [#3985](https://github.com/mapbox/mapbox-gl-js/pull/3985)
- Sửa lỗi hình ảnh (artifact) tại các điểm nối line ở góc rất nhọn [#4008](https://github.com/mapbox/mapbox-gl-js/pull/4008)

## 0.31.0 (Jan 10 2017)

#### Tính năng mới

- Thêm tùy chọn `renderWorldCopies` vào constructor của `Map` để người dùng kiểm soát việc có hiển thị nhiều bản sao thế giới trên bản đồ hay không [#3885](https://github.com/mapbox/mapbox-gl-js/pull/3885)

#### Sửa lỗi

- Sửa vấn đề hiệu năng khi `pitch` hoặc `bearing` của `Map` bị thay đổi [#3938](https://github.com/mapbox/mapbox-gl-js/pull/3938)
- Sửa lỗi con trỏ null (null pointer exception) do cố gắng clear một source `undefined` [#3903](https://github.com/mapbox/mapbox-gl-js/pull/3903)

#### Khác

- Tích hợp các integration test trước đây nằm ở [`mapbox-gl-test-suite`](https://github.com/mapbox/mapbox-gl-test-suite) vào repo này [#3834](https://github.com/mapbox/mapbox-gl-js/pull/3834)

## 0.30.0 (Jan 5 2017)

#### Tính năng mới

- Phát sinh lỗi khi canvas của bản đồ lớn hơn giới hạn cho phép bởi `gl.MAX_RENDERBUFFER_SIZE` [#2893](https://github.com/mapbox/mapbox-gl-js/issues/2893)
- Cải thiện thông báo lỗi khi tham chiếu đến một id layer không tồn tại [#2597](https://github.com/mapbox/mapbox-gl-js/issues/2597)
- Phát sinh lỗi khi layer sử dụng source `geojson` mà lại chỉ định `source-layer` [#3896](https://github.com/mapbox/mapbox-gl-js/pull/3896)
- Thêm cú pháp khai báo source nội tuyến (inline) [#3857](https://github.com/mapbox/mapbox-gl-js/issues/3857)
- Cải thiện cách xử lý ngắt dòng (line breaking) [#3887](https://github.com/mapbox/mapbox-gl-js/issues/3887)

#### Cải thiện hiệu năng

- Cải thiện hiệu năng `Map#setStyle` trong một số trường hợp [#3853](https://github.com/mapbox/mapbox-gl-js/pull/3853)

#### Sửa lỗi

- Sửa vị trí popup không như mong đợi khi một số offset không được chỉ định [#3367](https://github.com/mapbox/mapbox-gl-js/issues/3367)
- Sửa lỗi nội suy (interpolation) không chính xác trong các hàm [#3838](https://github.com/mapbox/mapbox-gl-js/issues/3838)
- Sửa độ mờ (opacity) không chính xác khi nhiều background được render [#3819](https://github.com/mapbox/mapbox-gl-js/issues/3819)
- Sửa lỗi ngoại lệ khi khởi tạo geolocation control trên Safari [#3844](https://github.com/mapbox/mapbox-gl-js/issues/3844)
- Sửa lỗi ngoại lệ khi set `showTileBoundaries` mà không có source nào [#3849](https://github.com/mapbox/mapbox-gl-js/issues/3849)
- Sửa lỗi render không đúng phần trong suốt của các raster layer trong một số trường hợp [#3723](https://github.com/mapbox/mapbox-gl-js/issues/3723)
- Sửa vòng lặp render không kết thúc khi zoom in trong một số trường hợp [#3399](https://github.com/mapbox/mapbox-gl-js/pull/3399)

## 0.29.0 (December 20 2016)

#### Tính năng mới

- Thêm hỗ trợ property function cho nhiều thuộc tính style trên line layer [#3033](https://github.com/mapbox/mapbox-gl-js/pull/3033)
- Làm cho `Map#setStyle` chuyển tiếp mượt mà sang style mới [#3621](https://github.com/mapbox/mapbox-gl-js/pull/3621)
- Thêm các sự kiện `styledata`, `sourcedata`, `styledataloading` và `sourcedataloading`
- Thêm thuộc tính `isSourceLoaded` và `source` vào `MapDataEvent` [#3590](https://github.com/mapbox/mapbox-gl-js/pull/3590)
- Gỡ bỏ giới hạn "max zoom" là 20 [#3683](https://github.com/mapbox/mapbox-gl-js/pull/3683)
- Thêm các thuộc tính style `circle-stroke-*` [#3672](https://github.com/mapbox/mapbox-gl-js/pull/3672)
- Thêm thông báo lỗi hữu ích hơn khi phần tử `container` được chỉ định không tồn tại [#3719](https://github.com/mapbox/mapbox-gl-js/pull/3719)
- Thêm tùy chọn `watchPosition` vào `GeolocateControl` [#3739](https://github.com/mapbox/mapbox-gl-js/pull/3739)
- Thêm tùy chọn `positionOptions` vào `GeolocateControl` [#3739](https://github.com/mapbox/mapbox-gl-js/pull/3739)
- Thêm `aria-label` vào canvas bản đồ [#3782](https://github.com/mapbox/mapbox-gl-js/pull/3782)
- Điều chỉnh hành vi render symbol đa điểm (multipoint) [#3763](https://github.com/mapbox/mapbox-gl-js/pull/3763)
- Thêm hỗ trợ property function cho `icon-offset` [#3791](https://github.com/mapbox/mapbox-gl-js/pull/3791)
- Cải thiện khử răng cưa (antialiasing) trên các line bị nghiêng (pitched) [#3790](https://github.com/mapbox/mapbox-gl-js/pull/3790)
- Cho phép attribution control thu gọn thành nút ⓘ trên màn hình nhỏ hơn [#3783](https://github.com/mapbox/mapbox-gl-js/pull/3783)
- Cải thiện thuật toán ngắt dòng [#3743](https://github.com/mapbox/mapbox-gl-js/pull/3743)

#### Cải thiện hiệu năng

- Sửa rò rỉ bộ nhớ khi gọi `Map#removeSource` [#3602](https://github.com/mapbox/mapbox-gl-js/pull/3602)
- Giảm kích thước bundle bằng cách thêm bản build tùy chỉnh của `gl-matrix` [#3734](https://github.com/mapbox/mapbox-gl-js/pull/3734)
- Cải thiện hiệu năng của code xử lý phép chiếu (projection) [#3721](https://github.com/mapbox/mapbox-gl-js/pull/3721)
- Cải thiện hiệu năng đánh giá (evaluation) hàm style [#3816](https://github.com/mapbox/mapbox-gl-js/pull/3816)

#### Sửa lỗi

- Sửa lỗi ngoại lệ khi sử dụng property function `line-color` [#3639](https://github.com/mapbox/mapbox-gl-js/issues/3639)
- Sửa lỗi ngoại lệ khi xóa một layer rồi thêm một layer khác có cùng id nhưng khác type [#3655](https://github.com/mapbox/mapbox-gl-js/pull/3655)
- Sửa lỗi ngoại lệ khi truyền một điểm duy nhất vào `Map#fitBounds` [#3655](https://github.com/mapbox/mapbox-gl-js/pull/3655)
- Sửa lỗi ngoại lệ thỉnh thoảng xảy ra trong quá trình thay đổi bản đồ nhanh (rapid map mutations) [#3681](https://github.com/mapbox/mapbox-gl-js/pull/3681)
- Sửa lỗi render khi pitch=0 trên một số hệ thống [#3740](https://github.com/mapbox/mapbox-gl-js/pull/3740)
- Sửa việc sử dụng CPU không cần thiết khi hiển thị raster layer [#3764](https://github.com/mapbox/mapbox-gl-js/pull/3764)
- Sửa lỗi sprite sau khi gọi `Map#setStyle` [#3829](https://github.com/mapbox/mapbox-gl-js/pull/3829)
- Sửa lỗi ngăn `Map` phát sự kiện `contextmenu` trên các trình duyệt Windows [#3822](https://github.com/mapbox/mapbox-gl-js/pull/3822)

## 0.28.0 (November 17 2016)

#### Tính năng mới và cải tiến

- Cải thiện hiệu năng cho `Map#addLayer` và `Map#removeLayer` [#3584](https://github.com/mapbox/mapbox-gl-js/pull/3584)
- Thêm phương thức thay đổi thứ tự layer khi runtime - `Map#moveLayer` [#3584](https://github.com/mapbox/mapbox-gl-js/pull/3584)
- Cập nhật logic dấu câu dọc (vertical punctuation) theo chuẩn Unicode 9.0 [#3608](https://github.com/mapbox/mapbox-gl-js/pull/3608)

#### Sửa lỗi

- Sửa render `fill-opacity` kiểu data-driven khi sử dụng `fill-pattern` [#3598](https://github.com/mapbox/mapbox-gl-js/pull/3598)
- Sửa lỗi hình ảnh khi render line [#3627](https://github.com/mapbox/mapbox-gl-js/pull/3627)
- Sửa render không đúng khi fill không trong suốt nằm trên fill trong suốt [#2628](https://github.com/mapbox/mapbox-gl-js/pull/2628)
- Ngăn `AssertionErrors` khi pitch raster layer bằng cách chỉ gọi `Worker#redoPlacement` trên các source vector và GeoJSON [#3624](https://github.com/mapbox/mapbox-gl-js/pull/3624)
- Khôi phục khả năng tương thích với IE11 [#3635](https://github.com/mapbox/mapbox-gl-js/pull/3635)
- Sửa vị trí đặt symbol cho các tile đã cache [#3637](https://github.com/mapbox/mapbox-gl-js/pull/3637)

## 0.27.0 (November 11 2016)

#### ⚠️ Thay đổi phá vỡ tương thích ⚠️

- Thay thế các thuộc tính `fill-extrude-height` và `fill-extrude-base` của render type `fill` bằng một type riêng `fill-extrusion` (với các thuộc tính tương ứng `fill-extrusion-height` và `fill-extrusion-base`), giải quyết các vấn đề về độ chính xác render và việc chuyển đổi khi runtime giữa fill phẳng và fill nổi khối (extruded). https://github.com/mapbox/mapbox-gl-style-spec/issues/554
- Đổi đơn vị của các thuộc tính chiều cao extrusion (`fill-extrusion-height`, `fill-extrusion-base`) từ "số ma thuật" (magic numbers) sang mét. [#3509](https://github.com/mapbox/mapbox-gl-js/pull/3509)
- Gỡ bỏ class `mapboxgl.Control` và thay đổi cách các control tùy chỉnh cần được triển khai. [#3497](https://github.com/mapbox/mapbox-gl-js/pull/3497)
- Gỡ bỏ các hàm `mapboxgl.util`: `inherit`, `extendAll`, `debounce`, `coalesce`, `startsWith`, `supportsGeolocation`. [#3441](https://github.com/mapbox/mapbox-gl-js/pull/3441) [#3571](https://github.com/mapbox/mapbox-gl-js/pull/3571)
- **`mapboxgl.util` đã bị loại bỏ dần** và sẽ được gỡ bỏ trong phiên bản kế tiếp. [#1408](https://github.com/mapbox/mapbox-gl-js/issues/1408)

#### Tính năng mới và cải tiến

- Rất nhiều **cải thiện hiệu năng** kết hợp lại giúp việc render **nhanh hơn tới 3 lần**, đặc biệt với các style phức tạp. [#3485](https://github.com/mapbox/mapbox-gl-js/pull/3485) [#3489](https://github.com/mapbox/mapbox-gl-js/pull/3489) [#3490](https://github.com/mapbox/mapbox-gl-js/pull/3490) [#3491](https://github.com/mapbox/mapbox-gl-js/pull/3491) [#3498](https://github.com/mapbox/mapbox-gl-js/pull/3498) [#3499](https://github.com/mapbox/mapbox-gl-js/pull/3499) [#3501](https://github.com/mapbox/mapbox-gl-js/pull/3501) [#3510](https://github.com/mapbox/mapbox-gl-js/pull/3510) [#3514](https://github.com/mapbox/mapbox-gl-js/pull/3514) [#3515](https://github.com/mapbox/mapbox-gl-js/pull/3515) [#3486](https://github.com/mapbox/mapbox-gl-js/pull/3486) [#3527](https://github.com/mapbox/mapbox-gl-js/pull/3527) [#3574](https://github.com/mapbox/mapbox-gl-js/pull/3574) ⚡️⚡️⚡️
- 🈯 Đã thêm **chế độ viết văn bản dọc (vertical text writing mode)** cho các ngôn ngữ hỗ trợ. [#3438](https://github.com/mapbox/mapbox-gl-js/pull/3438)
- 🈯 Cải thiện **cách ngắt dòng của văn bản tiếng Trung và tiếng Nhật** trong các nhãn đặt theo điểm (point-placed labels). [#3420](https://github.com/mapbox/mapbox-gl-js/pull/3420)
- Giảm số lượng worker thread mặc định (`mapboxgl.workerCount`) để cải thiện hiệu năng. [#3565](https://github.com/mapbox/mapbox-gl-js/pull/3565)
- Tự động sử dụng loại hàm style `categorical` khi giá trị đầu vào là chuỗi. [#3384](https://github.com/mapbox/mapbox-gl-js/pull/3384)
- Cải thiện khả năng truy cập (accessibility) của các nút control. [#3492](https://github.com/mapbox/mapbox-gl-js/pull/3492)
- Gỡ bỏ nút geolocation nếu geolocation bị tắt (ví dụ: trang không được phục vụ qua `https`). [#3571](https://github.com/mapbox/mapbox-gl-js/pull/3571)
- Thêm các phương thức `Map#getMaxZoom` và `Map#getMinZoom` [#3592](https://github.com/mapbox/mapbox-gl-js/pull/3592)

#### Sửa lỗi

- Sửa nhiều lỗi render line dash (nét đứt) [#3451](https://github.com/mapbox/mapbox-gl-js/pull/3451)
- Sửa hiện tượng nhấp nháy bản đồ không liên tục khi sử dụng image source. [#3522](https://github.com/mapbox/mapbox-gl-js/pull/3522)
- Sửa render không chính xác của các `background` layer bán trong suốt. [#3521](https://github.com/mapbox/mapbox-gl-js/pull/3521)
- Sửa thuộc tính `raster-fade-duration` bị hỏng. [#3532](https://github.com/mapbox/mapbox-gl-js/pull/3532)
- Sửa cách xử lý chiều cao extrusion có giá trị âm (bằng cách clamp về `0`). [#3463](https://github.com/mapbox/mapbox-gl-js/pull/3463)
- Sửa lỗi GeoJSON source không đặt nhãn/icon đúng sau khi xoay bản đồ. [#3366](https://github.com/mapbox/mapbox-gl-js/pull/3366)
- Sửa việc đặt icon/nhãn không tuân theo thứ tự đối với các layer có tên dạng số. [#3404](https://github.com/mapbox/mapbox-gl-js/pull/3404)
- Sửa `queryRenderedFeatures` hoạt động không đúng trên các nhãn bị va chạm (colliding labels). [#3459](https://github.com/mapbox/mapbox-gl-js/pull/3459)
- Sửa lỗi thay đổi thuộc tính extrusion khi runtime đôi khi ném ra lỗi. [#3487](https://github.com/mapbox/mapbox-gl-js/pull/3487) [#3468](https://github.com/mapbox/mapbox-gl-js/pull/3468)
- Sửa lỗi `map.loaded()` luôn trả về `true` khi sử dụng raster tile source. [#3302](https://github.com/mapbox/mapbox-gl-js/pull/3302)
- Sửa lỗi khi di chuyển bản đồ ra ngoài giới hạn đôi khi ném ra lỗi `failed to invert matrix`. [#3518](https://github.com/mapbox/mapbox-gl-js/pull/3518)
- Sửa `queryRenderedFeatures` ném ra lỗi nếu không có tham số nào được cung cấp. [#3542](https://github.com/mapbox/mapbox-gl-js/pull/3542)
- Sửa lỗi khi sử dụng nhiều `\n` trong một text field gây ra lỗi. [#3570](https://github.com/mapbox/mapbox-gl-js/pull/3570)

#### Khác

- 🐞 Sửa lỗi `npm install mapbox-gl` kéo theo toàn bộ `devDependencies`, khiến việc cài đặt cực kỳ chậm. [#3377](https://github.com/mapbox/mapbox-gl-js/pull/3377)
- Chuyển codebase sang ES6. [#c](https://github.com/mapbox/mapbox-gl-js/pull/3388) [#3408](https://github.com/mapbox/mapbox-gl-js/pull/3408) [#3415](https://github.com/mapbox/mapbox-gl-js/pull/3415) [#3421](https://github.com/mapbox/mapbox-gl-js/pull/3421)
- Rất nhiều tái cấu trúc (refactor) nội bộ để codebase đơn giản hơn và dễ bảo trì hơn.
- Nhiều sửa đổi tài liệu khác nhau. [#3440](https://github.com/mapbox/mapbox-gl-js/pull/3440)

## 0.26.0 (October 13 2016)

#### Tính năng mới & Cải tiến

- Thêm các thuộc tính style `fill-extrude-height` và `fill-extrude-base` (tòa nhà 3D) :cityscape: [#3223](https://github.com/mapbox/mapbox-gl-js/pull/3223)
- Thêm nội suy `colorSpace` có thể tùy chỉnh cho các hàm [#3245](https://github.com/mapbox/mapbox-gl-js/pull/3245)
- Thêm loại hàm `identity` [#3274](https://github.com/mapbox/mapbox-gl-js/pull/3274)
- Thêm kiểm tra độ sâu (depth testing) cho symbol có `'pitch-alignment': 'map'` [#3243](https://github.com/mapbox/mapbox-gl-js/pull/3243)
- Thêm các sự kiện `dataloading` cho style và source [#3306](https://github.com/mapbox/mapbox-gl-js/pull/3306)
- Thêm hậu tố `Control` vào tất cả các control :warning: THAY ĐỔI PHÁ VỠ TƯƠNG THÍCH :warning: [#3355](https://github.com/mapbox/mapbox-gl-js/pull/3355)
- Tự động tính toán `ref` của style layer và loại bỏ `ref` do người dùng chỉ định :warning: THAY ĐỔI PHÁ VỠ TƯƠNG THÍCH :warning: [#3486](https://github.com/mapbox/mapbox-gl-js/pull/3486)

#### Cải thiện hiệu năng

- Đảm bảo việc xóa style hoặc source sẽ giải phóng toàn bộ tài nguyên tile [#3359](https://github.com/mapbox/mapbox-gl-js/pull/3359)

#### Sửa lỗi

- Sửa lỗi gây ra lỗi khi gọi `Marker#setLngLat` [#3294](https://github.com/mapbox/mapbox-gl-js/pull/3294)
- Sửa lỗi khiến tọa độ trong `touchend` không chính xác trên Android Chrome [#3319](https://github.com/mapbox/mapbox-gl-js/pull/3319)
- Sửa lỗi khiến vị trí popup không chính xác ở phần trên màn hình [#3333](https://github.com/mapbox/mapbox-gl-js/pull/3333)
- Khôi phục thuộc tính `tile` trong các sự kiện `data` được phát ra khi một tile bị gỡ bỏ [#3328](https://github.com/mapbox/mapbox-gl-js/pull/3328)
- Sửa lỗi khiến liên kết "Improve this map" không preload vị trí bản đồ [#3356](https://github.com/mapbox/mapbox-gl-js/pull/3356)

## 0.25.1 (September 30 2016)

#### Sửa lỗi

- Sửa lỗi khiến attribution không được hiển thị [#3278](https://github.com/mapbox/mapbox-gl-js/pull/3278)
- Sửa lỗi gây ra ngoại lệ khi văn bản symbol có ký tự xuống dòng ở cuối [#3281](https://github.com/mapbox/mapbox-gl-js/pull/3281)

## 0.25.0 (September 29 2016)

#### Thay đổi phá vỡ tương thích

- `Evented#off` giờ đây yêu cầu hai tham số; việc bỏ tham số thứ hai để hủy đăng ký tất cả listener cho một loại
  sự kiện không còn được hỗ trợ nữa, vì nó có thể gây ra việc hủy đăng ký ngoài ý muốn các listener nội bộ.

#### Tính năng mới & Cải tiến

- Hợp nhất các sự kiện vòng đời dữ liệu (data lifecycle) chưa được ghi tài liệu vào các sự kiện `data` và `dataloading` ([#3255](https://github.com/mapbox/mapbox-gl-js/pull/3255))
- Thêm giá trị `auto` cho các thuộc tính trong đặc tả style ([#3203](https://github.com/mapbox/mapbox-gl-js/pull/3203))

#### Sửa lỗi

- Sửa lỗi khiến `Map#queryRenderedFeatures` không trả về feature nào sau khi xoay bản đồ hoặc thay đổi filter ([#3233](https://github.com/mapbox/mapbox-gl-js/pull/3233))
- Thay đổi quy trình build webpack ([#3235](https://github.com/mapbox/mapbox-gl-js/pull/3235)) :warning: THAY ĐỔI PHÁ VỠ TƯƠNG THÍCH :warning:
- Cải thiện thông báo lỗi cho `LngLat#convert` ([#3232](https://github.com/mapbox/mapbox-gl-js/pull/3232))
- Sửa lỗi trường `tiles` bị bỏ sót khỏi phương thức `RasterTileSource#serialize` ([#3259](https://github.com/mapbox/mapbox-gl-js/pull/3259))
- Tuân thủ đặc tả HTML bằng cách thay thế `div` bên trong `<button>` của control `Navigation` bằng phần tử `span` ([#3268](https://github.com/mapbox/mapbox-gl-js/pull/3268))
- Sửa lỗi khiến các instance `Marker` bị dịch chuyển đến tọa độ pixel không nguyên (non-whole pixel), gây ra hiện tượng nhòe ([#3270](https://github.com/mapbox/mapbox-gl-js/pull/3270))

#### Cải thiện hiệu năng

- Tránh việc validation style không cần thiết ([#3224](https://github.com/mapbox/mapbox-gl-js/pull/3224))
- Chia sẻ chung một blob URL giữa tất cả các worker ([#3239](https://github.com/mapbox/mapbox-gl-js/pull/3239))

## 0.24.0 (September 19 2016)

#### Tính năng mới & Cải tiến

- Cho phép querystring trong URL `mapbox://` [#3113](https://github.com/mapbox/mapbox-gl-js/issues/3113)
- Cho phép tương tác "drag rotate" điều khiển pitch [#3105](https://github.com/mapbox/mapbox-gl-js/pull/3105)
- Cải thiện hiệu năng bằng cách giảm kích thước `Blob` script của `Worker` [#3158](https://github.com/mapbox/mapbox-gl-js/pull/3158)
- Cải thiện hiệu năng vector tile [#3067](https://github.com/mapbox/mapbox-gl-js/pull/3067)
- Giảm kích thước thư viện phân phối bằng cách loại bỏ `package.json` [#3174](https://github.com/mapbox/mapbox-gl-js/pull/3174)
- Thêm hỗ trợ ký tự xuống dòng mới trong `text-field` [#3179](https://github.com/mapbox/mapbox-gl-js/pull/3179)
- Làm cho điều hướng bằng bàn phím mượt hơn [#3190](https://github.com/mapbox/mapbox-gl-js/pull/3190)
- Làm cho zoom bằng con lăn chuột mượt hơn [#3189](https://github.com/mapbox/mapbox-gl-js/pull/3189)
- Thêm thông báo lỗi hữu ích hơn khi gọi `Map#queryRenderedFeatures` trên layer không tồn tại [#3196](https://github.com/mapbox/mapbox-gl-js/pull/3196)
- Thêm hỗ trợ đơn vị đo lường Anh (imperial units) cho control `Scale` [#3160](https://github.com/mapbox/mapbox-gl-js/pull/3160)
- Thêm pitch của bản đồ vào URL hash [#3218](https://github.com/mapbox/mapbox-gl-js/pull/3218)

#### Sửa lỗi

- Sửa lỗi ngoại lệ khi sử dụng trình xử lý box zoom [#3078](https://github.com/mapbox/mapbox-gl-js/pull/3078)
- Đảm bảo filter của style không thể bị thay đổi qua tham chiếu (mutated by reference) [#3093](https://github.com/mapbox/mapbox-gl-js/pull/3093)
- Sửa lỗi ngoại lệ khi mở popup gắn với marker bằng click [#3104](https://github.com/mapbox/mapbox-gl-js/pull/3104)
- Sửa lỗi khiến fill có màu trong suốt và pattern không được render [#3107](https://github.com/mapbox/mapbox-gl-js/issues/3107)
- Sửa thứ tự vĩ độ trong `Map#getBounds` [#3081](https://github.com/mapbox/mapbox-gl-js/issues/3081)
- Sửa việc đánh giá không chính xác các hàm kết hợp zoom-và-property [#2827](https://github.com/mapbox/mapbox-gl-js/issues/2827) [#3155](https://github.com/mapbox/mapbox-gl-js/pull/3155)
- Sửa việc đánh giá không chính xác các property function [#2828](https://github.com/mapbox/mapbox-gl-js/issues/2828) [#3155](https://github.com/mapbox/mapbox-gl-js/pull/3155)
- Sửa lỗi khiến văn bản bị méo khi nhiều bản đồ được render trên cùng trang [#3086](https://github.com/mapbox/mapbox-gl-js/issues/3086)
- Sửa lỗi render do `Map#setFilter` và xoay bản đồ trên iOS 10 [#3207](https://github.com/mapbox/mapbox-gl-js/pull/3207)
- Sửa lỗi khiến image và video source biến mất khi zoom in [#3010](https://github.com/mapbox/mapbox-gl-js/issues/3010)

## 0.23.0 (August 25 2016)

#### Tính năng mới & Cải tiến

- Thêm hỗ trợ property function cho `line-color` [#2938](https://github.com/mapbox/mapbox-gl-js/pull/2938)
- Thêm control `Scale` [#2940](https://github.com/mapbox/mapbox-gl-js/pull/2940) [#3042](https://github.com/mapbox/mapbox-gl-js/pull/3042)
- Cải thiện việc đặt nhãn cho polygon bằng cách render nhãn tại điểm cực khó tiếp cận (pole of inaccessibility) [#3038](https://github.com/mapbox/mapbox-gl-js/pull/3038)
- Thêm tùy chọn `offset` cho `Popup` [#1962](https://github.com/mapbox/mapbox-gl-js/issues/1962)
- Thêm phương thức `Marker#bindPopup` [#3056](https://github.com/mapbox/mapbox-gl-js/pull/3056)

#### Cải thiện hiệu năng

- Cải thiện hiệu năng cho trang có nhiều bản đồ bằng cách dùng chung một pool `WebWorker` [#2952](https://github.com/mapbox/mapbox-gl-js/pull/2952)

#### Sửa lỗi

- Làm cho `LatLngBounds` tuân theo đúng thứ tự tham số đã ghi trong tài liệu (`southwest`, `northeast`), cho phép giới hạn (bounds) vượt qua đường đổi ngày (dateline) [#2414](https://github.com/mapbox/mapbox-gl-js/pull/2414) :warning: **THAY ĐỔI PHÁ VỠ TƯƠNG THÍCH** :warning:
- Sửa lỗi khiến property function `fill-opacity` không render như mong đợi [#3061](https://github.com/mapbox/mapbox-gl-js/pull/3061)

## 0.22.1 (August 18 2016)

#### Tính năng mới & Cải tiến

- Giảm kích thước thư viện bằng cách dùng phiên bản rút gọn của đặc tả style [#2998](https://github.com/mapbox/mapbox-gl-js/pull/2998)
- Thêm cảnh báo khi xảy ra lỗi hình ảnh render do quá nhiều symbol hoặc glyph được render trong một tile [#2966](https://github.com/mapbox/mapbox-gl-js/pull/2966)

#### Sửa lỗi

- Sửa lỗi khiến `Map#querySourceFeatures` ném ra ngoại lệ [#3022](https://github.com/mapbox/mapbox-gl-js/pull/3022)
- Sửa lỗi khiến `Map#loaded` trả về true trong khi vẫn còn cập nhật tile đang chờ xử lý [#2847](https://github.com/mapbox/mapbox-gl-js/pull/2847)

## 0.22.0 (August 11 2016)

#### Thay đổi phá vỡ tương thích

- Các constructor `GeoJSONSource`, `VideoSource`, `ImageSource` giờ đây là private. Vui lòng dùng `map.addSource({...})` để tạo source và `map.getSource(...).setData(...)` để cập nhật GeoJSON source. [#2667](https://github.com/mapbox/mapbox-gl-js/pull/2667)
- `Map#onError` đã bị gỡ bỏ. Bạn có thể bắt lỗi bằng cách lắng nghe sự kiện `error`. Nếu không có listener nào được gắn vào `error`, thông báo lỗi sẽ được in ra console. [#2852](https://github.com/mapbox/mapbox-gl-js/pull/2852)

#### Tính năng mới & Cải tiến

- Tăng kích thước tối đa của glyph atlas để phù hợp với các bảng chữ cái có số lượng ký tự lớn [#2930](https://github.com/mapbox/mapbox-gl-js/pull/2930)
- Thêm hỗ trợ lọc feature theo `$id` của GeoJSON / vector tile [#2888](https://github.com/mapbox/mapbox-gl-js/pull/2888)
- Cập nhật icon geolocate [#2973](https://github.com/mapbox/mapbox-gl-js/pull/2973)
- Thêm sự kiện `close` cho `Popup` [#2953](https://github.com/mapbox/mapbox-gl-js/pull/2953)
- Thêm tùy chọn `offset` cho `Marker` [#2885](https://github.com/mapbox/mapbox-gl-js/pull/2885)
- In các sự kiện `error` không có listener nào ra console [#2852](https://github.com/mapbox/mapbox-gl-js/pull/2852)
- Tái cấu trúc interface `Source` để chuẩn bị cho các loại source tùy chỉnh [#2667](https://github.com/mapbox/mapbox-gl-js/pull/2667)

#### Sửa lỗi

- Sửa property function opacity cho fill layer [#2971](https://github.com/mapbox/mapbox-gl-js/pull/2971)
- Sửa lỗi `DataCloneError` trên Firefox và IE11 [#2559](https://github.com/mapbox/mapbox-gl-js/pull/2559)
- Sửa lỗi ngăn animation camera được kích hoạt trong listener `moveend` [#2944](https://github.com/mapbox/mapbox-gl-js/pull/2944)
- Sửa lỗi ngăn `fill-outline-color` bị unset [#2964](https://github.com/mapbox/mapbox-gl-js/pull/2964)
- Sửa hỗ trợ webpack [#2887](https://github.com/mapbox/mapbox-gl-js/pull/2887)
- Ngăn các nút trong control hoạt động như nút submit form [#2935](https://github.com/mapbox/mapbox-gl-js/pull/2935)
- Sửa lỗi ngăn tương tác bản đồ gần hai control cùng nằm ở một góc [#2932](https://github.com/mapbox/mapbox-gl-js/pull/2932)
- Sửa crash do hàng đợi (queue) thay đổi style theo lô lớn [#2926](https://github.com/mapbox/mapbox-gl-js/issues/2926)

## 0.21.0 (July 13 2016)

#### Thay đổi phá vỡ tương thích

- Các vòng trong (inner ring) của polygon GeoJSON giờ đây được quấn lại (rewound) để tuân thủ [vector tile v2](https://github.com/mapbox/vector-tile-spec/blob/master/2.1/README.md#4344-polygon-geometry-type). Điều này có thể ảnh hưởng đến một số cách sử dụng `line-offset`, làm đảo ngược hướng của offset. [#2889](https://github.com/mapbox/mapbox-gl-js/issues/2889)

#### Tính năng mới & Cải tiến

- Thêm thuộc tính style `text-pitch-alignment` [#2668](https://github.com/mapbox/mapbox-gl-js/pull/2668)
- Cho phép tham số truy vấn (query parameter) trong URL `mapbox://` [#2702](https://github.com/mapbox/mapbox-gl-js/pull/2702)
- Thêm các thuộc tính style `icon-text-fit` và `icon-text-fit-padding` [#2720](https://github.com/mapbox/mapbox-gl-js/pull/2720)
- Kích hoạt property function cho `icon-rotate` [#2738](https://github.com/mapbox/mapbox-gl-js/pull/2738)
- Kích hoạt property function cho `fill-opacity` [#2733](https://github.com/mapbox/mapbox-gl-js/pull/2733)
- Phát sự kiện `Map#mouseout` [#2777](https://github.com/mapbox/mapbox-gl-js/pull/2777)
- Cho phép tham số truy vấn trên tất cả URL sprite [#2772](https://github.com/mapbox/mapbox-gl-js/pull/2772)
- Tăng kích thước sprite atlas lên 1024px vuông, cho phép sprite nhiều hơn và lớn hơn [#2802](https://github.com/mapbox/mapbox-gl-js/pull/2802)
- Thêm class `Marker` [#2725](https://github.com/mapbox/mapbox-gl-js/pull/2725) [#2810](https://github.com/mapbox/mapbox-gl-js/pull/2810)
- Thêm tham số URL `{quadkey}` [#2805](https://github.com/mapbox/mapbox-gl-js/pull/2805)
- Thêm thuộc tính style `circle-pitch-scale` [#2821](https://github.com/mapbox/mapbox-gl-js/pull/2821)

#### Sửa lỗi

- Sửa render layer có số lượng feature lớn [#2794](https://github.com/mapbox/mapbox-gl-js/pull/2794)
- Sửa lỗi ngoại lệ trong quá trình tương tác drag-rotate [#2840](https://github.com/mapbox/mapbox-gl-js/pull/2840)
- Sửa lỗi khi thêm và xóa một layer trong cùng một chu kỳ cập nhật [#2845](https://github.com/mapbox/mapbox-gl-js/pull/2845)
- Sửa cảnh báo "Geometry exceeds allowed extent" giả (sai) [#2568](https://github.com/mapbox/mapbox-gl-js/issues/2568)
- Sửa lỗi `Map#loaded` trả về true trong khi vẫn còn cập nhật tile đang chờ xử lý [#2847](https://github.com/mapbox/mapbox-gl-js/pull/2847)
- Sửa lỗi validation style bị ném ra khi xóa một filter [#2847](https://github.com/mapbox/mapbox-gl-js/pull/2847)
- Sửa lỗi đối tượng event data không được truyền cho sự kiện double click [#2814](https://github.com/mapbox/mapbox-gl-js/pull/2814)
- Sửa lỗi multipolygon biến mất khỏi bản đồ ở một số mức zoom nhất định [#2704](https://github.com/mapbox/mapbox-gl-js/issues/2704)
- Sửa lỗi ngoại lệ do `queryRenderedFeatures` gây ra trên Safari và Firefox [#2822](https://github.com/mapbox/mapbox-gl-js/pull/2822)
- Sửa lỗi `mapboxgl#supported()` trả về `true` trên các phiên bản cũ của IE11 [mapbox/mapbox-gl-supported#1](https://github.com/mapbox/mapbox-gl-supported/issues/1)

## 0.20.1 (June 21 2016)

#### Sửa lỗi

- Sửa lỗi ngoại lệ khi thay đổi các thuộc tính `*-translate` qua `setPaintProperty` ([#2762](https://github.com/mapbox/mapbox-gl-js/issues/2762))

## 0.20.0 (June 10 2016)

#### Tính năng mới & Cải tiến

- Thêm hỗ trợ WMS giới hạn [#2612](https://github.com/mapbox/mapbox-gl-js/pull/2612)
- Thêm tùy chọn constructor `workerCount` [#2666](https://github.com/mapbox/mapbox-gl-js/pull/2666)
- Cải thiện hiệu năng của `locationPoint` và `pointLocation` [#2690](https://github.com/mapbox/mapbox-gl-js/pull/2690)
- Gỡ bỏ thông báo cảnh báo "Not using VertexArrayObject extension" [#2707](https://github.com/mapbox/mapbox-gl-js/pull/2707)
- Thêm thuộc tính `version` vào mapboxgl [#2660](https://github.com/mapbox/mapbox-gl-js/pull/2660)
- Hỗ trợ property function trong `circle-opacity` và `circle-blur` [#2693](https://github.com/mapbox/mapbox-gl-js/pull/2693)

#### Sửa lỗi

- Sửa lỗi ngoại lệ do trình xử lý "drag rotate" gây ra [#2680](https://github.com/mapbox/mapbox-gl-js/issues/2680)
- Trả về một mảng rỗng thay vì một object rỗng từ `queryRenderedFeatures` [#2694](https://github.com/mapbox/mapbox-gl-js/pull/2694)
- Sửa lỗi bản đồ không render trên IE

## 0.19.1 (June 2 2016)

#### Sửa lỗi

- Sửa render polygon có hơn 35k đỉnh (vertices) [#2657](https://github.com/mapbox/mapbox-gl-js/issues/2657)

## 0.19.0 (May 31 2016)

#### Tính năng mới & Cải tiến

- Cho phép sử dụng ký tự đặc biệt trong tên trường thuộc tính (property field) [#2547](https://github.com/mapbox/mapbox-gl-js/pull/2547)
- Cải thiện tốc độ render trên fill layer [#1606](https://github.com/mapbox/mapbox-gl-js/pull/1606)
- Thêm hỗ trợ data-driven styling cho `fill-color` và `fill-outline-color` [#2629](https://github.com/mapbox/mapbox-gl-js/pull/2629)
- Thêm toán tử filter `has` và `!has` [mapbox/feature-filter#15](https://github.com/mapbox/feature-filter/pull/15)
- Cải thiện trình xử lý bàn phím khi giữ phím [#2530](https://github.com/mapbox/mapbox-gl-js/pull/2530)
- Hỗ trợ scheme tile 'tms' [#2565](https://github.com/mapbox/mapbox-gl-js/pull/2565)
- Thêm tùy chọn `trackResize` cho `Map` [#2591](https://github.com/mapbox/mapbox-gl-js/pull/2591)

#### Sửa lỗi

- Thu nhỏ vòng tròn (circle) khi bản đồ được hiển thị ở một góc pitch [#2541](https://github.com/mapbox/mapbox-gl-js/issues/2541)
- Sửa lỗi render pattern nền (background pattern) [#2557](https://github.com/mapbox/mapbox-gl-js/pull/2557)
- Sửa lỗi ngăn việc gỡ bỏ `fill-pattern` khỏi một fill layer [#2534](https://github.com/mapbox/mapbox-gl-js/issues/2534)
- Sửa render `line-pattern` và `fill-pattern` [#2596](https://github.com/mapbox/mapbox-gl-js/pull/2596)
- Sửa một số lỗi render đặc thù theo nền tảng [#2553](https://github.com/mapbox/mapbox-gl-js/pull/2553)
- Trả về object rỗng từ `queryRenderedFeatures` trước khi bản đồ được tải xong [#2621](https://github.com/mapbox/mapbox-gl-js/pull/2621)
- Sửa cảnh báo "there is no texture bound to the unit 1" [#2509](https://github.com/mapbox/mapbox-gl-js/pull/2509)
- Cho phép các giá trị đang transition được unset [#2561](https://github.com/mapbox/mapbox-gl-js/pull/2561)

## 0.18.0 (April 13 2016)

#### Tính năng mới & Cải tiến

- Triển khai hàm kết hợp zoom-và-property cho `circle-color` và `circle-size` [#2454](https://github.com/mapbox/mapbox-gl-js/pull/2454)
- Loại bỏ trùng lặp các attribution là chuỗi con của các attribution khác [#2453](https://github.com/mapbox/mapbox-gl-js/pull/2453)
- Nhiều cải thiện hiệu năng khác [#2483](https://github.com/mapbox/mapbox-gl-js/pull/2483) [#2488](https://github.com/mapbox/mapbox-gl-js/pull/2488)

#### Sửa lỗi

- Sửa lỗi khi unset rồi set lại một thuộc tính style [#2464](https://github.com/mapbox/mapbox-gl-js/pull/2464)
- Sửa lỗi khi cập nhật thuộc tính paint trong lúc sử dụng class [#2496](https://github.com/mapbox/mapbox-gl-js/pull/2496)
- Sửa lỗi do race condition trong unserializeBuckets [#2497](https://github.com/mapbox/mapbox-gl-js/pull/2497)
- Sửa lỗi tile bị overzoom trong các thế giới được wrap (wrapped worlds) [#2482](https://github.com/mapbox/mapbox-gl-js/issues/2482)
- Sửa lỗi do thay đổi một đối tượng filter sau khi gọi `Map#setFilter` [#2495](https://github.com/mapbox/mapbox-gl-js/pull/2495)

## 0.17.0 (April 13 2016)

#### Thay đổi phá vỡ tương thích

- Gỡ bỏ `map.batch` để thay bằng việc tự động gộp lô (batching) các thay đổi style (ví dụ: các lệnh gọi `Map#setLayoutProperty`, `Map#setPaintProperty`, `Map#setFilter`, `Map#setClasses`, v.v.) và áp dụng chúng một lần mỗi khung hình (frame), cải thiện đáng kể hiệu năng khi cập nhật style thường xuyên [#2355](https://github.com/mapbox/mapbox-gl-js/pull/2355) [#2380](https://github.com/mapbox/mapbox-gl-js/pull/2380)
- Gỡ bỏ `util.throttle` [#2345](https://github.com/mapbox/mapbox-gl-js/issues/2345)

#### Tính năng mới & Cải tiến

- Cải thiện hiệu năng của tất cả các phương thức thay đổi style bằng cách chỉ tính toán lại các thuộc tính bị ảnh hưởng [#2339](https://github.com/mapbox/mapbox-gl-js/issues/2339)
- Cải thiện hiệu ứng mờ dần (fading) của nhãn và icon [#2376](https://github.com/mapbox/mapbox-gl-js/pull/2376)
- Cải thiện hiệu năng render bằng cách giảm khối lượng công việc trên main thread [#2394](https://github.com/mapbox/mapbox-gl-js/pull/2394)
- Validate các filter được truyền cho `Map#queryRenderedFeatures` và `Map#querySourceFeatures` [#2349](https://github.com/mapbox/mapbox-gl-js/issues/2349)
- Hiển thị cảnh báo nếu extent hình học (geometry) của vector tile lớn hơn mức được hỗ trợ [#2383](https://github.com/mapbox/mapbox-gl-js/pull/2383)
- Triển khai property function (tức là data-driven styling) cho `circle-color` và `circle-size` [#1932](https://github.com/mapbox/mapbox-gl-js/pull/1932)
- Thêm phương thức `Popup#setDOMContent` [#2436](https://github.com/mapbox/mapbox-gl-js/pull/2436)

#### Sửa lỗi

- Sửa vấn đề hiệu năng do dùng 1 `WebWorker` thay vì `# cpus - 1` `WebWorker`, làm chậm thời gian tải tile [#2408](https://github.com/mapbox/mapbox-gl-js/pull/2408)
- Sửa lỗi `Map#queryRenderedFeatures` đôi khi trả về các feature đã bị xóa [#2353](https://github.com/mapbox/mapbox-gl-js/issues/2353)
- Sửa tùy chọn `clusterMaxZoom` trên `GeoJSONSource` không hoạt động như mong đợi [#2374](https://github.com/mapbox/mapbox-gl-js/issues/2374)
- Sửa render khử răng cưa (anti-aliased) cho các fill dạng pattern [#2372](https://github.com/mapbox/mapbox-gl-js/issues/2372)
- Sửa lỗi ngoại lệ khi gọi `Map#queryRenderedFeatures` hoặc `Map#querySourceFeatures` mà không có tham số nào
- Sửa lỗi ngoại lệ khi gọi `Map#setLayoutProperty` cho `text-field` hoặc `icon-image` [#2407](https://github.com/mapbox/mapbox-gl-js/issues/2407)

## 0.16.0 (March 24 2016)

#### Thay đổi phá vỡ tương thích

- Thay thế `Map#featuresAt` và `Map#featuresIn` bằng `Map#queryRenderedFeatures` và `map.querySourceFeatures` ([#2224](https://github.com/mapbox/mapbox-gl-js/pull/2224))
    - Thay `featuresAt` và `featuresIn` bằng `queryRenderedFeatures`
    - Làm cho `queryRenderedFeatures` đồng bộ (synchronous), gỡ bỏ callback và sử dụng giá trị trả về.
    - Đổi tên tham số `layer` thành `layers` và biến nó thành một mảng tên layer.
    - Gỡ bỏ tham số `radius`. `radius` trước đây được dùng với `featuresAt` để tính đến các thuộc tính style như `line-width` và `circle-radius`. `queryRenderedFeatures` đã tính đến các thuộc tính style này. Nếu bạn cần truy vấn một vùng lớn hơn, hãy dùng truy vấn bounding box thay vì truy vấn điểm.
    - Gỡ bỏ tham số `includeGeometry` vì `queryRenderedFeatures` luôn bao gồm geometry.
- `Map#debug` được đổi tên thành `Map#showTileBoundaries` ([#2284](https://github.com/mapbox/mapbox-gl-js/pull/2284))
- `Map#collisionDebug` được đổi tên thành `Map#showCollisionBoxes` ([#2284](https://github.com/mapbox/mapbox-gl-js/pull/2284))

#### Tính năng mới & Cải tiến

- Cải thiện hiệu năng render tổng thể. ([#2221](https://github.com/mapbox/mapbox-gl-js/pull/2221))
- Cải thiện hiệu năng của `GeoJSONSource#setData`. ([#2222](https://github.com/mapbox/mapbox-gl-js/pull/2222))
- Thêm phương thức `Map#setMaxBounds` ([#2234](https://github.com/mapbox/mapbox-gl-js/pull/2234))
- Thêm phương thức `isActive` và `isEnabled` cho các trình xử lý tương tác ([#2238](https://github.com/mapbox/mapbox-gl-js/pull/2238))
- Thêm phương thức `Map#setZoomBounds` ([#2243](https://github.com/mapbox/mapbox-gl-js/pull/2243))
- Thêm các sự kiện chạm (touch events) ([#2195](https://github.com/mapbox/mapbox-gl-js/issues/2195))
- Thêm `map.queryRenderedFeatures` để truy vấn các đại diện đã được style hóa và render của feature ([#2224](https://github.com/mapbox/mapbox-gl-js/pull/2224))
- Thêm `map.querySourceFeatures` để lấy feature trực tiếp từ vector tile, độc lập với style ([#2224](https://github.com/mapbox/mapbox-gl-js/pull/2224))
- Thêm control `mapboxgl.Geolocate` ([#1939](https://github.com/mapbox/mapbox-gl-js/issues/1939))
- Làm cho các pattern nền (background pattern) render liền mạch qua ranh giới tile ([#2305](https://github.com/mapbox/mapbox-gl-js/pull/2305))

#### Sửa lỗi

- Sửa các lệnh gọi `setFilter`, `setLayoutProperty` và `setLayerZoomRange` trên các ref children ([#2228](https://github.com/mapbox/mapbox-gl-js/issues/2228))
- Sửa lỗi bucket `undefined` sau khi gọi `setFilter` ([#2244](https://github.com/mapbox/mapbox-gl-js/issues/2244))
- Sửa các lỗi khiến symbol đang ẩn vẫn bị render ([#2246](https://github.com/mapbox/mapbox-gl-js/pull/2246), [#2276](https://github.com/mapbox/mapbox-gl-js/pull/2276))
- Sửa hiện tượng nhấp nháy raster [#2236](https://github.com/mapbox/mapbox-gl-js/issues/2236)
- Sửa độ chính xác của `queryRenderedFeatures` ở mức zoom cao ([#2292](https://github.com/mapbox/mapbox-gl-js/pull/2292))
- Sửa lỗi thủng lỗ (holes) trong dữ liệu GeoJSON do thứ tự quấn (winding order) không như mong đợi ([#2285](https://github.com/mapbox/mapbox-gl-js/pull/2285))
- Sửa lỗi các feature đã xóa vẫn được trả về bởi `queryRenderedFeatures` ([#2306](https://github.com/mapbox/mapbox-gl-js/pull/2306))
- Sửa lỗi các fill pattern không như mong đợi bị render ([#2307](https://github.com/mapbox/mapbox-gl-js/pull/2307))
- Sửa vị trí popup khi có các phần tử anh em (sibling) đứng trước [#2311](https://github.com/mapbox/mapbox-gl-js/pull/2311)
- Sửa khử răng cưa của polygon ([#2319](https://github.com/mapbox/mapbox-gl-js/pull/2319))
- Sửa các khe hở (slivers) giữa các polygon không liền kề ([#2319](https://github.com/mapbox/mapbox-gl-js/pull/2319))
- Sửa lỗi phím tắt (keyboard shortcut) khiến trang bị cuộn ([#2312](https://github.com/mapbox/mapbox-gl-js/pull/2312))

## 0.15.0 (March 1 2016)

#### Tính năng mới & Cải tiến

- Thêm `ImageSource#setCoordinates` và `VideoSource#setCoordinates` ([#2184](https://github.com/mapbox/mapbox-gl-js/pull/2184))

#### Sửa lỗi

- Sửa hiện tượng nhấp nháy trên raster layer ([#2211](https://github.com/mapbox/mapbox-gl-js/pull/2211))
- Sửa lỗi trình duyệt bị treo khi zoom nhanh trên raster layer ([#2211](https://github.com/mapbox/mapbox-gl-js/pull/2211))

## 0.14.3 (Feb 25 2016)

#### Tính năng mới & Cải tiến

- Cải thiện độ phản hồi khi zoom out bằng cách dùng các parent tile đã cache ([#2168](https://github.com/mapbox/mapbox-gl-js/pull/2168))
- Cải thiện các gợi ý ngữ cảnh (contextual clues) trong validation style API ([#2170](https://github.com/mapbox/mapbox-gl-js/issues/2170))
- Cải thiện hiệu năng của các phương thức bao gồm `setData` ([#2174](https://github.com/mapbox/mapbox-gl-js/pull/2174))

#### Sửa lỗi

- Sửa kích thước nét đứt (line dash) không chính xác ([#2099](https://github.com/mapbox/mapbox-gl-js/issues/2099))
- Sửa lỗi khiến filter feature `in` bỏ sót feature ([#2166](https://github.com/mapbox/mapbox-gl-js/pull/2166))
- Sửa lỗi ngăn `Map#load` được phát ra khi xảy ra lỗi tile "Not Found" ([#2176](https://github.com/mapbox/mapbox-gl-js/pull/2176))
- Sửa lỗi hình ảnh render trên GPU di động ([#2117](https://github.com/mapbox/mapbox-gl-js/pull/2117))

## 0.14.2 (Feb 19 2016)

#### Sửa lỗi

- Tìm kiếm các parent tile đã tải trong cache
- Đặt kích thước tile cache dựa theo kích thước viewport ([#2137](https://github.com/mapbox/mapbox-gl-js/issues/2137))
- Sửa thứ tự render tile theo từng layer
- Gỡ bỏ throttling khi cập nhật source ([#2139](https://github.com/mapbox/mapbox-gl-js/issues/2139))
- Làm cho việc pan trong lúc zoom mượt hơn (linear hơn) ([#2070](https://github.com/mapbox/mapbox-gl-js/issues/2070))
- Làm tròn các điểm được tạo trong quá trình tạo bucket ([#2067](https://github.com/mapbox/mapbox-gl-js/issues/2067))
- Sửa giới hạn (bounds) cho bản đồ bị xoay hoặc nghiêng ([#1842](https://github.com/mapbox/mapbox-gl-js/issues/1842))
- Sửa featuresAt bị overscale ([#2103](https://github.com/mapbox/mapbox-gl-js/issues/2103))
- Cho phép dùng `tileSize: 512` như một công tắc để đánh đổi hỗ trợ retina lấy tile raster 512px
- Sửa lỗi serialize các paint class ([#2107](https://github.com/mapbox/mapbox-gl-js/issues/2107))
- Sửa lỗi việc unset thuộc tính style có thể làm thay đổi giá trị của các thuộc tính style khác ([#2105](https://github.com/mapbox/mapbox-gl-js/pull/2105))
- Đường nét đứt ít bị nghiêng hơn gần các góc nhọn ([#967](https://github.com/mapbox/mapbox-gl-js/issues/967))
- Phát sự kiện map#load nếu không có style ban đầu nào được đặt ([#2042](https://github.com/mapbox/mapbox-gl-js/issues/2042))

## 0.14.1 (Feb 10 2016)

#### Sửa lỗi

- Sửa lỗi symbol bị xoay sai dọc theo line gần ranh giới tile ([#2062](https://github.com/mapbox/mapbox-gl-js/issues/2062))
- Sửa lỗi render bị hỏng khi một fill layer đứng sau một số symbol layer nhất định ([#2092](https://github.com/mapbox/mapbox-gl-js/issues/2092))

## 0.14.0 (Feb 8 2016)

#### Thay đổi phá vỡ tương thích

- Chuyển các tùy chọn clustering của `GeoJSONSource` từ đo bằng đơn vị extent sang đo bằng pixel ([#2026](https://github.com/mapbox/mapbox-gl-js/pull/2026))

#### Tính năng mới & Cải tiến

- Cải thiện thông báo lỗi cho màu không hợp lệ ([#2006](https://github.com/mapbox/mapbox-gl-js/pull/2006))
- Thêm hỗ trợ cho tile có extent thay đổi được ([#2010](https://github.com/mapbox/mapbox-gl-js/pull/2010))
- Cải thiện hiệu năng và kích thước tối đa của `filter` ([#2024](https://github.com/mapbox/mapbox-gl-js/issues/2024))
- Thay đổi cách render circle sao cho tất cả các node hình học đều được vẽ, không chỉ vòng ngoài (outer ring) của geometry ([#2027](https://github.com/mapbox/mapbox-gl-js/pull/2027))
- Thêm phương thức `Map#getStyle` ([#1982](https://github.com/mapbox/mapbox-gl-js/issues/1982))

#### Sửa lỗi

- Sửa lỗi khiến WebGL context bị "dùng hết" khi gọi `mapboxgl.supported()` ([#2018](https://github.com/mapbox/mapbox-gl-js/issues/2018))
- Sửa việc sắp xếp thứ tự z (z-order) của symbol không ổn định ([#2023](https://github.com/mapbox/mapbox-gl-js/pull/2023))
- Sửa nhãn bị méo khi zoom ([#2012](https://github.com/mapbox/mapbox-gl-js/issues/2012))
- Sửa lỗi icon bị nhảy khi chạm hai ngón tay lên trackpad ([#1990](https://github.com/mapbox/mapbox-gl-js/pull/1990))
- Sửa lỗi nhãn debug va chạm (collision debug) bị overzoom ([#2033](https://github.com/mapbox/mapbox-gl-js/issues/2033))
- Sửa lỗi nét đứt bị trượt dọc theo line trong lúc zoom ([#2039](https://github.com/mapbox/mapbox-gl-js/issues/2039))
- Sửa `minzoom` bị overscale không đúng cho GeoJSON source ([#1651](https://github.com/mapbox/mapbox-gl-js/issues/1651))
- Sửa việc validation hàm quá nghiêm ngặt đối với các stop trùng lặp ([#2075](https://github.com/mapbox/mapbox-gl-js/pull/2075))
- Sửa crash do `performance.now` không tồn tại trên một số trình duyệt ([#2056](https://github.com/mapbox/mapbox-gl-js/issues/2056))
- Sửa lỗi unset các thuộc tính paint ([#2037](https://github.com/mapbox/mapbox-gl-js/issues/2037))
- Sửa lỗi khiến nhiều event listener của trình xử lý tương tác bị gắn cùng lúc ([#2069](https://github.com/mapbox/mapbox-gl-js/issues/2069))
- Sửa lỗi chỉ một debug box duy nhất được vẽ ([#2034](https://github.com/mapbox/mapbox-gl-js/issues/2034))

## 0.13.1 (Jan 27 2016)

#### Sửa lỗi

- Sửa gói npm bị hỏng do các module đóng gói (bundled modules) đã lỗi thời

## 0.13.0 (Jan 27 2016)

#### Sửa lỗi

- Sửa easeTo khi pan, zoom và xoay lúc rotation ban đầu khác 0 ([#1950](https://github.com/mapbox/mapbox-gl-js/pull/1950))
- Sửa render tile có extent khác 4096 ([#1952](https://github.com/mapbox/mapbox-gl-js/issues/1952))
- Sửa lỗi thiếu collision box của icon ([#1978](https://github.com/mapbox/mapbox-gl-js/issues/1978))
- Sửa lỗi `Tile#buffers` null ([#1987](https://github.com/mapbox/mapbox-gl-js/pull/1987))

#### Tính năng mới & Cải tiến

- Thêm thuộc tính style `symbol-avoid-edges` ([#1951](https://github.com/mapbox/mapbox-gl-js/pull/1951))
- Cải thiện thuật toán kiểm tra `symbol-max-angle` ([#1959](https://github.com/mapbox/mapbox-gl-js/pull/1959))
- Đã thêm chức năng gom cụm marker (marker clustering)! ([#1931](https://github.com/mapbox/mapbox-gl-js/pull/1931))
- Thêm các sự kiện zoomstart, zoom và zoomend ([#1958](https://github.com/mapbox/mapbox-gl-js/issues/1958))
- Vô hiệu hóa drag khi mousedown lúc dùng boxzoom ([#1907](https://github.com/mapbox/mapbox-gl-js/issues/1907))

## 0.12.4 (Jan 19 2016)

#### Sửa lỗi

- Sửa lỗi giá trị null của elementGroups ([#1933](https://github.com/mapbox/mapbox-gl-js/issues/1933))
- Sửa một số trường hợp tràn (overflow) glyph atlas ([#1923](https://github.com/mapbox/mapbox-gl-js/pull/1923))

## 0.12.3 (Jan 14 2016)

#### Cải tiến API

- Hỗ trợ tùy chọn attribution nội tuyến trong tùy chọn bản đồ ([#1865](https://github.com/mapbox/mapbox-gl-js/issues/1865))
- Cải thiện các tùy chọn flyTo ([#1854](https://github.com/mapbox/mapbox-gl-js/issues/1854), [#1429](https://github.com/mapbox/mapbox-gl-js/issues/1429))

#### Sửa lỗi

- Sửa hiện tượng nhấp nháy với tile bị overscale ([#1921](https://github.com/mapbox/mapbox-gl-js/issues/1921))
- Gỡ bỏ các lệnh gọi Node.remove để tương thích trình duyệt IE ([#1900](https://github.com/mapbox/mapbox-gl-js/issues/1900))
- Khớp pattern tại ranh giới tile ([#1908](https://github.com/mapbox/mapbox-gl-js/pull/1908))
- Sửa Tile#positionAt, sửa các test truy vấn ([#1899](https://github.com/mapbox/mapbox-gl-js/issues/1899))
- Sửa hiện tượng nhấp nháy trên đường phố (streets) ([#1875](https://github.com/mapbox/mapbox-gl-js/issues/1875))
- Sửa thuộc tính text-max-angle ([#1870](https://github.com/mapbox/mapbox-gl-js/issues/1870))
- Sửa pattern line bị overscale ([#1856](https://github.com/mapbox/mapbox-gl-js/issues/1856))
- Sửa pattern và icon khi pixelRatio không khớp nhau ([#1851](https://github.com/mapbox/mapbox-gl-js/issues/1851))
- Sửa nhãn bị thiếu khi text size 0 ở mức zoom tối đa ([#1809](https://github.com/mapbox/mapbox-gl-js/issues/1809))
- Dùng nội suy tuyến tính (linear interp) khi tỷ lệ pixel không khớp nhau ([#1601](https://github.com/mapbox/mapbox-gl-js/issues/1601))
- Sửa vùng trống, hiện tượng nhấp nháy trên raster layer ([#1876](https://github.com/mapbox/mapbox-gl-js/issues/1876), [#675](https://github.com/mapbox/mapbox-gl-js/issues/675))
- Sửa nhãn bị trượt/bị cắt tại ranh giới tile ([#757](https://github.com/mapbox/mapbox-gl-js/issues/757))

#### Cải thiện trải nghiệm người dùng (UX)

- Cải thiện hiệu năng cảm nhận của trình xử lý cảm ứng (touch) ([#1844](https://github.com/mapbox/mapbox-gl-js/issues/1844))

## 0.12.2 (Dec 22 2015)

#### Cải tiến API

- Hỗ trợ LngLat.convert([w, s, e, n]) ([#1812](https://github.com/mapbox/mapbox-gl-js/issues/1812))
- GeoJSON không hợp lệ giờ đây được xử lý tốt hơn

#### Sửa lỗi

- Sửa `Popup#addTo` khi popup đã mở sẵn ([#1811](https://github.com/mapbox/mapbox-gl-js/issues/1811))
- Sửa hiện tượng méo hình (warping) khi xoay/zoom rất nhanh
- `Map#flyTo` giờ đây sẽ bay qua kinh tuyến đối diện (antimeridian) nếu đường đó ngắn hơn ([#1853](https://github.com/mapbox/mapbox-gl-js/issues/1853))

## 0.12.1 (Dec 8 2015)

#### Thay đổi phá vỡ tương thích

- Đảo ngược hướng của `line-offset` ([#1808](https://github.com/mapbox/mapbox-gl-js/pull/1808))
- Đổi tên trình xử lý tương tác `Pinch` thành `TouchZoomRotate` ([#1777](https://github.com/mapbox/mapbox-gl-js/pull/1777))
- Chuyển `Map#update` và `Map#render` thành phương thức private ([#1798](https://github.com/mapbox/mapbox-gl-js/pull/1798))
- Làm cho `Map#remove` gỡ bỏ các phần tử DOM đã tạo ([#1789](https://github.com/mapbox/mapbox-gl-js/issues/1789))

#### Cải tiến API

- Thêm phương thức để vô hiệu hóa xoay bằng cảm ứng (touch rotation) ([#1777](https://github.com/mapbox/mapbox-gl-js/pull/1777))
- Thêm tùy chọn `position` cho `Attribution` ([#1689](https://github.com/mapbox/mapbox-gl-js/issues/1689))

#### Sửa lỗi

- Đảm bảo lỗi tải tile được báo cáo đúng cách ([#1799](https://github.com/mapbox/mapbox-gl-js/pull/1799))
- Đảm bảo việc thêm lại một popup đã bị xóa trước đó hoạt động đúng ([#1477](https://github.com/mapbox/mapbox-gl-js/issues/1477))

#### Cải thiện trải nghiệm người dùng (UX)

- Không làm tròn mức zoom trong quá trình tương tác double-click ([#1640](https://github.com/mapbox/mapbox-gl-js/issues/1640))

## 0.12.0 (Dec 2 2015)

#### Cải tiến API

- Thêm thuộc tính style `line-offset` ([#1778](https://github.com/mapbox/mapbox-gl-js/issues/1778))

## 0.11.5 (Dec 1 2015)

#### Sửa lỗi

- Sửa thứ tự render symbol layer không ổn định khi thêm/xóa layer ([#1558](https://github.com/mapbox/mapbox-gl-js/issues/1558))
- Phát sự kiện map loaded ngay cả khi raster tile gặp lỗi
- Sửa animation pan trong lúc easeTo có thay đổi zoom
- Sửa animation pitch trong lúc flyTo
- Sửa animation pitch trong lúc easeTo
- Ngăn việc xoay phát ra sự kiện `mouseend` ([#1104](https://github.com/mapbox/mapbox-gl-js/issues/1104))

#### Cải tiến API

- Phát sự kiện `mousedown` và `mouseup` ([#1411](https://github.com/mapbox/mapbox-gl-js/issues/1411))
- Phát sự kiện `movestart` và `moveend` khi pan ([#1658](https://github.com/mapbox/mapbox-gl-js/issues/1658))
- Thêm các sự kiện drag ([#1442](https://github.com/mapbox/mapbox-gl-js/issues/1442))
- Yêu cầu ảnh webp cho raster tile của mapbox:// trên chrome ([#1725](https://github.com/mapbox/mapbox-gl-js/issues/1725))

#### Cải thiện trải nghiệm người dùng (UX)

- Thêm quán tính (inertia) khi xoay bản đồ ([#620](https://github.com/mapbox/mapbox-gl-js/issues/620))

## 0.11.4 (Nov 16 2015)

#### Sửa lỗi

- Sửa alpha blending của các layer có alpha ([#1684](https://github.com/mapbox/mapbox-gl-js/issues/1684))

## 0.11.3 (Nov 10 2015)

#### Sửa lỗi

- Sửa render và hiệu năng GeoJSON ([#1685](https://github.com/mapbox/mapbox-gl-js/pull/1685))

#### Cải thiện trải nghiệm người dùng (UX)

- Dùng tài nguyên SVG cho các control UI ([#1657](https://github.com/mapbox/mapbox-gl-js/pull/1657))
- Zoom out bằng shift + dblclick ([#1666](https://github.com/mapbox/mapbox-gl-js/issues/1666))

## 0.11.2 (Oct 29 2015)

- Nhiều cải thiện hiệu năng khác

#### Sửa lỗi

- Sửa sprite trên các hệ thống có `devicePixelRatio` không phải số nguyên ([#1029](https://github.com/mapbox/mapbox-gl-js/issues/1029) [#1475](https://github.com/mapbox/mapbox-gl-js/issues/1475) [#1476](https://github.com/mapbox/mapbox-gl-js/issues/1476))
- Sửa layer minZoom bị bỏ qua nếu không nhỏ hơn maxZoom của source
- Sửa việc đặt symbol tại điểm bắt đầu của một line ([#1461](https://github.com/mapbox/mapbox-gl-js/issues/1461))
- Sửa `raster-opacity` trên các source không phải dạng tile ([#1270](https://github.com/mapbox/mapbox-gl-js/issues/1270))
- Bỏ qua boxzoom khi shift-click ([#1655](https://github.com/mapbox/mapbox-gl-js/issues/1655))

#### Cải thiện trải nghiệm người dùng (UX)

- Cho phép ngắt dòng tại các dấu câu thông dụng ([#1115](https://github.com/mapbox/mapbox-gl-js/issues/1115))

#### Cải tiến API

- Thêm phương thức toString và toArray vào LngLat, LngLatBounds ([#1571](https://github.com/mapbox/mapbox-gl-js/issues/1571))
- Thêm phương thức `Transform#resize`
- Thêm phương thức `Map#getLayer` ([#1183](https://github.com/mapbox/mapbox-gl-js/issues/1183))
- Thêm thuộc tính `Transform#unmodified` ([#1452](https://github.com/mapbox/mapbox-gl-js/issues/1452))
- Truyền tiếp (propagate) các sự kiện WebGL context ([#1612](https://github.com/mapbox/mapbox-gl-js/pull/1612))

## 0.11.1 (Sep 30 2015)

#### Sửa lỗi

- Thêm thống kê và checkbox vào trang debug
- Sửa `Map#featuresAt` cho các vector source không phải extent 4096 ([#1529](https://github.com/mapbox/mapbox-gl-js/issues/1529))
- Không phát `mousemove` khi drag-pan
- Sửa các ràng buộc (constrains) của maxBounds ([#1539](https://github.com/mapbox/mapbox-gl-js/issues/1539))
- Sửa vòng lặp vô hạn của maxBounds ([#1538](https://github.com/mapbox/mapbox-gl-js/issues/1538))
- Sửa rò rỉ bộ nhớ trong worker
- Assert `TileCoord` hợp lệ, sửa cách tính wrap trong `TileCoord#cover` ([#1483](https://github.com/mapbox/mapbox-gl-js/issues/1483))
- Hủy tải raster tile nếu không nằm trong viewport ([#1490](https://github.com/mapbox/mapbox-gl-js/issues/1490))

#### Cải tiến API

- Thêm listener sự kiện `Map` cho `mouseup`, `contextmenu` (click chuột phải) ([#1532](https://github.com/mapbox/mapbox-gl-js/issues/1532))

## 0.11.0 (Sep 11 2015)

#### Cải tiến API

- Thêm `Map#featuresIn`: truy vấn feature theo bounding-box
- Phát ra lỗi validation stylesheet ([#1436](https://github.com/mapbox/mapbox-gl-js/issues/1436))

#### Cải thiện trải nghiệm người dùng (UX)

- Xử lý `center`, `zoom`, `bearing`, `pitch` theo style v8 ([#1452](https://github.com/mapbox/mapbox-gl-js/issues/1452))
- Cải thiện style cho loại circle ([#1446](https://github.com/mapbox/mapbox-gl-js/issues/1446))
- Cải thiện khử răng cưa cho line dạng nét đứt và pattern

#### Sửa lỗi

- Tải ảnh theo cách tuân thủ header Cache-Control
- Lọc các kết quả khớp rtree chỉ lấy những cái giao với bbox
- Ghi log lỗi theo mặc định ([#1463](https://github.com/mapbox/mapbox-gl-js/issues/1463))
- Sửa lỗi thay đổi `text-size` qua `setLayoutProperty` ([#1451](https://github.com/mapbox/mapbox-gl-js/issues/1451))
- Ném lỗi khi lat > 90 || < -90. ([#1443](https://github.com/mapbox/mapbox-gl-js/issues/1443))
- Sửa lỗi cắt hình (clipping) của circle ([#1457](https://github.com/mapbox/mapbox-gl-js/issues/1457))

## 0.10.0 (Aug 21 2015)

#### Thay đổi phá vỡ tương thích

- Chuyển sang thứ tự tọa độ [kinh độ, vĩ độ] (longitude, latitude), khớp với GeoJSON. Chúng tôi dự đoán rằng mapbox-gl-js sẽ được sử dụng rộng rãi
  cùng với GeoJSON, và về lâu dài việc có thứ tự tọa độ nhất quán với GeoJSON sẽ giúp giảm nhầm lẫn
  và sự không tương thích hơn là dùng thứ tự [vĩ độ, kinh độ].

    Các API sau đã được đổi tên:
    - `LatLng` được đổi tên thành `LngLat`
    - `LatLngBounds` được đổi tên thành `LngLatBounds`
    - `Popup#setLatLng` được đổi tên thành `Popup#setLngLat`
    - `Popup#getLatLng` được đổi tên thành `Popup#getLngLat`
    - Thuộc tính `latLng` của các sự kiện Map được đổi tên thành `lngLat`

    Các API sau đây giờ đây kỳ vọng tọa độ dạng mảng theo thứ tự [kinh độ, vĩ độ]:
    - `LngLat.convert`
    - `LngLatBounds.convert`
    - `Popup#setLngLat`
    - Tùy chọn `center` và `maxBounds` của constructor `Map`
    - Các tham số của `Map#setCenter`, `Map#fitBounds`, `Map#panTo` và `Map#project`
    - Tùy chọn `center` của `Map#jumpTo`, `Map#easeTo` và `Map#flyTo`
    - Tùy chọn `around` của `Map#zoomTo`, `Map#rotateTo` và `Map#easeTo`
    - Các thuộc tính `coordinates` của video source và image source

- Đã cập nhật lên mapbox-gl-style-spec v8.0.0 ([Changelog](https://github.com/mapbox/mapbox-gl-style-spec/blob/v8.0.0/CHANGELOG.md)). Style giờ đây
  được kỳ vọng là phiên bản 8. Bạn có thể dùng công cụ [gl-style-migrate](https://github.com/mapbox/mapbox-gl-style-lint#migrations)
  để cập nhật các style hiện có.

- Định dạng URL style và glyph của `mapbox://` đã thay đổi. Đối với URL style, giờ đây bạn nên dùng định dạng
  `mapbox://styles/:username/:style`. Phần `:style` của URL không còn chứa username nữa. Đối với URL font, bạn
  nên dùng định dạng `mapbox://fonts/:username/{fontstack}/{range}.pbf`.
- Các style mặc định của Mapbox giờ đây được phục vụ qua Styles API thay vì www.mapbox.com. Bạn có thể sử dụng Styles API
  bằng URL style `mapbox://` trỏ đến một style v8, ví dụ: `mapbox://styles/mapbox/streets-v8`.
- Style satellite v8 (`mapbox://styles/mapbox/satellite-v8`) giờ đây là một style vệ tinh thuần túy, không còn hỗ trợ nhãn
  hoặc đường đồng mức (contour lines) qua class nữa. Để có style vệ tinh có nhãn, hãy dùng `mapbox://styles/mapbox/satellite-hybrid`.

- Gỡ bỏ `mbgl.config.HTTP_URL` và `mbgl.config.FORCE_HTTPS`; https luôn được sử dụng khi kết nối tới Mapbox API.
- Đổi tên `mbgl.config.HTTPS_URL` thành `mbgl.config.API_URL`.

#### Sửa lỗi

- Không vẽ halo khi halo-width bằng 0 ([#1381](https://github.com/mapbox/mapbox-gl-js/issues/1381))
- Hoàn tác các thay đổi shader làm giảm hiệu năng trên IE

#### Cải tiến API

- Giờ đây bạn có thể unset các thuộc tính layout và paint qua API `setLayoutProperty` và `setPaintProperty`
  bằng cách truyền `undefined` làm giá trị thuộc tính.
- Tùy chọn `layer` của `featuresAt` giờ đây hỗ trợ một mảng các layer.

## 0.9.0 (Jul 29 2015)

- URL `glyphs` giờ đây được chuẩn hóa mà không có tiền tố `/v4/` đối với URL `mapbox://`. Hành vi cũ cho `mapbox://fontstacks` vẫn được giữ nguyên ([#1385](https://github.com/mapbox/mapbox-gl-js/issues/1385))
- Expose các tùy chọn `geojson-vt` cho GeoJSON source ([#1271](https://github.com/mapbox/mapbox-gl-js/issues/1271))
- bearing sẽ tự động khớp về "Bắc" trong phạm vi dung sai 7 độ ([#1059](https://github.com/mapbox/mapbox-gl-js/issues/1059))
- Giờ đây bạn có thể thay đổi trực tiếp các thuộc tính layer minzoom và maxzoom bằng `map.setLayerZoomRange(layerId, minzoom, maxzoom)`
- Expose `mapboxgl.Control`, một base class được tất cả các control UI sử dụng
- Tái cấu trúc các trình xử lý tương tác để có thể đưa riêng lẻ vào tùy chọn Map, hoặc bật/tắt riêng lẻ khi runtime, ví dụ: `map.scrollZoom.disable()`.
- Tính năng mới: Giờ đây có thể thực hiện các thao tác theo lô (batch) cùng lúc, cải thiện hiệu năng khi gọi nhiều hàm style: ([#1352](https://github.com/mapbox/mapbox-gl-js/pull/1352))

    ```js
    style.batch(function (s) {
        s.addLayer({ id: 'first', type: 'symbol', source: 'streets' });
        s.addLayer({ id: 'second', type: 'symbol', source: 'streets' });
        s.addLayer({ id: 'third', type: 'symbol', source: 'terrain' });
        s.setPaintProperty('first', 'text-color', 'black');
        s.setPaintProperty('first', 'text-halo-color', 'white');
    });
    ```

- Cải thiện tài liệu
- Cải thiện hiệu năng `featuresAt` bằng cách expose tùy chọn `includeGeometry`
- Cải thiện việc đặt nhãn dọc theo line ([#1283](https://github.com/mapbox/mapbox-gl-js/pull/1283))
- Cải thiện các điểm nối line dạng tròn (round linejoins) trên các line bán trong suốt (mapbox/mapbox-gl-native[#1771](https://github.com/mapbox/mapbox-gl-js/pull/1771))
- Làm tròn mức zoom khi tải raster tile ([@2a2aec](https://github.com/mapbox/mapbox-gl-js/commit/2a2aec44a39e11e73bdf663258bd6d52b83775f5))
- Không thể gọi Source#reload nếu source chưa được tải ([#1198](https://github.com/mapbox/mapbox-gl-js/issues/1198))
- Các sự kiện được nổi bọt (bubble) lên canvas container cho các overlay tùy chỉnh ([#1301](https://github.com/mapbox/mapbox-gl-js/pull/1301))
- Các trình xử lý di chuyển (move handler) giờ đây được gắn vào sự kiện mousedown và touchstart
- map.featuresAt() giờ đây hoạt động được qua đường đổi ngày (dateline)

## 0.8.1 (Jun 16 2015)

- Không có thay đổi code nào; chỉ phát hành để sửa lỗi build trong 0.8.0.

## 0.8.0 (Jun 15 2015)

#### Thay đổi phá vỡ tương thích

- `map.setView(latlng, zoom, bearing)` đã bị gỡ bỏ. Hãy dùng
  [`map.jumpTo(options)`](https://www.mapbox.com/mapbox-gl-js/api/#map/jumpto) thay thế:

    ```js
    map.setView([40, -74.5], 9); // 0.7.0 trở về trước
    map.jumpTo({ center: [40, -74.5], zoom: 9 }); // hiện tại
    ```

- [`map.easeTo`](https://www.mapbox.com/mapbox-gl-js/api/#map/easeto) và
  [`map.flyTo`](https://www.mapbox.com/mapbox-gl-js/api/#map/flyto) giờ đây nhận một
  đối tượng tùy chọn (options object) duy nhất thay vì các tham số theo vị trí:

    ```js
    map.easeTo([40, -74.5], 9, null, { duration: 400 }); // 0.7.0 trở về trước
    map.easeTo({ center: [40, -74.5], zoom: 9, duration: 400 }); // hiện tại
    ```

- `mapboxgl.Source` không còn được export nữa. Hãy dùng `map.addSource()` thay thế. Xem các ví dụ
  [GeoJSON line](https://www.mapbox.com/mapbox-gl-js/example/geojson-line/) hoặc
  [GeoJSON markers](https://www.mapbox.com/mapbox-gl-js/example/geojson-markers/)
  để biết thêm.
- `mapboxgl.util.supported()` đã được chuyển thành [`mapboxgl.supported()`](https://www.mapbox.com/mapbox-gl-js/api/#mapboxgl/supported).

#### Cải thiện trải nghiệm người dùng (UX)

- Thêm render phối cảnh (perspective rendering) ([#1049](https://github.com/mapbox/mapbox-gl-js/pull/1049))
- Đặt nhãn tốt hơn và nhanh hơn ([#1079](https://github.com/mapbox/mapbox-gl-js/pull/1079))
- Thêm hỗ trợ tương tác cảm ứng (touch) trên thiết bị di động ([#949](https://github.com/mapbox/mapbox-gl-js/pull/949))
- Mũi tên popup tương đối theo viewport ([#1065](https://github.com/mapbox/mapbox-gl-js/pull/1065))
- Chuẩn hóa tốc độ zoom bằng con lăn chuột ([#1060](https://github.com/mapbox/mapbox-gl-js/pull/1060))
- Thêm xử lý đúng cho các feature GeoJSON vượt qua đường đổi ngày ([#1275](https://github.com/mapbox/mapbox-gl-js/issues/1275))
- Sắp xếp các symbol chồng lấn theo hướng y ([#470](https://github.com/mapbox/mapbox-gl-js/issues/470))
- Các nút control giờ đây nằm trên lưới 30 pixel ([#1143](https://github.com/mapbox/mapbox-gl-js/issues/1143))
- Cải thiện hiệu năng xử lý GeoJSON

#### Cải tiến API

- Chuyển sang dùng JSDoc để viết tài liệu
- Giờ đây hỗ trợ đóng gói bằng browserify
- Validate các style bản đồ được truyền vào ([#1054](https://github.com/mapbox/mapbox-gl-js/pull/1054))
- Thêm `Map` `setPitch` `getPitch`
- Thêm sự kiện `Map` `dblclick`. ([#1168](https://github.com/mapbox/mapbox-gl-js/issues/1168))
- Thêm `Map` `getSource` ([@660a8c1](https://github.com/mapbox/mapbox-gl-js/commit/660a8c1e087f63282d24a30684d686523bce36cb))
- Thêm `Map` `setFilter` và `getFilter` ([#985](https://github.com/mapbox/mapbox-gl-js/issues/985))
- Thêm tùy chọn `Map` `failIfMajorPerformanceCaveat` ([#1082](https://github.com/mapbox/mapbox-gl-js/pull/1082))
- Thêm tùy chọn `Map` `preserveDrawingBuffer` ([#1232](https://github.com/mapbox/mapbox-gl-js/pull/1232))
- Thêm `VideoSource` `getVideo()` ([#1162](https://github.com/mapbox/mapbox-gl-js/issues/1162))
- Hỗ trợ vector tile có extent khác 4096 ([#1227](https://github.com/mapbox/mapbox-gl-js/pull/1227))
- Sử dụng cấu trúc phân cấp DOM hỗ trợ overlay có sự kiện (evented overlays) ([#1217](https://github.com/mapbox/mapbox-gl-js/issues/1217))
- Truyền `latLng` vào đối tượng sự kiện ([#1068](https://github.com/mapbox/mapbox-gl-js/pull/1068))

#### Sửa lỗi UX

- Sửa lỗi render trên iOS 8 ([#750](https://github.com/mapbox/mapbox-gl-js/issues/750))
- Sửa lỗi tam giác hóa (triangulation) đường line ([#1120](https://github.com/mapbox/mapbox-gl-js/issues/1120), [#992](https://github.com/mapbox/mapbox-gl-js/issues/992))
- Hỗ trợ dải unicode 65280-65535 ([#1108](https://github.com/mapbox/mapbox-gl-js/pull/1108))
- Sửa các vết nứt giữa các fill pattern ([#972](https://github.com/mapbox/mapbox-gl-js/issues/972))
- Sửa góc icon khi căn chỉnh theo line ([@37a498a](https://github.com/mapbox/mapbox-gl-js/commit/37a498a7aa2c37d6b94611b614b4efe134e6dd59))
- Sửa lỗi nét đứt cho tile bị overscale ([#1132](https://github.com/mapbox/mapbox-gl-js/issues/1132))
- Sửa lỗi hình ảnh icon do các sprite lân cận gây ra ([#1195](https://github.com/mapbox/mapbox-gl-js/pull/1195))

#### Sửa lỗi API

- Không phát sự kiện `moveend` giả khi mouseup ([#1107](https://github.com/mapbox/mapbox-gl-js/issues/1107))
- Sửa race condition trong `featuresAt` ([#1220](https://github.com/mapbox/mapbox-gl-js/pull/1220))
- Sửa quy ước đặt tên fontstack dễ vỡ (brittle) ([#1070](https://github.com/mapbox/mapbox-gl-js/pull/1070))
- Sửa `Popup` `setHTML` bị hỏng ([#1272](https://github.com/mapbox/mapbox-gl-js/issues/1272))
- Sửa vấn đề với các yêu cầu ảnh cross-origin ([#1269](https://github.com/mapbox/mapbox-gl-js/pull/1269))

## 0.7.0 (Mar 3 2015)

#### Thay đổi phá vỡ tương thích

- Đổi tên sự kiện `hover` của `Map` thành `mousemove`.
- Thay đổi `featuresAt` để trả về các đối tượng GeoJSON, bao gồm cả geometry ([#1010](https://github.com/mapbox/mapbox-gl-js/issues/1010))
- Gỡ bỏ thuộc tính `canvas` và `container` của `Map`, thay bằng phương thức `getCanvas` và `getContainer`

#### Cải thiện trải nghiệm người dùng (UX)

- Cải thiện mật độ nhãn line
- Thêm tương tác boxzoom ([#1038](https://github.com/mapbox/mapbox-gl-js/issues/1038))
- Thêm tương tác bàn phím ([#1034](https://github.com/mapbox/mapbox-gl-js/pull/1034))
- `GeoJSONSource` `setData` nhanh hơn mà không bị nhấp nháy ([#973](https://github.com/mapbox/mapbox-gl-js/issues/973))

#### Cải tiến API

- Thêm thành phần Popup ([#325](https://github.com/mapbox/mapbox-gl-js/issues/325))
- Thêm layer API ([#1022](https://github.com/mapbox/mapbox-gl-js/issues/1022))
- Thêm filter API ([#985](https://github.com/mapbox/mapbox-gl-js/issues/985))
- Filter API hiệu quả hơn ([#1018](https://github.com/mapbox/mapbox-gl-js/issues/1018))
- Chấp nhận đối tượng JS thuần túy (plain old JS object) cho `addSource` ([#1021](https://github.com/mapbox/mapbox-gl-js/issues/1021))
- Phân tích lại (reparse) các tile bị overscale

#### Sửa lỗi

- Sửa `featuresAt` cho LineStrings ([#1006](https://github.com/mapbox/mapbox-gl-js/issues/1006))
- Sửa tham số `tileSize` truyền cho worker `GeoJSON` ([#987](https://github.com/mapbox/mapbox-gl-js/issues/987))
- Loại bỏ các file thừa khỏi gói npm ([#1024](https://github.com/mapbox/mapbox-gl-js/issues/1024))
- Ẩn liên kết "improve map" khi in ([#988](https://github.com/mapbox/mapbox-gl-js/issues/988))

## 0.6.0 (Feb 9 2015)

#### Sửa lỗi

- Thêm padding wrap vào sprite cho các ảnh lặp lại (repeating images) ([#972](https://github.com/mapbox/mapbox-gl-js/issues/972))
- Xóa color buffer trước khi render ([#966](https://github.com/mapbox/mapbox-gl-js/issues/966))
- Làm cho line-opacity hoạt động với line-image ([#970](https://github.com/mapbox/mapbox-gl-js/issues/970))
- Cách xử lý dự phòng event.toElement cho Firefox ([#932](https://github.com/mapbox/mapbox-gl-js/issues/932))
- Bỏ qua các đỉnh trùng lặp ở đầu mút line ([#776](https://github.com/mapbox/mapbox-gl-js/issues/776))
- Cho phép dùng các ký tự ngoài \w trong token
- Xóa các tile cũ khi GeoJSON mới được tải ([#905](https://github.com/mapbox/mapbox-gl-js/issues/905))

#### Cải tiến

- Đã thêm `map.setPaintProperty()`, `map.getPaintProperty()`, `map.setLayoutProperty()` và `map.getLayoutProperty()`.
- Chuyển sang dùng ESLint và các quy tắc code nghiêm ngặt hơn ([#957](https://github.com/mapbox/mapbox-gl-js/pull/957))
- Lấy raster tile 2x nếu là retina ([#754](https://github.com/mapbox/mapbox-gl-js/issues/754))
- Hỗ trợ URL style dạng mapbox:// ([#875](https://github.com/mapbox/mapbox-gl-js/issues/875))

#### Thay đổi phá vỡ tương thích

- Đã cập nhật lên mapbox-gl-style-spec v7.0.0 ([Changelog](https://github.com/mapbox/mapbox-gl-style-spec/blob/a2b0b561ce16015a1ef400dc870326b1b5255091/CHANGELOG.md)). Style giờ đây
  được kỳ vọng là phiên bản 7. Bạn có thể dùng công cụ [gl-style-migrate](https://github.com/mapbox/mapbox-gl-style-lint#migrations)
  để cập nhật các style hiện có.
- Các tùy chọn cấu hình HTTP_URL và HTTPS_URL không còn được bao gồm tiền tố đường dẫn `/v4` nữa.
- `addClass`, `removeClass`, `setClasses`, `hasClass` và `getClasses` giờ đây là các phương thức
  của Map.
- `Style#cascade` giờ đây là private, chờ một API thay đổi style công khai ([#755](https://github.com/mapbox/mapbox-gl-js/pull/755)).
- Định dạng kết quả `featuresAt` đã thay đổi. Thay vì kết quả-theo-từng-geometry-cắt-qua-layer,
  mỗi kết quả giờ đây có một mảng `layers` chứa tất cả các layer có chứa feature đó. Điều này tránh
  việc trùng lặp geometry và thuộc tính trong tập kết quả.

## 0.5.2 (Jan 07 2015)

#### Sửa lỗi

- Gỡ bỏ các tile của các source không còn được sử dụng ([#863](https://github.com/mapbox/mapbox-gl-js/issues/863))
- Sửa lỗi căn chỉnh fill pattern

#### Cải tiến

- Thêm tùy chọn maxzoom cho GeoJSONSource ([#760](https://github.com/mapbox/mapbox-gl-js/issues/760))
- Trả về các ref layer trong featuresAt ([#847](https://github.com/mapbox/mapbox-gl-js/issues/847))
- Trả về mọi key layer bổ sung được cung cấp trong stylesheet trong featuresAt
- Phân tích protobuf nhanh hơn

## 0.5.1 (Dec 19 2014)

#### Sửa lỗi

- Sửa các race condition khi tải/render style
- Sửa các race condition với setStyle
- Sửa map.remove()
- Sửa các thuộc tính featuresAt

## 0.5.0 (Dec 17 2014)

#### Sửa lỗi

- Sửa lỗi gọi setStyle nhiều lần

#### Cải tiến

- `featuresAt` giờ đây trả về thêm thông tin
- Bộ sự kiện style/source/tile đầy đủ:
  style.load, style.error, style.change,
  source.add, source.remove, source.load, source.error, source.change,
  tile.add, tile.remove, tile.load, tile.error
- Cải thiện đáng kể hiệu năng và độ chính xác cho GeoJSON source
- Map#setStyle giờ đây chấp nhận URL style
- Hỗ trợ {prefix} trong tile URL template
- Cung cấp source map kèm theo bản minified

#### Thay đổi phá vỡ tương thích

- Định dạng kết quả trả về của `featuresAt` đã thay đổi

## 0.4.2 (Nov 14 2014)

#### Sửa lỗi

- Đảm bảo chỉ có một easing hoạt động tại một thời điểm ([#807](https://github.com/mapbox/mapbox-gl-js/issues/807))
- Không yêu cầu style để thực hiện easing ([#817](https://github.com/mapbox/mapbox-gl-js/issues/817))
- Sửa lỗi raster tile đôi khi không hiển thị ([#761](https://github.com/mapbox/mapbox-gl-js/issues/761))

#### Cải tiến

- Hỗ trợ Internet Explorer 11 (thử nghiệm)

## 0.4.1 (Nov 10 2014)

#### Sửa lỗi

- Nội suy đến bearing gần nhất khi thực hiện animation xoay ([#818](https://github.com/mapbox/mapbox-gl-js/issues/818))

## 0.4.0 (Nov 4 2014)

#### Thay đổi phá vỡ tương thích

- Đã cập nhật lên mapbox-gl-style-spec v6.0.0 ([Changelog](https://github.com/mapbox/mapbox-gl-style-spec/blob/v6.0.0/CHANGELOG.md)). Style giờ đây
  được kỳ vọng là phiên bản 6. Bạn có thể dùng công cụ [gl-style-migrate](https://github.com/mapbox/mapbox-gl-style-lint#migrations)
  để cập nhật các style hiện có.

## 0.3.2 (Oct 23 2014)

#### Sửa lỗi

- Sửa lỗi khởi tạo worker khi dùng script deferred hoặc async

#### Cải tiến

- Đã thêm map.remove()
- Các tài nguyên CDN giờ đây được phục vụ với nén gzip

## 0.3.1 (Oct 06 2014)

#### Sửa lỗi

- Sửa lỗi lặp (iteration) qua mảng bằng for/in
- Chuyển các dependency browserify thành non-dev ([#752](https://github.com/mapbox/mapbox-gl-js/issues/752))

## 0.3.0 (Sep 23 2014)

#### Thay đổi phá vỡ tương thích

- Đã cập nhật lên mapbox-gl-style-spec v0.0.5 ([Changelog](https://github.com/mapbox/mapbox-gl-style-spec/blob/v0.0.5/CHANGELOG.md)). Style giờ đây
  được kỳ vọng là phiên bản 5. Bạn có thể dùng công cụ [gl-style-migrate](https://github.com/mapbox/mapbox-gl-style-lint#migrations)
  để cập nhật các style hiện có.
- Gỡ bỏ hỗ trợ composite layer vì lý do hiệu năng. [#523](https://github.com/mapbox/mapbox-gl-js/issues/523#issuecomment-51731405)
- Đơn vị của `raster-hue-rotate` giờ đây là độ (degrees).

### Cải tiến

- Đã thêm LatLng#wrap
- Đã thêm hỗ trợ cho Mapbox fontstack API.
- Đã thêm hỗ trợ cho các TileJSON source từ xa không thuộc Mapbox và TileJSON source nội tuyến ([#535](https://github.com/mapbox/mapbox-gl-js/issues/535), [#698](https://github.com/mapbox/mapbox-gl-js/issues/698)).
- Đã thêm hỗ trợ thuộc tính `symbol-avoid-edges` để cho phép nhãn được đặt xuyên qua ranh giới tile.
- Sửa lỗi mkdir trên Windows ([#674](https://github.com/mapbox/mapbox-gl-js/issues/674)).
- Sửa lỗi vẽ các điểm nối line dạng vát (beveled line joins) không bị chồng lấn.

#### Sửa lỗi

- Sửa hiệu năng khi underzoom minzoom của một layer.
- Sửa `raster-opacity` cho raster layer thông thường.
- Sửa nhiều trường hợp biên (corner case) của các hàm easing.
- Không thay đổi stylesheet gốc ([#728](https://github.com/mapbox/mapbox-gl-js/issues/728)).
- Kế thừa video source từ source ([#699](https://github.com/mapbox/mapbox-gl-js/issues/699)).
- Sửa khả năng tương tác cho geojson layer.
- Dừng dblclick trên navigation để bản đồ không bị pan ([#715](https://github.com/mapbox/mapbox-gl-js/issues/715)).

## 0.2.2 (Aug 12 2014)

#### Thay đổi phá vỡ tương thích

- `map.setBearing()` không còn hỗ trợ tham số thứ hai nữa. Hãy dùng `map.rotateTo` với tùy chọn `offset` và duration 0
  nếu bạn cần xoay quanh một điểm khác với tâm bản đồ.

#### Cải tiến

- Cải thiện `GeoJSONSource` để cũng chấp nhận URL làm tùy chọn `data`, loại bỏ một điểm nghẽn hiệu năng lớn trong trường hợp file GeoJSON lớn.
  [#669](https://github.com/mapbox/mapbox-gl-js/issues/669) [#671](https://github.com/mapbox/mapbox-gl-js/issues/671)
- Chuyển sang một cách tiếp cận khác để render đường viền fill (fill outlines). [#668](https://github.com/mapbox/mapbox-gl-js/issues/668)
- Giảm kích thước bản build minified xuống 12% khi nén gzip (còn 66 KB).
- Thêm tùy chọn `around` cho `Map` `zoomTo`/`rotateTo`.
- Làm cho hash permalink gọn hơn.
- Các điểm nối line dạng vát (bevel linejoins) không còn chồng lấn nữa và trông đẹp hơn nhiều khi vẽ với độ trong suốt.

#### Sửa lỗi

- Sửa lỗi **build minified bị hỏng**. [#679](https://github.com/mapbox/mapbox-gl-js/issues/679)
- Sửa lỗi render **icon bị mờ**. [#666](https://github.com/mapbox/mapbox-gl-js/issues/666)
- Sửa lỗi `util.supports` phát hiện WebGL cho kết quả dương tính giả (false positive) trong một số trường hợp. [#677](https://github.com/mapbox/mapbox-gl-js/issues/677)
- Sửa lỗi cấu hình font không hợp lệ chặn hoàn toàn việc render tile. [#662](https://github.com/mapbox/mapbox-gl-js/issues/662)
- Sửa `Map` `project`/`unproject` để chấp nhận đúng giá trị dạng mảng.
- Sửa race condition khi tải sprite. [#593](https://github.com/mapbox/mapbox-gl-js/issues/593)
- Sửa lỗi `GeoJSONSource` `setData` không cập nhật bản đồ cho đến khi zoom hoặc pan. [#676](https://github.com/mapbox/mapbox-gl-js/issues/676)

## 0.2.1 (Aug 8 2014)

#### Thay đổi phá vỡ tương thích

- Thay đổi cách khai báo control `Navigation`: giờ đây không cần `map` trong constructor
  mà được thêm bằng `map.addControl(nav)` hoặc `nav.addTo(map)`.
- Cập nhật các class CSS để có tiền tố đặt tên nhất quán là `mapboxgl-`.

#### Cải tiến

- Đã thêm attribution control (hiển thị mặc định, có thể tắt bằng cách truyền `attributionControl: false` trong tùy chọn).
- Đã thêm khả năng xoay bằng cách kéo compass control.
- Đã thêm con trỏ dạng nắm tay (grabbing cursor) cho bản đồ theo mặc định.
- Đã thêm các hàm `util.inherit` và `util.debounce`.
- Đã đổi style trang debug mặc định thành OSM Bright.
- Việc thay thế token giờ đây hỗ trợ dấu gạch ngang.
- Cải thiện thiết kế navigation control.

#### Sửa lỗi

- Sửa lỗi compass control không xoay icon của nó cùng bản đồ.
- Sửa con trỏ (cursor) của navigation control.
- Sửa lỗi quán tính (inertia) đi sai hướng trên bản đồ đã xoay.
- Sửa race condition khi quán tính đôi khi ném ra lỗi sau khi pan/zoom thất thường.

## 0.2.0 (Aug 6 2014)

- Phiên bản phát hành công khai đầu tiên.
