### 版本控制 多人开发工具

工作区-->	暂存区-->	本地库-->	远程库
.gitignore 忽略上传文件

## 新电脑推送到push

- 前置准备
  - git软件，git在线网站，创建远程库
  - 安装配置ssh登录，配置本地设置
    ```git
    git config --global user.name "musaly"
    git config --global user.email "942273632@qq.com"
    ssh-keygen -t rsa -C "942273632@qq.com"
    cat ~/.ssh/id_rsa.pub

    ```
  - 
  - 查看是否有历史用户登录记录
- 初始化到本地库
- 连接远程库
  - `git remote add origin https://gitee.com/musaly/blog.git`
  - 
- 推送到远程库
  - git push -u origin git分支名(master)
  - git push -u origin master
  - https://gitee.com/musaly/rc.git
  - http://gitlabnew.dtsum.com/musaly/rc.git


## 分支合并提交
- `git add .`提交缓存区
- `git commit -m  '登录功能'`提交本地库
- `git checkout master`切换到合并后分支
- `git merge login`合并分支
- `git push`推送到git
- 
- `git checkout -b user`创建切换到分支
- 
## 推送分支
- `git checkout login`切换到分支
- 第一次
  - `git push -u origin git分支名`创建远程分支并推送
    - `git push -u origin login ` 
- `git push --mirror https://gitee.com/musaly/ant-design-vue-jeecg.git`
- `git push --mirror https://gitee.com/musaly/jx.git`
## 

```
git config 
git remote add 别名 http地址
git remote add origin https://gitee.com/musaly/jx.git

C:\Users\**name**\.gitconfig			#查看配置方式

git init					#初始化本地库
git status					#查看本地库状态
git rm --cached file				#从暂存区删除文件
git commit -m "版本信息" git.txt		#提交本地库
git reflog					#查看精简版本号
git log					#查看详细版本号
cat file					#查看文件
git reset --hard 版本编号			#版本穿梭

git branch b.name				#创建分支
git checkout -b login				# 创建分支并且切换改分支

git branch -v				#查看分支
git branch 				#查看所有分支和当前分支
git checkout b.name				#切换分支
git merge b.name				#合并到当前文件上
{冲突合并:	}

团队内协作	跨团队协作 fork

git remote -v				#查看远程库别名
git remote add 别名 http地址			#创建别名
git push 别名|地址 分支			#推送分支到远程库
git clone git@gitee.com:zpf_fronten/git-new.git	#下载

ssh-keygen -t rsa -C "邮箱"
cat ~/.ssh/id_rsa.pub
```


## github加速访问
- vpn
- UU加速器.学术资源加速


