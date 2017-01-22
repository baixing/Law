# 前端第三方库管理策略

1. 临时需求
  - 建议在页面中引用公共CDN的库

2. 长期需求
  - 想要原封不动放在 `s.baixing.net/3rd` 目录。步骤如下：
    1. 在 `htdocs/assets/bower.json` 中添加依赖的 lib 地址
    1. 在 `htdocs/assets/gulpfiles/copy.js` 中声明需要编译进 `3rd/` 目录中的文件清单
    1. 在页面中引用 `s.baixing.net/3rd/` 目录下的文件。