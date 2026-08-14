# 个人学术主页

Jiahao Li 的学术主页，基于 **Jekyll** 构建，托管在 **GitHub Pages** 上。
GitHub 会自动构建，**不需要**本地装任何东西，也不需要配置 CI —— push 上去就生效。

---

## 一、部署到 GitHub Pages

本站已配置为部署到 **https://lithium07.github.io**（仓库 `Lithium07/Lithium07.github.io`）。

首次推送：

```bash
cd /home/jiahali/Projects/person_page
git init -b main
git add .
git commit -m "Academic homepage"
git remote add origin https://github.com/Lithium07/Lithium07.github.io.git
git push -u origin main
```

然后打开仓库的 **Settings → Pages**，把 *Source* 设为 **Deploy from a branch**，
分支选 `main`、目录选 `/ (root)`，保存。等 1–2 分钟即可访问。

以后更新只要：

```bash
git add -A && git commit -m "update publications" && git push
```

> 若将来换成「项目页」（仓库名不是 `<用户名>.github.io`），必须把 `_config.yml` 里的
> `baseurl` 改成 `"/仓库名"`，否则 CSS 会 404、页面变成裸 HTML。

---

## 二、日常维护：改哪个文件？

| 想改什么 | 改哪个文件 |
| --- | --- |
| **加/改论文** | **`_includes/publications.md`** ← 主要就是这个 |
| 个人简介、研究方向、教育经历、联系方式 | `index.md` |
| 姓名、邮箱、站点地址等全局信息 | `_config.yml` |
| 配色、字体、间距 | `assets/css/site.css`（顶部的 CSS 变量） |
| 头像 | 放一张 `assets/img/profile.jpg` |

### 加一篇新论文

打开 `_includes/publications.md`，按时间倒序在最上面粘 3 行（**行末不用加空格**，换行会自动断行）：

```markdown
**Your Paper Title Here**
Author A, **Jiahao Li**, Author C
*CVPR 2026*
```

渲染规则：

- 第一处 `**加粗**` → 论文标题（大号深色）
- 后面的 `**加粗**` → 你自己的名字（高亮成主题色）
- `*斜体*` → venue，渲染成蓝色小徽章（年份就写在里面）
- **每条论文之间必须留一个空行**

论文是**不分年份的平铺列表**，顺序完全由文件里的先后决定，自己想怎么排就怎么排。
（如果哪天想恢复年份分组，插一行 `### 2026` 就能用，样式还在。）

想加链接就接在 venue 后面：

```markdown
*CVPR 2026* · [Paper](https://arxiv.org/abs/2601.00000) · [Code](https://github.com/xxx/yyy) · [Project](https://xxx.github.io)
```

### 加 Experience / Awards / Academic Service / News

在 `index.md` 里照抄 Education 那一段的结构即可：

```markdown
## Awards {#awards}

<ul class="timeline">
  <li>
    <div class="deg">Best Paper Award</div>
    <div class="where">Some Conference</div>
    <div class="when">2026</div>
  </li>
</ul>
```

章节顺序就是 `index.md` 里的书写顺序，直接上下挪动整段即可。

News 版块的样式（`.news` / `.tag`）也还在 `site.css` 里，想恢复的话在 `index.md` 写：

```html
## News {#news}

<ul class="news">
  <li><span class="tag">Feb 2026</span><span>消息内容，可以带 <a href="...">链接</a>。</span></li>
</ul>
```

### 换头像

把照片存成 `assets/img/profile.jpg`（建议正方形，短边 ≥ 400px）。
没放图片时会自动显示蓝色渐变 + 首字母 “JL”，不会出现裂图。

### 换配色

改 `assets/css/site.css` 最上面的 `--accent` 系列变量即可（浅色 / 深色两套要分别改）。
页面自动跟随系统深色模式，右上角也可以手动切换，选择会记在 localStorage 里。

---

## 三、本地预览

已经在本机验证可用（装的就是 GitHub Pages 官方的 `github-pages` gem，
jekyll 3.10.0，构建结果与线上一致）：

```bash
# 1. 一次性装编译依赖
sudo apt install -y ruby-dev build-essential zlib1g-dev

# 2. 一次性装 bundler，并把依赖装到项目内的 vendor/bundle
gem install --user-install bundler
export PATH="$HOME/.local/share/gem/ruby/3.2.0/bin:$PATH"   # 建议写进 ~/.bashrc
bundle config set --local path vendor/bundle
bundle install

# 3. 以后每次预览只要这一行
bundle exec jekyll serve --livereload
```

然后打开 <http://127.0.0.1:4000/>。

`--livereload` 会监听文件改动：改完 `_includes/publications.md` 存盘，浏览器自动刷新，不用重启。
只有改 `_config.yml` 需要 Ctrl-C 重启服务。

不想装 Ruby 的话也可以用 Docker：

```bash
docker run --rm -p 4000:4000 -v "$PWD":/srv/jekyll -it jekyll/jekyll jekyll serve
```

---

## 四、目录结构

```
.
├── _config.yml              # 站点配置（姓名 / 邮箱 / url / baseurl）
├── index.md                 # 首页内容：About / Interests / Education / Contact
├── _includes/
│   └── publications.md      # ★ 论文列表，日常主要编辑这个
├── _layouts/
│   └── default.html         # HTML 骨架、深色模式开关、SEO meta
├── assets/
│   ├── css/site.css         # 全部样式
│   └── img/                 # 放 profile.jpg
├── Gemfile                  # 仅本地预览用
└── .gitignore
```

## 说明

- 首页把 `_includes/publications.md` 通过 `{% raw %}{% include %}{% endraw %}` + `markdownify` 内联进来，
  所以论文列表**始终只有一份**，不会出现两处需要同步的问题。
- `_config.yml` 里的 `kramdown.hard_wrap: true` 是让论文那种「三行一条」的写法生效的关键，
  不要关掉。
- 页面不依赖任何第三方 JS/CSS/字体 CDN，纯静态、加载快、离线也能看。

### ⚠️ 三个 GitHub Pages 默认行为的坑（都已在 `_config.yml` 里处理好，别删）

1. **`theme:` 必须留空。** 不指定主题时 GitHub Pages 会自动套用 `jekyll-theme-primer`，
   而它自带的 `assets/css/style.scss` 会编译成 `assets/css/style.css`。如果本站的样式表
   也叫这个名字，就会被它覆盖，页面变成完全没有样式的裸 HTML。
   本站样式表因此改名为 **`assets/css/site.css`**，双重保险。
2. **论文列表必须放在 `_includes/` 里，不能放在仓库根目录。** 默认启用的
   `jekyll-optional-front-matter` 插件会把根目录下没有 front matter 的 md 也当成页面，
   多生成一个没有样式的 `/publications.html`。
   把它写进 `exclude` 虽然能挡住，但 Jekyll 的 watcher 同样会跳过 `exclude` 里的路径 ——
   结果就是**改论文文件不会触发重新构建，livereload 失效**。
   放进 `_includes/` 两个问题一起解决：这里的文件永远不会变成独立页面，但会被监听。
3. **`assets/img/README.md` 同理排除。** 默认启用的 `jekyll-readme-index` 插件会把任意目录下的
   `README.md` 变成该目录的 `index.html`。

正确构建后 `_site/` 里应该**只有** `index.html` 和 `assets/css/site.css` 两个文件
（放了头像的话再加一个 `assets/img/profile.jpg`）。
