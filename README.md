# 个人网站系统

一个功能完整的个人学术主页系统，包含前台展示和后台管理功能，可直接部署到 GitHub Pages。

## ✨ 功能特性

### 前台展示
- **个人首页** — 照片、姓名、职称、所属单位、个人简介
- **工作经历** — 时间线展示，支持当前在职标记
- **教育经历** — 时间线展示，学位、专业、学校信息
- **学术成果** — 三栏标签页切换：
  - 学术论文（标题、作者、期刊/会议、DOI 链接）
  - 科研项目（项目名称、角色、经费来源、预算）
  - 科技奖项（奖项名称、级别、排名、颁发机构）
- **项目经历** — 卡片式展示，技术栈标签、项目链接
- **联系方式** — 邮箱、电话、地址、社交链接

### 后台管理
- 🔐 密码登录保护（默认密码：`admin123`）
- 📝 可视化编辑所有栏目内容
- 📁 数组条目支持增删、排序
- 🖼️ 个人照片支持上传或 URL
- 💾 自动保存到浏览器本地（localStorage）
- 📤 一键导出 `data.json` 文件
- 📥 支持导入 JSON 数据
- 🔄 一键重置为默认数据
- 🔑 可修改管理密码

### 部署
- 🚀 GitHub Actions 自动构建部署
- 📱 响应式设计，适配手机/平板/桌面
- 🎨 现代化 UI，平滑动画
- ✅ 内置 `.nojekyll` + `404.html`，完美适配 GitHub Pages

## 🛠 技术栈

- React 18 + TypeScript
- Tailwind CSS 3
- Vite 5
- React Router 6 (HashRouter)

## 📦 本地开发

```bash
# 安装依赖
npm install

# 启动开发服务器
npm run dev

# 构建生产版本
npm run build

# 预览构建结果
npm run preview
```

## 🚀 部署到 GitHub Pages

### 方法一：使用 GitHub Actions（推荐）

1. **创建仓库并推送代码**
   ```bash
   git init
   git add .
   git commit -m "Initial commit: personal website"
   git branch -M main
   git remote add origin https://github.com/<你的用户名>/<仓库名>.git
   git push -u origin main
   ```

2. **开启 GitHub Pages**
   - 进入仓库的 `Settings` → `Pages`
   - `Source` 选择 **`GitHub Actions`**
   - 推送代码后会自动触发构建和部署

3. **访问网站**
   - 部署完成后，访问 `https://<你的用户名>.github.io/<仓库名>/`
   - 如果仓库名为 `<你的用户名>.github.io`，则访问 `https://<你的用户名>.github.io/`

### 方法二：手动上传静态文件（无需 Node.js）

1. 将 `dist/` 目录下的**所有文件**（含 `.nojekyll`）上传到 GitHub 仓库根目录
2. 进入仓库 `Settings` → `Pages`
3. `Source` 选择 `Deploy from a branch`
4. `Branch` 选择 `main`，文件夹选 `/ (root)`
5. 保存后等待 1-2 分钟即可访问

> ⚠️ **关键**：确保仓库根目录直接包含 `index.html`、`.nojekyll`、`data.json`、`assets/` 和 `404.html`，不要放在子文件夹中。

## ✏️ 编辑内容

### 在线编辑（推荐）

1. 访问网站，在导航栏点击「管理」或直接访问 `/#/admin`
2. 输入管理密码（默认：`admin123`）
3. 在后台编辑各栏目内容，修改自动保存到浏览器本地
4. 编辑完成后点击右上角「导出」下载 `data.json`
5. 将下载的 `data.json` 替换仓库中的 `public/data.json`
6. 提交并推送到 GitHub，等待自动部署完成

### 直接编辑文件

直接修改 `public/data.json` 文件，提交后重新部署即可。

## ⚙️ 配置说明

### 修改管理密码

1. 登录管理后台
2. 进入「系统设置」→「修改管理密码」
3. 输入旧密码和新密码

> 注意：密码存储在浏览器 localStorage 中。如果是多设备使用，需要在每个设备上分别设置。默认密码在代码中为 `admin123`（`src/context/DataContext.tsx`）。

### 修改部署路径

`vite.config.ts` 中的 `base` 已设为 `'./'`（相对路径），兼容根路径和子路径部署，通常无需修改。

## 🔧 常见问题

### Q: 部署后页面空白 / 无法显示？

**原因1：缺少 `.nojekyll` 文件**
GitHub Pages 默认使用 Jekyll 处理文件，可能拦截 `assets/` 目录。项目已在 `public/` 目录中包含 `.nojekyll` 文件，构建时会自动复制到 `dist/`。如果手动上传，请确保包含此文件。

**原因2：上传了源码而非构建产物**
源码中的 `index.html` 引用 `/src/main.tsx`，GitHub Pages 无法解析。请确保上传的是 `dist/` 目录下的文件，或使用 GitHub Actions 自动构建。

**原因3：GitHub Pages 设置错误**
- 使用 GitHub Actions 部署：Source 选择 `GitHub Actions`
- 手动上传：Source 选择 `Deploy from a branch`，Branch 选 `main` + `/ (root)`

### Q: 管理后台修改后网站内容没更新？

管理后台的修改保存在浏览器 localStorage 中，仅当前浏览器可见。需要点击「导出」下载 `data.json`，替换仓库中的 `public/data.json` 并提交，网站内容才会全局更新。

### Q: 如何修改默认管理密码？

编辑 `src/context/DataContext.tsx`，找到 `DEFAULT_PASSWORD = 'admin123'`，修改为你的密码，然后重新构建。

## 📁 项目结构

```
personal-website/
├── .github/workflows/deploy.yml  # GitHub Actions 自动部署
├── public/
│   ├── .nojekyll                 # 禁用 Jekyll 处理
│   ├── 404.html                  # 404 重定向页面
│   └── data.json                 # 网站数据文件
├── src/
│   ├── components/
│   │   ├── admin/                # 后台管理组件
│   │   │   ├── AdminApp.tsx      # 管理后台入口
│   │   │   ├── AdminLogin.tsx    # 登录页
│   │   │   ├── AdminDashboard.tsx# 管理面板
│   │   │   ├── Editors.tsx       # 各栏目编辑器
│   │   │   └── FormFields.tsx    # 通用表单组件
│   │   ├── HomePage.tsx          # 首页
│   │   ├── Header.tsx            # 导航栏
│   │   ├── Footer.tsx            # 页脚
│   │   ├── Hero.tsx              # 个人介绍区
│   │   ├── WorkExperience.tsx    # 工作经历
│   │   ├── Education.tsx         # 教育经历
│   │   ├── AcademicAchievements.tsx # 学术成果
│   │   ├── ProjectExperience.tsx # 项目经历
│   │   ├── Contact.tsx           # 联系方式
│   │   └── SectionTitle.tsx      # 章节标题
│   ├── context/DataContext.tsx   # 数据管理上下文
│   ├── types.ts                  # 类型定义
│   ├── defaultData.ts            # 默认数据
│   ├── App.tsx                   # 根组件
│   ├── main.tsx                  # 入口
│   └── index.css                 # 全局样式
├── index.html
├── package.json
├── vite.config.ts
├── tailwind.config.js
└── tsconfig.json
```

## 📄 License

MIT
