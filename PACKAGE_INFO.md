# 极地文本工具集 - 完整打包文件

## 📦 文件信息

**打包文件**: `polarsite-toolkit-complete.tar.gz`  
**文件大小**: 32.6 KB  
**打包时间**: 2025年11月18日  
**包含文件**: 12个文件

## 📁 文件清单

### 🌐 网站核心文件
- `index.html` - 主页面，工具总览
- `pdf.html` - PDF转换器 (Markdown/TXT/HTML转PDF)
- `rename.html` - 批量重命名工具
- `sheet.html` - 表格处理器 (CSV/Excel)
- `watermark.html` - 图片去水印工具
- `sign.html` - PDF电子签名工具
- `image.html` - 图片处理器 (新增功能)

### 📄 文档页面
- `about.html` - 关于我们页面
- `privacy.html` - 隐私政策页面

### 📋 部署文档
- `README.md` - 项目说明文档
- `DEPLOY.md` - VPS部署指南

## 🚀 快速部署到VPS

### 1. 上传压缩包到VPS
```bash
# 使用SCP上传
scp polarsite-toolkit-complete.tar.gz user@your-vps-ip:/tmp/

# 登录VPS解压
ssh user@your-vps-ip
cd /var/www/
sudo tar -xzf /tmp/polarsite-toolkit-complete.tar.gz
sudo chown -R www-data:www-data polarsite-toolkit/
```

### 2. 配置Nginx
按照 `DEPLOY.md` 中的详细指南配置Nginx站点。

### 3. 访问网站
部署完成后，访问您的域名即可使用所有工具功能。

## 🛠 工具功能概览

### 核心工具 (6个)
1. **图片处理器** - 元数据移除、压缩、尺寸调整、格式转换
2. **PDF转换器** - 支持Markdown/TXT/HTML转PDF
3. **批量重命名** - 文件批量重命名，支持ZIP下载
4. **表格处理** - CSV/Excel查看、过滤、导出
5. **去水印工具** - 智能图片水印去除
6. **电子签名** - PDF签名工具

### 特色功能
- ✅ 100%纯前端实现，无数据上传
- ✅ 中英双语支持，自动语言检测
- ✅ iOS风格设计，深色模式自适应
- ✅ 响应式布局，完美支持移动端
- ✅ 开源透明，可自由审计

## 📋 技术栈

- **前端**: 纯HTML/CSS/JavaScript
- **样式**: Tailwind CSS
- **PDF**: jsPDF, pdf-lib
- **Canvas**: html2canvas
- **Excel**: XLSX.js
- **压缩**: JSZip
- **签名**: signature_pad

## 🔒 隐私保护

- 无Cookie，无追踪代码
- 所有处理在浏览器本地完成
- 无数据上传到服务器
- 开源代码，透明可信

## 📞 技术支持

- **邮箱**: admin@polarsite.site
- **GitHub**: https://github.com/kayyoung/pdf-converter
- **文档**: 详见 `README.md` 和 `DEPLOY.md`

---

© 2025 极地文本工具集 - 安全、私密、专业的浏览器端工具集合