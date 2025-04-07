# MockImage

![License](https://img.shields.io/badge/license-MIT-green)
![PHP](https://img.shields.io/badge/php-%3E=8.0-blue)
![Made by tendayspace](https://img.shields.io/badge/made%20by-tendayspace-blueviolet)
![GitHub stars](https://img.shields.io/github/stars/tendayspace/MockImage?style=social)

**MockImage** 是一个用 PHP 8 编写的本地占位图（Placeholder Image）生成器，灵感来源于 [dummyimage.com](https://dummyimage.com/)，支持动态尺寸、背景颜色、文字颜色、文本内容，并自动缓存为 JPG 图像，右下角附加 "tendayspace" 水印。

**MockImage** is a lightweight image placeholder generator written in PHP 8, inspired by [dummyimage.com](https://dummyimage.com/). It supports dynamic size, background color, text color, text content, and outputs JPG images with automatic caching and bottom-right watermark.

---

## 🌐 语言 / Language

- [🇨🇳 中文说明](#快速开始)
- [🇬🇧 English Guide](#quick-start)

---

## 🚀 快速开始 / Quick Start

### ✅ 环境需求 / Requirements
- PHP 8.0+
- GD 扩展已启用 / GD extension enabled

### 📁 文件结构 / File Structure
```
mockimage/
├── index.php           # 主入口 / Entry point
├── cache/              # 自动缓存图片 / Cached images
├── arial.ttf           # 字体文件 / Font file
├── README.md
├── LICENSE
└── .gitignore
```

### 📦 安装步骤 / Installation
```bash
# 克隆项目 / Clone the project
$ git clone https://github.com/tendayspace/MockImage.git
$ cd MockImage

# 准备字体文件 / Prepare a font file
$ cp /usr/share/fonts/truetype/dejavu/DejaVuSans-Bold.ttf arial.ttf

# 创建缓存目录 / Create cache directory
$ mkdir cache && chmod 777 cache
```

---

## 🔍 使用示例 / Usage Example

```
http://yourdomain.com/{width}x{height}/{text}/{bg_color}/{text_color}
```

### 示例链接 / Sample Links
| 链接 / URL | 说明 / Description |
|------------|--------------------|
| `/600x400` | 默认灰底黑字，显示文字为 `600x400` <br> Gray background, black text, shows "600x400" |
| `/400x300/Hello` | 灰底黑字，显示 "Hello" <br> Gray background, text = Hello |
| `/300x300/Hi/000/fff` | 黑底白字，文字 "Hi" <br> Black background, white text "Hi" |

---

## ⚙️ 参数说明 / Parameters
| 参数 / Param         | 必需 / Required | 说明 / Description |
|----------------------|------------------|---------------------|
| `{width}x{height}`   | ✅ 是 / Yes       | 图片尺寸 / Image size |
| `{text}`             | ❌ 否 / No        | 显示文字 / Text to display |
| `{bg_color}`         | ❌ 否 / No        | 背景颜色 / Background color (default `cccccc`) |
| `{text_color}`       | ❌ 否 / No        | 字体颜色 / Text color (default `000000`) |

---

## 🌐 去除 index.php 的访问路径 / Remove index.php from URLs

### ✅ Nginx 重写 / Nginx Rewrite
```nginx
location / {
    try_files $uri /index.php?$args;
}
```
Ensure your `root` points to the MockImage directory, and PHP FastCGI is properly set.

### ✅ Apache 重写 / Apache .htaccess
```apacheconf
RewriteEngine On
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule ^(.*)$ index.php [QSA,L]
```
Enable `mod_rewrite` and make sure `AllowOverride All` is set.

---

## 📂 缓存策略 / Caching Strategy
- 每张图像生成后自动保存为 JPG / JPG image is cached after generation
- 缓存路径为 `/cache` 文件夹 / Stored in `/cache` folder
- 相同请求会读取缓存，提升性能 / Identical requests load from cache

---

## 🖋️ 水印说明 / Watermark
- 默认右下角显示 `tendayspace` / Shows `tendayspace` on bottom right
- 半透明字体 / Semi-transparent font

---

## 🪪 License
MIT License © 2025 [tendayspace]
