title: MAC环境下SVN的使用
date: 2015-01-22 20:55:10
tags:
---
###MAC环境下SVN的使用
1.创建代码仓库,用来存储客户端所上传的代码

     在/User/apple目录下新建一个svn目录,以后可以在svn目录下创建多个仓库目录
     打开终端,创建一个mycode仓库,输入指令 :svnadmin create /Users/apple/svn/mycode
2.配置svn的用户权限
   
    主要是修改/svn/myceode/conf目录下的三个文件
      1.打开svnserve.conf,将下列配置项前面的#和空格都去掉
		  anon-access = read 代表匿名访问的时候是只读的,若改为anon-access = none 代表禁止匿名访问,需要账号密码才能访问
		
      2.  打开passwd,在[users]下面添加账号和密码账号是mj,密码是123
      
      3.打开authz,配置用户组和权限
      
     	我们可以将在passwd里添加的用户分配到不同的用户,就可以对不同的用户设置不同权限.
     	在[groups]下面添加组名和用户名,多个用户之间用逗号隔开
	 	说明mj和jj都是属于topgroup这个组的,接下来在进行权限配置使用[/]代表svn服务器中的所有资源库
		上面的配置说明topgroup这个组中的所有用户对所有资源库都有读写(r/w)权限,组名前面要用@
		如果使用户名,不用加@,比如mj这个用户有读写权限
	
	4.启动svn服务器
	        
    	在终端输入下列指令:svnserve -d -r /Users/apple/svn 或者输入:svnserve -d -r /Users/apple/svn
          5.关闭svn服务器

          如果你想要关闭svn服务器,最有效的办法是打开实用工具里面的活动监控器.
          
3.使用svn客户端功能
	
	1.从本地导入代码到服务器(第一次初始化导入)
	在终端输入:svn import /Users/apple/Documents/eclipse_workspace/weibo svn://localhost/mycode/weibo — username=mj —passed =123 -m “初始化导入”   
    意思是:将svn import /Users/apple/Documents/eclipse_workspace/weibo 中所有内容,上传到服务器my code仓库的weibo目录下,后面双引号中的”初始化导入”是注释.
    2.从服务器端下载代码到客户端本地
    在终端中输入svn checkout svn://localhost/mycode — username=mj — password=123 /Users/apple/Document/code 
    意思:将服务器中的mycode仓库的内容下载到/Users/apple/Documents/code目录中
    3.提交更改过的代码到服务器
    将服务器端的代码都下载到/Users/apple/Documents/code目录中,现在可以修改里面的代码,然后提交这些修改到服务器
       1> 打开终端,先定位到/Users/apple/Documents/code目录,输入:cd /Users/apple/Documents/code
       2> 输入提交指令:svn commit -m “修改了main.m “文件
     	这个指令会将/Users/apple/Documents/code下的所有修改都同步到服务器端,例如:只修改了main.m文件,可以看到终端的打印信息:
     4.更新服务器端的代码到客户端
       在终端中定位到客户端代码目录后,比如上面的/Users/apple/Document/code目录,然后再输入指令:svn update
     5.至于svn的其他用法,可以在终端输入:svn help
     这里列出一大堆svn指令,后面括号中的内容一般代表着指令的简称,例如:我们可以用svn ci代替svn commit 用svn co 代替 svn checkout
