# im
blog on github

# Description:
...

# Start:

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
# 支持图片黏贴上传，不支持图片文件上传
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
# 支持图片文件上传，不支持图片黏贴上传
```

安装上述插件后，在hexo工作目录下执行以下脚本，可以实时预览，实时修改：
```shell
#!/bin/bash
# description: livereload + hexo + markdown

HexoEditorDir=/Users/wall-e/web/hexo/hexo-editor
WatchPath=$1

if [ ! -x "$1" ]; then
        echo "Usage: ihexo <hexo project path>"
        exit 1
fi

cd $1
#hexo clean  # Clean cache

#livereload -e ".md, .html, .png, .svg, .jpg, .gif, .css, .js, .json" | hexo server --debug
npm start --prefix $HexoEditorDir > $HexoEditorDir/he.log | livereload -p $WatchPath -e ".md, .html, .png, .svg, .jpg, .gif, .css, .js, .json" > $WatchPath/livereload.log | hexo s
```
可用另存为 ihexo 文件，并放到 PATH 目录下，然后 简单 执行： `ihexo <hexo project path>`

日志文件路径：

- livereload： ${WatchPath}/livereload.log
- hexo-editor: ${<HexoEditorDir}/he.log