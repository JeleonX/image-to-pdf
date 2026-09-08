# PDF & 图片转换工具

纯浏览器端轻量转换工具，无需安装任何软件或依赖后端服务，支持 **图片转 PDF** 与 **PDF 转图片** 双向互转。

所有文件解析与渲染均在客户端本地完成，文件**绝不上传**至任何远程服务器，最大程度保障您的数据隐私与文件安全。

---

## 核心功能

### 1. 图片转 PDF (Image → PDF)
- **拖拽与批量添加**：支持将多张 JPG / PNG 图片批量拖拽或点击上传。
- **顺序调整与管理**：提供上移、下移调整页面顺序，支持单张移除或一键清空。
- **A4 智能排版**：每页标准 A4 尺寸（210×297mm），图片以最长边等比居中适应，四周自动补白填充，避免裁切变形。
- **格式容错与自适应**：支持读取二进制文件头（Magic Number）识别真实格式，并内置 Canvas 自动转码回退机制，确保兼容各种来源的图片。

### 2. PDF 转图片 (PDF → Image)
- **多格式导出**：支持导出为 **PNG（无损高清）** 或 **JPG** 格式。
- **多档清晰度倍率**：
  - 1x（标准大小）
  - 1.5x
  - 2x（推荐高清，视觉平衡）
  - 3x（超清打印级解析）
- **JPG 质量精细调节**：可按需调节 JPG 压缩质量百分比（10% - 100%），平衡画质与文件体积。
- **灵活下载**：
  - 支持对任意单页卡片单独下载。
  - 支持一键打包下载全部页面（自动生成 ZIP 压缩包）。

---

## 限制与规格

- **图片转 PDF**：单张图片限制 10 MB 以内，支持 JPG / JPEG / PNG。
- **PDF 转图片**：PDF 文档最大支持 100 MB。
- **浏览器兼容性**：支持现代主流浏览器（Chrome、Edge、Safari、Firefox 等）。

---

## 项目结构

```
image-to-pdf/
├── package.json        # 项目脚本配置
├── README.md           # 项目使用与部署文档
└── public/
    └── index.html      # 单文件完整 Web 应用（含样式、多功能模块与交互）
```

---

## 本地运行

无需复杂的构建流程，直接使用任何静态服务器运行：

```bash
# 进入项目目录
cd image-to-pdf

# 方式一：使用 npm run dev（基于 wrangler pages dev）
npm run dev

# 方式二：使用 Python 内置静态服务器
python -m http.server 8788 --directory public

# 方式三：使用 Node.js npx serve
npx serve public -p 8788
```

浏览器访问 `http://localhost:8788` 即可使用。

---

## 部署到 Cloudflare Pages

### 方式一：直接网页上传（最简便）
1. 登录 [Cloudflare Pages 控制台](https://dash.cloudflare.com/)。
2. 导航至 **Workers & Pages** → **Create application** → **Pages** → **Upload assets**。
3. 输入自定义项目名称。
4. 将本项目的 `public` 文件夹直接拖拽上传。
5. 点击 **Deploy**，部署完成后即可获得免费的 `*.pages.dev` 访问链接。

### 方式二：通过 Git 仓库自动部署
1. 将本项目推送到 GitHub / GitLab 仓库。
2. 在 Cloudflare Pages 中关联该仓库。
3. 构建配置参数：
   - **Framework preset**: None
   - **Build output directory**: `public`
4. 点击 **Save and Deploy** 即可实现每次 push 自动部署。

### 方式三：使用 Wrangler CLI 命令行部署
```bash
# 安装 wrangler
npm install -g wrangler

# 登录 Cloudflare
wrangler login

# 执行一键部署
cd image-to-pdf
npx wrangler pages deploy public
```

---

## 技术实现栈

- **前端架构**：原生 HTML5 + CSS3 + ES6+，无框架依赖，单页面轻量秒开。
- **PDF 生成**：[pdf-lib](https://pdf-lib.js.org/) — 在浏览器中快速合成 PDF 文档。
- **PDF 解析与渲染**：[PDF.js (pdfjs-dist)](https://mozilla.github.io/pdf.js/) — Mozilla 开源的客户端 Canvas 渲染引擎。
- **多图压缩打包**：[JSZip](https://stuk.github.io/jszip/) — 客户端纯内存 ZIP 归档与打包下载。
