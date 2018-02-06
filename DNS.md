# 深入理解 DNS

## dig
```
$ dig www.aliyun.com

; <<>> DiG 9.8.3-P1 <<>> www.aliyun.com
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 42772
;; flags: qr rd ra; QUERY: 1, ANSWER: 6, AUTHORITY: 0, ADDITIONAL: 0

;; QUESTION SECTION:
;www.aliyun.com.			IN	A

;; ANSWER SECTION:
www.aliyun.com.		82	IN	CNAME	www-jp-de-intl-adns.aliyun.com.
www-jp-de-intl-adns.aliyun.com.	262 IN	CNAME	www-jp-de-intl-adns.aliyun.com.gds.alibabadns.com.
www-jp-de-intl-adns.aliyun.com.gds.alibabadns.com. 119 IN CNAME	wagbridge.aliyun.com.
wagbridge.aliyun.com.	232	IN	CNAME	sh.wagbridge.aliyun.com.
sh.wagbridge.aliyun.com. 232	IN	CNAME	sh.wagbridge.aliyun.com.gds.alibabadns.com.
sh.wagbridge.aliyun.com.gds.alibabadns.com. 119	IN A 140.205.32.8

;; Query time: 158 msec
;; SERVER: 192.168.1.234#53(192.168.1.234)
;; WHEN: Mon Feb  5 14:52:33 2018
;; MSG SIZE  rcvd: 210
```

## Ref
- [DNS 原理入门](http://www.ruanyifeng.com/blog/2016/06/dns.html) by 阮一峰 2016