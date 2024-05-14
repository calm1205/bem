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
