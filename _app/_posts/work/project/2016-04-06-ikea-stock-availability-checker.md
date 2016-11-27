---
layout: post
title: IKEA Stock Availability Checker
category: work
tag: project
head: |
  <link rel="chrome-webstore-item" href="https://chrome.google.com/webstore/detail/hjdnnkppfadnemodjjnbacnagkgbhekm">
foot: |
  <script>
  +function update_install_button() {
    var install_button = document.getElementById('install-button');
    install_button.removeAttribute(chrome.app.isInstalled ? "onclick" : "disabled");
  }();
  </script>
---

## Intro

Get all stock availability for current IKEA product in your selected country.

## Downloads

<div class="largetype">
  <div><a href="#!" onclick="chrome.webstore.install()" id="install-button" disabled>Add to Chrome</a></div>
</div>

## Love this?

Please consider [buying me a cup of coffee]({{ '/donate/' | prepend: site.base }}).
