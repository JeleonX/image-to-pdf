# 图片转 PDF

浏览器端图片转 PDF 工具，支持 JPG / PNG 格式，生成 A4 尺寸 PDF 文件。所有处理均在本地浏览器中完成，图片不会上传到任何服务器。

## 功能

- 拖拽或点击上传图片（JPG / PNG）
- 支持批量上传，无数量限制
- 可调整图片顺序（上移 / 下移）
- 可单独移除或一键清空
- 每页 A4（210×297mm），图片以最长边居中撑满，空白区域自动补白
- 进度条显示处理状态

## 限制

- 单张图片最大 10 MB
- 仅支持 JPG 和 PNG 格式

## 项目结构

```
image-to-pdf/
├── package.json
├── README.md
└── public/
    └── index.html
```

## 部署到 Cloudflare Pages

### 方式一：直接上传（推荐）

1. 登录 [Cloudflare Pages 控制台](https://dash.cloudflare.com/)
2. 进入 **Workers & Pages** → **Create application** → **Pages** → **Upload assets**
3. 输入项目名称（如 `image-to-pdf`）
4. 上传 `public` 文件夹
5. 点击 Deploy

部署完成后会获得一个 `*.pages.dev` 域名。

### 方式二：通过 Git 部署

1. 将项目推送到 GitHub / GitLab 仓库
2. 在 Cloudflare Pages 控制台创建项目，关联该仓库
3. 构建设置：
   - **Framework preset**: None
   - **Build output directory**: `public`
4. 点击 Save and Deploy

### 方式三：使用 Wrangler CLI

```bash
# 安装 wrangler
npm install -g wrangler

# 登录 Cloudflare
wrangler login

# 部署
cd image-to-pdf
npx wrangler pages deploy public
```

### 本地开发

```bash
cd image-to-pdf
npm install
npm run dev
```

浏览器访问 `http://localhost:8788`。

## 使用方法

1. 打开网页
2. 拖拽图片到上传区域，或点击选择文件
3. 在图片列表中调整顺序（▲▼），或移除不需要的图片（✕）
4. 点击「生成 PDF」
5. 浏览器自动下载生成的 `images.pdf` 文件

## 技术栈

- 纯前端，无后端依赖
- [pdf-lib](https://pdf-lib.js.org/) — 客户端 PDF 生成
- 可直接部署为 Cloudflare Pages 静态站点
