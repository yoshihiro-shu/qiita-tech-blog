---
title: Nuxtのvuex-persistedstateをSSRで使ってみる
tags:
  - cookie
  - Vue.js
  - Vuex
  - ssr
  - Nuxt
private: false
updated_at: '2023-10-29T20:01:17+09:00'
id: 6be9acbb7c70ff5bc05b
organization_url_name: null
slide: false
ignorePublish: false
---
## 自己紹介
初めまして。私は都内でwebエンジニアをしています。

今の会社にインターンとして経て、入社しました。

業務では、Nuxtjs, Golang, Kubernetesを用いて運用保守開発や

最近はPandasを用いてデータ分析など日々苦戦している若輩者です。

vuex-persistedstateを使うにあたり、あまり情報がなかったので、記事にしました。

様々なご意見いただけると励みになりますので、よろしくお願い致します。

## 背景

NuxtのSSRを行うライフサイクルにて`vuex-persistedstate`によるvuexのデータの更新が行えなかったことが今回のつまずき、解決するのにかなり時間を要したので記事にしました。

## 前提

続きは[こちら](https://yoshihiro-shu.com/ja/article/16)
