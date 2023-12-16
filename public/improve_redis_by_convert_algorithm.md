---
title: improve_redis_by_convert_algorithm
tags:
  - 'Go'
  - 'Redis'
private: false
updated_at: ''
id: null
organization_url_name: null
slide: false
ignorePublish: false
---
## はじめに

私は[株式会社ZUU](https://zuu.co.jp/)で、主にバックエンドの開発を担当しており、フロントエンド、インフラに関する業務も担当しています。

今回は、先輩エンジニアが10行ほどの変更でRedisの負荷を1/3に削減することに成功した実例をもとに記述して行きます。

- 先輩エンジニア(通称 [ichigozero](https://github.com/ichigozero))は、vimmer, hacker, rustが得意なエンジニアです。

## サービスの概要

月間〇〇万人が利用する金融に関する記事を掲載するWebメディアを運用しています。

## 背景

現在運用しているメディアでは約100万記事掲載しており、直近一年で約50万記事と急激に増加し、Redisのパフォーマンスが劣化する課題がありました。

RedisのCPU使用率が高負荷状態になると、インスタンスを増やすなどの力技で対応するなど、イタチごっこが続いていました。

そこで根本的なアプローチをし、改善を行うとなったのが背景です。

## 解決策

Redisに保存するデータのバイト変換アルゴリズムをより、パフォーマンスの高いアルゴリズムである〇〇と〇〇を採用することで、大幅な改善に成功しました。

### 実装

### ベンチマーク

## 結果

## まとめ

...
