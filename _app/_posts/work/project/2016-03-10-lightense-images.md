---
layout: post
title: Lightense Images
category: work
tag: project
scheme-text: "#3b1599"
scheme-link: "#ff3f00"
scheme-hover: "#ff6300"
scheme-code: "#ff65d2"
scheme-bg: "#dbf5ff"
scheme-bg-light: true
plugin: lightense
hidden: true
---

A dependency-free pure JavaScript image lightbox library less than 2 KB (not gzipped!). Inspired by [tholman/intense-images](https://github.com/tholman/intense-images).

This library is mainly used by [Almace Scaffolding](/lab/amsf/).

## Features

- High performance
- One script, no additional dependencies, no bloated styles
- Safari `backdrop-filter` support
- 1 KB gzipped

## Setup

```html
<script src="lightense.js"></script>
<img src="photo.jpg">
<script>
  window.addEventListener('load', function () {
    var el = document.querySelectorAll('img');
    Lightense(el);
  }, false);
</script>
```

<p><img src="{{ site.file }}/girls_dead_monster_logo.png"></p>

## Custom Background Color

```html
<img src="screenshot.png" data-background="rgba(0, 0, 0, .96)">
```

<p><img src="{{ site.file }}/railgun-logo.png" data-background="rgba(0, 10, 45, .6)"></p>

## Arbitrary Elements

```html
<p>Enter the CVV number <a class="lightense" data-image="card.jpg">on your credit card</a></p>.
<script>
  window.addEventListener('load', function () {
    var el = document.querySelectorAll('.lightense');
    Lightense(el);
  }, false);
</script>
```

Enter the CVV number <a class="lightense" data-image="{{ site.file }}/fun/shut-up-and-take-my-money-nichijou.jpg">on your credit card</a>.

## Disable Lightense for Specific Elements

```html
<img src="photo.jpg" class="no-lightense">
<script>
  window.addEventListener('load', function () {
    var el = document.querySelectorAll('img:not(.no-lightense)');
    Lightense(el);
  }, false);
</script>
```

<p><img src="{{ site.file }}/imouto-logo-large.png" class="no-lightense"></p>

## Download

<div class="largetype">
  <div><a href="https://github.com/sparanoid/lightense-images">Github</a></div>
</div>

## Love this?

Please consider [buying me a cup of coffee]({{ '/donate/' | prepend: site.base }}).
