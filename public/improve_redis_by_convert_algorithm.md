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

そこで根本的なアプローチをし、改善を行うとなったのが背景です。（*別アプローチも行っており、大幅な改善が見られました。別記事にて紹介いたします。）

## 解決策

データ圧縮アルゴリズムのGob形式から、パフォーマンスの高いアルゴリズムであるMgspack形式と〇〇を採用することで、大幅な改善に成功しました。

### 実装

[snappy](https://github.com/golang/snappy)と[Mgspack](https://github.com/vmihailenco/msgpack)をインストールします。

```zsh
go get github.com/golang/snappy \
go get github.com/vmihailenco/msgpack/v5
```

データ圧縮ロジックを変更します。

```golang
func serialize(value interface{}) ([]byte, error) {
  b, err := msgpack.Marshal(value)
  if err != nil {
    return nil, err
  }
  return snappy.Encode(nil, b), nil
}
func deserialize(input []byte, ptr interface{}) (err error) {
  b, err := snappy.Decode(nil, input)
  if err != nil {
    return err
  }
  return msgpack.Unmarshal(b, ptr)
}
```

### ベンチマーク

データ圧縮アルゴリズムのベンチマーク

```zsh
BenchmarkJSONMarshal-12               	   45304	     25614 ns/op	   17984 B/op	      35 allocs/op
BenchmarkJSONUnmarshal-12             	   14763	     81072 ns/op	   31334 B/op	      74 allocs/op
BenchmarkGobMarshal-12                	  120536	     10011 ns/op	   29876 B/op	      51 allocs/op
BenchmarkGobUnmarshal-12              	   56109	     21446 ns/op	   36464 B/op	     243 allocs/op
BenchmarkMsgpackMarshal-12            	  373802	      2888 ns/op	   28005 B/op	       5 allocs/op
BenchmarkMsgpackUnmarshal-12          	  369746	      3261 ns/op	   15286 B/op	      34 allocs/op
BenchmarkMsgpackSnappyMarshal-12      	   55236	     21330 ns/op	   44386 B/op	       5 allocs/op
BenchmarkMsgpackSnappyUnmarshal-12    	  140824	      8507 ns/op	   28951 B/op	      35 allocs/op
```

Redisベンチマーク

```zsh
BenchmarkRedisGob-12                  	    3412	    354128 ns/op	   80158 B/op	     299 allocs/op
BenchmarkRedisMsgpackSnappy-12              3891	    318373 ns/op	   76750 B/op	      46 allocs/op
```

バイトサイズ

```zsh
json: 14602
gob: 13441
msgpack: 13304
msgpack + snappy: 7789
```

## リリース時の懸念

## 結果

## まとめ

...
