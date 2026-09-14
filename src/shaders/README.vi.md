# Shader của MapLibre GL JS

Repository này chứa các shader GLSL

## Pragmas

Một số biến thay đổi kiểu tùy theo ngữ cảnh của chúng:

 - nếu biến giống nhau cho mọi feature, ta khai báo nó là một `uniform`
 - nếu biến khác nhau cho mỗi feature, ta khai báo nó là một `attribute` (trong vertex shader) và một `varying` đi kèm (trong cả vertex lẫn fragment shader).
 - nếu biến khác nhau cho mỗi feature và là một hàm của zoom, ta khai báo nhiều `attribute` và `uniform` rồi tính giá trị bằng phép nội suy (interpolation)

Chúng ta trừu tượng hóa chức năng này bằng các pragma.

```glsl
#pragma maplibre: define highp vec4 color

main() {
    #pragma maplibre: initialize highp vec4 color
    ...
    fragColor = color;
}
```

Chương trình này khai báo một biến bên trong `main` tên là `color`, khởi tạo giá trị của `color`, sau đó gán `fragColor` bằng giá trị của `color`.

Pragma có dạng như sau.

```glsl
#pragma maplibre: (define|initialize) (lowp|mediump|highp) (float|vec2|vec3|vec4) {name}
```

Khi sử dụng pragma, các yêu cầu sau được áp dụng.

 - tất cả các biến được khai báo bằng pragma phải có cả pragma `define` và `initialize`
 - pragma `define` phải nằm ở phạm vi file (file scope)
 - pragma `initialize` phải nằm ở phạm vi hàm (function scope)
 - tất cả các biến được khai báo bằng pragma và được khởi tạo trong fragment shader cũng phải được khai báo và khởi tạo trong vertex shader, vì `attribute` không thể truy cập được từ fragment shader

## Prelude

Các file `_prelude.fragment.glsl` và `_prelude.vertex.glsl` được trình biên dịch tự động include vào tất cả các shader.
