---
title: Get-CsVoicemailReroutingConfiguration
TOCTitle: Get-CsVoicemailReroutingConfiguration
ms:assetid: 25e401eb-6a84-468f-b0eb-5b794f20b5bc
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg425732(v=OCS.15)
ms:contentKeyID: 48271512
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsVoicemailReroutingConfiguration

 

_**トピックの最終更新日:** 2015-03-09_

Exchange UM のサブスクライバー アクセス機能と自動応答機能を利用する目的で、公衆交換電話網 (PSTN) 電話番号を指定する設定を取得します。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Get-CsVoicemailReroutingConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsVoicemailReroutingConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 例

## 例 1

この例では、この Lync Server 展開で定義されているすべてのボイスメール再ルーティング構成設定を取得します。たとえば、存続可能ブランチ アプライアンスが展開されている支店のオフィスが 3 か所存在する場合、このコマンドは 3 つのボイスメール再ルーティング構成設定を戻します。

    Get-CsVoicemailReroutingConfiguration

## 例 2

この例では、BranchOffice\_Portland サイトのボイスメール再ルーティング構成設定を取得します。

    Get-CsVoicemailReroutingConfiguration -Identity site:BranchOffice_Portland

## 例 3

この例では、サイト名が文字列 BranchOffice (BranchOffice\_Portland, BranchOffice\_Sacramento など) で始まるすべてのサイトのボイスメール再ルーティング設定をすべて取得します。

    Get-CsVoicemailReroutingConfiguration -Filter *:BranchOffice*

## 例 4

この例では、有効になっていないすべてのボイスメール再ルーティング構成を取得します。このコマンドの最初の部分で、**Get-CsVoicemailReroutingConfiguration** コマンドレットを呼び出して、すべてのボイスメール再ルーティング構成のコレクションを取得します。次に、このコレクションは、**Where-Object** コマンドレットにパイプ処理されます。**Where-Object** コマンドレットは、Enabled プロパティが False に等しい (-eq) 構成のみが含まれるように、コレクションを絞り込みます。

    Get-CsVoicemailReroutingConfiguration | Where-Object {$_.Enabled -eq $False}

## 解説

このコマンドレットは、支店サイトの Lync Server からデータ センターに配置されている Exchange UM サーバーへの IP 接続が利用できない場合に、自動応答およびサブスクライバー アクセス通話の再ルーティング先を判断する設定を取得します。

自動応答およびサブスクライバー アクセスは、Exchange UM の機能です。自動応答機能では、外部の発信者が会社の電話システム内を移動して目的の部門や従業員に到達できるよう、音声認識とタッチトーン制御 (デュアルトーン多重周波数、つまり DTMF) を行ったり、留守番電話モードでユーザーのメッセージを録音したりできます (留守番電話モードの音声再ルーティングを推奨します)。サブスクライバー アクセスでは、内部ユーザーが電話から自分の Microsoft Outlook のメールボックスにアクセスできます。これらの設定により提供された番号では、発信者は、エンタープライズ VoIP ユーザーにボイスメール メッセージを残すことができ (AutoAttendantNumber 設定)、これらのユーザーは、リモート サイトの Lync Server 展開からデータ センター内の Exchange UM への IP 接続が利用できない場合でも、ボイスメールを取得できます (SubscriberAccessNumber 設定)。

パラメーターを指定せずにこのコマンドレットを呼び出すと、すべてのボイスメール再ルーティング構成が戻されます。

このコマンドレットを実行できるメンバー。既定では、次のグループのメンバーが、**Get-CsVoicemailReroutingConfiguration** コマンドレットをローカルで実行することを承認されています。RTCUniversalUserAdmins、RTCUniversalServerAdmins。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsVoicemailReroutingConfiguration"}

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
<td><p>Filter パラメーターにより、ワイルドカードの一致に基づいて特定のサイト セットの構成設定を取得できます。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>省略可能</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>取得する構成の一意の識別子。このコマンドレットの場合、Identity は Global または Site:&lt;サイト名&gt; のいずれかになります。&lt;サイト名&gt; は、設定が適用されるサイトの名前です。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>中央管理ストア 自体からではなく、中央管理ストア のローカル レプリカからボイスメール再ルーティング構成を取得します。</p></td>
</tr>
</tbody>
</table>


## 入力の種類

なし。

## 戻り値の種類

Microsoft.Rtc.Management.WritableConfig.Settings.ExumRouting.VoicemailReroutingConfiguration 型の 1 つ以上のオブジェクトを取得します。

## 関連項目

#### その他のリソース

[New-CsVoicemailReroutingConfiguration](new-csvoicemailreroutingconfiguration.md)  
[Remove-CsVoicemailReroutingConfiguration](remove-csvoicemailreroutingconfiguration.md)  
[Set-CsVoicemailReroutingConfiguration](set-csvoicemailreroutingconfiguration.md)

