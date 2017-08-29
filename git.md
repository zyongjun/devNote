###### TAG 创建附注标签
$ git tag -a v0.1.2 -m “0.1.2版本”

通常的git push不会将标签对象提交到git服务器，我们需要进行显式的操作：
$ git push origin v0.1.2 # 将v0.1.2标签提交到git服务器   
$ git push origin –tags # 将本地所有标签一次性提交到git服务器

###### 撤销跟踪
- 撤销git跟踪记录   
$ git rm cached README.md   
$ git push 
- 本地忽略对文件的跟踪 除非远程该文件改变了或者本地撤销该标识   
$ git update-index --assume-unchanged    
$ git update-index --no-assume-unchanged

bbbb
