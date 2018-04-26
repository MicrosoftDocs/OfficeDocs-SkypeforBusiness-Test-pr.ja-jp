---
title: New-CsNetworkMediaBypassConfiguration
TOCTitle: New-CsNetworkMediaBypassConfiguration
ms:assetid: 24055ae5-7fc8-4ca5-9e65-ac3a1f17b405
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg425718(v=OCS.15)
ms:contentKeyID: 48271500
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsNetworkMediaBypassConfiguration

 

_**トピックの最終更新日:** 2015-03-09_

メディア バイパスの新規グローバル設定を作成します。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    New-CsNetworkMediaBypassConfiguration [-AlwaysBypass <$true | $false>] [-BypassID <String>] [-Enabled <$true | $false>] [-EnableDefaultBypassID <$true | $false>] [-EnabledForAudioVideoConferences <$true | $false>] [-ExternalBypassMode <Off | ICE | Any>] [-InternalBypassMode <Off | ICE | Any>]

## 例

## 例 1

この例のコマンドにより、メディア バイパスを有効にし、常にバイパスを試みるように構成されます。例の 1 行目は、**New-CsNetworkMediaBypassConfiguration** コマンドレットの呼び出しです。このコマンドレットに、AlwaysBypass と Enabled の 2 つのパラメーターを、両方を True ($true) に設定した状態で渡します。Enabled を True に設定するとメディア バイパスが有効になるのに対し、AlwaysBypass を True に設定すると、すべての通話で必ずメディア バイパスが試みられます。(これら 2 つのパラメーターを設定すると、BypassID プロパティの値が自動的に生成されます。)**New-CsNetworkMediaBypassConfiguration** コマンドレットは、メモリ内でのみオブジェクトを作成するため、そのオブジェクトを変数 $a に割り当てます。

メディア バイパス構成はネットワーク構成の設定と一緒に保存されます。したがって、例の 2 行目では、**Set-CsNetworkConfiguration** コマンドレットを呼び出し、1 行目で作成したメディア バイパス構成オブジェクト ($a) を MediaBypassSettings パラメーターに渡すことによって、メディア バイパス構成の変更点をネットワーク構成に保存します。

    $a = New-CsNetworkMediaBypassConfiguration -AlwaysBypass $true -Enabled $true
    Set-CsNetworkConfiguration -MediaBypassSettings $a

## 例 2

Lync Server には **Set-CsNetworkMediaBypassConfiguration** コマンドレットがないため、既存の設定を変更するには、(例 1 に示すように) 新しい構成を作成して既存の構成と置き換えるか、既存の設定を取得し、それらの設定を変更し、変更点を保存する **Set-CsNetworkConfiguration** コマンドレットを使用して設定を変更する必要があります。この例では、後者のオプションを使用することによって AlwaysBypass オプションをオフにする方法を示しています。

例の最初の行は、既存のメディア バイパス設定を取得します。これを実行するには、**Get-CsNetworkConfiguration** コマンドレットを呼び出します。このコマンドレットへの呼び出しは、コマンドレットが必ずコマンドの他の部分が実行される前に完了するようにするため、かっこで囲まれています。**Get-CsNetworkConfiguration** コマンドレットは、ネットワーク構成全体のすべての設定を取得します。関心の対象はメディア バイパスの設定のみであるため、それらの設定のみを取得するように MediaBypassSettings プロパティを指定します。それらの設定を変数 $a に割り当てます。

2 行目では、値として False ($false) を AlwaysBypass プロパティに割り当てることによって、変数 $a に保存されている設定を変更します。最後に、3 行目では、**Set-CsNetworkConfiguration** コマンドレットを呼び出して MediaBypassSettings パラメーターに変数 $a を渡して、AlwaysBypass プロパティに対して行った変更を保存します。

    $a = (Get-CsNetworkConfiguration).MediaBypassSettings
    $a.AlwaysBypass = $false
    Set-CsNetworkConfiguration -MediaBypassSettings $a

## 解説

このコマンドレットは、オーディオ接続のメディア バイパスについてのグローバル設定を作成します。

Lync Server のほとんどの New- コマンドレットとは異なり、このコマンドレットは新しい構成をすぐには保存せず、メモリ内で設定を作成するだけです。このコマンドレットによって作成されたオブジェクトは、変数に保存してから、ネットワーク構成の MediaBypassSettings プロパティに割り当てる必要があります (詳細については、このトピックの「例」セクションを参照してください)。

このコマンドレットによって作成された設定は、グローバル ネットワーク構成の MediaBypassSettings プロパティにアクセスすることによってのみ取得することができます。これらの設定を取得するには、次のコマンドを実行します。(Get-CsNetworkConfiguration).MediaBypassSettings。

このコマンドレットを実行できるメンバー。既定では、次のグループのメンバーが、**New-CsNetworkMediaBypassConfiguration** コマンドレットをローカルで実行することを承認されています。RTCUniversalServerAdmins。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsNetworkMediaBypassConfiguration"}

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
<td><p><em>AlwaysBypass</em></p></td>
<td><p>省略可能</p></td>
<td><p>Boolean</p></td>
<td><p>このパラメーターを True に設定すると、すべての通話でメディア バイパスが試みられます。</p>
<p>このパラメーターの値は、通話受付管理 (CAC) が無効になっている場合のみ True に設定します。このパラメーターを True に設定するのは、次のような展開の場合のみです。</p>
<p>- 帯域幅の制御が必要ない。</p>
<p>- バイパスが発生する場合を指定する、詳細な構成が必要ない。</p>
<p>- ゲートウェイとクライアント間に十分な接続がある。</p>
<p>Enabled パラメーターを True に設定して AlwaysBypass を False に設定している場合、バイパス ロジックは、ネットワーク構成サイトと地域を使用して、いつバイパスを実行できるのかを判断します。</p>
<p>AlwaysBypass を True に設定する場合は、同時に Enable パラメーターの値も True に設定しないと、警告メッセージが表示されます。AlwaysBypass 設定は、Enabled が False に設定されている場合は無視されます。</p>
<p>AlwaysBypass と Enabled の両方を True に設定すると、バイパス ID が自動生成され、BypassID プロパティに保存されます。</p>
<p>既定値は次のとおりです。False</p></td>
</tr>
<tr class="even">
<td><p><em>BypassID</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>メディア バイパス ID。AlwaysBypass パラメーターを True に設定してこのパラメーターの値を指定している場合、この BypassID はすべてのサブネットに関連付けられます。AlwaysBypass が False の場合、BypassID の値はネットワーク構成サイトと地域にないすべてのサブネットに関連付けられます。</p>
<p>この ID の形式は GUID (たとえば、96f14dea-5170-429a-b92b-f1cb909c4bb6) でなければなりません。ただし、通常、このパラメーターを設定したり変更したりする必要はありません。この値は、Enabled を True に設定している場合、および1) AlwaysBypass を True に設定しているか、2) EnableDefaultBypassID パラメーターを True に設定している場合、自動的に生成されます。</p></td>
</tr>
<tr class="odd">
<td><p><em>Enabled</em></p></td>
<td><p>省略可能</p></td>
<td><p>Boolean</p></td>
<td><p>このパラメーターを True に設定してメディア バイパスを有効にします。その時点で、バイパスの判断は、次のように AlwaysBypass 設定の値に基づきます。</p>
<p>- AlwaysBypass が True の場合、すべての通話でバイパスが試みられます。</p>
<p>- AlwaysBypass が False の場合、ネットワーク構成サイトと地域を使用して、バイパスを実行できるかどうかを判断します。</p>
<p>既定値は次のとおりです。False</p></td>
</tr>
<tr class="even">
<td><p><em>EnableDefaultBypassID</em></p></td>
<td><p>省略可能</p></td>
<td><p>Boolean</p></td>
<td><p>この値は、AlwaysBypass を False に設定している場合のみ適用されます。</p>
<p>この値を True に設定すると、既定のバイパス ID が自動的に生成されます。この自動生成された値は、BypassID プロパティに保存されます。</p>
<p>このパラメーターは、帯域幅に制約のあるリンクを持つリモート サイトとの接続状態が良好なコアが存在する場合に便利です。管理者が定義する必要があるのは、ネットワーク構成サイトと地域によってリモート サイトに関連付けられているサブネットだけです。コアに関連付けられているサブネットは定義の必要がなく、バイパスはこれらのサブネット間で自動的に試みられます。</p>
<p>既定値は次のとおりです。False</p></td>
</tr>
<tr class="odd">
<td><p><em>EnabledForAudioVideoConferences</em></p></td>
<td><p>省略可能</p></td>
<td><p>Boolean</p></td>
<td><p>メディア バイパスを音声ビデオ会議に使用するかどうかを指定します。既定値は False ($False) です。</p></td>
</tr>
<tr class="even">
<td><p><em>ExternalBypassMode</em></p></td>
<td><p>省略可能</p></td>
<td><p>BypassModeEnumType</p></td>
<td><p>今後の使用のために予約されています。Lync Server では、外部メディア バイパスはサポートされていません。</p>
<p>既定値は次のとおりです。オフ</p></td>
</tr>
<tr class="odd">
<td><p><em>InternalBypassMode</em></p></td>
<td><p>省略可能</p></td>
<td><p>BypassModeEnumType</p></td>
<td><p>このパラメーターの値は、組織のネットワーク内から接続しているクライアントが、いつメディア バイパスの実行を試みることができるのかを制御します。Enabled を True に設定すると、この値は自動的に Any に変更されます。このパラメーターの他の値は、今後の使用のために予約されています。</p>
<p>既定値は次のとおりです。オフ</p></td>
</tr>
</tbody>
</table>


## 入力の種類

なし。

## 戻り値の種類

Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.MediaBypassSettingsType 型のオブジェクト参照を作成します。

## 関連項目

#### その他のリソース

[Get-CsNetworkConfiguration](get-csnetworkconfiguration.md)  
[Set-CsNetworkConfiguration](set-csnetworkconfiguration.md)

