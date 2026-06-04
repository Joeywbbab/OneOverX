# OneOverX / X分之一 — Hugo + PaperMod

中英双语周刊,Hugo + PaperMod 主题,蓝色主色。`y = 1/x` — 保持非零。

> 说明:这个项目我在沙箱里**没法跑 `hugo` 验证**(下载 Hugo 二进制被网络限制拦了)。
> 配置、主题、CSS、文章我都按 PaperMod 官方约定写好并对照主题模板静态核对过,
> 但请你本地跑一次 `hugo server` 确认,有问题对照下面的排错清单。

---

## 0. 装 Hugo

PaperMod 用纯 CSS(不需要 Sass),所以标准版/扩展版都行。建议直接装**扩展版**省心。

- **macOS**: `brew install hugo`
- **Windows**: `winget install Hugo.Hugo.Extended` 或 `scoop install hugo-extended`
- **验证**: `hugo version`(需 ≥ 0.146,本项目主题要求)

## 1. 本地运行

主题已经打包在 `themes/PaperMod/` 里,clone 下来直接能跑:

```bash
hugo server -D        # 本地预览 http://localhost:1313 (-D 显示草稿)
```

中文首页 http://localhost:1313/zh/ ,英文 http://localhost:1313/en/ 。

构建生产版本:

```bash
hugo --minify         # 输出到 public/
```

## 2. 写文章

放 Markdown 到对应语言目录(文件名即网址 slug):

- 中文:`content/zh/posts/`
- 英文:`content/en/posts/`

front matter:

```yaml
---
title: "标题"
date: 2026-06-15
tags: ["X"]            # 栏目就是 tag:  beta / X / 1·x
summary: "一句话摘要"
draft: false           # true 则不发布
---
正文用 Markdown...
```

**三个栏目 = 三个 tag**:`beta`、`X`、`1·x`。点击 tag 或菜单「栏目」可按栏目浏览。
中英文用相同文件名,右上角 EN/中文 切换。

## 3. 部署到 GitHub Pages

主题已经直接放在 `themes/` 里(不是 git submodule),所以部署很简单:

1. 新建 GitHub 仓库,把整个文件夹 push 到 `main`。
2. 仓库 Settings → Pages → Build and deployment → Source 选 **GitHub Actions**。
3. push 后 `.github/workflows/deploy.yml` 自动构建发布。

> workflow 里 Hugo 版本固定为 `0.162.1`。若将来主题升级要更新,改 `.github/workflows/deploy.yml` 里的 `HUGO_VERSION`。
> 注意:workflow 里有 `submodules: recursive`,因为主题是直接放进来的而非 submodule,这行无害(没有 submodule 就跳过)。

## 4. 绑定子域名 oneoverx.joeyconnects.world

1. 域名 DNS 后台加 CNAME:Name=`oneoverx`,Value=`你的用户名.github.io`。
2. 仓库 Settings → Pages → Custom domain 填 `oneoverx.joeyconnects.world` → 勾 Enforce HTTPS。
3. Cloudflare 用户:CNAME 先设 DNS only,证书签好再开代理。
4. 把 `hugo.yaml` 顶部的 `baseURL` 改成 `https://oneoverx.joeyconnects.world/`(已预填,确认即可)。

## 5. 改外观

- **蓝色主色 / 配色**:`assets/css/extended/blue.css`(改 `--blue` 等变量)。
- **栏目 tag 样式**:`assets/css/extended/tags.css`。
- **笑脸 logo**:`hugo.yaml` 里 `params.label.iconSVG`,以及 `static/favicon.svg`。
- **首页大标题/副文案**:`hugo.yaml` 里每个语言的 `params.homeInfoParams`。

> PaperMod 会自动加载 `assets/css/extended/` 下的所有 css,这是官方推荐的不改主题源码的定制方式。

---

## 排错清单(本地跑不起来时对照)

- **报 "found no layout file"**:确认 `themes/PaperMod/` 不是空的(里面应有 `layouts/`)。
- **报 Hugo 版本太低**:升级到 ≥ 0.146(`hugo version` 查看)。
- **首页没有副标题文案**:`homeInfoParams` 必须在**每个语言**的 `params:` 下(本项目已这么配)。
- **tag 颜色没区分**:`1·x` 的 URL 会被 Hugo 转成 `1-x`,`X` 转成 `x`,`tags.css` 的选择器已按此匹配。若你改了栏目名,记得同步改 `tags.css` 里的 `[href$="/tags/xxx/"]`。
- **logo 不显示**:确认 `iconSVG` 的值以 `<svg` 开头(PaperMod 据此判断渲染 SVG)。
