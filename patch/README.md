# 增量包（Patch）使用说明

本目录存放 Word-Formatter-Pro 的增量更新包。增量包包含相对上一版本的**新增/修改文件**，配合本仓库 `.github/workflows/build.yml` 采用 **unzip-and-overwrite（解压覆盖）** 式集成，也可手动集成。

## 文件清单

| 文件 | 说明 |
|------|------|
| `Word-Formatter-Pro.patch.v2.8.1.zip` | v2.8.1 增量包（新增 4 个文件 + 修改 4 个文件） |
| `Word-Formatter-Pro.patch.v2.8.0.zip` | v2.8.0 增量包（历史版本，已被 v2.8.1 取代） |

## v2.8.1 增量包内容

**新增：**
- `wfp_template_tools.py` — 从 Word 模板文档导入排版参数
- `wfp_pdf_tools.py` — PDF 转 Word、从 PDF 导入排版参数
- `wfp_pdf_editor.py` — PDF 编辑器（文本框/矩形/直线/高亮/撤销）
- `.github/workflows/build.yml` — GitHub Actions 自动构建工作流（修复 YAML 语法错误，runner 规格 4 vCPU + 16 GB RAM）

**修改：**
- `wfp_version.py` — 版本号 2.8.0 → 2.8.1
- `requirements.txt` — 新增 `pymupdf>=1.24.0`、`pillow>=10.0.0`
- `README.md` — 新增功能说明与版本记录
- `wfp_gui.py` — 性能与稳定性优化：
  - 窗口打开/关闭/拖动动画更流畅（布局调整防抖，避免反复重算）
  - 日志窗口批量刷新、空闲时降低轮询频率，减少空转
  - 进度条更新节流，大批量文件处理时界面不再卡顿
  - 文件列表批量插入，添加大文件夹速度提升
  - 日志窗口增加行数上限，长时间运行不再无限占用内存

## 使用方法

### 方式一：GitHub Actions 自动集成（推荐）

1. 将增量包 zip 放入本仓库 **`patch/`** 目录（命名需为 `Word-Formatter-Pro.patch.<tag>.zip`），随代码一并推送到 `main` 分支；
2. 推送代码到 `main`，或创建 Release，或手动触发 `Build Release` 工作流；
3. 工作流会自动从 `patch/` 目录读取最新增量包并解压**覆盖**到源码树，安装依赖后构建 Windows/Linux 产物并上传 artifact。

> 说明：工作流优先使用 `workflow_dispatch` 手动输入的 `patch_url`；未输入时才从 `patch/` 目录自动查找最新增量包。

### 方式二：手动集成

1. 下载本目录的增量包 zip；
2. 解压到项目根目录，覆盖同名文件；
3. 安装依赖：`pip install -r requirements.txt`（需 `pymupdf`、`pillow`）；
4. 运行 `python wfp_gui.py` 或按原有方式启动。

## 版本历史

- **v2.8.1**：性能与稳定性优化（布局防抖、日志批量刷新、进度节流、列表批量插入、日志行数上限）；修复 build.yml YAML 语法错误。
- **v2.8.0**：新增模板/PDF 参数导入、PDF 转 Word（含图片）、PDF 编辑器、GitHub Actions 自动构建。
