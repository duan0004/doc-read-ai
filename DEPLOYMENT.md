# 🚀 文献智能解读模块 - 部署指南

## 📋 部署概述

本项目支持多种部署方式，推荐使用云平台部署以获得最佳的稳定性和可扩展性。

## 🌟 推荐部署方案

### 方案一：Render 云平台部署（推荐）

**优势**：
- ✅ 免费额度充足
- ✅ 自动SSL证书
- ✅ 自动从Git部署
- ✅ 内置负载均衡
- ✅ 自动健康检查

**部署步骤**：

1. **准备代码仓库**
   ```bash
   # 推送代码到GitHub
   git add .
   git commit -m "准备生产环境部署"
   git push origin main
   ```

2. **配置Render服务**
   - 访问 [render.com](https://render.com)
   - 注册账号并连接GitHub
   - 选择 "New" → "Blueprint"
   - 选择你的仓库
   - 使用项目根目录的 `render-simple.yaml` 配置文件

3. **配置环境变量**
   - 后端服务环境变量：
     ```
     NODE_ENV=production
     PORT=8000
     DEEPSEEK_API_KEY=sk-9d268b2ffcc64b68a62e81b4eb31f18f
     CORS_ORIGIN=https://your-frontend-url.onrender.com
     ```
   - 前端服务环境变量：
     ```
     NODE_ENV=production
     NEXT_PUBLIC_API_URL=https://your-backend-url.onrender.com/api
     ```

4. **部署验证**
   - 后端健康检查：`https://your-backend-url.onrender.com/health`
   - 前端访问：`https://your-frontend-url.onrender.com`

### 方案二：Docker Compose 本地/VPS部署

**适用场景**：有自己的服务器或VPS

**部署步骤**：

1. **环境准备**
   ```bash
   # 安装Docker和Docker Compose
   curl -fsSL https://get.docker.com -o get-docker.sh
   sh get-docker.sh
   
   # 安装Docker Compose
   sudo curl -L "https://github.com/docker/compose/releases/download/v2.20.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
   sudo chmod +x /usr/local/bin/docker-compose
   ```

2. **克隆项目**
   ```bash
   git clone <your-repo-url>
   cd doc-read-ai
   ```

3. **配置环境变量**
   ```bash
   # 编辑 .env.production 文件
   cp .env.production.example .env.production
   # 修改其中的配置
   ```

4. **一键部署**
   ```bash
   ./deploy.sh
   ```

### 方案三：分离部署到不同平台

**后端部署**：推荐 Railway 或 Render
**前端部署**：推荐 Vercel 或 Netlify
**数据库**：推荐 Supabase 或 PlanetScale
**文件存储**：推荐 AWS S3 或 Cloudinary

## 🔧 生产环境配置

### 必需环境变量

**后端 (Backend)**：
```bash
NODE_ENV=production
PORT=8000
DEEPSEEK_API_KEY=your_deepseek_api_key
CORS_ORIGIN=https://your-frontend-domain.com
JWT_SECRET=your_jwt_secret
UPLOAD_MAX_SIZE=50MB
```

**前端 (Frontend)**：
```bash
NODE_ENV=production
NEXT_PUBLIC_API_URL=https://your-backend-domain.com/api
```

**可选环境变量**：
```bash
# 数据库 (如果使用)
DATABASE_URL=postgresql://user:password@host:port/dbname

# Redis缓存 (如果使用)
REDIS_URL=redis://host:port

# Semantic Scholar API (可选)
SEMANTIC_API_KEY=your_semantic_scholar_api_key
```

## 📊 性能优化建议

### 后端优化
1. **启用Redis缓存**
   - AI分析结果缓存
   - 文献检索结果缓存
   
2. **数据库优化**
   - 使用PostgreSQL持久化存储
   - 添加数据库索引
   
3. **文件存储优化**
   - 使用云存储服务 (AWS S3, Google Cloud Storage)
   - 启用CDN加速

### 前端优化
1. **构建优化**
   - 启用生产模式构建
   - 代码分割和懒加载
   
2. **缓存策略**
   - 静态资源缓存
   - API响应缓存

## 🔒 安全配置

### 基础安全
- ✅ HTTPS强制跳转
- ✅ CORS配置
- ✅ 文件上传限制
- ✅ API密钥保护

### 高级安全
- 📋 IP限流
- 📋 请求频率限制
- 📋 文件类型验证
- 📋 输入数据验证

## 📈 监控和日志

### 推荐监控工具
- **应用监控**：Sentry
- **性能监控**：New Relic
- **日志收集**：LogRocket
- **健康检查**：UptimeRobot

### 日志配置
```javascript
// 生产环境日志级别
const logLevel = process.env.NODE_ENV === 'production' ? 'error' : 'debug';
```

## 🛠️ 故障排除

### 常见问题

1. **AI功能不工作**
   - 检查DEEPSEEK_API_KEY是否正确配置
   - 验证API密钥余额和权限

2. **文件上传失败**
   - 检查UPLOAD_MAX_SIZE配置
   - 验证磁盘空间

3. **CORS错误**
   - 检查CORS_ORIGIN配置
   - 确保前后端域名配置正确

4. **服务启动失败**
   - 检查端口占用：`netstat -tlnp | grep :8000`
   - 查看服务日志：`docker-compose logs`

### 调试命令
```bash
# 查看服务状态
docker-compose ps

# 查看实时日志
docker-compose logs -f

# 重启服务
docker-compose restart

# 进入容器调试
docker-compose exec backend sh
```

## 📞 技术支持

如遇问题，请提供以下信息：
- 部署平台和版本
- 错误日志
- 环境变量配置（敏感信息请脱敏）
- 复现步骤

## 🔄 更新部署

### Git部署更新
```bash
git pull origin main
docker-compose build --no-cache
docker-compose up -d
```

### 云平台自动更新
大多数云平台支持Git推送自动部署，推送到main分支即可自动更新。

---

## 🎉 部署完成检查清单

- [ ] 后端服务健康检查通过
- [ ] 前端页面正常访问
- [ ] PDF上传功能正常
- [ ] AI分析功能正常
- [ ] 文献检索功能正常
- [ ] SSL证书配置正确
- [ ] 环境变量配置完整
- [ ] 监控和日志配置完成

**恭喜！🎊 您的文献智能解读系统已成功部署上线！**