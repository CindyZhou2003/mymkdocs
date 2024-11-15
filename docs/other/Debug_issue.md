# Mkdocs网站部署时的问题

1. 图片用图片相对路径无法成功解析：`mkdocs.yml`中加一行：`use_directory_urls: false` 

2. 网站部署过程中，参考多个`.github/workflows/main.yml`文件没问题，action也成功，但是404：要建立两个分支，docs文件夹+`mkdocs.yml`上传到`master(default)`分支，保留`gh-deploy`分支，部署时网站（本地`mkdocs build`生成的`site`文件夹）就在`gh-deploy`分支下，这样就能加载资源了

   官方：<https://squidfunk.github.io/mkdocs-material/publishing-your-site/#with-github-actions-material-for-mkdocs>

