1. 我们注意看这两个函数的返回值：nullable表示可以是空值，所以我们用它的时候如果没有cell的话要自己创建，而下面函数返回值中并没有nullable，证明它一定会存在，不需要我们再实现判断cell的逻辑了，__kindof用来说明返回值是UITableViewCell或者它的子类，类似于泛型，比之前用的id类型再强转要好多了。
	
		- (nullable __kindof UITableViewCell *)dequeueReusableCellWithIdentifier:(NSString *)identifier; 

		- (__kindof UITableViewCell *)dequeueReusableCellWithIdentifier:(NSString *)identifier forIndexPath:(NSIndexPath *)indexPath NS_AVAILABLE_IOS(6_0);

2. [xib讲解简书](http://www.jianshu.com/p/2f9e71ef7f52)