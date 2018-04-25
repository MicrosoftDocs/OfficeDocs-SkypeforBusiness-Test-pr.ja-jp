---
title: パブリック IM プロバイダーとのフェデレーションの有効化/無効化
TOCTitle: パブリック IM プロバイダーとのフェデレーションの有効化/無効化
ms:assetid: 8609682c-97d3-48e6-a243-d84c1f9c8419
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn362809(v=OCS.15)
ms:contentKeyID: 56270124
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# パブリック IM プロバイダーとのフェデレーションの有効化/無効化

 

_**トピックの最終更新日:** 2015-06-22_

パブリック インスタント メッセージング (IM) プロバイダーにアカウントがあるユーザーと通信できるようにするには、[Set-CsTenantFederationConfiguration](set-cstenantfederationconfiguration.md) コマンドレットを使用して AllowPublicUsers プロパティを True ($True) に設定します。

    Set-CsTenantFederationConfiguration -AllowPublicUsers $True

次に、[Set-CsTenantPublicProvider](set-cstenantpublicprovider.md) コマンドレットを使用して通信相手のパブリック IM プロバイダーを指定する必要があります。

パブリック プロバイダーのフェデレーションを無効にするには、AllowPublicUsers プロパティを false ($False) に設定し直します。

    Set-CsTenantFederationConfiguration -AllowPublicUsers $False

## 関連項目

#### 概念

[クイック リファレンス: Windows PowerShell を使用した一般的な Lync Online の管理タスクの実行](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

