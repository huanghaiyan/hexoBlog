title: CocoaPods的使用及安装
date: 2015-01-10 18:49:06
tags:
---
#CocoaPods的安装及使用
===
##CocoaPods介绍
***
	在iOS开发过程中，我们不可避免地使用第三方类库，但是类库的循环引用、更新等用手动操作的话会很费时和费力，所以，我们需要一款类库管理工具来管理我们使用的第三方类库。CocoaPods是iOS开发中最常用的类库管理工具。而且，绝大多数开源类库都支持CocoaPods。
	
##CocoaPods的安装
***
1.CocoaPods的依赖环境

（1.1）系统支持包安装：

	<1>安装Xcode
	<2>安装Homebrew（包管理器）：$ ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
（1.2）Ruby配置

	在安装Ruby之前，需要安装RVM（Ruby版本管理工具）：$ curl -L https://get.rvm.io | bash -s stable
	载入RVM：$ source ~/.rvm/scripts/rvm
	[检查RVM安装是否正确：$ rvm -v]
	使用RVM安装Ruby：$ rvm install 2.0.0
	设置Ruby版本：$ rvm 2.0.0 --default
	（如果安装的Ruby为其他版本，也可以设置为默认版本。查看Ruby版本号：$ ruby -v）
	（注意：由于国内的网络环境，导致 rubygems.org 存放在 Amazon S3 上面的资源文件间歇性连接失败，因此使用gem或bundle时常常会遇到长久无响应的情况。解决方案是使用淘宝的 RubyGems 镜像，它是一个完整 rubygems.org 镜像，你可以用此代替官方版本，同步频率目前为15分钟一次以保证尽量与官方服务同步。，使用淘宝Rubygems镜像访问配置如下： 
	$ gem source --remove https//rubygems.org/
	$ gem source -a http://ruby.taobao.org/
	验证命令：$ gem source -l）
（1.3）安装CocoaPods
	
	运行命令：$ sudo gem install cocoapods
	CocoaPods安装完成

##CocoaPods的使用
***
`使用CocoaPods管理第三方库首先要创建一个#Podfile#的文件，注意文件名必须是而且只有一个#Podfile#，有两种做法可以把第三方库文件导入工程`

1.1 直接在工程文件夹里加入Podfile文件
	
	利用终端cd到工程文件夹下创建Podfile
	
1.2 不在工程文件夹下创建Podfile
	
	注意：这种做法需在Podfile文件头写入：
	#xcodeproj "<文件路径>/<工程名>.xcodeproj"#
	
2 Podfile文件的编写格式
	
	Podfile 是一个文件，用于定义项目所需要使用的第三方库。该文件支持高度定制，你可以根据个人喜好对其做出定制。
	source 'https://github.com/CocoaPods/Specs.git'
	
	platform :ios, '6.0'（指定支持的iOS系统最高版本版本）
	inhibit_all_warnings!

	xcodeproj 'MyProject'

	pod 'ObjectiveSugar', '~> 0.5'

	target :test do
  		pod 'OCMock', '~> 2.0.1'
	end

	post_install do |installer|
  		installer.project.targets.each do |target|
    		puts "#{target.name}"
  		end
	end
	（导入第三方库的版本规定的一些方式
	pod 'AFNetworking'      //不显式指定依赖库版本，表示每次都获取最新版本
	pod 'AFNetworking', '2.0'     //只使用2.0版本
	pod 'AFNetworking', '> 2.0'     //使用高于2.0的版本
	pod 'AFNetworking', '>= 2.0'     //使用大于或等于2.0的版本
	pod 'AFNetworking', '< 2.0'     //使用小于2.0的版本
	pod 'AFNetworking', '<= 2.0'     //使用小于或等于2.0的版本
	pod 'AFNetworking', '~> 0.1.2'     //使用大于等于0.1.2但小于0.2的版本
	pod 'AFNetworking', '~>0.1'     //使用大于等于0.1但小于1.0的版本
	pod 'AFNetworking', '~>0'     //高于0的版本，写这个限制和什么都不写是一个效果，都表示使用最新版本）
	
3.CocoaPods的一些常用命令
	
	3.1、pod install
	根据Podfile文件指定的内容，安装依赖库，如果有Podfile.lock文件而且对应的Podfile文件未被修改，则会根据Podfile.lock文件指定的版本安装。
	每次更新了Podfile文件时，都需要重新执行该命令，以便重新安装Pods依赖库。
	3.2、pod update
	若果Podfile中指定的依赖库版本不是写死的，当对应的依赖库有了更新，无论有没有Podfile.lock文件都会去获取Podfile文件描述的允许获取到的最新依赖库版本。
	3.3、pod list 
	列出所有可用的第三方库
	3.4、pod search <类库名称>
	查看类库是否支持CocoaPods
	
4.CocoaPods更新

	cocoapods更新：sudo gem update cocoapods
	更新预览版：sudo gem update cocoapods pre


