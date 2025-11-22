# Polarsite Toolkit - 极地文本工具集

## 🌐 项目概述

极地文本工具集是一个纯前端的工具集合，所有处理都在浏览器中完成，确保您的数据安全私密。

**访问地址**: https://polarsite.site/

## 📁 项目结构

```
/var/www/polarsite/
├── index.html          # 主页面
├── pdf.html            # PDF转换器
├── rename.html         # 批量重命名
├── sheet.html          # 表格处理
├── watermark.html      # 去水印工具
├── sign.html           # 电子签名
├── image.html          # 图片编辑器
├── about.html          # 关于页面
├── privacy.html        # 隐私政策
└── README.md           # 说明文档
```

## 🛠 功能特性

### ✅ 已完成的功能

1. **PDF转换器** (pdf.html)
   - 支持 Markdown、TXT、HTML 转 PDF
   - 实时预览
   - 文件拖拽上传
   - 5MB文件大小限制

2. **批量重命名** (rename.html)
   - 查找替换
   - 添加前缀后缀
   - 序列号生成
   - ZIP打包下载

3. **表格处理** (sheet.html)
   - CSV/Excel 文件读取
   - 数据搜索过滤
   - CSV导出
   - 最多显示100行预览

4. **去水印工具** (watermark.html)
   - 图片水印去除
   - 矩形选择工具
   - 智能填充算法
   - PNG/JPG支持

5. **电子签名** (sign.html)
   - 手绘签名
   - 文字签名
   - 图片签名上传
   - PDF签名应用
 
 6. **图片处理器** (image.html)
   - 元数据去除
   - 图片压缩
   - 格式转换
   - 尺寸调整

### 🌟 核心特性

- **100%私密**: 所有处理在浏览器中完成，无数据上传
- **多语言**: 支持中英文切换
- **响应式**: 适配桌面和移动设备
- **深色模式**: 自动根据系统设置切换
- **开源免费**: 代码完全开放，可自由审计

## 🎨 设计特色

- **iOS风格**: 采用苹果设计语言，简洁优雅
- **深色主题**: 自动适配系统深色模式
- **流畅动画**: 使用CSS过渡效果
- **一致体验**: 所有工具保持统一设计风格

## 🔧 技术栈

- **前端框架**: 纯HTML/CSS/JavaScript
- **样式框架**: Tailwind CSS
- **PDF处理**: jsPDF, pdf-lib
- **Canvas操作**: html2canvas
- **Markdown**: marked.js
- **Excel处理**: XLSX.js
- **CSV处理**: PapaParse
- **ZIP压缩**: JSZip
- **签名绘制**: signature_pad

## 📱 浏览器兼容性

- Chrome 80+
- Firefox 75+
- Safari 13+
- Edge 80+

## 🚀 部署说明

项目为纯静态网站，可直接部署到任何静态托管服务：

```bash
# 使用Python本地测试
python -m http.server 8000

# 使用Node.js本地测试
npx serve .

# 部署到Nginx
sudo cp -r /var/www/polarsite
sudo nginx -s reload
```

## 🔒 隐私保护

- 无Cookie
- 无追踪代码
- 无数据收集
- 纯客户端处理
- 开源透明

## 📞 联系方式

- **邮箱**: admin@polarsite.site
- **GitHub**: https://github.com/kayyoung/polarsite

## 📄 许可证

本项目采用开源许可证，详见GitHub仓库。

---

© 2025 Polarsite Toolkit - Secure, Private, Professional Tools
