# 文献智能解读模块 - Vercel + Railway 部署

## 🚀 快速部署方案

### 方案：前端Vercel + 后端Railway

这是最简单快速的部署方案，完全免费且稳定可靠。

## 📋 部署步骤

### 第一步：准备Git仓库

1. 在GitHub创建新仓库
2. 推送代码：
```bash
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/duan0004/doc-read-ai.git
git push -u origin main
```

### 第二步：部署后端到Railway

1. 访问 [railway.app](https://railway.app)
2. 使用GitHub登录
3. 点击 "New Project" → "Deploy from GitHub repo"
4. 选择您的仓库
5. 选择 `backend` 目录作为根目录
6. 设置环境变量：
   ```
   NODE_ENV=production
   PORT=8000
   DEEPSEEK_API_KEY=sk-9d268b2ffcc64b68a62e81b4eb31f18f
   CORS_ORIGIN=https://您的前端域名.vercel.app
   ```
7. 部署完成后记录后端URL（如：https://xxx.railway.app）

### 第三步：部署前端到Vercel

1. 访问 [vercel.com](https://vercel.com)
2. 使用GitHub登录
3. 点击 "New Project"
4. 选择您的仓库
5. 配置项目：
   - Framework Preset: Next.js
   - Root Directory: `frontend`
   - Build Command: `npm run build`
   - Output Directory: `.next`
6. 设置环境变量：
   ```
   NODE_ENV=production
   NEXT_PUBLIC_API_URL=https://您的后端域名.railway.app/api
   ```
7. 点击Deploy

### 第四步：更新CORS配置

1. 获取Vercel分配的前端域名
2. 回到Railway后端项目
3. 更新CORS_ORIGIN环境变量为前端域名
4. 重新部署后端

## ✅ 验证部署

1. **后端健康检查**：访问 `https://你的后端域名.railway.app/health`
2. **前端访问**：访问 `https://你的前端域名.vercel.app`
3. **功能测试**：上传PDF测试AI分析功能

## 🔧 配置优化

### Railway后端优化
- 启用自动部署
- 配置健康检查
- 设置环境变量

### Vercel前端优化
- 启用自动部署
- 配置自定义域名
- 启用分析功能

## 💰 成本说明

- **Railway**: 免费额度每月$5，足够轻中度使用
- **Vercel**: 免费额度非常充足，支持自定义域名
- **总成本**: 完全免费（在免费额度内）

## 🎯 域名配置（可选）

### 自定义域名
1. **前端域名**：在Vercel项目设置中添加自定义域名
2. **后端域名**：Railway支持自定义域名（需要升级计划）
3. **SSL证书**：两个平台都自动提供SSL证书

## 📊 监控建议

- **Vercel Analytics**: 内置网站分析
- **Railway Metrics**: 内置性能监控
- **Sentry**: 错误监控（可选）
- **UptimeRobot**: 服务可用性监控（可选）

---

**🎉 按照以上步骤，您的项目将在10分钟内上线！**