---
# title: 'Indexを一件付与したら、CPU使用率が60%から5%まで改善した話'
title: 'Indexを一件付与したら、DBインスタンスをピーク時6台から2台までに改善できた話'
tags:
  - SQL
  - PostgreSQL
  - DB
private: false
updated_at: ''
id: null
organization_url_name: null
slide: false
ignorePublish: false
---
## 概要

現在とある金融系Webメディアを運営する会社で、主にバックエンドの開発を担当しており、フロントエンド、インフラに関する業務も担当しています。

今回は肥大化したDBにインデックスを付与することで、DBインスタンス数を最大6台から2台までに改善することができたので説明していきたいと思います。

## 前提

使用しているDBMSはPostgreSQL12です。

## メイン

## EXPLAIN ANALYZEの分析

## 処理時間の比較

## DBのCPUの効果

## APIのレイテンシの効果

## まとめ

![slow-query-explain-analysis](slow-query-query-plan.png)