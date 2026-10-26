# 工具棚 · Shed

个人项目的汇总站：所有项目的隐私政策放在一起，以后小演示也往这儿放。
纯静态 HTML，没有构建步骤，直接由 GitHub Pages 托管。

## 目录结构

```
site/
  index.html                  # 首页：项目列表
  style.css                   # 全站样式（含暗色模式）
  404.html                    # 自定义 404
  .nojekyll                   # 关掉 Jekyll，否则 _template 目录会被忽略
  assets/icon128.png
  privacy/
    index.html                # 隐私政策列表
    block-reader/index.html   # 块朗读的隐私政策
    _template/index.html      # 新项目模板，复制改名即可
```

## 本地预览

在仓库根目录执行：

```bash
node tools/serve.mjs 8124 site
# 打开 http://127.0.0.1:8124
```

## 发布到 GitHub Pages（一次性）

**① 建仓库**

GitHub → New repository → 名字填 `shed`（或你选的名字）→ **Public** → 不要勾选任何初始化文件 → Create。

**② 把这个目录推上去**

在 `site/` 目录里执行（把 `<用户名>` 换成你的 GitHub 用户名）：

```bash
cd site
git init
git add .
git commit -m "init: 工具棚"
git branch -M main
git remote add origin https://github.com/<用户名>/shed.git
git push -u origin main
```

**③ 开启 Pages**

仓库 → Settings → Pages →
Source 选 **Deploy from a branch**，Branch 选 **main**，目录选 **/ (root)** → Save。

等 1–2 分钟，访问：

```
https://<用户名>.github.io/shed/
```

**④ 隐私政策地址**

```
https://<用户名>.github.io/shed/privacy/block-reader/
```

把它填进 Chrome Web Store 后台的「隐私政策」字段。

> 注意结尾的斜杠别丢。GitHub Pages 会用目录下的 `index.html` 响应。

## 加一个新项目

1. 复制 `privacy/_template/` 整个文件夹，重命名为项目名（英文小写、连字符，如 `focus-timer`）
2. 把 `[方括号]` 占位符替换成实际内容
3. 在 `privacy/index.html` 的表格里加一行，在根目录 `index.html` 加一张卡片
4. 提交推送，Pages 会自动更新

如果新项目有自己的图标，放到 `assets/` 下引用即可。

## 可选：自定义域名

有域名的话，Settings → Pages → Custom domain 填进去，然后在域名商加一条 CNAME 记录。
好处是隐私政策地址更稳定，将来换托管也不用改。

## 为什么不放在扩展仓库里

扩展仓库要打包上传商店，只应包含 `manifest.json` 和运行时代码。
隐私政策和演示页放在独立仓库，更新它们不用重新提交扩展审核。
