# 需求文档管理系统 - Vercel部署说明

## 部署信息

- **部署平台**: Vercel
- **项目名称**: requirements-management-system
- **生产环境URL**: https://requirements-management-system-1ypb46rbx.vercel.app
- **部署时间**: 2025-06-20

## 部署步骤

### 1. 准备工作

1. 创建 `vercel.json` 配置文件，指定项目配置：
   ```json
   {
     "version": 2,
     "outputDirectory": "./",
     "cleanUrls": true,
     "trailingSlash": false
   }
   ```

2. 创建 `package.json` 文件，定义项目信息：
   ```json
   {
     "name": "需求文档管理系统",
     "version": "1.0.0",
     "description": "系统化维护所有需求文档",
     "main": "index.html",
     "scripts": {
       "dev": "vercel dev",
       "build": "echo 'No build step required'",
       "deploy": "vercel --prod"
     },
     "keywords": [
       "需求管理",
       "文档系统",
       "PRD"
     ],
     "author": "产品团队",
     "license": "MIT",
     "devDependencies": {
       "vercel": "^32.4.1"
     }
   }
   ```

3. 创建 `.gitignore` 文件，排除不需要上传的文件：
   ```
   # Dependencies
   node_modules/
   
   # Vercel
   .vercel
   
   # OS generated files
   .DS_Store
   .DS_Store?
   ._*
   .Spotlight-V100
   .Trashes
   ehthumbs.db
   Thumbs.db
   
   # IDE
   .vscode/
   .idea/
   *.swp
   *.swo
   
   # Logs
   *.log
   npm-debug.log*
   yarn-debug.log*
   yarn-error.log*
   
   # Temporary files
   *.tmp
   *.temp
   ```

### 2. 初始化Git仓库

```bash
git init
git config user.name "Vicliu Corporation"
git config user.email "dev@vicliu.com"
git add .
git commit -m "Initial commit: 需求文档管理系统"
```

### 3. 安装Vercel CLI

```bash
npm install -g vercel
```

### 4. 登录Vercel

```bash
vercel login
```

### 5. 部署到Vercel

```bash
vercel --prod
```

## 部署注意事项

1. **静态网站部署**: 本项目是一个静态网站，不需要构建过程，直接部署HTML、CSS和JavaScript文件。

2. **文件路径**: 确保所有文件路径使用相对路径，以便在Vercel上正确解析。

3. **中文文件名**: Vercel支持中文文件名，但建议在URL中使用英文或拼音，以避免潜在的编码问题。

4. **自定义域名**: 如需使用自定义域名，可以在Vercel控制台中设置。

5. **环境变量**: 如需环境变量，可以在Vercel控制台中添加。

## 更新部署

每次更新项目后，按照以下步骤重新部署：

1. 提交更改到Git仓库：
   ```bash
   git add .
   git commit -m "更新描述"
   ```

2. 重新部署到Vercel：
   ```bash
   vercel --prod
   ```

## 故障排除

### 常见问题

1. **部署失败**: 检查 `vercel.json` 配置文件是否正确，特别是路由配置。

2. **文件路径错误**: 确保所有文件路径使用相对路径，而不是绝对路径。

3. **中文编码问题**: 确保所有HTML文件使用UTF-8编码。

4. **资源加载失败**: 检查资源文件路径是否正确，确保所有资源文件都已上传。

### 调试方法

1. 使用 `vercel dev` 命令在本地启动开发服务器，检查项目是否正常运行。

2. 使用浏览器开发者工具检查网络请求和错误信息。

3. 查看Vercel控制台中的部署日志，获取详细的错误信息。

## 联系方式

如有任何问题或建议，请联系系统管理员。