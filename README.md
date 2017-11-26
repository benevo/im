# im
blog on github


# Start

```bash
~ # git clone --branch hexo https://github.com/benevo/im.git
~ # cd im
~ # npm install hexo
~ # npm install
~ # hexo s
# open http://localhost:4000/
```


# Plugins dependencies:

[hexo-admin](https://github.com/jaredly/hexo-admin)：
```bash
~ # npm install --save hexo-admin
~ # hexo server -d
# open http://localhost:4000/admin/
```

[Livereload](http://www.hahack.com/codes/livereload-for-hexo/#more)：
```bash
~ # npm install -g node-livereload
~ # livereload -e ".md, .html, .png, .svg, .jpg, .gif, .css, .js, .json" -p <hexo workpath>
```
chrome需安装插件livereload，在需要的实时刷新的页面点击一下该扩展按钮

[hexo-editor](https://github.com/tajpure/hexo-editor)：
```bash
~ # git clone https://github.com/tajpure/hexo-editor.git
~ # cd hexo-editor
~ # npm install --production
~ # npm start
# open http://localhost:2048/
```