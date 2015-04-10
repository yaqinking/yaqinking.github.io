---
layout: post
title: 使用 rangeOfString 過濾 NSArray 中的 NSString 對象  
date: 2015-04-10  10:13:45
categories: 日常
---
假如想要在NSArray中得到包含Nisekoi的NSString數據

思路：
聲明一組包含 Nisekoi 和 Plastic Memories 的 NSArray
從NSArray 中過濾出帶有 Nisekoi 的 NSString 對象


{% highlight objective-c %}

NSMutableArray *tasks = [[NSMutableArray alloc] init];
    
for (int i = 0 ; i<24; i++) {
    [tasks addObject:[NSString stringWithFormat:@"Nisekoi %i",i+1]];
    [tasks addObject:[NSString stringWithFormat:@"Plastic Memories %i",i+1]];
    
}

NSMutableArray *queryTasks = [[NSMutableArray alloc] init];
for (NSString *task in tasks) {
    //使用 rangeOfString 過濾
    NSRange r = [task rangeOfString:@"Nisekoi"
			    options:NSCaseInsensitiveSearch];
    if (r.location != NSNotFound) {
	[queryTasks addObject:task];
    }
}

for (NSString *t in queryTasks) {
    NSLog(@"To do list -> %@",t);
}

{% endhighlight %}



其實沒必要這麼麻煩，直接一個NSMutableDictionary  setObject:forKey: 設定好就可以了，過濾什麼的，0X23XD 喵。


