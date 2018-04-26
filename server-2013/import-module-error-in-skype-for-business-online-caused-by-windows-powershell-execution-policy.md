---
title: Windows PowerShell の実行ポリシーが原因である Import-Module エラー
TOCTitle: Windows PowerShell の実行ポリシーが原因である Import-Module エラー
ms:assetid: 4bc093ca-fd30-44c9-a0a3-16f78698df2b
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn362786(v=OCS.15)
ms:contentKeyID: 56270071
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Windows PowerShell の実行ポリシーが原因である Import-Module エラー

 

_**トピックの最終更新日:** 2016-12-08_

Windows PowerShell の実行ポリシーは、どの構成ファイルを Windows PowerShell コンソールに読み込むことができ、またそのコンソールからユーザーがどのスクリプトを実行できるかを確認するのに役立ちます。少なくとも、実行ポリシーが RemoteSigned に設定されている場合を除き、Skype for Business Online Connector モジュールをインポートすることはできません。このように設定されていない場合は、モジュールをインポートしようとすると次のエラー メッセージが表示されます。

    Import-Module : このシステムではスクリプトの実行が無効になっているため、ファイル C:\Program Files\Common Files\Microsoft Lync Server 2013\Modules\LyncOnlineConnector\LyncOnlineConnectorStartup.psm1 を読み込むことができません。詳しくは、http://go.microsoft.com/fwlink/?LinkID=135170 の「about_Execution_Policies」をご覧ください。

この問題を解決するには、管理者として Windows PowerShell を起動し、次のコマンドを実行します。

    Set-ExecutionPolicy RemoteSigned

実行ポリシーについて詳しくは、[http://go.microsoft.com/fwlink/?LinkID=135170](http://go.microsoft.com/fwlink/?linkid=135170) のヘルプ トピックをご覧ください。

## 関連項目

#### 概念

[Lync Online との接続の問題の診断と解決](diagnosing-and-resolving-connection-problems-with-skype-for-business-online.md)

