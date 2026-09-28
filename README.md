# 玛町货运代理官网（Mading Freight Forwarding）

中国至伊拉克专线货运代理的静态官网，纯 HTML/CSS，无构建步骤，可直接部署到任何静态托管服务。

## 目录结构

```
.
├── index.html        # 中文版单页官网（首页）
├── en/
│   └── index.html    # 英文版单页官网
├── refine.css        # 中英文共用的响应式视觉样式
├── robots.txt        # 搜索引擎抓取规则
├── sitemap.xml       # 站点地图
├── _headers          # Cloudflare Pages / Netlify 响应头配置
├── .nojekyll         # 禁用 GitHub Pages 的 Jekyll 处理
└── README.md
```

## 本地预览

在项目根目录执行：

```bash
python -m http.server 4173
```

然后打开：

- 中文：`http://localhost:4173/`
- English：`http://localhost:4173/en/`

## 站点信息

- 官网定位：中国至伊拉克国际货运代理，主打"伊拉克专线"
- 首页结构：① 伊拉克专线大图 → ② 实力数字条（2007 / 5,000 m² / 53 人 / 19 年）→ ③ 核心业务（伊拉克专线、海运、空运、仓储集运）→ ④ 为什么选择玛町 → ⑤ 中国→伊拉克运输路线 → ⑥ 运输场景照片（6 图）→ ⑦ 公司介绍 → ⑧ 联系我们
- 电话：`+86 18757873636`（移动端右下角有悬浮"电话咨询"按钮）
- 域名：`www.yiwumading.com`
- 语言切换：中文版顶部切换到 `/en/`，英文版切换回 `/`
- SEO：中英文 meta description、keywords、JSON-LD LocalBusiness 结构化数据、hreflang

## 部署方式

### 方式一：GitHub Pages（最简单，免费）

1. 在 GitHub 创建仓库，把本项目推上去：

   ```bash
   git init
   git add .
   git commit -m "Initial commit: Mading website"
   git branch -M main
   git remote add origin https://github.com/<你的用户名>/<仓库名>.git
   git push -u origin main
   ```

2. 仓库 **Settings → Pages → Source** 选择 `Deploy from a branch`，分支选 `main`，目录选 `/ (root)`，保存。

3. 几分钟后站点会在 `https://<用户名>.github.io/<仓库名>/` 上线。

4. 绑定自定义域名：**Settings → Pages → Custom domain** 填入 `www.yiwumading.com`，并在域名 DNS 处添加 CNAME 记录指向 `<用户名>.github.io`。

### 方式二：Cloudflare Pages（推荐，配合自有域名）

1. 推送到 GitHub（同上）。
2. Cloudflare 控制台 → **Workers & Pages → Create → Pages → Connect to Git**，选择该仓库，构建命令留空，输出目录填 `/`。
3. 部署完成后，在项目 **Custom domains** 添加 `www.yiwumading.com`，按提示在 DNS 添加 CNAME。
4. `_headers` 文件会被 Cloudflare Pages 自动读取，附加安全响应头。

### 方式三：自有服务器（Nginx）

1. 服务器上克隆仓库或上传文件：

   ```bash
   git clone https://github.com/<你的用户名>/<仓库名>.git /var/www/mading
   ```

2. Nginx 配置示例：

   ```nginx
   server {
       listen 80;
       server_name www.yiwumading.com yiwumading.com;
       root /var/www/mading;
       index index.html;

       location / {
           try_files $uri $uri/ =404;
       }
   }
   ```

3. `nginx -t && nginx -s reload`，再把域名 DNS A 记录指向服务器 IP。

> 注意：域名若解析到中国大陆服务器需要 ICP 备案；解析到香港、新加坡等海外节点不需要。

## 待办 / 后续优化

- [ ] 将图库 URL 下载到本地 `assets/`，减少对外部图片服务的依赖
- [ ] 用真实企业 Logo 替换当前文字 M 标识
- [ ] 将真实仓库、装柜和团队照片替换到服务卡片与图片展示区域
- [ ] 域名 DNS 完成后，将 `www.yiwumading.com` 指向新的静态站点
