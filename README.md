# MockImage

![License](https://img.shields.io/badge/license-MIT-green)
![PHP](https://img.shields.io/badge/php-%3E=8.0-blue)
![Made by tendayspace](https://img.shields.io/badge/made%20by-tendayspace-blueviolet)
![GitHub stars](https://img.shields.io/github/stars/tendayspace/MockImage?style=social)


**MockImage** 是一个用 PHP 8 编写的本地占位图（Placeholder Image）生成器，灵感来源于 [dummyimage.com](https://dummyimage.com/)，支持动态尺寸、背景颜色、文字颜色、文本内容，并自动缓存为 JPG 图像，右下角附加 "tendayspace" 水印。

---

## 🚀 快速开始

### ✅ 环境需求
- PHP 8.0+
- GD 扩展启用（默认启用）

### 📁 文件结构
```
mockimage/
├── index.php           # 主入口文件
├── cache/              # 自动生成的缓存图像
├── arial.ttf           # 字体文件（需手动放置）
├── README.md
├── LICENSE
└── .gitignore
```

### 📦 安装步骤
```bash
# 克隆项目
$ git clone https://github.com/yourname/mockimage.git
$ cd mockimage

# 准备字体文件（例如从系统复制）
$ cp /usr/share/fonts/truetype/dejavu/DejaVuSans-Bold.ttf arial.ttf

# 创建缓存目录
$ mkdir cache && chmod 777 cache
```

---

## 🔍 使用示例

```
http://yourdomain.com/{width}x{height}/{text}/{bg_color}/{text_color}
```

### 示例链接：
| 链接 | 说明 |
|------|------|
| `/600x400` | 默认灰底黑字，显示文字为 `600x400` |
| `/400x300/Hello` | 灰底黑字，显示文字为 `Hello` |
| `/300x300/Hi/000/fff` | 黑底白字，显示文字为 `Hi` |

---

## ⚙️ 参数说明
| 参数         | 是否必需 | 说明                             |
|--------------|----------|----------------------------------|
| `{width}x{height}` | ✅       | 图片尺寸                           |
| `{text}`           | ❌       | 显示文字，默认显示尺寸值               |
| `{bg_color}`       | ❌       | 背景色（默认 `cccccc`）               |
| `{text_color}`     | ❌       | 字体颜色（默认 `000000`）             |

---

## 🌐 去除 index.php 的访问路径

### ✅ Nginx 重写设置
在你的 `server` 配置中加入：
```nginx
location / {
    try_files $uri /index.php?$args;
}
```
确保 `root` 指向 MockImage 项目目录，PHP FastCGI 配置正常。

### ✅ Apache 设置（.htaccess）
在项目根目录添加 `.htaccess` 文件：
```apacheconf
RewriteEngine On
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule ^(.*)$ index.php [QSA,L]
```
确保 Apache 开启了 `mod_rewrite` 模块，并允许 `.htaccess` 重写（`AllowOverride All`）。

---

## 📂 缓存策略
- 每张图像生成后自动保存为 `.jpg` 文件
- 存储于 `/cache` 文件夹中，命名包含尺寸、颜色和文字哈希
- 后续访问相同参数时直接读取缓存，加速响应

---

## 🖋️ 水印说明
- 默认右下角显示 `tendayspace` 标志
- 字体颜色较淡（半透明）

---

## 🪪 License
MIT License © 2025 [tendayspace]
