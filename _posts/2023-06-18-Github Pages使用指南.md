# Github Pages 使用指南

Github Pages 是一个免费的静态网站托管服务，它允许你通过简单的几个步骤就可以把你的项目、博客或者个人网站托管在 Github 上。在这篇文章中，我们将详细介绍如何使用 Github Pages 服务来建立和部署你的第一个静态网站。

## 一、创建 Github 账户

首先，你需要一个 Github 账户。如果你还没有，请访问 [Github 官网](https://github.com/) 注册一个新账户。

## 二、创建仓库

1. 登录到你的 Github 账户，点击右上角的 "+" 按钮，然后选择 "New repository"。

   ![创建仓库](https://docs.github.com/assets/images/help/repository/repo-create.png)

2. 为新仓库起一个名字。如果你想要创建一个个人网站，那么仓库的名称必须是 `yourusername.github.io`（将 `yourusername` 替换为你的 Github 用户名）。如果你想要创建一个项目网站，可以为仓库起一个与项目相关的名字。

3. 选择 "Public"（公开）作为仓库的可见性，并勾选 "Initialize this repository with a README"（用 README 初始化此仓库），然后点击 "Create repository"。

   ![命名仓库](https://docs.github.com/assets/images/help/repository/create-repository-public.png)

## 三、为仓库添加内容

1. 进入你刚刚创建的仓库，点击 "Add file"（添加文件）按钮，选择 "Create new file"（创建新文件），创建一个名为 `index.html` 的文件。

   ![创建文件](https://docs.github.com/assets/images/help/repository/create_new_file.png)

2. 在 `index.html` 文件的编辑器中，输入以下 HTML 代码：

   ````html
   <!DOCTYPE html>
   <html lang="zh-CN">
   <head>
     <meta charset="UTF-8">
     <meta name="viewport" content="width=device-width, initial-scale=1.0">
     <title>欢迎来到我的 Github Pages 网站</title>
   </head>
   <body>
     <h1>欢迎来到我的 Github Pages 网站</h1>
     <p>这是一个简单的示例页面。</p>
   </body>
   </html>
   ```

3. 点击 "Commit new file"（提交新文件），将 `index.html` 文件添加到仓库中。

## 四、启用 Github Pages
### 默认配置
1. 进入仓库的 "Settings"（设置）选项卡，滚动到 "GitHub Pages" 部分。

   ![Github Pages 设置](https://docs.github.com/assets/images/help/pages/pages-settings.png)

2. 在 "Source"（来源）下拉菜单中选择 "main" 分支，然后点击 "Save"（保存）按钮。

   ![启用 Github Pages](https://docs.github.com/assets/images/help/pages/select-main-as-source.png)

3. 页面将自动刷新，滚动回到 "GitHub Pages" 部分。你会看到一个绿色的提示框，显示 "Your site is published at [yourusername.github.io](https://yourusername.github.io)"（你的网站发布在 [yourusername.github.io](https://yourusername.github.io)）。

   ![发布成功](https://docs.github.com/assets/images/help/pages/pages-success.png)

### 使用 Github Actions 配置和部署 Github Pages

在本节中，我们将介绍如何使用 Github Actions 配置和部署你的 Github Pages 网站。Github Actions 是一种自动化工具，它可以帮助你自动构建、测试和部署你的代码。接下来，我们将创建一个简单的 Github Actions 工作流程来部署我们的 Github Pages 网站。

#### 1. 创建工作流文件

在你的仓库根目录下，创建一个名为 `.github/workflows` 的文件夹。然后，在这个文件夹中创建一个名为 `deploy.yml` 的文件。你的仓库结构应该如下：

```
your_repository/
  |-- .github/
  |     |-- workflows/
  |           |-- deploy.yml
  |-- index.html
  |-- README.md
```

#### 2. 编写 Github Actions 工作流配置

打开 `deploy.yml` 文件，将以下 YAML 代码复制到其中：

```yaml
name: Deploy to Github Pages

on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout repository
      uses: actions/checkout@v2
      
    - name: Setup Node.js
      uses: actions/setup-node@v2
      with:
        node-version: 14

    # 可选：在此处添加构建步骤，例如安装依赖、运行构建命令等。
    # - name: Install dependencies
    #   run: npm ci
    # - name: Build
    #   run: npm run build

    - name: Deploy to Github Pages
      uses: peaceiris/actions-gh-pages@v3
      with:
        github_token: ${{ secrets.GITHUB_TOKEN }}
        publish_dir: ./ # 将此更改为你的构建输出目录，例如：./dist
```

这个工作流配置的主要步骤如下：

1. 当代码推送到 `main` 分支时，触发工作流。
2. 使用 `ubuntu-latest` 作为运行环境。
3. 检出仓库代码。
4. 设置 Node.js 环境（可根据你的项目需要调整版本）。
5. （可选）添加构建步骤，例如安装依赖、运行构建命令等。
6. 使用 `peaceiris/actions-gh-pages` Github Action 部署到 Github Pages。

#### 3. 提交更改

将 `.github` 文件夹添加到仓库，并提交更改：

```
git add .github
git commit -m "Add Github Actions workflow"
git push origin main
```

#### 4. 查看 Github Actions 运行结果

提交更改后，转到你的仓库页面，点击 "Actions" 选项卡，你应该能看到一个正在运行或已完成的工作流。点击工作流名称，查看详细信息和运行结果。

![Github Actions 运行结果](https://docs.github.com/assets/images/help/repository/actions-tab.png)

#### 5. 访问 Github Pages 网站

如果 Github Actions 工作流运行成功，你的 Github Pages 网站应该已经更新并部署。访问 `https://yourusername.github.io`（将 `yourusername` 替换为你的 Github 用户名）来查看你的网站。

现在，每当你将更改推送到 `main` 分支时，Github Actions 都会自动构建和部署你的 Github Pages 网站。你可以根据你的项目需求自定义工作流配置，例如添加构建步骤、运行测试等。更多关于 Github Actions 的信息，请参考 [官方文档](https://docs.github.com/en/actions)。

## 五、访问你的 Github Pages 网站

现在，你可以通过访问 `https://yourusername.github.io`（将 `yourusername` 替换为你的 Github 用户名）来查看你的 Github Pages 网站。

## 六、自定义域名（可选）

如果你想要为你的 Github Pages 网站使用自定义域名，可以参照 [Github 官方文档](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site) 进行设置。

## 总结

现在你已经成功创建了一个 Github Pages 网站。你可以随时更新你的网站内容，只需将更改提交到仓库的 "main" 分支上即可。随着你对 Github Pages 的熟悉，你还可以尝试使用 [Jekyll](https://jekyllrb.com/) 等静态站点生成器来构建更复杂的网站。
