# 部署指南

## 方式一：Vercel 部署（推荐，最简单）

### 步骤：

1. **注册 Vercel 账号**
   - 访问 https://vercel.com
   - 使用 GitHub 账号登录

2. **准备代码**
   - 将代码推送到 GitHub 仓库

3. **一键部署**
   - 在 Vercel 点击 "New Project"
   - 选择你的 GitHub 仓库
   - 点击 "Deploy"
   - 等待部署完成（约 1-2 分钟）

4. **获取访问链接**
   - 部署完成后会生成一个链接，如：`https://your-app.vercel.app`
   - 将这个链接发送到微信即可使用

### 绑定自定义域名（可选）：
- 在 Vercel 项目设置中添加你的域名
- 按提示配置 DNS 解析

---

## 方式二：阿里云/腾讯云部署

### 步骤：

1. **购买服务器**
   - 选择 Node.js 环境
   - 推荐配置：2核4G，带宽 5M+

2. **安装环境**
   ```bash
   # 安装 Node.js
   curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
   sudo apt-get install -y nodejs
   
   # 安装 pnpm
   npm install -g pnpm
   ```

3. **上传代码**
   ```bash
   # 方式1：Git 克隆
   git clone <你的仓库地址>
   
   # 方式2：SCP 上传
   scp -r ./projects root@<服务器IP>:/var/www/
   ```

4. **安装依赖并构建**
   ```bash
   cd /var/www/projects
   pnpm install
   pnpm build
   ```

5. **启动服务**
   ```bash
   # 使用 PM2 保持运行
   npm install -g pm2
   pm2 start "pnpm start" --name prompt-generator
   pm2 save
   pm2 startup
   ```

6. **配置 Nginx 反向代理**
   ```nginx
   server {
       listen 80;
       server_name your-domain.com;
       
       location / {
           proxy_pass http://localhost:3000;
           proxy_http_version 1.1;
           proxy_set_header Upgrade $http_upgrade;
           proxy_set_header Connection 'upgrade';
           proxy_set_header Host $host;
           proxy_cache_bypass $http_upgrade;
       }
   }
   ```

7. **配置 HTTPS**
   ```bash
   # 使用 Let's Encrypt 免费证书
   apt install certbot python3-certbot-nginx
   certbot --nginx -d your-domain.com
   ```

---

## 方式三：Docker 部署

### Dockerfile:
```dockerfile
FROM node:20-alpine AS builder
WORKDIR /app
RUN npm install -g pnpm
COPY package.json pnpm-lock.yaml ./
RUN pnpm install --frozen-lockfile
COPY . .
RUN pnpm build

FROM node:20-alpine AS runner
WORKDIR /app
RUN npm install -g pnpm
COPY --from=builder /app/.next ./.next
COPY --from=builder /app/public ./public
COPY --from=builder /app/package.json ./package.json
EXPOSE 3000
CMD ["pnpm", "start"]
```

### 部署命令：
```bash
docker build -t prompt-generator .
docker run -p 3000:3000 prompt-generator
```

---

## 环境变量配置

部署时需要配置以下环境变量（如果使用 LLM 功能）：

```bash
# .env.local
COZE_API_KEY=your_api_key_here
```

---

## 微信访问注意事项

1. **必须是 HTTPS** - 微信要求链接使用 HTTPS 协议
2. **域名备案** - 国内服务器需要域名备案
3. **内容审核** - 如果涉及用户生成内容，可能需要接入内容审核

---

## 快速开始

最简单的方式是 **Vercel**：
1. 注册 Vercel
2. 推送代码到 GitHub
3. 一键部署
4. 复制链接到微信

全程免费，5 分钟搞定！
