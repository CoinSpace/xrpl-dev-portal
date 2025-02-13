---
html: manifest.html
parent: server-info-methods.html
blurb: 既知のバリデータに関する公開情報を調べます。
labels:
  - ブロックチェーン
---
# manifest
[[ソース]](https://github.com/XRPLF/rippled/blob/master/src/ripple/rpc/handlers/Manifest.cpp "ソース")

`{{currentpage.name}}`メソッドは、指定したバリデータ公開鍵の現在の"マニフェスト"情報を報告します。"マニフェスト"は、バリデータのマスターキーペアから署名付きの公開鍵(ephemeral signing key)を認証するためのデータブロックです。[更新: rippled 1.7.0][].


### リクエストのフォーマット

リクエストのフォーマットの例:

<!-- MULTICODE_BLOCK_START -->

*WebSocket*

```json
{
    "command": "{{currentpage.name}}",
    "public_key": "nHUFE9prPXPrHcG3SkwP1UzAQbSphqyQkQK9ATXLZsfkezhhda3p"
}
```

*JSON-RPC*

```json
{
    "method": "{{currentpage.name}}",
    "params": [{
        "public_key":"nHUFE9prPXPrHcG3SkwP1UzAQbSphqyQkQK9ATXLZsfkezhhda3p"
    }]
}
```

*コマンドライン*

```sh
#Syntax: {{currentpage.name}} public_key
rippled {{currentpage.name}} nHUFE9prPXPrHcG3SkwP1UzAQbSphqyQkQK9ATXLZsfkezhhda3p
```

<!-- MULTICODE_BLOCK_END -->

リクエストには以下のパラメータが含まれます。

| `Field`      | 型   　| 説明                               |
|:-------------|:------|:-----------------------------------|
| `public_key` | 文字列 | 検索するバリデータの[base58][]エンコードされた公開鍵。マスター公開鍵あるいはエフェメラル公開鍵を指定します。 |


### レスポンスのフォーマット

成功したレスポンスの例:

<!-- MULTICODE_BLOCK_START -->

*WebSocket*

```json
{
  "result": {
    "details": {
      "domain": "",
      "ephemeral_key": "n9J67zk4B7GpbQV5jRQntbgdKf7TW6894QuG7qq1rE5gvjCu6snA",
      "master_key": "nHUFE9prPXPrHcG3SkwP1UzAQbSphqyQkQK9ATXLZsfkezhhda3p",
      "seq": 1
    },
    "manifest": "JAAAAAFxIe3AkJgOyqs3y+UuiAI27Ff3Mrfbt8e7mjdo06bnGEp5XnMhAhRmvCZmWZXlwShVE9qXs2AVCvhVuA/WGYkTX/vVGBGwdkYwRAIgGnYpIGufURojN2cTXakAM7Vwa0GR7o3osdVlZShroXQCIH9R/Lx1v9rdb4YY2n5nrxdnhSSof3U6V/wIHJmeao5ucBJA9D1iAMo7YFCpb245N3Czc0L1R2Xac0YwQ6XdGT+cZ7yw2n8JbdC3hH8Xu9OUqc867Ee6JmlXtyDHzBdY/hdJCQ==",
    "requested": "nHUFE9prPXPrHcG3SkwP1UzAQbSphqyQkQK9ATXLZsfkezhhda3p"
  },
  "status": "success",
  "type": "response"
}
```

*JSON-RPC*

```json
200 OK

{
  "result": {
    "details": {
      "domain": "",
      "ephemeral_key": "n9J67zk4B7GpbQV5jRQntbgdKf7TW6894QuG7qq1rE5gvjCu6snA",
      "master_key": "nHUFE9prPXPrHcG3SkwP1UzAQbSphqyQkQK9ATXLZsfkezhhda3p",
      "seq": 1
    },
    "manifest": "JAAAAAFxIe3AkJgOyqs3y+UuiAI27Ff3Mrfbt8e7mjdo06bnGEp5XnMhAhRmvCZmWZXlwShVE9qXs2AVCvhVuA/WGYkTX/vVGBGwdkYwRAIgGnYpIGufURojN2cTXakAM7Vwa0GR7o3osdVlZShroXQCIH9R/Lx1v9rdb4YY2n5nrxdnhSSof3U6V/wIHJmeao5ucBJA9D1iAMo7YFCpb245N3Czc0L1R2Xac0YwQ6XdGT+cZ7yw2n8JbdC3hH8Xu9OUqc867Ee6JmlXtyDHzBdY/hdJCQ==",
    "requested": "nHUFE9prPXPrHcG3SkwP1UzAQbSphqyQkQK9ATXLZsfkezhhda3p",
    "status": "success"
  }
}
```

*コマンドライン*

```json
Loading: "/etc/rippled.cfg"
Connecting to 127.0.0.1:5005

{
  "result": {
    "details": {
      "domain": "",
      "ephemeral_key": "n9J67zk4B7GpbQV5jRQntbgdKf7TW6894QuG7qq1rE5gvjCu6snA",
      "master_key": "nHUFE9prPXPrHcG3SkwP1UzAQbSphqyQkQK9ATXLZsfkezhhda3p",
      "seq": 1
    },
    "manifest": "JAAAAAFxIe3AkJgOyqs3y+UuiAI27Ff3Mrfbt8e7mjdo06bnGEp5XnMhAhRmvCZmWZXlwShVE9qXs2AVCvhVuA/WGYkTX/vVGBGwdkYwRAIgGnYpIGufURojN2cTXakAM7Vwa0GR7o3osdVlZShroXQCIH9R/Lx1v9rdb4YY2n5nrxdnhSSof3U6V/wIHJmeao5ucBJA9D1iAMo7YFCpb245N3Czc0L1R2Xac0YwQ6XdGT+cZ7yw2n8JbdC3hH8Xu9OUqc867Ee6JmlXtyDHzBdY/hdJCQ==",
    "requested": "nHUFE9prPXPrHcG3SkwP1UzAQbSphqyQkQK9ATXLZsfkezhhda3p",
    "status": "success"
  }
}
```

<!-- MULTICODE_BLOCK_END -->

<!-- Note, the CLI response above is mocked up to compensate for https://github.com/XRPLF/rippled/issues/3317 -->

レスポンスは[標準フォーマット][]に従い、成功した結果には以下のフィールドが含まれます。

| `Field`     | 型         | 説明                                                   |
|:------------|:-----------|:------------------------------------------------------|
| `details`   | オブジェクト | _(省略される場合があります)_ このマニフェストに含まれるデータ。サーバがリクエストからの`public_key`に対するマニフェストを持っていない場合は省略されます。その内容の完全な説明については、以下の **オブジェクトの詳細** をご覧ください。 |
| `manifest`  | 文字列      | _(省略される場合があります)_ base64形式の完全なマニフェストデータ。このデータは[シリアライズ](serialization.html)され、base64エンコードされる前にバイナリになります。サーバがリクエストからの`public_key`に対するマニフェストを持っていない場合は省略されます。 |
| `requested` | 文字列      | リクエストの`public_key`。                               |

#### オブジェクトの詳細

もし指定された場合、`details`オブジェクトは以下のフィールドを含みます。

| `Field`         | 型    | 説明                                       |
|:----------------|:------|:--------------------------------------------------|
| `domain`        | 文字列 | このバリデータが関連していると示すドメイン名。マニフェストにドメインが含まれていない場合、これは空文字列になります。 |
| `ephemeral_key` | 文字列 | このバリデータのエフェメラル公開鍵を、[base58][]で指定します。 |
| `master_key`    | 文字列 | このバリデータのマスター公開鍵を、[base58][]で指定します。 |
| `seq`           | 数値   | このマニフェストのシーケンス番号。この番号は、バリデータのオペレータがバリデータのトークンを更新してエフェメラルキーをローテーションしたり、設定を変更したりするたびに増加します。 |


## 考えられるエラー

* いずれかの[汎用エラータイプ][]。
- `invalidParams` - `public_key`フィールドが見つからないか、正しく指定されていません。
- `reportingUnsupported` - ([レポートモード][]サーバのみ) このメソッドはレポートモードでは使用できません。

<!--{# common link defs #}-->
{% include '_snippets/rippled-api-links.md' %}
{% include '_snippets/tx-type-links.md' %}
{% include '_snippets/rippled_versions.md' %}
