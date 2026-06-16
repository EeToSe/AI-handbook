
## 一、本地部署

新建项目目录并进入目录：

```bash
mkdir ai-handbook
cd ai-handbook
```

安装 MkDocs 和 Material 主题：

```bash
pip install mkdocs mkdocs-material
```

初始化 MkDocs 项目， 本地预览：

```bash
mkdocs new .
mkdocs serve
```

启动后访问 http://127.0.0.1:8000/


## 二、GitHub Pages 自动部署

### 1. 推送到 GitHub

先在 GitHub 新建仓库，例如：

```text
ai-handbook
```

然后本地执行：

```bash
git init
git add .
git commit -m "init mkdocs material site"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/ai-handbook.git
git push -u origin main
```

### 2. 添加 GitHub Actions

新建文件：

```text
.github/workflows/ci.yml
```

内容如下：

```yaml
name: ci

on:
  push:
    branches:
      - main

permissions:
  contents: write

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: Configure Git Credentials
        run: |
          git config user.name github-actions[bot]
          git config user.email 41898282+github-actions[bot]@users.noreply.github.com

      - uses: actions/setup-python@v5
        with:
          python-version: 3.x

      - name: Install dependencies
        run: pip install mkdocs-material

      - name: Deploy
        run: mkdocs gh-deploy --force
```


### 3. GitHub Pages 设置

第一次 push 后，进入 GitHub 仓库：

```text
Settings -> Pages -> Build and deployment
```

选择：

```text
Source: Deploy from a branch
Branch: gh-pages
Folder: /root
```

访问地址 https://<你的GitHub用户名>.github.io/<仓库名>/
