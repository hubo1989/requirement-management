# 本地开发服务器启动指南

## 问题解决

原来的 `npm run dev` 命令使用了 `vercel dev`，这会导致递归调用错误，因为 Vercel 的项目设置中可能已经配置了相同的命令。

## 新的启动方式

### 方法 1: 使用 npm scripts (推荐)

```bash
# 启动本地开发服务器 (端口 8080)
npm run dev

# 或者使用 serve 命令
npm run serve

# 预览模式
npm run preview
```

### 方法 2: 直接使用 Python

```bash
# Python 3
python3 -m http.server 8080

# Python 2 (如果还有环境在用)
python -m SimpleHTTPServer 8080
```

### 方法 3: 使用 serve 包

```bash
# 安装 serve (如果还没安装)
npm install -g serve

# 启动服务器
serve . -p 8080
```

### 方法 4: 使用 Node.js http-server

```bash
# 安装 http-server
npm install -g http-server

# 启动服务器
http-server . -p 8080
```

## 访问网站

启动服务器后，在浏览器中访问：
- http://localhost:8080

## 静态网站特性

这是一个纯静态网站，特点：
- ✅ 无需构建步骤
- ✅ 直接服务 HTML 文件
- ✅ 支持相对路径引用
- ✅ 适合部署到任何静态托管平台

## 部署

部署到生产环境仍然使用：
```bash
npm run deploy
```

## 故障排除

如果遇到端口占用问题：
```bash
# 使用不同端口
python3 -m http.server 3000
# 或
serve . -p 3000
```

如果 Python 不可用，确保已安装 Node.js 和 serve 包：
```bash
npm install -g serve
```