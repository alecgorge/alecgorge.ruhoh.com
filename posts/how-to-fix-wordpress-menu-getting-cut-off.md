---
title: How to fix WordPress' menu getting cut off on save
date: '2012-12-22'
description: Sometimes WordPress will apparently randomly cut off the last couple items from your menu. The fix is simple.

categories: [php, wordpress]

---

Earlier today I ran into an odd issue where it seemed like WordPress just didn't want to save the last few menu items I was modifiying.

Upon further testing, I realized that this problem only affected the last few items on the list and only since my recent upgrade of PHP from 5.3.0 to 5.4.10. Armed with this information, I discovered a little gem in new `php.ini`'s: `max_input_vars`:

> How many input variables may be accepted (limit is applied to `$_GET`, `$_POST` and `$_COOKIE` superglobal separately).

Apparently the default is `1000`. Each menu item in a WordPress menu consumes 12 `POST` values, so the most menu items you can have with this limit is about 83. I dropped the following value in my `php.ini` file and now my menu works just like it was before:

	max_input_vars = 5000
	suhosin.post_max_vars = 5000
	suhosin.request_max_vars = 5000