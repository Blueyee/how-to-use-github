GitHub使用教程 

【首次创建仓库】

Part A：[创建本地Git仓库]

1.在本地创建一个文件夹作为本地的git仓库

2.cmd进入仓库路径，git init 将这个文件夹变成git可管理的仓库，这时多了个隐藏的.git文件夹，它是Git用来跟踪和管理版本库的

3.可以把文件、项目粘贴到这个本地Git仓库里面，git status查看你当前的状态，git add * 把*添加至仓库，git add .把该目录下的所有文件添加到仓库

4.git commit -m "注释内容"把项目提交到仓库

Part B：[连接远程仓库（连接Github）]

由于本地Git仓库和Github仓库之间的传输是通过SSH加密的，所以连接时需要设置一下

5.创建SSH KEY。先看一下你C:/user/username目录下有没有.ssh目录（默认是隐藏文件夹），有的话看下里面有没有id_rsa和id_rsa.pub这两个文件，有就跳到下一步，没有就通过下面命令创建
ssh -keygen -t rsa -C "youremail@example.com"
然后一路回车,这时就会在C:/user/username下的.ssh目录里找到id_rsa和id_rsa.pub这两个文件

6：登录Github,找到右上角的图标，打开点进里面的Settings，再选中里面的SSH and GPG KEYS，点击右上角的New SSH key，然后Title里面随便填，再把刚才id_rsa.pub里面的内容复制到Title下面的Key内容框里面，最后点击Add SSH key，这样就完成了SSH Key的加密

7.第七步：在Github上创建一个Git仓库，点New repository来创建，为了方便尽量名称和本地仓库一致

8.将GitHub仓库和本地仓库进行关联，根据创建好的Git仓库页面的提示，找到这个仓库的SSH，形如https://github.com/你的GitHub用户名/这个仓库名.git， 然后在本地仓库的命令行输入：git remote add origin https://github.com/你的GitHub用户名/这个仓库名.git

9.上一步将本地git仓库和GitHub仓库关联之后，就可以通过这个关联将本地Git仓库的内容推送到GitHub仓库上了，git push -u origin master，加上-u这个参数是因为新建的远程仓库是空的。等远程仓库里面有了内容之后，下次再从本地库上传内容就去掉这个参数，git push origin master

10.这时候你再重新刷新你的Github页面进入刚才新建的那个仓库里面就会发现项目已经成功上传了
注意：第7步创建远程仓库的时候，如果你勾选了Initialize this repository with a README（就是创建仓库的时候自动给你创建一个README文件），那么到了第9步你将本地仓库内容推送到远程仓库的时候就会报一个failed to push some refs to  https://github.com/**/***.git 的错。这是由于你新创建的那个仓库里面的README文件不在本地仓库目录中，这时我们可以通过以下命令先将内容合并以下：git pull --rebase origin master，再push就能成功了


以上是首次创建的完整步骤。

【再次创建仓库】

SSH加密的步骤只需要一次，因此再次创建仓库的话第5步，第六步需要跳过，其他类似

【日常更新】

将本地仓库的更新内容更新至GitHub
进入本地仓库路径
1.git status查看当前状态，可以时不时查看一下，红色表示本地文件的被修改或加入的新文件，但此时只是放在这个路径下并没有添加进仓库，下一步git add过后git status 绿色表示已添加进本地的Git仓库，但并没有push进GitHub仓库。

2.修改本地文件，或拖进去新的文件（注意此时还未加入这个仓库，需要下面的命令add进去），git status查看当前状态，git add . 添加所有新的文件，或git add * 将单个文件*加进去，git status

3.用注释内容描述此次更新，和后面会和新文件一起push进去，命令 git commit -m "注释内容”，没有这步的话会连接失败

4.git push origin master将更新的文价和commit一起push到GitHub仓库。


【GitHub仓库的更新同步到本地git仓库】

git pull --rebase origin master


