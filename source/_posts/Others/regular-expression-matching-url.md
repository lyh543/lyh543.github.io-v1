---
title: 匹配网址的正则表达式
date: 2019-6-26
tags: 
---

```
( regexpTaobao = regexp.MustCompile(`￥([\w\s]+)￥`) regexpURL = regexp.MustCompile(`(?:http|https|www)(?:[\s\.:\/\/]{1,})([\w%+:\s\/\.?=]{1,})`) regexpWhitelist = regexp.MustCompile(`((acg|im9|bili|gov).*(com|html|cn|tv)|(av\d{8,}|AV\d{8,}))`) regexpQQ = regexp.MustCompile(`(?:[加qQ企鹅号码\s]{2,}|[群号]{1,})(?:[\x{4e00}-\x{9eff}]*)(?:[:，：]?)([\d\s]{6,})`) regexpWechat = regexp.MustCompile(`(?:[加+微＋+➕薇？vV威卫星♥❤姓xX信]{2,}|weixin|weix)(?:[，❤️.\s]?)(?:[\x{4e00}-\x{9eff}]?)(?:[:，：]?)([\w\s]{6,})`) )
```