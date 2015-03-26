---
layout: post
title: SDWebImage有种情况并不需要把self改为weakSelf
---


看下面代码

	- (void)viewDidLoad {
	    [super viewDidLoad];
	    // Do any additional setup after loading the view.
	    NSString *urlString = @"http://img.hb.aicdn.com/154fc0b70d9693759e9d66861b15e920f7d3d16648e10-9MxqJz_fw658";
	    [self.imageView sd_setImageWithURL:[NSURL URLWithString:urlString] completed:^(UIImage *image, NSError *error, SDImageCacheType cacheType, NSURL *imageURL) {
	        self.imageView.image = image;
	    }];
	}

发现有人在使用时会把`- (void)sd_setImageWithURL:(NSURL *)url completed:(SDWebImageCompletionBlock)completedBlock {
`方法里的`self`改为`weakSelf`，防止RetainCycle，其实根本不用改，因为self.imageView并不持有`completedBlock`。（因为最近看了一些SDWebImage的源码才知道的）。我自己写了个简单DEMO也证实直接用`self`，并不会导致RetainCycle。
