---
title: インフラストラクチャおよび展開のコマンドレット
TOCTitle: インフラストラクチャおよび展開のコマンドレット
ms:assetid: 0a6e872a-9f70-4f23-a4a5-8820dbf55370
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg398153(v=OCS.15)
ms:contentKeyID: 48271206
ms.date: 12/10/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# インフラストラクチャおよび展開のコマンドレット

 

_**トピックの最終更新日:** 2016-12-08_

Microsoft Lync Server 2013 に含まれるインフラストラクチャと展開のコマンドレットは、製品の初期のセットアップと展開の際に役立ちます。Lync Server を展開した後、これらのコマンドレットを使用して、コンポーネントが正しく動作していることの確認、レプリケーション設定の管理、Lync Server のトポロジ、ポリシー、および構成設定のバックアップと復元などを実行できます。

## インフラストラクチャおよび展開のコマンドレット

インフラトラクチャと展開を管理者が直接呼び出す必要性はほとんどありません。セットアップやトポロジ ビルダーの実行時に、これらのコマンドレットが自動的に起動するからです (主な例外として **Export-CsConfiguration** コマンドレットがあります。このコマンドレットを使用すると、Lync Server のトポロジ、ポリシー、および構成設定のバックアップ コピーを作成できます)。ただし必要に応じて、インフラストラクチャと展開のコマンドレットを Lync Server 管理シェルやスクリプト内で実行することもできます。スクリプトを使用すると、特定のタスクを自動化できます。以下は、インフラストラクチャと展開に直接関連するコマンドレットの一覧です。

**[Active Directory のコマンドレット](lync-server-2013-active-directory-cmdlets.md)**

  -   
    [Disable-CsAdDomain](disable-csaddomain.md)

  -   
    [Enable-CsAdDomain](enable-csaddomain.md)

  -   
    [Get-CsAdDomain](get-csaddomain.md)

  -   
    [Disable-CsAdForest](disable-csadforest.md)

  -   
    [Enable-CsAdForest](enable-csadforest.md)

  -   
    [Get-CsAdForest](get-csadforest.md)

  -   
    [Get-CsAdServerSchema](get-csadserverschema.md)

  -   
    [Install-CsAdServerSchema](install-csadserverschema.md)

**[レプリケーションのコマンドレット](lync-server-2013-replication-cmdlets.md)**

  -   
    [Debug-CsInterPoolReplication](debug-csinterpoolreplication.md)

  -   
    [Invoke-CsManagementStoreReplication](invoke-csmanagementstorereplication.md)

  -   
    [Get-CsManagementStoreReplicationStatus](get-csmanagementstorereplicationstatus.md)

  -   
    [Enable-CsReplica](enable-csreplica.md)

  -   
    [Test-CsReplica](test-csreplica.md)

  -   
    [Get-CsUserReplicatorConfiguration](get-csuserreplicatorconfiguration.md)

  -   
    [New-CsUserReplicatorConfiguration](new-csuserreplicatorconfiguration.md)

  -   
    [Remove-CsUserReplicatorConfiguration](remove-csuserreplicatorconfiguration.md)

  -   
    [Set-CsUserReplicatorConfiguration](set-csuserreplicatorconfiguration.md)

**[トポロジのコマンドレット](lync-server-2013-topology-cmdlets.md)**

  -   
    [Get-CsPool](get-cspool.md)

  -   
    [Get-CsSite](get-cssite.md)

  -   
    [Set-CsSite](set-cssite.md)

  -   
    [Enable-CsTopology](enable-cstopology.md)

  -   
    [Get-CsTopology](get-cstopology.md)

  -   
    [Publish-CsTopology](publish-cstopology.md)

  -   
    [Test-CsTopology](test-cstopology.md)

  -   
    [Export-CsConfiguration](export-csconfiguration.md)

  -   
    [Import-CsConfiguration](import-csconfiguration.md)

  -   
    [Get-CsServerVersion](get-csserverversion.md)

  -   
    [Disable-CsComputer](disable-cscomputer.md)

  -   
    [Enable-CsComputer](enable-cscomputer.md)

  -   
    [Get-CsComputer](get-cscomputer.md)

  -   
    [Test-CsComputer](test-cscomputer.md)

  -   
    [Get-CsNetworkInterface](get-csnetworkinterface.md)

**[バックアップおよび高可用性のコマンドレット](lync-server-2013-backup-and-high-availability-cmdlets.md)**

  - [Get-CsBackupServiceConfiguration](get-csbackupserviceconfiguration.md)

  - [Remove-CsBackupServiceConfiguration](remove-csbackupserviceconfiguration.md)

  - [Set-CsBackupServiceConfiguration](set-csbackupserviceconfiguration.md)

  - [Get-CsBackupServiceStatus](get-csbackupservicestatus.md)

  - [Invoke-CsBackupServiceSync](invoke-csbackupservicesync.md)

  - [Debug-CsIntraPoolReplication](debug-csintrapoolreplication.md)

  - [Backup-CsPool](backup-cspool.md)

  - [Get-CsPoolBackupRelationship](get-cspoolbackuprelationship.md)

  - [Get-CsPoolFabricState](get-cspoolfabricstate.md)

  - [Invoke-CsPoolFailBack](invoke-cspoolfailback.md)

  - [Invoke-CsPoolFailOver](invoke-cspoolfailover.md)

  - [Get-CsPoolUpgradeReadinessState](get-cspoolupgradereadinessstate.md)

  - [Invoke-CsStorageServiceFlush](invoke-csstorageserviceflush.md)

  - [Sync-CsUserData](sync-csuserdata.md)

  - [Remove-CsUserStoreBackupData](remove-csuserstorebackupdata.md)

## 関連項目

#### その他のリソース

[Lync Server PowerShell ブログ](http://go.microsoft.com/fwlink/?linkid=203150%26clcid=0x411)

