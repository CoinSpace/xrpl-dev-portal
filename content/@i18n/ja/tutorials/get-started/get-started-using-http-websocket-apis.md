---
html: get-started-using-http-websocket-apis.html
parent: http-websocket-apis-tutorials.html
blurb: XRP Ledgerの操作に使用できるAPIとライブラリを使い始めましょう。
cta_text: 開始しよう
top_nav_name: HTTP / WebSocket
top_nav_grouping: 始めましょう
labels:
  - 開発
showcase_icon: assets/img/logos/globe.svg
---
# HTTP / WebSocket APIの使用開始

自分の好みのプログラミング言語の[クライアント・ライブラリ](client-libraries.html)を持っていなかったり、使いたくなかったりする場合は、XRP Ledgerのコアサーバソフトウェアである[`rippled`](xrpl-servers.html)のAPIを通して直接XRP Ledgerにアクセスすることができます。このサーバはJSON-RPCとWebSocketプロトコルでAPIを提供します。もし`rippled`(install-rippled.html)のインスタンスを実行しない場合でも、[公開サーバ][public servers]を利用することができます。

**ヒント:** [**WebSocket API ツール**](websocket-api-tool.html)を使ってAPIを利用することもできますし、[XRP Ledger Explorer](https://livenet.xrpl.org/)を使ってレジャーの進捗をライブで見ることもできます。

## JSON-RPCとWebSocketの違い

JSON-RPCとWebSocketはどちらもHTTPベースのプロトコルであり、ほとんどの場合、両方のプロトコルで提供されるデータは同じです。主な違いは次の通りです。

- JSON-RPCは、RESTful APIと同様に、呼び出しごとに個別のHTTPリクエストとレスポンスを使用します。このAPIにアクセスするには、[curl](https://curl.se/)、[Postman](https://www.postman.com/downloads/)、[Requests](https://requests.readthedocs.io/)などの一般的なHTTPクライアントを使用できます。
- WebSocketは、サーバがクライアントにデータをプッシュできる持続的な接続を使用します。[イベント購読](subscribe.html)のようなプッシュメッセージを必要とする機能は、WebSocketを使用してのみ利用可能です。

どちらのAPIも暗号化されていない接続(`http://`と`ws://`)とTLSを使って暗号化された接続(`https://`と`wss://`)があります。暗号化されていない接続はオープンネットワーク上で提供すべきではありませんが、クライアントがサーバと同じマシン上にある場合は使用できます。


## 管理者アクセス権限

`rippled`サーバの[管理メソッド](admin-api-methods.html)を使用するには、次のように行います。この場合、サーバのバインド用として設定したIPアドレスとポートを使用する必要があります（例えば`127.0.0.1:54321`）。また、管理機能にアクセスするには、構成ファイルで**管理用としてマークされているポートおよびIPアドレス**から接続しなければなりません。

[構成ファイルの例](https://github.com/XRPLF/rippled/blob/8429dd67e60ba360da591bfa905b58a35638fda1/cfg/rippled-example.cfg#L1050-L1073)では、ローカルループバックネットワーク上（127.0.0.1）のポート5005でJSON-RPC（HTTP）、ポート6006でWebSocket（WS）の接続をリッスンし、接続されるすべてのクライアントを管理者として扱っています。


## WebSocket API

いくつかのメソッドをXRP Ledgerで試すことを予定している場合は、独自のWebSocketコードを記述することなく、[WebSocket APIツール](websocket-api-tool.html)でAPIをすぐに使用できます。後ほど、独自の`rippled`サーバへの接続が必要となった時点で、Web Socket接続をサポートした[独自のクライアントを構築](monitor-incoming-payments-with-websocket.html)したり[クライアントライブラリ](client-libraries.html)を利用することが可能です。

WebSocket APIによるリクエストの例:

```json
{
  "id": "my_first_request",
  "command": "server_info",
  "api_version": 1
}
```

レスポンスには、サーバの現在のステータスが表示されます。

さらに見る: [リクエストのフォーマット >](request-formatting.html) [レスポンスのフォーマット >](response-formatting.html) [server_infoメソッドについて >][server_info method]

## JSON-RPC

任意のHTTPクライアント（[RESTED for Firefox](https://addons.mozilla.org/en-US/firefox/addon/rested/)、[Postman for Chrome](https://chrome.google.com/webstore/detail/postman/fhbjgbiflinjbdggehcddcbncdddomop?hl=en)、[Online HTTP client ExtendsClass](https://extendsclass.com/rest-client-online.html)など）を使用して、JSON-RPCで`rippled`サーバを呼び出すことができます。ほとんどのプログラミング言語には、HTTPリクエストを組み込むためのライブラリが用意されています。

JSON-RPCによるリクエストの例:

```json
POST http://s1.ripple.com:51234/
Content-Type: application/json

{
    "method": "server_info",
    "params": [
        {
            "api_version": 1
        }
    ]
}
```

レスポンスには、サーバの現在のステータスが表示されます。

さらに見る: [リクエストのフォーマット >](request-formatting.html#json-rpcフォーマット) [レスポンスのフォーマット >](response-formatting.html) [server_infoメソッドについて >][server_info method]

## コマンドライン

このコマンドラインインターフェイスは、JSON-RPCのものと同一のサービスに接続するため、公開サーバおよびサーバ構成は同一です。コマンドラインクライアントとして、`rippled`がローカルインスタンスに接続します。

コマンドラインによるリクエストの例:

```
rippled --conf=/etc/rippled.cfg server_info
```

さらに見る: [dコマンドライン使用リファレンス >](commandline-usage.html)

**注記:** コマンドラインインターフェイスは、管理の目的でのみ使用されることを想定しており _サポートされるAPIではありません_。`rippled`の将来のバージョンでは、警告なしにコマンドラインAPIに破壊的変更を加える可能性があります！

## 利用可能なメソッド

APIメソッドの完全なリストについては、こちらをご覧ください。

- [パブリックな`rippled`メソッド](public-api-methods.html): レジャーからのデータの検索やトランザクションの送信など、パブリックサーバで利用可能なメソッドです。
- [管理用`rippled`メソッド](admin-api-methods.html): [管理者向け](manage-the-rippled-server.html)の`rippled`サーバを管理するためのメソッドです。


## 関連項目

- **コンセプト:**
  - [XRP Ledgerの概要](xrp-ledger-overview.html)
  - [ソフトウェアエコシステム](software-ecosystem.html)
  - [並列ネットワーク](parallel-networks.html)
- **チュートリアル:**
  - [JavaScriptの使用開始](get-started-using-javascript.html)
  - [信頼できるトランザクションの送信](reliable-transaction-submission.html)
  - [rippledサーバの管理](manage-the-rippled-server.html)
- **リファレンス:**
  - [rippled APIリファレンス](http-websocket-apis.html)

<!--{# common link defs #}-->
{% include '_snippets/rippled-api-links.md' %}
{% include '_snippets/tx-type-links.md' %}
{% include '_snippets/rippled_versions.md' %}
