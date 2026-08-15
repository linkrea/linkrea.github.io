# 云计算及算力网络研发团队网站

一个专为技术研发团队设计的展示型网站，支持前台展示与后台管理，可一键部署到 GitHub Pages 免费空间。

## 功能特性

- **前台展示**：首页、关于我们、新闻动态、专家团队、研发项目
- **后台管理**：可视化内容管理，支持增删改查所有栏目内容
- **数据持久化**：默认使用浏览器本地存储，支持导出/导入 JSON 备份
- **GitHub 同步**：可选配置 GitHub Token，实现数据云端自动同步
- **响应式设计**：适配桌面端与移动端
- **科技感 UI**：粒子动画背景，深蓝渐变主题

## 快速部署到 GitHub Pages

### 步骤 1：创建 GitHub 仓库

1. 登录 [GitHub](https://github.com)
2. 点击右上角 **+** → **New repository**
3. 仓库名称填写：`ccn-team-website`（可自定义）
4. 选择 **Public**（公开仓库才能使用免费 Pages）
5. 勾选 **Add a README file**
6. 点击 **Create repository**

### 步骤 2：上传网站文件

1. 在新仓库页面，点击 **Add file** → **Upload files**
2. 将 `index.html` 文件拖拽到上传区域
3. 点击页面底部的 **Commit changes**

### 步骤 3：启用 GitHub Pages

1. 进入仓库的 **Settings** 标签页
2. 左侧菜单选择 **Pages**
3. **Source** 选择 **Deploy from a branch**
4. **Branch** 选择 **main** / **master**，文件夹选择 **/(root)**
5. 点击 **Save**
6. 等待 1-2 分钟，页面会显示访问地址：`https://你的用户名.github.io/仓库名/`

### 步骤 4：配置自定义域名（可选）

1. 在仓库根目录创建 `CNAME` 文件（无后缀）
2. 文件内容填写你的域名，如：`www.yourteam.com`
3. 在域名 DNS 服务商添加 CNAME 记录指向 `你的用户名.github.io`
4. 在 GitHub Pages 设置中勾选 **Enforce HTTPS**

## 使用管理后台

1. 访问网站后，点击导航栏右侧的 **齿轮图标** 进入管理后台
2. 默认密码：`admin123`
3. 登录后可管理：
   - 新闻动态（增删改查）
   - 专家团队（增删改查）
   - 研发项目（增删改查）
   - 关于我们（编辑内容）
   - 同步设置（导出/导入/ GitHub 同步）

## 数据管理说明

### 方式一：本地存储（默认）
- 所有数据保存在浏览器 `localStorage` 中
- 更换浏览器或清除缓存会丢失数据
- 建议定期在「同步设置」中导出 JSON 备份

### 方式二：GitHub 自动同步（推荐）

配置后可实现：
- 多台设备数据同步
- 数据永久保存在 GitHub 仓库中
- 支持多人协作管理

**配置步骤：**

1. 生成 GitHub Token
   - 点击头像 → **Settings** → 最下方 **Developer settings**
   - **Personal access tokens** → **Tokens (classic)**
   - 点击 **Generate new token (classic)**
   - Note 填写：`CCN Website Admin`
   - Expiration 选择：**No expiration**（或自定义）
   - 勾选 **repo** 权限（完整控制仓库）
   - 点击 **Generate token**
   - **立即复制 Token**（页面关闭后无法再次查看）

2. 在网站管理后台的「同步设置」中填入：
   - **Token**：刚才复制的 `ghp_xxxx`
   - **仓库所有者**：你的 GitHub 用户名
   - **仓库名称**：你创建的仓库名（如 `ccn-team-website`）
   - 点击 **保存配置**

3. 在仓库中创建 `data.json` 文件（初始为空对象 `{}` 或从本地导出）

4. 之后点击「推送至 GitHub」即可同步数据，点击「从 GitHub 拉取」可恢复数据

## 修改管理密码

当前密码硬编码在 `index.html` 中。如需修改：

1. 打开 `index.html`
2. 搜索 `ADMIN_PASSWORD = 'admin123'`
3. 将 `'admin123'` 修改为你自己的密码
4. 重新上传文件

## 技术栈

- 纯 HTML5 / CSS3 / ES6+（零依赖，除 Tailwind CDN）
- Tailwind CSS（样式）
- Font Awesome（图标）
- Canvas 粒子动画
- localStorage / GitHub REST API（数据持久化）

## 目录结构

```
ccn-team-website/
├── index.html      # 主文件（包含所有前台与后台代码）
├── README.md       # 本文件
└── CNAME           # 可选：自定义域名配置
```

## 注意事项

1. **GitHub Pages 限制**：
   - 仓库需为 Public（免费版）
   - 每月有 100GB 带宽限制（一般展示型网站足够）
   - 静态网站，不支持服务端代码

2. **图片资源**：
   - 示例中使用的是 Unsplash 网络图片
   - 实际使用时建议替换为自有图片链接或上传到图床
   - 也可将图片放入仓库，使用相对路径引用

3. **安全性**：
   - 前端密码验证仅为基础防护
   - 如配置 GitHub Token，请勿将 Token 泄露给他人
   - 建议 Token 仅授予 repo 权限

## 自定义修改

### 修改团队名称 / Logo
在 `index.html` 中搜索相关文本直接替换即可。

### 修改主题色
在 `<style>` 标签内修改 CSS 变量：
- `--primary`: 主背景色
- `--accent`: 强调色（蓝色）
- `--accent2`: 次要强调色（紫色）

### 添加新栏目
如需添加新的内容类型，需在 `defaultData` 中定义数据结构，并在管理后台添加对应的管理界面。

## 开源协议

MIT License
