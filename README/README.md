# MyBlog 安装与配置
```bash
npm install
```

## 安装 [yilia](https://github.com/litten/hexo-theme-yilia) themes
```bash
git clone https://github.com/litten/hexo-theme-yilia.git themes/yilia
```

配置 _config.yml

## 添加 sitemap 和 feed 插件
```bash
npm install hexo-generator-feed --save
npm install hexo-generator-sitemap --save
npm install hexo-generator-baidu-sitemap --save
```
修改_config.yml (根目录，非 themes 中)，增加以下内容
```yaml
# Extensions
Plugins:
- hexo-generator-feed
- hexo-generator-sitemap

#Feed Atom
feed:
  type: atom
  path: atom.xml
  limit: 20

#sitemap
sitemap:
  path: sitemap.xml
baidusitemap:
  path: baidusitemap.xml
```
配完之后，就可以访问 `http://jiji262.github.io/atom.xml` 和
 `http://jiji262.github.io/sitemap.xml`，发现这两个文件已经成功生成了。
## 生成静态文件
```bash
hexo generate
```

## 开启本地服务
```bash
hexo server
```

## 发布(Generate before deployment)
```bash
hexo deploy -g
```

## 在 hexo 中无痛使用本地图片
```bash
npm install https://github.com/CodeFalling/hexo-asset-image --save
```
`_config.yml` 中有 `post_asset_folder:true`

## 使用 不算子 添加网站访问计数
在 `themes/your themes/layout/_partial/footer.ejs` 底部加入这段脚本
```html
<script async src="//dn-lbstatics.qbox.me/busuanzi/2.3/busuanzi.pure.mini.js">
</script>
```
之后任意位置添加
```html
<span id="busuanzi_container_page_pv">
    本文总阅读量<span id="busuanzi_value_page_pv"></span>次
</span>
```