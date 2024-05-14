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

<br/><br/>

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

<br/><br/>

## Element

Element は、Block を構成し、Block の外では使用できない。

要点

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

```css
/* NG Elementの詳細度が高い */
.menu {
}
.menu.menu__item {
}
.menu.menu__item.menu__link {
}

/* OK Elementも含めて詳細度が均一*/
.menu {
}
.menu__item {
}
.menu__link {
}
```

### Element はなくても良い

それぞれ独立した Block

```html
<!--サーチフォームBlock-->
<div class="search-form">
  <!-- インプットBlock -->
  <input class="input" />
  <!-- ボタンBlock -->
  <button class="button">Search</button>
</div>
```

### Element が多くなったとき

Element を Block に昇格させる

```html
<ul class="menu">
  <li class="menu__item">
    <a class="menu__link" href="tab1/">Tab1</a
    ><a class="menu__btn" href="lp/"><span class="menu__icon"></span>ToLP</a>
  </li>
</ul>
```

↓

```html
<ul class="menu">
  <li class="menu__item">
    <a class="menu__link" href="tab1/">Tab1</a>
    <!--.btnBlockを新たに作成した-->
    <a class="btn" href="lp/"><span class="btn__icon"></span>ボタン</a>
  </li>
</ul>
```
