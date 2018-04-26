---
title: Live ID Server への接続エラー
TOCTitle: Live ID Server への接続エラー
ms:assetid: 701af721-dd6a-4f48-96f9-94e89c644201
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn362811(v=OCS.15)
ms:contentKeyID: 56270094
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Live ID Server への接続エラー

 

_**トピックの最終更新日:** 2015-06-22_

次のエラー メッセージが表示されて接続試行が失敗する原因としては、通常は次の 3 つがあります。

    Get-CsWebTicket : Live ID サーバーに接続できませんでした。プロキシが有効であること、またはコンピューターから Live ID サーバーへのネットワーク接続ができることをご確認ください。

多くの場合、このエラーは、Microsoft Online Services サインイン アシスタントが実行されていないことを意味します。Windows PowerShell プロンプトから次のコマンドを実行すると、このサービスの状態を確認できます。

    Get-Service "msoidsvc"

サービスが実行されていない場合は、次のコマンドを使用してサービスを開始します。

    Start-Service "msoidsvc"

サービスが実行されている場合、コンピューターと Microsoft Live ID Authentication Server との間のネットワーク接続に関する問題が発生している可能性があります。これを調べるには、Internet Explorer を開き、<https://login.microsoftonline.com/> にアクセスします。ここから、Office 365 へのログオンを試行します。ログオンが失敗した場合は、ネットワーク接続の問題が発生していると考えられます。

まれに、Microsoft Live ID Authentication Server の接続 URI が正しくない値に構成されている可能性があります。サインイン アシスタントが実行されていて、ネットワーク接続の問題が発生していないことを既に確認した場合は、このことが問題である可能性があります。この場合は、Office 365 サポートに連絡してください。

## 関連項目

#### 概念

[Lync Online との接続の問題の診断と解決](diagnosing-and-resolving-connection-problems-with-skype-for-business-online.md)

