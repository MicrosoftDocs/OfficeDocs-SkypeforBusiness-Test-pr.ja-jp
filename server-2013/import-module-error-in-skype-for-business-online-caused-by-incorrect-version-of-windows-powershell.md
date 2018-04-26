---
title: 不適切なバージョンの Windows PowerShell が原因である Import-Module エラー
TOCTitle: 不適切なバージョンの Windows PowerShell が原因である Import-Module エラー
ms:assetid: 6c209f41-2b97-4dda-b0b7-e5b582d3e6b6
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn362802(v=OCS.15)
ms:contentKeyID: 56270098
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 不適切なバージョンの Windows PowerShell が原因である Import-Module エラー

 

_**トピックの最終更新日:** 2015-06-22_

Skype for Business Online Connector モジュールは Windows PowerShell 3.0 のみで実行できます。以前のバージョンの Windows PowerShell でモジュールをインポートしようとすると、次のようなメッセージが表示されてインポート プロセスが失敗します。

    Import-Module : 読み込まれた PowerShell のバージョンは '2.0' です。モジュール 'D:\Program Files\Common Files\Microsoft Lync Server 2013\Modules\LyncOnlineConnector\LyncOnlineConnector.psd1' の実行に必要な PowerShell の最小バージョンは '3.0' です。インストールされている PowerShell を確認し、再度お試しください。

この問題を修正する唯一の方法としては、Microsoft ダウンロードセンター ([http://www.microsoft.com/en-us/download/details.aspx?id=29939](http://search.microsoft.com/ja-jp/downloadresults.aspx?rf=sp%26q=%26sortby=+weight%26ftapplicableproducts=%5e%22servers%22)) から入手できる Windows PowerShell 3.0 をインストールします。

## 関連項目

#### 概念

[Lync Online との接続の問題の診断と解決](diagnosing-and-resolving-connection-problems-with-skype-for-business-online.md)

