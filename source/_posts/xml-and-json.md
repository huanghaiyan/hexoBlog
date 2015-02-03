title: 'xml and json'

date: 2014-11-27 20:37:16
tags:
---
###XML
####SMX解析
1. 创建XML解析对象

		NSURL *fileURL = [[NSBundle mainBundle] URLForResource:@"bookstore" withExtension:@"xml"];
		NSXMLParser *xmlParser = [[NSXMLParser alloc] initWithContentsOfURL:fileURL];

2. 设置XML解析对象代理
3. 开始解析

		BOOL flag = [xmlParser parse];
		if(!flag){
			NSLog(@"xmlParser parse error.");
		} 

####NSXMLPqrser对象代理方法

- (void)parserDidStartDocument:(NSXMLParser *)parser //当开始解析XML文档的时候，调用这个方法。通常在这个方法⾥， 创建存储









	/*


		NSData *data = [NSData dataWithContentsOfURL:fileURL];

2. 根据NSData对象创建GDataXMLDocument对象(即DOM模型对象),该对象在内存中是以树形结构存储的

		GDataXMLDocument *doc = [[GDataXMLDocument alloc] initWithData:data options:0 error:nil];
	
3. 通过DOM模型对象,取出XML文件的根元素
	
		GDataXMLElement *rootElement = [doc rootElement];
		
4. 由于是树形结构,所以,可以根据子元素的名字使用根元素获取到所有子元素,并类推获得子元素的子元素

		for (GDataXMLElement *element in elements) {
		}
####JSON

从结构上看,所有的数据(data)最终都可以分解成三种类型:

- 第一种类型是标量(scalar),也就是一个单独的字符串(string)或数字(numbers),比如"北京"这个单独的次

-  第二种类型是序列(sequence),也就是若干个相关的数据按照一定顺序并列在一起,又叫做数组(array)或列表(List),比如"北京,上海"

- 第三种类型是映射(mapping),也就是一个名/值对(Name/value),即数据有一个名称,还有一个与之相对应的值,这又称作散列(hash)或字典(dictionary),比如"首都:北京"

Json的规定

1. 并列的数据之间用逗号(",")分隔
2. 映射用冒号(":")表示  
3. 并列数据的集合(数组)用方括号("[]")表示
4. 映射的集合(对象)用大括号("{}")表示

		rfc-4627



####JSONKit
使用:-fno-objc-arc
序列化:NSArray  NSDictionary  NSString
		
	– JSONData
