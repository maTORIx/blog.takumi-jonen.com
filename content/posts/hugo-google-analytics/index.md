---
title: "HugoブログにGoogle Analytics導入"
date: 2020-04-16T08:40:19+09:00
draft: false
hideLastModified: true
summaryImage: "images/google-analytics.png" 
keepImageRatio: true
tags: []
showInMenu: false
summary: "Hugoを用いたブログに Google Analytics を導入する方法を3つ説明。"
---

{{< analytics >}}
{{< style >}}

{{< container "header-image" >}}
![header-image](images/google-analytics.png)
{{< /container >}}

この記事では、Hugoを用いたブログに Google Analytics を導入する方法を3つ説明します。

# Hugo と Google Analytics

HugoとGoogle Analyticsの親和性は非常に高いです。

しかし、別のThemeをHugoブログに引用すると、導入の難易度は少々あがります。

そのため、この記事では、３つの方法でGoogle AnalyticsをHugoブログに導入する方法をご紹介します。

# 事前準備 Google Analytics のトラッキングコードを入手する

https://analytics.google.com

上記のサイトにアクセスし、利用するドメインを用いてトラッキングコードを入手しましょう。

`UA-xxxxxxx` といった形のコードが入手できると思います。

# 方法1 themes 以下の情報を変更する


