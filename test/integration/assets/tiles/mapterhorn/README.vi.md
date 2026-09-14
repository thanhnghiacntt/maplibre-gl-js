# Fixture độ cao Mapterhorn

Các file PNG mã hóa theo chuẩn Terrarium này chứa các mẫu độ cao (elevation) không chỉnh sửa từ
[Mapterhorn](https://mapterhorn.com/), được tải xuống ngày 2026-09-05. Các tile nguồn
là `https://tiles.mapterhorn.com/10/{x}/{y}.webp`, với `x` thuộc `531, 532` và `y`
thuộc `361, 362`. Xem [thông tin ghi công của Mapterhorn](https://mapterhorn.com/attribution/)
để biết các nguồn dữ liệu của họ, bao gồm cả [swissALTI3D](https://www.swisstopo.admin.ch/en/height-model-swissalti3d)
của Federal Office of Topography swisstopo.

Mỗi fixture là góc 64 × 64 pixel gần nhất với điểm giao nhau chung của bốn tile
tại kinh độ 7.03125, vĩ độ 46.55886030311718. Phần crop bắt đầu tại pixel 448 trên
mỗi trục đối với tile phía tây hoặc phía bắc, và tại pixel 0 đối với các trường hợp còn lại. Việc crop
các tile nguồn 512 × 512 mà không resample sẽ cho ra các tile 64 × 64 ở mức zoom 13 với
cùng khoảng cách mẫu địa lý (geographic sample spacing). Tọa độ tile của chúng là `4255, 4256` theo
trục x và `2895, 2896` theo trục y. Render test sẽ overzoom điểm giao nhau này để làm lộ ra
các đường nối (seam) nội suy dọc theo cả hai trục.
