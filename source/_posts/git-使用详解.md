title: git 使用详解
date: 2014-10-23 21:05:49
tags:
---
1. git是什么？
	
		Git是一个开源的分布式版本控制系统，用以有效、高速的处理从很小到非常大的项目版本管理。是 Linus Torvalds 为了帮助管理 Linux 内核开发而开发的一个开放源码的版本控制软件。
		
2. git功能

		从一般开发者的角度来看，git有以下功能：
		1.从服务器上克隆数据库（包括代码和版本信息）到单机上。
		2.在自己的机器上创建分支，修改代码。
		3.在单机上自己创建的分支上提交代码。
		4.在单机上合并分支。
		5.新建一个分支，把服务器上最新版的代码fetch下来，然后跟自己的主分支合并。
		6.生成补丁（patch），把补丁发送给主开发者。
		7.看主开发者的反馈，如果主开发者发现两个一般开发者之间有冲突（他们之间可以合作解决的冲突），就会要求他们先解决冲突，然后再由其中一个人提交。如果主开发者可以自己解决，或者没有冲突，就通过。
		8.一般开发者之间解决冲突的方法，开发者之间可以使用pull 命令解决冲突，解决完冲突之后再向主开发者提交补丁。
		
3. git的三种状态
	
		staged(已暂存)：表示把已经修改的文件放入下次提交时要保存的清单中。
		modified(已修改)：表示修改了整个文件，但是还没有提交保存。
		committed(已提交)：表示该文件已经安全地保存在本地数据库中了。

4. git的常用操作命令
	
		1.初始化仓库
			git init
			git init --bare 建立的是裸仓库
		2.配置用户信息
			git config --global user.name "username"
			git config --global user.email tom@qq.com
		3.查看配置信息
			git config --list
		4.添加文件到暂存区
			git add filename
			git add *(添加所有文件到暂存区)或者git add --all
		5.移除文件
			git rm filename
		6.重命名一个文件
			git mv oldfilename newfilename
		7.提交到暂存区
			git commit -m "message" 只会提交暂存区（staged）里面的内容
		8.查看工作目录的状态
			git status
		9.查看提交的历史记录
			git log
		10.查看文件的改变
			git diff filename 跟工作区进行比较
			git diff --cached filename 跟暂存区比较
		11.撤销加入暂存区的操作
			git reset --filename 
		12.撤销修改的操作
			git checkout --file
		13.将本地的操作放回回收站
			git stash
		14.从回收站中恢复本地的修改
			git stash apply
	
	- 分支操作
		
			1.查看分支
				git branch
			2.创建分支
				git branch branchname
			3.删除分支
				git branch -d branchname
			4.切换分支
				git checkout branchname
			5.创建并切换分支
				git checkout -b branchname
	- 远端仓库操作
	
			1.克隆一个远端仓库
				git clone URL
			2.添加远端仓库
				git remote add name URL
			3.更新远端仓库的分支和数据
				git fetch origin master
			4.合并
				git merge origin master
			5.上传本地分支和数据到远端仓库
				git push origin master
			6.跟踪远端仓库上的分支
				git checkout --track origin/testbranch
			