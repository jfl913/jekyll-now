---
layout: post
title: 试试会不会动
---

用[**Jekyll Now**](https://github.com/barryclark/jekyll-now)创建的第一篇博客。看看图片会不会动。

![_config.yml](../images/1-images/test.gif)

	- (RACSignal *)doNext:(void (^)(id x))block {
	    NSCParameterAssert(block != NULL);
	
	    return [[RACSignal createSignal:^(id<RACSubscriber> subscriber) {
	        return [self subscribeNext:^(id x) {
	            block(x);
	            [subscriber sendNext:x];
	        } error:^(NSError *error) {
	            [subscriber sendError:error];
	        } completed:^{
	            [subscriber sendCompleted];
	        }];
	    }] setNameWithFormat:@"[%@] -doNext:", self.name];
	}
