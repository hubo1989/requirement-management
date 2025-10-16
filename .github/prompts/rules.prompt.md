# Repository Guidelines / 代码库指南

## Project Structure & Module Organization / 项目结构与模块组织

### English / 英文

This is a requirements document management system built with static HTML files and deployed on Vercel. The repository follows a documentation-centric structure:

### 中文 / Chinese

这是一个基于静态HTML文件构建的需求文档管理系统，部署在Vercel平台上。代码库遵循以文档为核心的结构：

```
项目主目录/
├── index.html                 # Main navigation file / 主导航文件
├── README.md                  # System documentation / 系统文档
├── package.json               # Project metadata and scripts / 项目元数据和脚本
├── vercel.json                # Vercel deployment configuration / Vercel部署配置
├── 归档/                      # Archived requirements / 已归档的需求
├── 模板/                      # Document templates / 文档模板
├── [category_folders]/        # Business requirement categories / 业务需求分类
└── DEPLOYMENT.md              # Deployment instructions / 部署说明
```

### English / 英文

Each requirement folder contains: `原始文档/`, `相关资源/`, `版本历史/`, and `index.html`.

### 中文 / Chinese

每个需求文件夹包含：`原始文档/`、`相关资源/`、`版本历史/` 和 `index.html`。

## Build, Test, and Development Commands / 构建、测试和开发命令

### English / 英文

This is a static site with minimal build requirements:

- `npm run dev` - Start local development server using Vercel CLI
- `npm run build` - No build step required (static files)
- `npm run deploy` - Deploy to production on Vercel

For local development, install dependencies with `npm install` then run `npm run dev`.

### 中文 / Chinese

这是一个静态网站，构建需求极少：

- `npm run dev` - 使用 Vercel CLI 启动本地开发服务器
- `npm run build` - 无需构建步骤（静态文件）
- `npm run deploy` - 部署到 Vercel 生产环境

本地开发时，先运行 `npm install` 安装依赖，然后运行 `npm run dev`。

## Coding Style & Naming Conventions / 编码风格和命名规范

### Folder Structure / 文件夹结构

#### English / 英文

- Category folders: Use business module names (e.g., "银行联合营销平台")
- Requirement folders: `[需求名称]V[版本号]` format (e.g., "机构新增优化需求V1.0")
- Use underscores `_` instead of spaces
- Avoid special characters in folder names

#### 中文 / Chinese

- 分类文件夹：使用业务模块名称（例如："银行联合营销平台"）
- 需求文件夹：`[需求名称]V[版本号]` 格式（例如："机构新增优化需求V1.0"）
- 使用下划线 `_` 代替空格
- 避免在文件夹名称中使用特殊字符

### File Naming / 文件命名

#### English / 英文

- Requirement documents: `[需求名称]_[版本号].[扩展名]`
- Index files: Always use `index.html`
- Template files: `[文档类型]_模板.[扩展名]`

#### 中文 / Chinese

- 需求文档：`[需求名称]_[版本号].[扩展名]`
- 索引文件：始终使用 `index.html`
- 模板文件：`[文档类型]_模板.[扩展名]`

### HTML Standards / HTML 标准

#### English / 英文

- Use semantic HTML5 elements
- Maintain UTF-8 encoding
- Include proper meta tags for SEO
- Follow responsive design principles

#### 中文 / Chinese

- 使用语义化 HTML5 元素
- 保持 UTF-8 编码
- 包含适当的 SEO 元标签
- 遵循响应式设计原则

## Testing Guidelines / 测试指南

### English / 英文

This is a documentation system without traditional unit tests. Quality assurance includes:

- Manual verification of navigation links in `index.html`
- Checking document accessibility and download functionality
- Validating HTML structure with online validators
- Testing responsiveness across devices
- Ensuring all template references are functional

Run `npm run dev` locally to test changes before deployment.

### 中文 / Chinese

这是一个没有传统单元测试的文档系统。质量保证包括：

- 手动验证 `index.html` 中的导航链接
- 检查文档可访问性和下载功能
- 使用在线验证器验证 HTML 结构
- 测试跨设备响应式设计
- 确保所有模板引用功能正常

部署前在本地运行 `npm run dev` 测试更改。

## Commit & Pull Request Guidelines / 提交和拉取请求指南

### Commit Message Format / 提交信息格式

#### English / 英文

Use conventional commits with Chinese descriptions:

- `feat: 添加新的需求分类模块`
- `docs: 更新README文档`
- `fix: 修复导航链接错误`
- `refactor: 重构需求文件夹结构`

#### 中文 / Chinese

使用带有中文描述的约定式提交：

- `feat: 添加新的需求分类模块`
- `docs: 更新README文档`
- `fix: 修复导航链接错误`
- `refactor: 重构需求文件夹结构`

### Pull Request Requirements / 拉取请求要求

#### English / 英文

- Include clear description of changes
- Reference specific requirement documents if applicable
- Test all modified navigation links
- Ensure new requirements follow the standard folder structure
- Update main `index.html` when adding new requirements

#### 中文 / Chinese

- 包含清晰的更改描述
- 如适用，引用具体的需求文档
- 测试所有修改的导航链接
- 确保新需求遵循标准文件夹结构
- 添加新需求时更新主 `index.html`

### Documentation Updates / 文档更新

#### English / 英文

Always update relevant documentation when:

- Adding new requirement categories
- Modifying folder structures
- Changing naming conventions
- Updating deployment processes

#### 中文 / Chinese

在以下情况下始终更新相关文档：

- 添加新的需求分类
- 修改文件夹结构
- 更改命名约定
- 更新部署流程

## Deployment Notes / 部署说明

### English / 英文

- Deployed on Vercel platform
- Uses static file serving
- No build process required
- Automatic deployments on main branch pushes
- Custom domain configuration available in Vercel dashboard

Ensure all file paths use relative references for proper deployment functionality.

### 中文 / Chinese

- 部署在 Vercel 平台上
- 使用静态文件服务
- 无需构建过程
- 主分支推送时自动部署
- 自定义域名配置可在 Vercel 仪表板中设置

确保所有文件路径使用相对引用以实现正确的部署功能。
