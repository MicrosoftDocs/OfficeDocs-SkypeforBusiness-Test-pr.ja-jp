---
title: アドレス帳管理用の new-cswebserviceconfiguration
TOCTitle: アドレス帳管理用の new-cswebserviceconfiguration
ms:assetid: 49e4ecc5-aa3e-4dd4-a32c-b0dea3758fab
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg429703(v=OCS.15)
ms:contentKeyID: 48271988
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# アドレス帳管理用の new-cswebserviceconfiguration

 

_**トピックの最終更新日:** 2012-11-01_

このコマンドレットを実行できる人は次のとおりです。 既定では、次のグループのメンバーが new-cswebserviceconfiguration コマンドレットをローカルで実行することを承認されています。 RTCUniversalServerAdmins。 このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

    Get-CsAdminRole | Where-Object {$_.Cmdlets -match "new-cswebserviceconfiguration"}

コマンドレット new-cswebserviceconfiguration は、組織内の Web サービスの新しい構成を定義します。 Web サービス構成のスコープは、サイトまたはサービスのレベルのみです。 グローバル レベルで新しい Web サービス構成を作成することはできません。 アドレス帳で特に注目すべきなのは EnableGroupExansion 属性です。 これが True に設定されていると、Web サービスがグループ拡張の要求に応答できます。

次にその例を示します。

    new-cswebserviceconfiguration -Identity site:Redmond -EnableGroupExpansion $False -UseCertificateAuth $True

コマンド全体の詳細については、Lync Server Windows PowerShell RTCCmdlets メイン リファレンスの次の項目を参照してください。

## 関連項目

#### その他のリソース

[new-cswebserviceconfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsWebServiceConfiguration)

