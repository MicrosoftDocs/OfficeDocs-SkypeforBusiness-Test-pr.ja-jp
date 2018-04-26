---
title: 'Lync Online: Lync Online レポート生成コマンドレットと REST Web サービス'
TOCTitle: Lync Online のレポート生成コマンドレットと REST Web サービス
ms:assetid: cadd73a7-c08a-4102-b73a-ccb3ad4987bf
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn362845(v=OCS.15)
ms:contentKeyID: 56270147
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Online のレポート生成コマンドレットと REST Web サービス

 

_**トピックの最終更新日:** 2016-12-08_

Skype for Business Online にはレポート機能と、これらのレポートを生成し、管理者がカスタマイズしたレポート データを取得できる 5 つの Windows PowerShell コマンドレットがあります。Skype for Business Online には REST (Representational State Transfer) も含まれており、開発者はカスタマイズされたレポート情報を取得できます。

管理者が使用できるレポート用コマンドレットには次のようなものがあります。

  - Get-CsActiveUserReport。アクティブ ユーザー (Skype for Business Online にログオンしており、少なくとも 1 つの会議かピアツーピアの通信セッションに参加しているユーザー) の数に関する情報を取得できます。

  - Get-CsAVConferenceTimeReport。音声/ビデオ会議にかかった時間 (分単位) に関する情報を取得できます。

  - Get-CsConferenceReport。ユーザーが参加した会議の数と種類に関する情報を取得できます。

  - Get-CsP2PAVTimeReport。音声やビデオを含むピアツーピア セッションにかかった時間 (分単位) に関する情報を取得できます。

  - Get-CsP2PSessionReport。ユーザーが参加したピアツーピア セッションの数と種類に関する情報を取得できます。

ほとんどの管理者は Office 365 管理センターで入手できるレポートを使用します。ここには自動生成されるレポートだけでなく、データがグラフィカル表示されるレポートもあるため、多くの管理者は、レポート用コマンドレットで返される生の数値より簡単に内容を理解できます。ただし Windows PowerShell に精通した管理者は、レポート用コマンドレットを使用して、 Lync Online レポートからは簡単に使用できないデータを取得できます。たとえば、レポート用コマンドレットでセッション期間 (各セッションの分単位の継続時間) に関する情報が返されるとします。Lync Online のレポートではセッション期間はわかりません。同様に、Lync Online のレポートの日ビューには前の 14 日間の情報しか表示されません。別の日 (4 か月前の日付など) の日単位の合計を表示したい場合は、レポート用コマンドレットを使用して実行できます。

Microsoft Excel の OData データ クエリ機能を使用する方法についての記事 [Excel を使用して Office 365 レポート データを取得する](http://msdn.microsoft.com/en-us/library/dn781442.aspx) も参照してください。カスタム レポートでは、Office 365 のレポート サービスから返されるデータ (およびデータの量) を指定できます。また、カスタム レポートでは、データを並べ替えおよびグループ化する方法を指定できます。また、Office 365 管理センター レポートでは利用できない情報にアクセスすることもできます。

開発スキルのある管理者は、REST Web サービスを使用して、Skype for Business Online 管理センターに表示されない情報を取得できます。REST サービスは、クライアントとサーバー間の XML データ転送を可能にするという点で、SOAP サービスと似ています。ただし、REST サービスは SOAP サービスと比べて少なくとも 2 つの利点があります。1 つは、REST では ATOM 配信形式という標準的な形式で、XML データ転送が実行されるという点です。これに対し、SOAP ではデータ転送に標準以外の形式が使用されます。また、REST では (GET と POST 以外の) HTTP 動詞が禁止されているネットワーク間でデータを転送できます。

## 関連項目

#### その他のリソース

[Lync Online のレポート機能](https://technet.microsoft.com/ja-jp/library/dn362827\(v=ocs.15\))  
[Office 365 レポート Web サービス](http://msdn.microsoft.com/en-us/library/office/jj984325.aspx)  
[Office 365 レポート Web サービスの概要](http://msdn.microsoft.com/en-us/library/office/jj984321.aspx)  
[Exchange Online のレポート用コマンドレット](http://technet.microsoft.com/en-us/library/jj200780\(v=exchg.150\).aspx)  
[Excel を使用して Office 365 レポート データを取得する Excel を使用して Office 365 レポート データを取得する](http://msdn.microsoft.com/en-us/library/dn781442.aspx)

