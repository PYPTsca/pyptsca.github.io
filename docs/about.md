# MkDocs 完全使用教程（中文版）

## 1. MkDocs 简介

MkDocs 是一个快速、简单、优雅的静态站点生成器，专门用于构建项目文档。它使用 Markdown 格式编写文档，通过简单的配置文件即可生成美观的文档网站。

### 主要特点：
- **简单易用**：只需 Markdown 文件和简单的 YAML 配置
- **实时预览**：内置开发服务器支持实时重载
- **主题丰富**：支持多种主题，特别是 Material for MkDocs
- **部署简单**：可轻松部署到 GitHub Pages、GitLab Pages 等
- **插件系统**：支持丰富的插件扩展功能

## 2. 安装和初始化
- navigation.top    # 显示返回顶部按钮
### 2.1 安装 MkDocs

```bash
# 使用 pip 安装
pip install mkdocs

# 安装 Material 主题（推荐）
pip install mkdocs-material

# 验证安装
mkdocs --version
```

### 2.2 创建新项目

```bash
# 创建新项目
mkdocs new my-project

# 进入项目目录
cd my-project
```

项目创建后会生成以下结构：
```
my-project/
├── docs/
│   └── index.md      # 文档首页
└── mkdocs.yml        # 配置文件
```

## 3. 基本命令详解

### 3.1 开发服务器

```bash
# 启动开发服务器（默认端口 8000）
mkdocs serve

# 指定端口和地址
mkdocs serve -a 0.0.0.0:8080

# 启用严格模式（检查链接等）
mkdocs serve --strict
```

开发服务器支持：
- **实时重载**：修改文件后自动刷新浏览器
- **热重载**：CSS/JS 修改无需刷新页面
- **错误提示**：实时显示构建错误

### 3.2 构建网站

```bash
# 构建网站到 site/ 目录
mkdocs build

# 清理后重新构建
mkdocs build --clean

# 详细输出构建信息
mkdocs build --verbose
```

### 3.3 其他命令

```bash
# 创建新项目
mkdocs new [项目名称]

# 显示帮助信息
mkdocs --help
mkdocs [命令] --help

# 检查链接有效性
mkdocs build --strict
```

## 4. 配置文件详解

MkDocs 的核心是 `mkdocs.yml` 配置文件。以下是一个完整的配置示例（基于当前项目）：

```yaml
# 站点基本信息
site_name: pyptsca.github.io
site_url: https://pyptsca.github.io/
site_description: 我的个人文档站点
site_author: PYPTsca

# 主题配置（使用 Material 主题）
theme:
  name: material
  language: zh  # 中文界面
  features:
    - navigation.tabs       # 启用顶部导航选项卡
    - navigation.indexes    # 允许子目录有索引页
    - toc.integrate         # 将页面内目录集成到侧边栏
    - search.suggest        # 搜索建议
    - search.highlight      # 搜索结果高亮
    - content.code.copy     # 代码块复制按钮
    - content.action.edit   # 页面编辑链接

  # 自定义调色板
  palette:
    - scheme: default
      primary: indigo
      accent: indigo
      toggle:
        icon: material/brightness-7
        name: 切换到深色模式
    - scheme: slate
      primary: indigo
      accent: indigo
      toggle:
        icon: material/brightness-4
        name: 切换到浅色模式

  # 字体配置
  font:
    text: Roboto
    code: Roboto Mono

# 仓库信息（显示在右上角）
repo_url: https://github.com/PYPTsca/pyptsca.github.io/
repo_name: pyptsca.github.io
edit_uri: edit/main/docs/

# 版权信息
copyright: Copyright &copy; 2024 PYPTsca

# Markdown 扩展
markdown_extensions:
  - admonition
  - codehilite
  - extra
  - meta
  - toc:
      permalink: true
  - pymdownx.highlight:
      anchor_linenums: true
      line_spans: __span
      pygments_lang_class: true
  - pymdownx.inlinehilite
  - pymdownx.snippets
  - pymdownx.superfences
  - pymdownx.tabbed:
      alternate_style: true
  - pymdownx.tasklist:
      custom_checkbox: true

# 插件配置
plugins:
  - search
  - minify:
      minify_html: true
  - git-committers:
      repository: PYPTsca/pyptsca.github.io
      branch: main

# 导航配置
nav:
  - 首页: index.md
  - 关于: about.md
  - 教程:
    - 快速开始: tutorials/quickstart.md
    - 高级配置: tutorials/advanced.md
  - API 参考:
    - 概述: api/overview.md
    - 函数: api/functions.md
  - 常见问题: faq.md

# 额外配置
extra:
  social:
    - icon: fontawesome/brands/github
      link: https://github.com/PYPTsca
    - icon: fontawesome/brands/twitter
      link: https://twitter.com/username
    - icon: fontawesome/brands/telegram
      link: https://t.me/username

# 排除文件
exclude_docs: |
  /tests/
  /temp/
```

## 5. Material 主题深度配置

### 5.1 主题特性

Material 主题提供了丰富的特性，可以通过 `features` 配置启用：

```yaml
theme:
  name: material
  features:
    # 导航相关
    - navigation.tabs           # 顶部标签页导航
    - navigation.tabs.sticky    # 固定标签页
    - navigation.sections       # 章节导航
    - navigation.expand         # 可展开的导航
    - navigation.indexes        # 目录索引页
    - navigation.top            # 返回顶部按钮
    
    # 内容相关
    - content.tabs              # 内容标签页
    - content.code.copy         # 代码复制按钮
    - content.code.annotate     # 代码注释
    - content.action.edit       # 编辑按钮
    - content.action.view       # 查看源文件
    
    # 搜索相关
    - search.suggest            # 搜索建议
    - search.highlight          # 搜索结果高亮
    - search.share              # 分享搜索结果
    
    # 其他
    - toc.integrate             # 集成目录
    - toc.follow                # 目录跟随滚动
    - header.autohide           # 自动隐藏标题栏
    - announce.dismiss          # 可关闭的公告
```

### 5.2 自定义样式

创建 `docs/stylesheets/extra.css` 文件来自定义样式：

```css
/* 自定义主色调 */
:root {
  --md-primary-fg-color: #4051b5;
  --md-primary-fg-color--light: #5d6cc0;
  --md-primary-fg-color--dark: #303fa1;
  --md-accent-fg-color: #ff4081;
}

/* 自定义代码块样式 */
.highlight .hll { background-color: #ffc; }
.highlight .c { color: #999; }
.highlight .err { color: #a00; }

/* 自定义表格样式 */
.md-typeset table:not([class]) {
  font-size: .64rem;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0,0,0,.1);
}

/* 自定义警告框样式 */
.admonition {
  border-radius: 8px;
  border-left-width: 4px;
}
```

在 `mkdocs.yml` 中引用自定义样式：

```yaml
extra_css:
  - stylesheets/extra.css
```

## 6. 页面组织和导航

### 6.1 页面结构

推荐的文件组织方式：

```
docs/
├── index.md              # 首页
├── about.md              # 关于页面
├── getting-started/      # 入门指南
│   ├── index.md
│   ├── installation.md
│   └── configuration.md
├── guides/               # 指南
│   ├── advanced.md
│   └── best-practices.md
├── api/                  # API 文档
│   ├── index.md
│   ├── module-a.md
│   └── module-b.md
├── examples/             # 示例
│   ├── basic.md
│   └── advanced.md
└── images/               # 图片资源
    ├── logo.png
    └── screenshots/
```

### 6.2 导航配置技巧

```yaml
nav:
  # 简单页面
  - 首页: index.md
  - 关于: about.md
  
  # 分组页面
  - 入门指南:
    - 简介: getting-started/index.md
    - 安装: getting-started/installation.md
    - 配置: getting-started/configuration.md
  
  # 嵌套分组
  - 用户指南:
    - 基础使用:
      - 创建页面: guides/basic/creating-pages.md
      - 添加图片: guides/basic/adding-images.md
    - 高级功能:
      - 自定义主题: guides/advanced/custom-themes.md
      - 使用插件: guides/advanced/using-plugins.md
  
  # 外部链接
  - 相关资源:
    - GitHub 仓库: https://github.com/username/project
    - 在线演示: https://demo.example.com
    - 问题反馈: https://github.com/username/project/issues
```

### 6.3 页面元数据

在 Markdown 文件顶部添加元数据：

```yaml
---
title: 页面标题
description: 页面描述
date: 2024-01-01
tags:
  - 标签1
  - 标签2
---
```

## 7. Markdown 扩展功能

### 7.1 警告框（Admonitions）

```markdown
!!! note "注意"
    这是一个注意提示。

!!! warning "警告"
    这是一个警告提示。

!!! danger "危险"
    这是一个危险提示。

!!! success "成功"
    这是一个成功提示。

!!! info "信息"
    这是一个信息提示。

!!! tip "提示"
    这是一个提示。
```

### 7.2 代码块增强

````markdown
```python title="示例代码" linenums="1"
def hello_world():
    """打印 Hello World"""
    print("Hello, World!")
    
    # 这是一个注释
    return True
```
````

### 7.3 标签页（Tabs）

````markdown
=== "Python"
    ```python
    print("Hello from Python!")
    ```

=== "JavaScript"
    ```javascript
    console.log("Hello from JavaScript!");
    ```

=== "Bash"
    ```bash
    echo "Hello from Bash!"
    ```
````

### 7.4 任务列表

```markdown
- [x] 已完成的任务
- [ ] 未完成的任务
- [ ] 另一个任务
```

### 7.5 数学公式

```markdown
$$
\frac{n!}{k!(n-k)!} = \binom{n}{k}
$$

行内公式：$E = mc^2$
```

### 7.6 属性列表

```markdown
[链接文字]{: .button .primary target="_blank" }

![图片描述](image.png){: .shadow width="100%" }

这是一个普通段落。
{: .notice .warning}
```

## 8. 部署到 GitHub Pages

### 8.1 手动部署

```bash
# 构建网站
mkdocs build

# 部署到 GitHub Pages
mkdocs gh-deploy
```

### 8.2 自动部署（GitHub Actions）

创建 `.github/workflows/deploy.yml`：

```yaml
name: Deploy to GitHub Pages

on:
  push:
    branches:
      - main
      - master
  pull_request:
    branches:
      - main
      - master

jobs:
  deploy:
    runs-on: ubuntu-latest
    permissions:
      contents: write
    steps:
      - uses: actions/checkout@v4
      
      - name: Setup Python
        uses: actions/setup-python@v5
        with:
          python-version: '3.x'
          
      - name: Install dependencies
        run: |
          python -m pip install --upgrade pip
          pip install mkdocs mkdocs-material
          
      - name: Build site
        run: mkdocs build
        
      - name: Deploy to GitHub Pages
        if: github.ref == 'refs/heads/main' || github.ref == 'refs/heads/master'
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./site
          publish_branch: gh-pages
```

### 8.3 自定义域名

1. 在 `mkdocs.yml` 中配置：
```yaml
site_url: https://docs.example.com/
```

2. 在 GitHub Pages 设置中添加自定义域名
3. 在域名服务商处配置 CNAME 记录

## 9. 插件系统

### 9.1 常用插件

```yaml
plugins:
  # 搜索插件（默认启用）
  - search
  
  # 图片懒加载
  - lazy-load-images
  
  # Git 提交者信息
  - git-committers:
      repository: username/repo
      branch: main
      
  # 站点地图生成
  - sitemap:
      sitemap_url: https://example.com/sitemap.xml
      
  # RSS 订阅
  - rss:
      match_path: ".*\.md"
      
  # 离线搜索
  - offline-search
  
  # 代码高亮
  - highlight:
      linenums: true
      
  # 目录生成
  - awesome-pages:
      filename: .pages
      
  # 最小化
  - minify:
      minify_html: true
      minify_js: true
      minify_css: true
```

### 9.2 自定义插件开发

创建 `plugins/my_plugin.py`：

```python
from mkdocs.plugins import BasePlugin
from mkdocs.config import config_options

class MyPlugin(BasePlugin):
    config_scheme = (
        ('enabled', config_options.Type(bool, default=True)),
    )
    
    def on_page_markdown(self, markdown, page, config, files):
        if self.config['enabled']:
            # 处理 Markdown 内容
            markdown = markdown.replace('旧文本', '新文本')
        return markdown
    
    def on_page_content(self, html, page, config, files):
        # 处理 HTML 内容
        return html
```

在 `mkdocs.yml` 中启用：

```yaml
plugins:
  - my_plugin:
      enabled: true
```

## 10. 最佳实践和常见问题

### 10.1 最佳实践

1. **版本控制**：将 `docs/` 目录和 `mkdocs.yml` 加入版本控制
2. **图片管理**：使用相对路径引用图片，统一放在 `docs/images/` 目录
3. **链接检查**：定期使用 `mkdocs build --strict` 检查链接
4. **备份配置**：备份自定义的 CSS 和插件配置
5. **文档测试**：为重要功能编写示例代码

### 10.2 常见问题

**Q: 如何解决中文搜索问题？**
A: 安装 `jieba` 分词库：
```bash
pip install jieba
```
在 `mkdocs.yml` 中配置：
```yaml
plugins:
  - search:
      lang: zh
```

**Q: 如何添加评论系统？**
A: 使用 Giscus 或 Utterances：
```html
<!-- 在 extra.html 中添加 -->
<script src="https://giscus.app/client.js"
        data-repo="username/repo"
        data-repo-id="..."
        data-category="..."
        data-category-id="..."
        data-mapping="pathname"
        data-strict="0"
        data-reactions-enabled="1"
        data-emit-metadata="0"
        data-input-position="bottom"
        data-theme="preferred_color_scheme"
        data-lang="zh-CN"
        crossorigin="anonymous"
        async>
</script>
```

**Q: 如何添加分析统计？**
A: 使用 Google Analytics 或 Umami：
```yaml
extra:
  analytics:
    provider: google
    property: G-XXXXXXXXXX
```

**Q: 如何优化网站性能？**
A:
1. 启用 `minify` 插件压缩资源
2. 使用 CDN 加速静态资源
3. 优化图片大小和格式
4. 启用浏览器缓存

### 10.3 调试技巧

```bash
# 详细调试输出
mkdocs serve --verbose

# 检查配置
mkdocs build --strict

# 查看生成的 HTML
find site/ -name "*.html" | head -5

# 检查链接
python -c "import mkdocs; print(mkdocs.__version__)"
```

## 11. 进阶功能

### 11.1 多语言支持

```yaml
# mkdocs.yml
theme:
  name: material
  language: zh
  
plugins:
  - i18n:
      default_language: zh
      languages:
        zh: 中文
        en: English
        
# 创建多语言目录
docs/
├── zh/
│   ├── index.md
│   └── about.md
└── en/
    ├── index.md
    └── about.md
```

### 11.2 API 文档自动生成

使用 `mkdocstrings` 插件：

```bash
pip install mkdocstrings-python
```

```yaml
plugins:
  - mkdocstrings:
      handlers:
        python:
          options:
            docstring_style: google
            show_source: true
```

### 11.3 版本化文档

```yaml
plugins:
  - mike:
      version_selector: true
      alias_type: symlink
      
# 发布新版本
mike deploy 1.0 latest
mike set-default latest
```

## 12. 资源推荐

### 12.1 官方资源
- [MkDocs 官方文档](https://www.mkdocs.org/)
- [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/)
- [MkDocs 插件目录](https://github.com/mkdocs/mkdocs/wiki/MkDocs-Plugins)

### 12.2 社区资源
- [Awesome MkDocs](https://github.com/mkdocs/awesome-mkdocs)
- [MkDocs 中文社区](https://github.com/mkdocs-cn)
- [Material 主题示例](https://squidfunk.github.io/mkdocs-material/examples/)

### 12.3 工具推荐
- [Typora](https://typora.io/) - Markdown 编辑器
- [Draw.io](https://draw.io/) - 图表绘制
- [Carbon](https://carbon.now.sh/) - 代码截图
- [Mermaid Live Editor](https://mermaid.live/) - 流程图绘制

---

**最后更新：2024年1月**

这个教程涵盖了 MkDocs 的各个方面，从基础安装到高级配置。建议根据实际需求选择适合的功能进行配置。如有问题，请参考官方文档或社区资源。

祝你使用愉快！ 🚀