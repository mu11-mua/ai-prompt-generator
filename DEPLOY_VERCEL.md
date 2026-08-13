# 一键部署到 Vercel（免费）

## 步骤 1：下载代码

由于代码在沙箱中，你需要先下载到本地：

### 方法 A：通过 Git（推荐）
```bash
# 在本地电脑执行
git clone <你的GitHub仓库地址>
```

### 方法 B：直接下载
1. 在沙箱中打包代码
2. 下载 zip 文件
3. 解压到本地

## 步骤 2：推送到 GitHub

```bash
# 在本地项目目录执行
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/你的用户名/你的仓库名.git
git push -u origin main
```

## 步骤 3：部署到 Vercel

1. 访问 https://vercel.com
2. 点击 "Sign Up" 注册（可用 GitHub 登录）
3. 登录后点击 "Add New Project"
4. 选择你的 GitHub 仓库
5. 点击 "Import"
6. Vercel 会自动检测 Next.js 项目
7. 点击 "Deploy"
8. 等待 1-2 分钟
9. 部署完成！获得永久链接

## 步骤 4：获取永久链接

部署成功后，你会得到类似这样的链接：
```
https://your-project-name.vercel.app
```

这个链接：
- ✅ 永久有效
- ✅ 免费 HTTPS
- ✅ 全球 CDN 加速
- ✅ 可在微信中打开

## 步骤 5：在微信中使用

1. 复制链接
2. 发送到微信聊天窗口
3. 点击即可打开
4. 可以收藏到微信收藏

## 更新代码

以后修改代码后：
```bash
git add .
git commit -m "Update description"
git push
```
Vercel 会自动重新部署！

## 注意事项

1. **Supabase 配置**：当前使用的是沙箱的 Supabase，部署后需要配置自己的 Supabase 项目
2. **环境变量**：如有环境变量，需要在 Vercel 项目设置中配置
3. **域名**：可以绑定自己的域名（可选）

## 获取帮助

如有问题，访问：
- Vercel 文档：https://vercel.com/docs
- Next.js 文档：https://nextjs.org/docs
