---
title: 如何使用 GitHub + Hexo 搭建个人博客（完整教程）
date: 2026-04-08 15:12:42
tags:
  - Hexo
  - GitHub
  - 博客
  - 教程
---

## 前言

想要拥有一个属于自己的个人博客，但又不想花钱购买服务器？GitHub + Hexo 是一个完美的解决方案！Hexo 是一个快速、简洁且高效的博客框架，配合 GitHub Pages 的免费托管服务，你可以轻松搭建一个美观、功能完善的个人博客。

本教程将手把手教你从零开始搭建自己的博客，适合完全没有基础的新手。

## 一、准备工作

### 1.1 安装 Node.js

Hexo 基于 Node.js 运行，所以首先需要安装 Node.js。

1. 访问 [Node.js 官网](https://nodejs.org/)
2. 下载 LTS（长期支持版）版本
3. 安装时一路 Next 即可
4. 打开命令行输入以下命令验证安装：
```bash
node -v
npm -v
```
显示版本号则安装成功。

### 1.2 安装 Git

Git 用于版本控制和将博客部署到 GitHub。

1. 访问 [Git 官网](https://git-scm.com/) 下载
2. 安装时保持默认选项即可
3. 验证安装：
```bash
git --version
```

### 1.3 注册 GitHub 账号

如果还没有 GitHub 账号：
1. 访问 [GitHub](https://github.com/)
2. 点击 Sign up 注册
3. 建议使用常用邮箱，方便接收通知

## 二、安装 Hexo

### 2.1 全局安装 Hexo CLI

打开命令行（Windows 用户建议使用 Git Bash 或 PowerShell），输入：

```bash
npm install -g hexo-cli
```

安装完成后验证：
```bash
hexo -v
```

### 2.2 初始化博客

选择一个合适的文件夹，执行以下命令创建博客：

```bash
# 创建博客文件夹
hexo init my-blog

# 进入博客目录
cd my-blog

# 安装依赖
npm install
```

### 2.3 本地预览博客

```bash
# 生成静态文件
hexo generate
# 或简写为
hexo g

# 启动本地服务器
hexo server
# 或简写为
hexo s
```

打开浏览器访问 `http://localhost:4000`，即可看到你的博客！

> 提示：按 `Ctrl + C` 可以停止本地服务器。

## 三、GitHub Pages 配置

### 3.1 创建仓库

1. 登录 GitHub，点击右上角的 `+` → `New repository`
2. 仓库名必须是：`你的用户名.github.io`
   - 例如：用户名是 `zhangsan`，仓库名就是 `zhangsan.github.io`
3. 选择 Public（公开）
4. 点击 `Create repository` 创建

### 3.2 配置 SSH 密钥（推荐）

使用 SSH 可以避免每次部署都输入密码。

```bash
# 检查是否已有 SSH 密钥
ls ~/.ssh

# 生成新的 SSH 密钥
ssh-keygen -t rsa -C "你的GitHub邮箱"
# 一路回车使用默认设置

# 查看公钥
cat ~/.ssh/id_rsa.pub
```

复制公钥内容，然后：
1. GitHub → Settings → SSH and GPG keys → New SSH key
2. 粘贴公钥内容，保存

验证连接：
```bash
ssh -T git@github.com
```
看到 `Hi 用户名! You've successfully authenticated` 表示成功。

## 四、部署博客到 GitHub

### 4.1 安装部署插件

在博客目录下执行：

```bash
npm install hexo-deployer-git --save
```

### 4.2 修改配置文件

打开博客目录下的 `_config.yml` 文件，找到 `deploy` 部分，修改为：

```yaml
deploy:
  type: git
  repo: git@github.com:你的用户名/你的用户名.github.io.git
  branch: main
```

> 注意：`repo` 地址可以是 HTTPS 或 SSH 格式，SSH 格式更方便。

### 4.3 部署博客

```bash
# 清除缓存
hexo clean

# 生成静态文件
hexo generate

# 部署到 GitHub
hexo deploy
# 或简写为
hexo d
```

部署完成后，访问 `https://你的用户名.github.io` 即可看到你的博客！

## 五、写作与发布

### 5.1 创建新文章

```bash
hexo new "文章标题"
# 或简写为
hexo n "文章标题"
```

文章会生成在 `source/_posts/` 目录下，文件格式为 Markdown。

### 5.2 文章格式

Hexo 文章采用 Markdown 格式，文件头部有 Front Matter：

```markdown
---
title: 文章标题
date: 2026-04-08 15:00:00
tags:
  - 标签1
  - 标签2
categories: 分类名
---

这里是正文内容...

## 一级标题

正文...

### 二级标题

更多内容...
```

### 5.3 创建新页面

```bash
hexo new page "页面名称"
```

页面会生成在 `source/页面名称/` 目录下。

### 5.4 常用命令总结

| 命令 | 简写 | 说明 |
|------|------|------|
| hexo new "title" | hexo n | 新建文章 |
| hexo generate | hexo g | 生成静态文件 |
| hexo server | hexo s | 启动本地服务器 |
| hexo deploy | hexo d | 部署到远程仓库 |
| hexo clean | - | 清除缓存 |
| hexo new page "name" | - | 新建页面 |

## 六、更换主题

Hexo 有丰富的主题资源，让博客更加美观。

### 6.1 安装主题

以安装 Next 主题为例：

```bash
# 进入博客目录
cd my-blog

# 下载主题
git clone https://github.com/next-theme/hexo-theme-next themes/next
```

### 6.2 启用主题

修改 `_config.yml` 中的 `theme` 配置：

```yaml
theme: next
```

### 6.3 更多主题推荐

- [Next](https://github.com/next-theme/hexo-theme-next) - 简洁优雅
- [Butterfly](https://github.com/jerryc127/hexo-theme-butterfly) - 功能丰富
- [Yilia](https://github.com/litten/hexo-theme-yilia) - 简约风格
- [Fluid](https://github.com/fluid-dev/hexo-theme-fluid) - Material Design 风格

## 七、进阶配置

### 7.1 绑定自定义域名

如果你有自己的域名：

1. 在 `source` 目录下创建 `CNAME` 文件，写入你的域名
2. 在域名服务商处添加 DNS 解析：
   - 类型：CNAME
   - 记录值：你的用户名.github.io
3. 在 `_config.yml` 中配置：
```yaml
url: https://你的域名
```

### 7.2 添加评论系统

常用的评论系统：
- **Gitalk**：基于 GitHub Issues
- **Valine**：基于 LeanCloud
- **Waline**：功能更完善

以 Gitalk 为例，在主题配置文件中添加相应配置即可。

### 7.3 添加统计与分析

- **百度统计**：添加百度统计代码
- **Google Analytics**：添加 Google 分析
- **不蒜子**：简单的访问量统计

### 7.4 SEO 优化

1. 安装 SEO 插件：
```bash
npm install hexo-generator-sitemap --save
npm install hexo-generator-baidu-sitemap --save
```

2. 提交站点到搜索引擎：
   - [Google Search Console](https://search.google.com/search-console)
   - [百度搜索资源平台](https://ziyuan.baidu.com/)

## 八、常见问题

### 8.1 部署失败

- 检查 SSH 配置是否正确
- 确认仓库地址配置正确
- 尝试删除 `.deploy_git` 文件夹后重新部署

### 8.2 页面样式错乱

- 执行 `hexo clean` 清除缓存
- 检查主题是否正确安装
- 确认 `_config.yml` 格式正确（注意缩进）

### 8.3 中文乱码

确保文件编码为 UTF-8，并在 `_config.yml` 中设置：
```yaml
language: zh-CN
```

### 8.4 更新 Hexo

```bash
# 查看当前版本
hexo -v

# 更新 Hexo
npm update hexo

# 更新所有依赖
npm update
```

## 九、备份博客源文件

建议将博客源文件也备份到 GitHub：

```bash
# 在博客目录初始化 git
git init

# 添加 .gitignore 文件
echo "node_modules/" > .gitignore
echo ".deploy_git/" >> .gitignore
echo "public/" >> .gitignore
echo "db.json" >> .gitignore

# 提交并推送到另一个分支
git add .
git commit -m "备份博客源文件"
git remote add origin git@github.com:你的用户名/你的用户名.github.io.git
git push origin main:source
```

这样源文件会在 `source` 分支，部署的静态文件在 `main` 分支。

## 十、总结

恭喜你完成了个人博客的搭建！现在你可以：

1. 使用 `hexo n "文章标题"` 创建新文章
2. 在 `source/_posts/` 编辑 Markdown 文件
3. 使用 `hexo s` 本地预览
4. 使用 `hexo g -d` 一键生成并部署

坚持写博客，记录学习和生活，让知识沉淀下来。Happy Blogging!

## 参考资料

- [Hexo 官方文档](https://hexo.io/zh-cn/docs/)
- [GitHub Pages 官方文档](https://docs.github.com/cn/pages)
- [Markdown 语法教程](https://markdown.com.cn/)
