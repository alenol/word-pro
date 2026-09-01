# 增量包（Patch）使用说明

本目录存放 Word-Formatter-Pro 的增量更新包。增量包包含相对上一版本的**新增/修改文件**，配合本仓库 `.github/workflows/build.yml` 采用 **unzip-and-overwrite（解压覆盖）** 式集成，也可手动集成。

## 文件清单

| 文件 | 说明 |
|------|------|
| `Word-Formatter-Pro.patch.v2.8.0.zip` | v2.8.0 增量包（新增 4 个文件 + 修改 4 个文件） |

## v2.8.0 增量包内容

**新增：**
- `wfp_template_tools.py` — 从 Word 模板文档导入排版参数
- `wfp_pdf_tools.py` — PDF 转 Word、从 PDF 导入排版参数
- `wfp_pdf_editor.py` — PDF 编辑器（文本框/矩形/直线/高亮/撤销）
- `.github/workflows/build.yml` — GitHub Actions 自动构建工作流

**修改：**
- `wfp_version.py` — 版本号 2.7.7 → 2.8.0
- `requirements.txt` — 新增 `pymupdf>=1.24.0`、`pillow>=10.0.0`
- `README.md` — 新增功能说明 5 条
- `wfp_gui.py` — 新增「工具」菜单（模板导入/PDF 导入/PDF 转 Word/PDF 编辑器）

## 使用方法

### 方式一：GitHub Actions 自动集成（推荐）

1. 将增量包 zip 上传到本仓库的 **Release**（命名需为 `Word-Formatter-Pro.patch.<tag>.zip`）；
2. 推送代码到 `main` 分支，或创建 Release，或手动触发 `Build Release` 工作流；
3. 工作流会自动下载增量包并解压**覆盖**到源码树，安装依赖后构建 Windows/Linux 产物并上传 artifact。

### 方式二：手动集成

1. 下载本目录的增量包 zip；
2. 解压到项目根目录，覆盖同名文件；
3. 安装依赖：`pip install -r requirements.txt`（需 `pymupdf`、`pillow`）；
4. 运行 `python wfp_gui.py` 或按原有方式启动。

## 版本历史

- **v2.8.0**：新增模板/PDF 参数导入、PDF 转 Word（含图片）、PDF 编辑器、GitHub Actions 自动构建。
