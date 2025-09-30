# 文档更新与资料增添指南

本文档说明如何在 `docs/` 目录下维护 GitHub Pages，以及如何新增资料下载条目。

## 1. 本地预览

1. 安装 Node.js（若尚未安装）。
2. 在项目根目录运行：
   ```bash
   npx docsify-cli@latest serve docs
   ```
3. 浏览器访问 `http://localhost:3000`，实时查看修改效果。若使用 `python3 -m http.server --directory docs 9000`，则访问 `http://localhost:9000`。

## 2. 更新文档内容

1. 在 `docs/` 下找到对应的 Markdown 文件进行编辑，例如：
   - 推免指南：`docs/guide/*`
   - 院校信息：`docs/universities/*`
   - 文档资料：`docs/doc/*`
2. 保存后在本地预览确认排版和图片是否正常。
3. 若新增页面，请同步修改：
   - `docs/_sidebar.md`：添加侧边栏导航条目。
   - 如需顶部入口，更新 `docs/_navbar.md`。
4. 使用 Markdown 标准语法，避免在标题中嵌套链接，保持段落结构清晰。

## 3. 新增资料下载条目

1. 将 PDF/ZIP/DOCX 等文件放入 `docs/other/` 对应子目录（建议继续使用现有分类，如 `复习准备/`、`文书/`）。
2. 在 `docs/other/README.md` 的相应部分新增表格或列表条目：
   ```html
   <tr>
     <td><a data-no-routing="true" target="_blank" rel="noopener" download href="other/复习准备/示例资料.pdf">示例资料</a></td>
     <td>简短介绍内容</td>
   </tr>
   ```
   - `data-no-routing="true"` 防止 docsify 将链接当作路由。
   - `target="_blank" rel="noopener"` 在新标签页打开并避免安全隐患。
   - `download` 将提示浏览器下载（对 PDF/ZIP 等生效）。
3. 本地预览测试下载链接是否正常。

## 4. 图片与 favicon

- 公共图片放在 `docs/assets/`。使用 Markdown 插入时采用相对路径（例如 `![](assets/example.png)`）。
- 若需更新封面头像或站点小图标，分别修改：
  - 封面：`docs/custom.css` 中 `.cover-hero` 的 `background-image`。
  - favicon：`docs/index.html` 中 `<link rel="icon" ...>`。

## 5. 提交与发布

1. 修改完成后运行：
   ```bash
   git status
   git add <修改的文件>
   git commit -m "feat: update docs/xxx"
   git push
   ```
2. GitHub Pages 已配置为使用 `docs/` 目录。推送到默认分支后，等待 1-2 分钟即可生效。

## 6. 常见问题

- **链接 404**：确认 `docs/index.html` 中 `noCompileLinks` 包含相应文件类型；检查 `href` 路径是否以 `other/` 等正确目录开头。
- **图片不显示**：确认文件已置于 `docs/assets/` 内，Markdown 引用路径正确。
- **导航不生效**：顶部导航仅支持一级菜单。若需层级结构，请在 `_sidebar.md` 中配置。

如有其他问题，可在 GitHub 提 Issue 或在保研交流群反馈。
