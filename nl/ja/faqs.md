---

copyright:
  years: 2017
lastupdated: "2017-08-21"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# FAQ

このセクションでは、IBM Bluemix Load Balancer サービスに関するよくある質問の答えを記載しています。

## ロード・バランサー・サービスで定義できる仮想ポートの最大数を教えてください。

新しいロード・バランサー・サービスの作成を試行している間は、最大 2 個の仮想ポートを定義できます。サービスが作成された後、追加の仮想ポートを定義できます。許可される仮想ポートの最大数は 10 個です。 

## ロード・バランサーに関連付けることができるコンピュート・インスタンスの最大数を教えてください。

50 です。## 内部のクライアントだけがアクセスできる、内部専用のプライベート・ロード・バランサーを作成することはできますか?   

現時点ではできません。IBM Bluemix Load Balancer でホストされているサービスには、パブリック・インターネットからアクセス可能な完全修飾ドメイン・ネームが割り当てられます。 

## さまざまなヘルス・チェック・パラメーターのデフォルト設定と許可される値を教えてください。

デフォルト設定および許可される値を以下にリストします。

* **ヘルス・チェックの間隔:** デフォルトは 5 秒。2 秒から 60 秒の範囲
* **ヘルス・チェックの応答タイムアウト:** デフォルトは 2 秒。1 秒から 59 秒の範囲
* **最大再試行回数:** デフォルトは 2 回。1 回から 10 回の範囲

**注:** ヘルス・チェックの応答タイムアウトの値は、常にヘルス・チェックの間隔の値よりも小さくなければなりません。 

## このサービスで、リモート・データ・センターにあるコンピュート・インスタンスを使用できますか? 

ロード・バランサー・サービスとコンピュート・インスタンスは、同じデータ・センター内にローカルに配置されることが推奨されます。ロード・バランサー・サービスのグラフィカル・インターフェース (GUI) は、他のリモート・データ・センターのコンピュート・インスタンスを表示しません。ただし、GUI には、同じ市区町村内の他のデータ・センター (例えば、`DALxx` のように、名前の最初の 3 文字を共有するデータ・センター) のコンピュート・インスタンスは含まれます。しかし、API インスタンスを使用すると、どのリモート・データ・センターからのコンピュート・インスタンスも追加できます。 

## SSL オフロードでは、どの TLS バージョンがサポートされますか? どの暗号がサポートされますか? 

Bluemix Load Balancer サービスは、TLS 1.2 を SSL 終端処理とともにサポートしています。 

以下のリストは、サポートされる暗号の詳細を示しています (優先順でリスト)。  

* ECDHE-RSA-AES256-GCM-SHA384 
* ECDHE-RSA-AES256-SHA384 
* DHE-RSA-AES256-GCM-SHA384 
* DHE-RSA-AES256-SHA256 
* AES256-GCM-SHA384 
* AES256-SHA256 
* ECDHE-RSA-AES128-GCM-SHA256 
* ECDHE-RSA-AES128-SHA256 
* DHE-RSA-AES128-GCM-SHA256 
* DHE-RSA-AES128-SHA256 
* AES128-GCM-SHA256 
* AES128-SHA256 

## SSL 暗号リストをカスタマイズできますか? 

現時点ではできません。

## 自分のアカウント内に作成できるロード・バランサーのサービス・インスタンスの最大数を教えてください。 

現在、最大 20 個のサービス・インスタンスを作成できます。それより多くのインスタンスが必要な場合は、IBM サポートにお問い合わせください。 


