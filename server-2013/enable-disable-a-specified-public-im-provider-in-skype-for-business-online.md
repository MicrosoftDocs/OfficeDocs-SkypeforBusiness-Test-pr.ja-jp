---
title: 指定したパブリック IM プロバイダーの有効化/無効化
TOCTitle: 指定したパブリック IM プロバイダーの有効化/無効化
ms:assetid: 9d3e2607-01c0-4ae9-accc-39f03ce253bb
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn362825(v=OCS.15)
ms:contentKeyID: 56270116
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 指定したパブリック IM プロバイダーの有効化/無効化

 

_**トピックの最終更新日:** 2015-06-22_

Skype for Business Online では、次の少なくとも 1 つのパブリック インスタント メッセージング (IM) プロバイダーのユーザーとのフェデレーションを確立できます。

  - インターネット サービスの Windows Live ネットワーク

  - Yahoo\!

  - AOL

これらのうち、少なくとも 1 つのプロバイダーとフェデレーションできるようにするには、[Set-CsTenantPublicProvider](set-cstenantpublicprovider.md) コマンドレットを使用して、Provider プロパティの値に、次の値のうちの少なくとも 1 つを設定します。

  - Windows Live

  - Yahoo

  - AOL

たとえば、次のコマンドで Windows Live と AOL とのフェデレーションが確立されます。

    Set-CsTenantPublicProvider -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -Provider "AOL","WindowsLive"

プロバイダーを追加または削除する際には、必ず関連するフェデレーション プロバイダーをすべてコマンドに含める必要があります。たとえば Yahoo\! を追加する場合は次のコマンドを実行します。

    Set-CsTenantPublicProvider -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -Provider "Yahoo"

このコマンドを実行すると、Yahoo\! がコマンドで呼び出されるプロバイダーとなるため、唯一のフェデレーション プロバイダーとして残ります。3 つのパブリック IM プロバイダーすべてとフェデレーションを確立するには、これら 3 つのプロバイダーをすべて含める必要があります。

    Set-CsTenantPublicProvider -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -Provider "Yahoo", "AOL","WindowsLive"

Set-CsTenantPublicProvider コマンドレットを呼び出す際には、Tenant パラメーターを含める必要があります。このパラメーターを含めないと、テナント ID の入力を求められます。次のコマンドを使用して、Skype for Business Online テナントのテナント ID を返すことができます。

    Get-CsTenant | Select-Object TenantID

または、次のコマンドを使用してテナント ID を変数に保存します。

    $tenantID = (Get-CsTenant | Select-Object TenantID)

こうすれば、Set-CsTenantPublicProvider を呼び出す際にこの変数 (この例では $tenantID) を使用できます。

    Set-CsTenantPublicProvider -Tenant $tenantID -Provider "Yahoo", "AOL","WindowsLive"

## 関連項目

#### 概念

[クイック リファレンス: Windows PowerShell を使用した一般的な Lync Online の管理タスクの実行](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

