---
html: validator_info.html
parent: status-and-debugging-methods.html
blurb: バリデータとして設定されている場合、サーバのバリデーション設定を取得します。
labels:
  - コアサーバー
  - ブロックチェーン
---
# validator_info
[[ソース]](https://github.com/XRPLF/rippled/blob/master/src/ripple/rpc/handlers/ValidatorInfo.cpp "ソース")

`{{currentpage.name}}`メソッドは、サーバがバリデータとして設定されている場合に、現在のバリデータの設定を返します。

_`{{currentpage.name}}`メソッドは[管理メソッド](admin-api-methods.html)で、権限のないユーザは実行できません。_


### リクエストのフォーマット

リクエストのフォーマットの例:

<!-- MULTICODE_BLOCK_START -->

*WebSocket*

```json
{
    "command": "{{currentpage.name}}"
}
```

*JSON-RPC*

```json
{
    "method": "{{currentpage.name}}"
}
```

*コマンドライン*

```sh
#Syntax: {{currentpage.name}}
rippled {{currentpage.name}}
```

<!-- MULTICODE_BLOCK_END -->

リクエストはパラメータを使用しません。


### レスポンスのフォーマット

成功したレスポンスの例:

<!-- MULTICODE_BLOCK_START -->

*WebSocket*

```json
{
  "result": {
    "domain": "mduo13.com",
    "ephemeral_key": "n9KnrcCmL5psyKtk2KWP6jy14Hj4EXuZDg7XMdQJ9cSDoFSp53hu",
    "manifest": "JAAAAAFxIe002KClGBUlRA7h5J2Y5B7Xdlxn1Z5OxY7ZC2UmqUIikHMhAkVIeB7McBf4NFsBceQQlScTVUWMdpYzwmvs115SUGDKdkcwRQIhAJnKfYWnPsBsATIIRfgkAAK+HE4zp8G8AmOPrHmLZpZAAiANiNECVQTKktoD7BEoEmS8jaFBNMgRdcG0dttPurCAGXcKbWR1bzEzLmNvbXASQPjO6wxOfhtWsJ6oMWBg8Rs5STAGvQV2ArI5MG3KbpFrNSMxbx630Ars9d9j1ORsUS5v1biZRShZfg9180JuZAo=",
    "master_key": "nHBk5DPexBjinXV8qHn7SEKzoxh2W92FxSbNTPgGtQYBzEF4msn9",
    "seq": 1
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
    "domain": "mduo13.com",
    "ephemeral_key": "n9KnrcCmL5psyKtk2KWP6jy14Hj4EXuZDg7XMdQJ9cSDoFSp53hu",
    "manifest": "JAAAAAFxIe002KClGBUlRA7h5J2Y5B7Xdlxn1Z5OxY7ZC2UmqUIikHMhAkVIeB7McBf4NFsBceQQlScTVUWMdpYzwmvs115SUGDKdkcwRQIhAJnKfYWnPsBsATIIRfgkAAK+HE4zp8G8AmOPrHmLZpZAAiANiNECVQTKktoD7BEoEmS8jaFBNMgRdcG0dttPurCAGXcKbWR1bzEzLmNvbXASQPjO6wxOfhtWsJ6oMWBg8Rs5STAGvQV2ArI5MG3KbpFrNSMxbx630Ars9d9j1ORsUS5v1biZRShZfg9180JuZAo=",
    "master_key": "nHBk5DPexBjinXV8qHn7SEKzoxh2W92FxSbNTPgGtQYBzEF4msn9",
    "seq": 1,
    "status": "success"
  }
}
```

*コマンドライン*

```json
Loading: "/etc/rippled.cfg"
Connecting to 127.0.0.1:5005

{
   "result" : {
      "domain" : "mduo13.com",
      "ephemeral_key" : "n9KnrcCmL5psyKtk2KWP6jy14Hj4EXuZDg7XMdQJ9cSDoFSp53hu",
      "manifest" : "JAAAAAFxIe002KClGBUlRA7h5J2Y5B7Xdlxn1Z5OxY7ZC2UmqUIikHMhAkVIeB7McBf4NFsBceQQlScTVUWMdpYzwmvs115SUGDKdkcwRQIhAJnKfYWnPsBsATIIRfgkAAK+HE4zp8G8AmOPrHmLZpZAAiANiNECVQTKktoD7BEoEmS8jaFBNMgRdcG0dttPurCAGXcKbWR1bzEzLmNvbXASQPjO6wxOfhtWsJ6oMWBg8Rs5STAGvQV2ArI5MG3KbpFrNSMxbx630Ars9d9j1ORsUS5v1biZRShZfg9180JuZAo=",
      "master_key" : "nHBk5DPexBjinXV8qHn7SEKzoxh2W92FxSbNTPgGtQYBzEF4msn9",
      "seq" : 1,
      "status" : "success"
   }
}
```

<!-- MULTICODE_BLOCK_END -->

レスポンスは[標準フォーマット][]に従い、成功した結果には以下のフィールドが含まれます.

| `Field`         | 型    | 説明                                               |
|:----------------|:------|:----------------------------------------------------------|
| `domain`        | 文字列 | _(省略される場合があります)_ このバリデータに関連付けられたドメイン名 (ドメイン名が設定されている場合)。 |
| `ephemeral_key` | 文字列 | _(省略される場合があります)_ このサーバが検証メッセージに署名する際に使用する公開鍵。この鍵は、バリデータが設定したトークンを変更した際に変更されます。 |
| `manifest`      | 文字列 | _(省略される場合があります)_ このバリデータが設定したトークンに対応するパブリックな「マニフェスト」を[バイナリにシリアライズ](serialization.html)して、base64でエンコードしたもの。このフィールドには個人情報は含まれません。 |
| `master_key`    | 文字列 | このバリデータのマスターキーペアの公開鍵。このキーはバリデータを一意に識別するもので、バリデータが公開鍵をローテーションする場合でも同じです。サーバが`[validator_token]`ではなく`[validation_seed]`を用いて設定されている場合、レスポンスのフィールドはこれだけとなります。 |
| `seq`           | 数値   | _(省略される場合があります)_ このバリデータのバリデーション用トークンおよび設定のシーケンス番号。この番号は、バリデータのオペレータがトークンを更新して鍵をローテーションしたり設定を変更したりするたびに増加します。 |

バリデータトークンとキーローテーションの詳細については、[validator-keys-toolガイド](https://github.com/ripple/validator-keys-tool/blob/master/doc/validator-keys-tool-guide.md)をご覧ください。


### 考えられるエラー

* [汎用エラータイプ][]のすべて。
- `invalidParams` - サーバが[バリデータとして設定されていない](run-rippled-as-a-validator.html)場合、サーバはこのエラーを`"error_message" : "not a validator"`と共に返します。

<!--{# common link defs #}-->
{% include '_snippets/rippled-api-links.md' %}
{% include '_snippets/tx-type-links.md' %}
{% include '_snippets/rippled_versions.md' %}
