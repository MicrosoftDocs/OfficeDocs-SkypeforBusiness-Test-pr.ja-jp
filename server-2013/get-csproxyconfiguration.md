---
title: Get-CsProxyConfiguration
TOCTitle: Get-CsProxyConfiguration
ms:assetid: e4836619-026f-4df0-adbd-aa5216e36368
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg399011(v=OCS.15)
ms:contentKeyID: 48273864
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsProxyConfiguration

 

_**トピックの最終更新日:** 2015-03-09_

組織で現在使用されているプロキシ サーバーの構成設定に関する情報を戻します。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Get-CsProxyConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsProxyConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 例

## 例 1

例 1 に示すコマンドでは、組織内で現在使用されているすべてのプロキシの構成設定のコレクションを戻します。**Get-CsProxyConfiguration** コマンドレットをパラメーターなしで呼び出すことで、これを実行しています。

    Get-CsProxyConfiguration

## 例 2

例 2 では、service:EdgeServer:atl-cs-001.litwareinc.com という Identity を持つプロキシ構成設定に関する情報を戻しています。Identity は一意である必要があるため、このコマンドが複数の設定のコレクションを戻すことはありません。

    Get-CsProxyConfiguration -Identity "service:EdgeServer:atl-cs-001.litwareinc.com"

## 例 3

例 3 では、サービス スコープで構成されているすべてのプロキシ設定に関する情報を返します。そのために、このコマンドは **Get-CsProxyConfiguration** コマンドレットに Filter パラメーターを指定して呼び出しています。フィルター値 "service:\*" により、文字列値 "service:" で始まる ID を持つ設定のみが返されます。

    Get-CsProxyConfiguration -Filter "service:*"

## 例 4

例 4 では、認証メカニズムとしてクライアント証明書を使用することが許可されていないプロキシの構成設定に関する情報を戻します。このタスクを実行するため、まず **Get-CsProxyConfiguration** コマンドレットを使用して、現在使用されているすべてのプロキシの構成設定のコレクションを戻しています。次に、このコレクションを **Where-Object** コマンドレットにパイプ処理し、UseCertificateForClientToProxyAuth プロパティが False に等しい設定のみを選択しています。

    Get-CsProxyConfiguration | Where-Object {$_.UseCertificateForClientToProxyAuth -eq $False}

## 例 5

例 5 では、クライアント メッセージの本文の最大サイズが 5,000 KB 未満のすべてのプロキシ構成設定が返されます。そのために、このコマンドは最初に **Get-CsProxyConfiguration** コマンドレットをパラメーターなしで呼び出しています。これにより、現在使用されているすべてのプロキシ構成設定のコレクションが返されます。次に、このコレクションを **Where-Object** コマンドレットにパイプ処理し、MaxClientMessageBodySizeKb プロパティが 5,000 KB 未満の設定を抽出しています。

    Get-CsProxyConfiguration | Where-Object {$_.MaxClientMessageBodySizeKb -lt 5000}

## 解説

Lync Server では、プロキシ サーバー構成設定によってプロキシ サーバーを管理できます。こうした設定は、グローバル スコープとサービス スコープ (ただし、エッジ サーバー サービスおよびレジストラー サービスの場合のみ) の両方で適用でき、クライアント エンドポイントによって使用できる認証プロトコルや、受信および送信のプロキシ サーバー接続での圧縮の使用の有無といった項目の制御を可能にします。Lync Server をインストールすると、プロキシ サーバー構成設定のグローバル コレクションが自動的に作成されます。既に説明したように、サービス スコープで追加のコレクションを作成することもできます。

**Get-CsProxyConfiguration** コマンドレットを使用すると、組織内で現在使用されているプロキシ サーバーの任意の構成設定に関する情報を戻すことができます。

このコマンドレットを実行できるユーザー: 既定では、次のグループのメンバーは **Get-CsProxyConfiguration** コマンドレットのローカル実行を承認されています。RTCUniversalUserAdmins、RTCUniversalServerAdmins。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsProxyConfiguration"}

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
<th>必須かどうか</th>
<th>型</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>Filter</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.String</p></td>
<td><p>戻すプロキシの構成設定を指定するときに、ワイルドカードを使用できます。たとえば次の構文では、サービス スコープで構成されたすべての設定を戻します。-Filter &quot;service:*&quot; です。</p>
<p>Filter パラメーターと Identity パラメーターの両方を同じコマンドで使用することはできません。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>省略可能</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>戻すプロキシ サーバーの構成設定の一意の識別子です。グローバル設定を戻すには、次の構文を使用します。-Identity global です。サービス スコープで構成された設定を戻すには、次のような構文を使用します。-Identity &quot;service:EdgeServer:atl-cs-001.litwareinc.com&quot; です。Identity 指定時はワイルドカードを使用できないことに注意してください。ワイルドカードを使用する (またはその必要がある) 場合は、代わりに Filter パラメーターを使用してください。</p>
<p>このパラメーターを指定しないと、<strong>Get-CsProxyConfiguration</strong> コマンドレットは組織内で現在使用されているプロキシ サーバーの構成設定をすべて戻します。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>中央管理ストア 自体からではなく、中央管理ストア のローカル レプリカからプロキシ構成データを取得します。</p></td>
</tr>
</tbody>
</table>


## 入力の種類

なし。**Get-CsProxyConfiguration** コマンドレットは、パイプライン処理された入力を受け入れません。

## 戻り値の種類

**Get-CsProxyConfiguration** コマンドレットを実行すると、Microsoft.Rtc.Management.WritableConfig.Settings.SipProxy.ProxySettings オブジェクトのインスタンスが戻されます。

## 関連項目

#### その他のリソース

[New-CsProxyConfiguration](new-csproxyconfiguration.md)  
[Remove-CsProxyConfiguration](remove-csproxyconfiguration.md)  
[Set-CsProxyConfiguration](set-csproxyconfiguration.md)

