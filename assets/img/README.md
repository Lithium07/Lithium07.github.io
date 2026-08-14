# 头像图片

把你的照片命名为 **`profile.jpg`** 放在这个目录下，即 `assets/img/profile.jpg`。

- 建议正方形，短边 ≥ 400px（例如 600×600），页面会自动裁成圆形。
- 也可以用 png，但要同时把 `assets/css/site.css` 里 `.avatar::after` 的
  `url("../img/profile.jpg")` 改成 `profile.png`。
- 如果没有放图片，页面会自动回退成蓝色渐变 + 首字母 “JL”，不会显示裂图。
