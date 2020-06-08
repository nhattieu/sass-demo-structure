**VI**
# Cấu trúc trong SASS


## Gồm:


> **Base:**  Chứa các element cơ bản của HTML như các thẻ `body`, `h1`, `h2`, ...

> **Layouts:** Chứa cá phần bố cục có trong page như `header`, `footer`, `sections`.

> **Modules:** Là các `components` như các thẻ có thuộc tính được người dùng thêm vào được gán `class` hoặc `id`.

---

## Thêm ký tự `_` trước tên file trong SASS

Mục đích của việc này là để khi dùng lệnh `sass --watch sass:css` để nó ko tạo ra thư mục tương tự có trong SASS ở trong CSS.

```
css
    > app.css
    > app.css.map
sass
    > base
        _base-dir.sass
        _base.sass
    > layouts
        _footer.sass
        _header.sass
        _layouts-dir.sass
        _sections.sass
    > modules
        _alerts.sass
        _button.sass
        _modules-dir.sass
        _navbar.sass
        _pro-img.sass
    app.sass
index.html
```

---

Trong mỗi thư mục `base`, `layouts`, `modules` đều có file `*-dir.sass`. Mục đích là để file này import tới các file còn lại trong thư mục, từ đó file `app.sass` chỉ cần `@import` file `*-dir.sass`. Điều này giúp dễ quản lý hơn, nhanh hơn.

> `base-dir.sass` :

```
@import "base"
```

> `app.sass`:

```
@import "base/base"
```

Khi `@import` thì không cần thêm đuôi file như ở đầy là `base.sass`


---

## Các tính năng được hỗ trợ

Dùng các tính năng được hỗ trợ có sẵn trong SASS như `variables`, `mixins`, `extend`.
> **Variables**: Lưu trữ giá trị vào 1 biến để khi nào cần thì lấy ra sài hoy, khai báo bằng cách `$ + tên biến: giá trị` và dùng bằng cách gọi lại tên biến.

```
$brand-red: #dc3545

body
    background-color: $brand-red
```

> **Mixins**: Gom các thuộc tính thành 1 phương thức, khai báo bằng cách `= + tên phương thức(thuộc tính 1, thuộc tính 2, ...)` khi dùng thì sử dụng lệnh `+ + tên phương thức`

```

=btn($bg, $color, $padding)
    background-color: $bg
    color: $color

.btn-pro
    +btn(white, black, 10px 15px)

```

> **Extend**: Như tên gọi là nó được dùng để  kế thừa thuộc tính của 1 element, dùng bằng lệnh `@extend + element`.

```

.primay
    border: 1px solid black
    margin: 10px 0
    padding: 15px

.red
    @extend .alert
    background-color: red

.gray-dark
    @extend .alert
    background-color: gray


```

Ta sẽ tạo 3 file để chứa 3 loại này, và để `app.sass` import chúng và sử dụng cho toàn bộ file sass.

```
css
sass

        ***

    _extends.sass
    _mixins.sass
    _variables.sass
    app.sass
index.html
```

> ***Lưu ý***: `@import` các file `variables`, `mixins`, `extends` trước cái file khác ở trong `app.sass`.

```
@import "variables"
@import "mixins"
@import "extends"
@import "base/base-dir"
@import "layouts/layouts-dir"
@import "modules/modules-dir"
```


---

![neko](https://cdn.nekos.life/neko/neko122.jpeg)