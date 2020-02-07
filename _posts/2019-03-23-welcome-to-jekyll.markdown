---
layout: post
title:  "Blog"
date:   2020-02-06 12:26:36 +0530
categories:  博客
---
这是测试文件--

```javascript
const Razorpay = require('razorpay');

let rzp = Razorpay({
	key_id: 'KEY_ID',
	secret: 'name'
});

// capture request
rzp.capture(payment_id, cost)
	.then(function (data) {
		return 2;
	})
```
