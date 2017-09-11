###### TAG 创建附注标签
$ git tag -a v0.1.2 -m “0.1.2版本”

通常的git push不会将标签对象提交到git服务器，我们需要进行显式的操作：
$ git push origin v0.1.2 # 将v0.1.2标签提交到git服务器   
$ git push origin –tags # 将本地所有标签一次性提交到git服务器

###### 撤销跟踪
- 撤销git跟踪记录   
$ git rm cached README.md   
$ git add .gitignore
$ git push 
会删除对该文件的跟踪状态，也删除了远程的该文件
如果删除的是目录要带上-r
$ git rm cached .idea -r

- 本地忽略对文件的跟踪 除非远程该文件改变了或者本地撤销该标识   
$ git update-index --assume-unchanged    
$ git update-index --no-assume-unchanged
git update-index --assume-unchanged 的真正用法是这样的：   
>
>你正在修改一个巨大的文件，你先对其 git update-index --assume-unchanged，这样 Git 暂时不会理睬你对文件做的修改；
当你的工作告一段落决定可以提交的时候，重置改标识：git update-index --no-assume-unchanged，于是 Git 只需要做一次更新，这是完全可以接受的了；
提交＋推送。


#### **替换本地记录**
```
$ git fetch --all  #拉取服务端代码到本地
$ git reset --hard origin/master #强制替换本地分支代码

