# bem

## 基本

### 要素型セレクターや ID セレクターは使わない

```css
/* NG */
a.button {
}

/* OK */
.button {
}
```

### 詳細度は均一

```css
/* NG */
.button.button_theme_caution {
}

/* OK */
.button_theme_caution {
}
```

## Block

特定のコンテキストに依存していない、どこでも使いわませるパーツ

### クラス名は見た目ではなく機能・役割に基づく

```css
/* NG */
.red-button {
}

/* OK */
.error-button {
}
```

## Element

Block を構成し、Block の外では使用できない。

- クラス名から影響範囲が想像できること
- クラス名から見た目・機能・役割が想像できる
- Element の中に Element をネストしない

```html
<ul class="menu">
  <!--×a要素がmenu__linkではなく、menu__item__linkとlinkがitemの中にネストされたクラス名になっている -->
  <li class="menu__item">
    <a class="menu__item__link" href="tab1/">Tab1</a>
  </li>
  <!-- ○a要素が親のElement名を含まず、menu__linkとなっている-->
  <li class="menu__item">
    <a class="menu__link" href="tab1/">Tab1</a>
  </li>
  ...
</ul>
```
