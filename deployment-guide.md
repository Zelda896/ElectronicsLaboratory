# 210创新实验室网站外部访问部署指南

## 🚀 部署方案选择

### 方案1：GitHub Pages（免费，推荐）

**优势：**
- 完全免费
- 自动HTTPS
- 全球CDN加速
- 简单易用

**部署步骤：**

1. **创建GitHub仓库**
   ```bash
   # 在GitHub上创建新仓库，命名为：210-innovation-lab
   ```

2. **上传网站文件**
   ```bash
   git init
   git add .
   git commit -m "Initial commit: 210创新实验室网站"
   git branch -M main
   git remote add origin https://github.com/你的用户名/210-innovation-lab.git
   git push -u origin main
   ```

3. **启用GitHub Pages**
   - 进入仓库设置 → Pages
   - Source选择"Deploy from a branch"
   - Branch选择"main"，文件夹选择"/ (root)"
   - 点击Save

4. **访问网站**
   - 网址：`https://你的用户名.github.io/210-innovation-lab`
   - 通常5-10分钟后生效

### 方案2：Vercel（免费，性能优秀）

**优势：**
- 免费额度充足
- 部署速度快
- 自动HTTPS
- 支持自定义域名

**部署步骤：**

1. **注册Vercel账号**
   - 访问：https://vercel.com
   - 使用GitHub账号登录

2. **导入项目**
   - 点击"New Project"
   - 选择GitHub仓库
   - 点击"Deploy"

3. **访问网站**
   - 自动生成网址：`https://项目名.vercel.app`

### 方案3：Netlify（免费）

**优势：**
- 免费托管
- 拖拽部署
- 表单处理功能
- 自动HTTPS

**部署步骤：**

1. **注册Netlify账号**
   - 访问：https://netlify.com

2. **拖拽部署**
   - 将整个项目文件夹拖拽到Netlify部署区域
   - 自动部署完成

3. **访问网站**
   - 自动生成网址：`https://随机名称.netlify.app`

### 方案4：自有服务器部署

**适用场景：**
- 需要完全控制
- 有服务器资源
- 需要后端功能

**部署步骤：**

1. **准备服务器**
   ```bash
   # 安装Nginx
   sudo apt update
   sudo apt install nginx
   
   # 启动Nginx
   sudo systemctl start nginx
   sudo systemctl enable nginx
   ```

2. **上传网站文件**
   ```bash
   # 将文件上传到服务器
   scp -r ./* user@your-server:/var/www/html/
   ```

3. **配置Nginx**
   ```nginx
   # /etc/nginx/sites-available/210lab
   server {
       listen 80;
       server_name your-domain.com;
       root /var/www/html;
       index index.html;
       
       location / {
           try_files $uri $uri/ =404;
       }
   }
   ```

4. **启用站点**
   ```bash
   sudo ln -s /etc/nginx/sites-available/210lab /etc/nginx/sites-enabled/
   sudo nginx -t
   sudo systemctl reload nginx
   ```

## 🔧 部署前准备

### 1. 创建部署配置文件

创建以下文件以优化部署：

**`.gitignore`**
```
# 系统文件
.DS_Store
Thumbs.db

# 编辑器文件
.vscode/
.idea/

# 临时文件
*.tmp
*.log
```

**`README.md`**
```markdown
# 210创新实验室招生网站

## 项目简介
沈阳农业大学信息与电气工程学院210创新实验室官方招生网站

## 技术栈
- HTML5
- CSS3 (Tailwind CSS)
- JavaScript (ES6+)
- 响应式设计

## 本地运行
直接打开 index.html 文件即可

## 在线访问
[网站地址](https://your-domain.com)
```

### 2. 性能优化建议

**压缩图片**（如果有图片文件）
```bash
# 使用在线工具压缩图片
# 推荐：TinyPNG, ImageOptim
```

**启用缓存**（服务器部署时）
```nginx
# Nginx缓存配置
location ~* \.(css|js|png|jpg|jpeg|gif|ico|svg)$ {
    expires 1y;
    add_header Cache-Control "public, immutable";
}
```

## 🌍 自定义域名配置

### GitHub Pages自定义域名

1. **购买域名**
   - 推荐：阿里云、腾讯云、GoDaddy

2. **配置DNS**
   ```
   类型: CNAME
   名称: www
   值: 你的用户名.github.io
   
   类型: A
   名称: @
   值: 185.199.108.153
   值: 185.199.109.153
   值: 185.199.110.153
   值: 185.199.111.153
   ```

3. **GitHub设置**
   - 仓库设置 → Pages → Custom domain
   - 输入域名：`www.your-domain.com`
   - 勾选"Enforce HTTPS"

## 📊 访问统计

### 添加Google Analytics

在 `index.html` 的 `<head>` 部分添加：

```html
<!-- Google Analytics -->
<script async src="https://www.googletagmanager.com/gtag/js?id=GA_TRACKING_ID"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());
  gtag('config', 'GA_TRACKING_ID');
</script>
```

## 🔒 安全配置

### 添加安全头

```html
<!-- 在 <head> 中添加 -->
<meta http-equiv="Content-Security-Policy" content="default-src 'self'; script-src 'self' 'unsafe-inline'; style-src 'self' 'unsafe-inline' https://cdn.jsdelivr.net;">
<meta http-equiv="X-Content-Type-Options" content="nosniff">
<meta http-equiv="X-Frame-Options" content="DENY">
<meta http-equiv="X-XSS-Protection" content="1; mode=block">
```

## 📱 移动端优化

网站已经具备响应式设计，在移动端访问体验良好。

## 🚀 推荐部署方案

**对于210创新实验室，推荐使用GitHub Pages：**

1. **免费且稳定**
2. **GitHub.io域名专业**
3. **全球访问速度快**
4. **维护简单**
5. **支持自定义域名**

## 📞 技术支持

如需部署协助，请联系：
- 邮箱：ElectronicsLaboratory@arcadia120.com
- 或通过网站联系表单

---

**部署完成后，全世界任何地方的用户都可以通过网址访问210创新实验室网站！**
