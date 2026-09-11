# 发布到 GitHub Pages — 操作步骤

这个文件夹就是可以直接上传的成品：

- `index.html` —— 述职看板（已从原文件复制；文件名必须是 index.html，GitHub Pages 才会默认打开它）
- `.nojekyll` —— 告诉 GitHub Pages 不要用 Jekyll 处理，避免意外报错

> 提醒：用免费 GitHub 账号时，GitHub Pages 只能从 **公开仓库** 发布，也就是说页面在公网上任何人拿到链接都能打开。这份材料含姓名、绩效等内部信息，请先确认可以公开。我已在页面里加了 `noindex,nofollow`，搜索引擎不会收录它，但"不收录"不等于"外人看不到"。

## 方式一：网页上传（不用敲命令）

1. 打开 https://github.com/new
2. Repository name 填一个英文名，例如 `hr-report`（这会影响最终网址，建议用英文）
3. 选 **Public**，勾上 `Add a README file`，点 `Create repository`
4. 进入仓库后点 `Add file` → `Upload files`
5. 把本文件夹里的 **`index.html`** 拖进去（`.nojekyll` 也一起拖，如果看不到它，在文件管理器里开启"显示隐藏文件"）
6. 下面点 `Commit changes`
7. 仓库页点 `Settings` → 左侧 `Pages`
8. `Build and deployment` 的 Source 选 `Deploy from a branch`，Branch 选 `main`，目录选 `/ (root)`，点 `Save`
9. 等 1—3 分钟刷新，页面顶部会出现网址：

```
https://你的用户名.github.io/hr-report/
```

这个网址就是可以发给别人的网页链接。

## 方式二：命令行（一次配置好，后续更新方便）

先在 GitHub 上按上面第 1—3 步建好空仓库（这次 _不要_ 勾 README），然后在 PowerShell 里执行：

```powershell
cd "C:\Users\admin\Documents\Codex\2026-09-11\file-c-users-admin-documents-codex\outputs\github-pages"
git init -b main
git add .
git commit -m "add hr report dashboard"
git remote add origin https://github.com/你的用户名/hr-report.git
git push -u origin main
```

首次 push 会弹出浏览器让你登录 GitHub 授权，授权一次之后电脑会记住。

推上去之后，同样去 `Settings` → `Pages` 设置一次 `main` + `/ (root)` 即可。

以后改内容只需要覆盖 `index.html`，然后：

```powershell
git add .
git commit -m "update"
git push
```

## 几个常见坑

- **文件名**：入口页必须叫 `index.html`。叫原名"人力资源部管培生三个月工作汇报-数据看板.html"的话，链接得写成 `.../hr-report/人力资源部管培生三个月工作汇报-数据看板.html`，中文会被转义成一长串百分号编码，很难看也容易出错。
- **仓库名**：`用户名.github.io` 这种仓库名会变成主站根地址，容易和别的项目冲突；普通项目名（如 `hr-report`）更合适。
- **私有仓库**：免费账号的私有仓库不能用 Pages，设置里会直接把 Pages 置灰或要求升级。如果一定不能公开，需要改用公司内网或对象存储。
- **更新延迟**：改完文件后页面不是立刻生效，通常要等 1—3 分钟，浏览器缓存还需要强刷（Ctrl+F5）。
- **访问统计**：GitHub Pages 本身不提供访问量统计，看不了谁打开过。
