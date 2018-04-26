---
title: Get-CsTenantHybridConfiguration
TOCTitle: Get-CsTenantHybridConfiguration
ms:assetid: 4b2e6781-8f46-4ba3-be76-3a95460e3132
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ994034(v=OCS.15)
ms:contentKeyID: 52056597
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsTenantHybridConfiguration

 

_**トピックの最終更新日:** 2015-03-09_

Microsoft Lync Online に属するユーザーがメディア バイパス、Enhanced 9-1-1、コール パークなどのエンタープライズ VoIP 機能にアクセスできるようにするハイブリッド構成設定の値を返します。ハイブリッドのシナリオ (分割ドメインのシナリオとも呼ばれます) は、社内バージョンに属するアカウントを持つユーザーだけでなく、Lync Online に属するアカウントを持つユーザーも存在する Lync Server 展開です。

Get-CsTenantHybridConfiguration コマンドレットは、Skype for Business Online でのみ使用できます。

## 構文

    Get-CsTenantHybridConfiguration [[-Identity] <XdsIdentity>] [-Tenant <guid>] [-LocalStore] [<CommonParameters>]Get-CsTenantHybridConfiguration [-Tenant <guid>] [-Filter <string>] [-LocalStore] [<CommonParameters>]

## 例

## 例 1

例 1 に示すコマンドは、テナント ハイブリッド構成設定のグローバル コレクションのプロパティ値を返します。

    Get-CsTenantHybridConfiguration -Identity "Global"

## 例 2

例 2 では、TenantId が "bf19b7db-6960-41e5-a139-2aa373474354" のテナントに適用されたカスタム テナント ハイブリッド構成設定のプロパティ値が返されます。

    Get-CsTenantHybridConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354"

## 例 3

例 3 では、使用可能なすべてのテナントに関するテナント ハイブリッド構成情報を返します。これを行うために、このコマンドは最初に **Get-CsTenant** コマンドレットを呼び出して、これらのテナントすべてのコレクションを返します。次に、このコレクションを **ForEach-Object** コマンドレットにパイプ処理し、コレクション内の各テナントを取得して、テナントごとに 2 つのタスクを実行します。まず、このコマンドレットは、テナントの Active Directory 表示名を出力します。これにより、設定の各コレクションを簡単に識別できるようになります。その後、**ForEach-Object** コマンドレットは、**Get-CsTenantHybridConfiguration** コマンドレットを実行して、該当のテナントのテナント ハイブリッド構成設定を返します。

    Get-CsTenant | ForEach-Object {$_.DisplayName; Get-CsTenantHybridConfiguration -Tenant $_.TenantId}

## 解説

ハイブリッド展開または "分割ドメイン" 展開では、組織に Lync Online に属するアカウントを持つユーザーと Lync Server の社内バージョンに属するアカウントを持つユーザーが同時に存在します。既定では、Lync Online に属するユーザーは、エンタープライズ VoIP によって提供される全機能にアクセスできません。これは、Lync Online サーバーが Lync Server 展開およびネットワーク構成設定情報に直接アクセスすることができないためです。特に、Lync Online ユーザーは、以下のような機能に既定でアクセスできません。

  - Enhanced 9-1-1。これは、緊急電話の発信に使用する Lync Server サービスです。

  - コール パーク。これは、ユーザーが電話 A の通話を保留して、電話 B からその通話の保留を解除できるようにする Lync Server サービスです。

  - メディア バイパス。これを使用すると、公衆交換電話通信網 (PSTN) の通話で仲介サーバーをバイパスすることができます。これにより、コード変換とネットワーク遅延が最小限に抑えられます。

  - PSTN 会議のダイヤルインおよびダイヤルアウト。これを使用すると、ユーザーは、任意の PSTN 電話またはモバイル デバイスを使用してオンライン会議の音声部分に参加できます。

  - 応答グループ アプリケーション。これを使用すると、ヘルプ デスクや顧客サポート ラインなどのエンティティに通話を自動的にルーティングすることができます。既定では、Lync Server ユーザーは、応答グループ エージェントの役割を果たすことはできません。

Lync Online ユーザーがこれらのエンタープライズ VoIP 機能にアクセスできるようにするには、管理者は Web サービスの内部および外部 URL、組織のアクセス エッジ サーバーの完全修飾ドメイン名などのハイブリッド構成設定に、適切な値を割り当てる必要があります。**Set-CsTenantHybridConfiguration** コマンドレットを使用してのみ構成できるこれらの値により、高度なエンタープライズ VoIP 機能を使用するために必要な情報が Lync Online サーバーに提供されます。

**Get-CsTenantHybridConfiguration** コマンドレットを使用すると、組織で現在使用されているテナント ハイブリッド構成設定に関する情報を返すことができます。

## パラメーター


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>パラメーター</th>
<th>必須</th>
<th>型</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>Filter</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.String</p></td>
<td><p>ワイルドカード文字を使用して、テナント ハイブリッド構成設定のコレクションを返すことができます。ハイブリッド構成設定のグローバル コレクションは 1 つに制限されるため、Filter パラメーターを使用する必要はありません。ただし、次の構文は <strong>Get-CsTenantHybridConfiguration</strong> コマンドレットに有効です。</p>
<p>Get-CsTenantHybridConfiguration –Filter &quot;g*&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>省略可能</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>返されるテナント ハイブリッド構成設定の一意の識別子です。ハイブリッド構成設定のグローバル コレクションは 1 つに制限されるため、次の Identity パラメーターを使用して返されるコレクションは、グローバル コレクションのみです。</p>
<p>-Identity global</p>
<p>個別のテナントの設定を変更するには、Identity パラメーターではなく、Tenant パラメーターを使用します。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>中央管理ストア自体からではなく、中央管理ストアのローカル レプリカからテナント ハイブリッド構成データを取得します。</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Guid</p></td>
<td><p>ハイブリッド構成設定が返されるテナント アカウントのグローバル一意識別子 (GUID) です。次に例を示します。</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>次のコマンドを実行することにより、テナントの各々についてテナント ID を返すことができます。</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p>
<p>Windows PowerShell のリモート セッションを使用していて、 Skype for Business Online のみに接続している場合、Tenant パラメーターを含める必要はありません。代わりに、接続情報に基づいてテナント ID が自動的に入力されます。Tenant パラメーターはハイブリッド展開で主に使用されます。</p></td>
</tr>
</tbody>
</table>


## 入力の種類

なし。**Get-CsTenantHybridConfiguration** コマンドレットはパイプライン入力を受け入れません。

## 戻り値の種類

**Get-CsTenantHybridConfiguration** コマンドレットは、Microsoft.Rtc.Management.WritableConfig.Settings.HybridConfiguration.TenantHybridConfiguration オブジェクトのインスタンスを返します。

## 関連項目

#### その他のリソース

[Set-CsTenantHybridConfiguration](set-cstenanthybridconfiguration.md)

