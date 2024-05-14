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

<br/><br/>

## Modifier

Modifier は 、Block もしくは Element の見た目や状態、振る舞いを定義するもの

要点

- Modifier は単独で存在できない。必ず Block か Element が有る状態で２つ目以降のクラスとして使用する

```html
<!-- NG Modifierを単独で使用している-->
<a class="button_size_s" href="#">ボタン</a>

<!-- OK ○ふたつ目のクラス名としてModifierを付けている-->
<a class="button button_size_s" href="#">ボタン</a>
```

### キーと値

キーと値は`_`でつなぐ

```css
/* textがキー、largeやsmallが値 */
.menu__item_text_large {
}
.menu__item_text_small {
}
```

### 命名は「それがどうであるか」

- 見た目
  - size_s
  - theme_caution
- 状態
  - active
  - disabled
  - focused
- 振る舞い
  - directions_right-to-left
  - position_bottom-right

### Modifier 名は省略しない

命名が長くなりやすいが、style の衝突回避、詳細度の担保、検索しやすさを考慮して省略しない

user-login-button という Block に size_s という Modifier を付ける場合

```html
<a class="user-login-button user-login-button_size_s" href="#">ボタン</a>
```

```html
<!-- NG -->
<a class="user-login-button size_s" href="#">ボタン</a>
<img class="hero-image_size_s" src="dummy.png" />

<style>
  /* NG styleの衝突*/
  .size_s {
    padding: 5px;
  }
  .size_s {
    width: 200px;
  }

  /* NG 詳細度が上がる */
  .user-login-button.size_s {
  }
  .hero-image.size_s {
  }
</style>
```

## Mix

Mix は単一の DOM ノードに、異なる BEM エンティティが複数付与されたもの

```html
<header class="head">
  <div class="menu head__menu">...</div>
  <div class="logo head__logo">...</div>
  <form class="search head__search">...</form>
  <form class="auth head__auth">...</form>
</header>

<main>
  <div class="logo main__logo">...</div>
</main>
```

```css
.logo {
  width: 100px;
}

.head__logo {
  margin-top: 5px;
}
```

`.head__logo`は`.head`Block に依存する`.logo`Element である。
分割することで`.logo`Block の独立性が保たれる。
`.logo`Block を`.company-logo`に改名しても`.head__logo`には影響が出ない。

## レイアウト

Block にはそれ自身のレイアウトを持たせない。
Element にレイアウトを持たせる。

レイアウトとは`position`, `padding`, `margin`等の配置を制御するような style を指す。

なぜなら、Block 自体がレイアウトをもってしまうと`特定のコンテキストに依存していない、どこでも使いわませるパーツ`を満たせないため。

```html
<header class="head">
  <div class="menu head__menu">...</div>
  <div class="logo head__logo">...</div>
  <form class="search head__search">...</form>
  <form class="auth head__auth">...</form>
</header>

<main>
  <div class="logo main__logo">...</div>
</main>

<style>
  /* NG header,main上で同じレイアウトとは限らない */
  .logo {
    margin-top: 5px;
  }

  /* OK どこに配置するとしても必要なstyleのみ */
  .logo {
    width: 100px;
  }

  .head__logo {
    margin-top: 5px;
  }
  .main__logo {
    margin-top: 5px;
    margin-left: 5px;
  }
</style>
```
