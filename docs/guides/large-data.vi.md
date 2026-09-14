# Tối ưu hiệu năng MapLibre: Mẹo xử lý tập dữ liệu GeoJSON lớn

Hiệu năng là một khía cạnh quan trọng để mang lại trải nghiệm mượt mà, phản hồi nhanh cho người dùng. Hướng dẫn này tập trung vào các kỹ thuật cải thiện hiệu năng của MapLibre, đặc biệt khi làm việc với các tập dữ liệu lớn ở định dạng GeoJSON. Chúng ta sẽ phân loại các chiến lược thành hai nhóm chính:

1. Tải dữ liệu
1. Hiển thị dữ liệu

## Tải dữ liệu

### Giảm kích thước file

Khi làm việc với các tập dữ liệu GeoJSON lớn, một trong những cách hiệu quả nhất để cải thiện hiệu năng tải là giảm kích thước dữ liệu. Bạn có thể áp dụng các cách sau bằng các package như [Turf](https://turfjs.org/) hoặc các công cụ web như [Reduce GeoJSON](https://reducegeojson.radicaldata.org/) và [Mapshaper](https://github.com/mbloch/mapshaper).

#### Loại bỏ các property không dùng đến

Các file GeoJSON thường chứa rất nhiều property không thực sự cần thiết cho chức năng của bản đồ. Bằng cách loại bỏ các property không dùng đến hoặc dư thừa, bạn có thể giảm đáng kể kích thước file, giúp thời gian tải nhanh hơn.

#### Giảm độ chính xác của tọa độ

Tọa độ trong GeoJSON thường mặc định có độ chính xác cực cao, thường lên tới 15-17 chữ số thập phân — mức chính xác ở quy mô nguyên tử. Với hầu hết ứng dụng thực tế, bạn có thể giảm độ chính xác tọa độ xuống khoảng 6 chữ số thập phân, tương đương với [độ chính xác khoảng 1cm](https://en.wikipedia.org/wiki/Decimal_degrees#Precision). Điều này giúp giảm kích thước file mà không ảnh hưởng đến tính khả dụng.

#### Đơn giản hóa geometry

Nếu GeoJSON của bạn chứa các geometry (không chỉ là điểm), hãy cân nhắc sử dụng các thuật toán khác nhau để đơn giản hóa geometry. Các công cụ như [Mapshaper](https://github.com/mbloch/mapshaper) cung cấp giao diện thân thiện cho việc này.

#### Rút gọn (Minify)

Rút gọn (minify) dữ liệu GeoJSON bằng cách loại bỏ khoảng trắng không cần thiết có thể giảm thêm kích thước file, giúp truyền dữ liệu nhanh hơn.

#### Nén dữ liệu

Một cách khác là nén dữ liệu GeoJSON và gửi file đã nén đến trình duyệt của người dùng. Cách này tạo ra một đánh đổi nhỏ giữa việc xử lý và kích thước file, nhưng nhìn chung vẫn chấp nhận được, nhờ hiệu suất của JavaScript hiện đại.

### Chia nhỏ dữ liệu (Data Chunking)

Nếu tập dữ liệu GeoJSON của bạn vẫn còn khá lớn sau khi đã giảm kích thước, hãy cân nhắc chia nhỏ nó thành các phần (chunk) nhỏ hơn, dễ quản lý hơn. Ngay cả việc chia thành 2 hoặc 3 phần cũng có thể mang lại lợi ích. Các tập dữ liệu đã chia này có thể được thêm vào bản đồ như bình thường bằng `addSource()` và `addLayer()`.

Kỹ thuật này đặc biệt hữu ích khi các phần khác nhau của tập dữ liệu có đặc tính khác nhau. Ví dụ, nếu bản đồ khởi đầu với zoom vào một khu vực địa lý cụ thể, dữ liệu trong khu vực đó có thể là một chunk, còn phần còn lại là một chunk khác. Tương tự, nếu một phần dữ liệu được cập nhật liên tục (live) còn phần còn lại phần lớn là tĩnh, việc tách hai phần này thành các chunk riêng biệt có thể hợp lý.

Việc chia nhỏ dữ liệu mang lại hiệu quả rõ rệt hơn trên trình duyệt desktop so với trình duyệt di động.

### Streaming dữ liệu

Áp dụng các kỹ thuật streaming dữ liệu có thể cải thiện thêm hiệu năng tải. Thay vì tải toàn bộ tập dữ liệu cùng lúc, streaming dữ liệu cho phép bạn tải từng phần nhỏ khi người dùng tương tác với bản đồ. Cách tiếp cận này giúp giảm thiểu thời gian tải ban đầu và mang lại trải nghiệm phản hồi nhanh hơn. Bạn có thể tham khảo mẫu streaming dữ liệu trong ví dụ [Update a feature in realtime](../examples/update-a-feature-in-realtime.md).

### Lưu trữ GeoJSON tại một URL

Để cải thiện hiệu năng trong MapLibre, bạn nên tải dữ liệu GeoJSON từ một URL dữ liệu thay vì nhúng trực tiếp vào code JavaScript. Cách làm này giúp giảm chi phí bộ nhớ ở phía client.

### Chuyển sang Vector Tile

Hãy cân nhắc chuyển đổi dữ liệu GeoJSON của bạn thành vector tile, vốn được thiết kế chuyên biệt để render hiệu quả. Có sẵn một ví dụ hướng dẫn cách [thêm một vector tile source](../examples/add-a-vector-tile-source.md).

### Tiling ở phía server

Với các tập dữ liệu thậm chí còn lớn hơn, bạn có thể dùng công cụ như [Martin](https://maplibre.org/martin/) để chuyển một database thành tile ngay ở phía server. Các tile này sau đó có thể được hiển thị trực tiếp cho người dùng. [Bản demo của Martin](https://martin.maplibre.org/) cho thấy nó xử lý thoải mái một database dung lượng 13GB. Tuy nhiên, cách tiếp cận này đòi hỏi nhiều công sức thiết lập hơn các cách khác.

## Hiển thị dữ liệu

Sau khi dữ liệu đã được tải, để đảm bảo trải nghiệm người dùng mượt mà, điều quan trọng là phải tối ưu cách bạn hiển thị dữ liệu trên bản đồ.

### Gộp nhóm (Cluster)

Một cách đơn giản là hiển thị ít điểm hơn. Nếu bạn đang dùng GeoJSON source (tức là không phải vector tile), bạn có thể dùng 'clustering' (gộp nhóm) để nhóm các điểm gần nhau lại. Cách tiếp cận này giúp giảm số lượng feature được hiển thị trên bản đồ, cải thiện hiệu năng render và vẫn giữ được khả năng đọc hiểu bản đồ.

Để làm điều này, khi thêm dữ liệu, bạn có thể điều chỉnh các [tùy chọn cluster](../API/type-aliases/SetClusterOptions.md). Ví dụ:

```javascript
map.addSource('earthquakes', {
            type: 'geojson',
            data: 'https://maplibre.org/maplibre-gl-js/docs/assets/earthquakes.geojson',
            cluster: true,
            clusterMaxZoom: 14, // Max zoom to cluster points on
            clusterRadius: 50 // Radius of each cluster when clustering points (defaults to 50)
        });
```

Bạn có thể xem ví dụ đầy đủ tại đây: [Create and style clusters](../examples/create-and-style-clusters.md).

### Cho phép chồng lấn (Allow Overlap)

Theo mặc định, MapLibre sẽ tính toán xem các feature như điểm, chữ, hoặc icon có bị chồng lấn lên nhau hay không. Việc này có thể tốn nhiều tài nguyên tính toán, đặc biệt khi có nhiều feature. Thay đổi [overlap mode](https://maplibre.org/maplibre-style-spec/layers/#layout-symbol-icon-allow-overlap) để tất cả các điểm đều được hiển thị và không kiểm tra chồng lấn nữa có thể giảm đáng kể chi phí này.

### Đơn giản hóa style

Các style bản đồ phức tạp, chi tiết có thể làm chậm quá trình render, đặc biệt khi làm việc với tập dữ liệu lớn. Hãy đơn giản hóa style bản đồ của bạn bằng cách giảm số lượng layer, symbol và các feature phức tạp, đồng thời dùng ký hiệu (symbology) đơn giản hơn khi phù hợp.

### Mức Zoom (Zoom Levels)

Việc tối ưu các mức zoom giúp đảm bảo bản đồ tải hiệu quả và hiển thị đúng mức độ chi tiết ở từng mức zoom khác nhau, góp phần mang lại trải nghiệm người dùng mượt mà hơn.

#### Mức Zoom tối đa (Max Zoom Level)

Để cải thiện hiệu năng bản đồ khi pan và zoom, hãy đặt tùy chọn maxZoom trên GeoJSON source của bạn về một giá trị thấp hơn mặc định (22). Với hầu hết các source dạng điểm, giá trị maxZoom là 12 mang lại sự cân bằng tốt giữa độ chính xác và tốc độ.

#### Mức Zoom tối thiểu (Min Zoom Level)

Điều chỉnh property minZoom trên layer tham chiếu đến GeoJSON source về một giá trị lớn hơn 0. Thiết lập này ngăn bản đồ cố gắng tải và render tile ở các mức zoom thấp, vốn thường không cần thiết vì không đủ pixel trên màn hình để hiển thị hết mọi feature của một tập dữ liệu lớn. Bằng cách điều chỉnh property minZoom, bạn sẽ đạt được tốc độ tải bản đồ nhanh hơn và hiệu năng render được cải thiện.

Bạn có thể áp dụng cả hai như sau:

```javascript
let map = new maplibregl.Map({
  container: 'map',
  maxZoom: 12,
  minZoom: 5
});
```
</content>
