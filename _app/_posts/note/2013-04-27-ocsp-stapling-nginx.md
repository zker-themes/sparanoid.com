---
layout: post
title: OCSP Stapling and Nginx
category: note
lang: zh-cn
---

I've already [deployed OCSP Stapling]({% post_url /note/2012-11-04-playing-with-ocsp-stapling %}) back in November, 2012. Now I'd like to share how to setup OCSP Stapling on CentOS with you.

Configurate OCSP for sparanoid.com. Get your current SSL certificates chain order:

```sh
$ openssl s_client -showcerts -connect sparanoid:443  ("level" c ".crt")} /---END CERTIFICATE-----/{inc=0}'
```

Print out the OCSP server:

```sh
$ openssl x509 -noout -text -in sparanoid.com.crt | grep OCSP
```

Validate certs against the OCSP server:

```sh
$ openssl ocsp -text -no_nonce -issuer PositiveSSLCA2.crt -CAfile sparanoid_com.crt -cert sparanoid_com.crt -VAfile PositiveSSLCA2.crt -url http://ocsp.comodoca.com -respout /etc/ssl/certs/sparanoid.com_staple
```

Add OCSP Stapling support for Nginx, for more infomation you should refer to [Nginx's `ngx_http_ssl_module`](http://nginx.org/en/docs/http/ngx_http_ssl_module.html):

```nginx
ssl_stapling            on;
resolver                8.8.8.8;
ssl_stapling_file       /etc/ssl/certs/sparanoid.com_staple;
ssl_stapling_verify     on;
```

Reload nginx to validate if OCSP Stapling is working:

```sh
$ openssl s_client -connect sparanoid.com:443 -tls1_1 -tlsextdebug -status
```
