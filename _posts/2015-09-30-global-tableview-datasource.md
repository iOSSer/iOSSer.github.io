---
layout: post
title: "Global UITableView DataSource"
date: 2015-09-30
comments: true
categories: Objective-C
tags: [UITableView][DataSource]
keywords: UITableView DataSource
description: 
---

<!--<img src="http://7xl8q7.com1.z0.glb.clouddn.com/Coredata_Create.png" width="900" height="600">-->

---
#####开始
在项目中，有很多界面的UITableViewCell都很简单，Cell高度都一样，不像聊天界面的Cell高度不确定，对于处理这种高度一样、布局简单的Cell，每个界面都要重写一次`UITableViewDataSource`的2个方法：
  <br><br>
  
  ```
  - (NSInteger)tableView:(UITableView *)tableView numberOfRowsInSection:(NSInteger)section;

- (UITableViewCell *)tableView:(UITableView *)tableView cellForRowAtIndexPath:(NSIndexPath *)indexPath；
```
这样做未免有些繁琐，而我有是一个比较懒的程序员，能用1行搞定的事情绝不写10行。所以在看了相关的文章对DataSource的封装之后，自己写了一个，希望以后项目中遇到这样的界面就这一个类搞定了。
<br><br>
#####DataSource 应该做些什么事情？

写这个通用的DataSource无非就是想让`UITableViewDataSource`与VC代码分离，也能使代码更加清晰，我新建了一个类：`LPGlobalTableViewDataSource`

 `LPGlobalTableViewDataSource.h`代码如下:
 
 ```
 #import <Foundation/Foundation.h>

typedef void(^CellConfigureBlock)(id cell,id item, NSIndexPath *indexPath);

@interface LPGlobalTableViewDataSource : NSObject<UITableViewDataSource>

- (instancetype) initWithItems:(NSArray *)items reuseIdentifier:(NSString *)reuseIdentifier configureCellBlock:(CellConfigureBlock) cellConfigureBlock;
@end
 
 ```
  `CellConfigureBlock `这个Block用于在`cellForRowAtIndexPath：`中初始化Cell时，将此Cell及indexPath回传给VC，VC可在Block中自由操作Cell中界面元素的显示。
  <br><br>
  
  `LPGlobalTableViewDataSource`实现了`UITableViewDataSource`协议，也实现了`UITableViewDataSource`中的2个`@required`方法，所以VC中直接使用实现`LPGlobalTableViewDataSource`这个就好了
  
  
 `LPGlobalTableViewDataSource.m`代码如下:
  
```

#import "LPGlobalTableViewDataSource.h"

@interface LPGlobalTableViewDataSource ()

@property (nonatomic, strong) NSArray *items;
@property (nonatomic, copy) NSString *reuseIdentifier;
@property (nonatomic, copy) CellConfigureBlock cellConfigureBlock;

@end

@implementation LPGlobalTableViewDataSource

- (instancetype)initWithItems:(NSArray *)items reuseIdentifier:(NSString *)reuseIdentifier configureCellBlock:(CellConfigureBlock)cellConfigureBlock
{
    self = [super init];
    if (self) {
        self.items = items;
        self.reuseIdentifier = reuseIdentifier;
        self.cellConfigureBlock = cellConfigureBlock ;
    }
    return self;
}

- (id) itemWithIndexPath:(NSIndexPath *) indexPath
{
    return [_items objectAtIndex:indexPath.row];
}

- (NSInteger)tableView:(UITableView *)tableView numberOfRowsInSection:(NSInteger)section
{
    return _items.count;
}

- (UITableViewCell *)tableView:(UITableView *)tableView cellForRowAtIndexPath:(NSIndexPath *)indexPath
{
    id cell = [tableView dequeueReusableCellWithIdentifier:_reuseIdentifier forIndexPath:indexPath];
    id item = [self itemWithIndexPath:indexPath];
    !_cellConfigureBlock ?: _cellConfigureBlock(cell, item, indexPath);
    
    return cell;
}

@end
```

#####使用

```

_tableViewDataSource = [[LPGlobalTableViewDataSource alloc] initWithItems:_items reuseIdentifier:reuseIdentifier configureCellBlock:^(UITableViewCell *cell, NSDictionary *item, NSIndexPath *indexPath) {
        
        cell.textLabel.text = item.allKeys.lastObject;
        cell.imageView.image = [UIImage imageNamed:item.allValues.lastObject];
    }];
    _addressManagerTableView.dataSource = _tableViewDataSource;
    [_addressManagerTableView registerClass:[UITableViewCell class] forCellReuseIdentifier:reuseIdentifier];
    
```    
是不是简单多了~😏