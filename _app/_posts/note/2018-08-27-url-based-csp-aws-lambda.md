---
layout: post
title: URL<span class="of-case">-</span>Based CSP for AWS Lambda
category: note
---

If you followed my [last post](/note/cloudfront-hsts/) you would know you can set HSTS headers via AWS Lambda, this time let me show you how to add Content Security Policy (CSP), Expect-CT, and other security headers based on URLs that clients request, and only for `text/html` content type.

I'll modify the production code built from my last post. This time you need to catch the request URL:

```js
const request = event.Records[0].cf.request;
```

Then you can add Content Security Policy headers based on URLs:

```js
// We only need these headers for `text/html` requests.
if (headers['content-type'][0]['value'].includes('text/html')) {
  headers['expect-ct'] = [{ key: 'Expect-CT', value: 'max-age=604800' }];
  headers['referrer-policy'] = [{ key: 'Referrer-Policy', value: 'strict-origin-when-cross-origin' }];
  headers['feature-policy'] = [{ key: 'Feature-Policy', value: "camera 'none'; geolocation 'self'; usb 'none'" }];

  // Exclude all /lab content
  if (!request.uri.startsWith('/lab')) {
    headers['content-security-policy'] = [{ key: 'Content-Security-Policy', value: "default-src 'self';" }];
  }

  // Target /lab/7z
  if (request.uri.startsWith('/lab/7z')) {
    headers['content-security-policy'] = [{ key: 'Content-Security-Policy', value: "default-src 'self'; style-src 'self' 'unsafe-inline'; img-src 'self' www.7-zip.org;" }];
  }
}
```

Bonus: you can do many things on Lambda, like fixing wrong `content-type` sent by CloudFront:

```js
const path = require('path');
const request = event.Records[0].cf.request;

if (typeof headers['content-type'] !== 'undefined') {

  // ...other stuff here

  // Fix wrong MIME headers for woff2
  if (path.extname(request.uri).startsWith('.woff2')) {
    headers['content-type'] = [{ key: 'Content-Type', value: "application/font-woff2" }];
  }
}
```

Additional loot: You'd better test your code with AWS Lambda builtin test events. Or you may break your site with these security headers.
