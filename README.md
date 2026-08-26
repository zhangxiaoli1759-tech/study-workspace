# 学习工作台 · 作文批改档案

一个**单文件、零依赖**的静态页面，用于长期保管孩子的作文批改档案。

## 架构说明（重要）
- **作文内容 → 腾讯文档**：每篇作文的详细批改（原文 / 六维赏析 / 润色定稿 / 95 分冲刺版 / 错字本 / 好字词本）都写在一篇腾讯文档里，**一篇一地址，地址写死、长期不变**。
- **本页面 → 索引 + 档案展示**：页面只存每篇的「标题 / 日期 / 评分 / 状态 / 腾讯文档链接」以及一份离线兜底快照。点卡片上的「📄 腾讯文档」按钮即跳转到对应文档。
- **更新作文**：直接在腾讯文档里改，地址不变，本页面无需任何改动。
- **新增作文**：见下方「如何新增一篇」。

## 如何新增一篇
1. 在腾讯文档新建该篇批改文档，复制文档地址（形如 `https://docs.qq.com/aio/...`）。
2. 打开本仓库的 `index.html`，在 `SEED_ESSAYS = [` 数组里**追加一条**（照着已有格式抄）：
   ```js
   {
     "id": "唯一id",
     "title": "作文标题",
     "content": "原文（可留空）",
     "date": "2026-08-26",
     "img": [],
     "tdocUrl": "https://docs.qq.com/aio/你的文档地址",
     "dims": { "liyi":"","jiegou":"","yuyan":"","sucai":"","shuxie":"","liangdian":"" },
     "polish": "润色定稿",
     "score": "88",
     "status": "已批改",
     "createdAt": "2026-08-26",
     "score95": "", "polish95": "", "cuo": [], "hao": []
   }
   ```
3. `git add -A && git commit -m "新增作文：xxx" && git push`

## 部署（GitHub Pages，永久免费）
1. 安装并登录 GitHub CLI：`gh auth login`（一次性，按提示用浏览器授权）。
2. 在本目录执行：
   ```bash
   gh repo create study-workspace --public --source=. --push -d "学习工作台 - 作文批改档案"
   ```
3. 仓库创建后，到 GitHub → 该仓库 **Settings → Pages → Source 选 `main` / root → Save**。
4. 几分钟后访问：`https://<你的用户名>.github.io/study-workspace/`

> 想用私有仓库也行：把 `--public` 改成 `--private`，Pages 同样可用（私有仓库的 Pages 仅限你本人可见）。

## 隐私提示
公开仓库会暴露作文标题与评分。若含敏感信息，请用**私有仓库**，或把 `index.html` 里的 `content`/`polish` 字段留空、只保留标题与腾讯文档链接（腾讯文档本身可设权限）。

## 本地预览
直接用浏览器打开 `index.html` 即可，无需服务器。
