---
title: Test-CsLocationPolicy
TOCTitle: Test-CsLocationPolicy
ms:assetid: 49f7d148-d46d-4bcc-af9d-6a3a0fdde8ee
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg425962(v=OCS.15)
ms:contentKeyID: 48272001
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsLocationPolicy

 

_**トピックの最終更新日:** 2015-03-09_

パラメーター値に指定された条件に基づき、使用する場所ポリシーを決定するテストを実行します。場所ポリシーには、高度 9-1-1 (E9-1-1) を適用するかどうかと、その適用方法を決定する設定が含まれています。E9-1-1 を使用すると、911 の緊急電話に応答した人が、発信者の地理的な場所を判断できるようになります。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Test-CsLocationPolicy -UserCredential <PSCredential> -UserSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] <COMMON PARAMETERS>

    Test-CsLocationPolicy -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-UserSipAddress <String>] <COMMON PARAMETERS>

    Test-CsLocationPolicy [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>] [-Subnet <String>]

## 例

## 例 1

この例では、現在のユーザー (または現在構成されているユーザー) の場所のポリシーを決定しています。TargetFqdn は必須です。

    Test-CsLocationPolicy -TargetFqdn atl-cs-001.litwareinc.com 

## 例 2

例 2 の最初の行は、Windows PowerShell の **Get-Credential** コマンドレットの呼び出しです。このコマンドレットでは、ユーザー資格情報を取得し、保護されたオブジェクトとして戻します。このコマンドレットで指定する唯一のパラメーターはユーザー ID です。このコマンドレットを実行すると、ユーザー ID の値が事前に入力され、ユーザー パスワードを入力するテキスト ボックスが配置されたダイアログ ボックスが開きます。これらのユーザー資格情報は変数 $cred に保存されます。

2 行目では、**Test-CsLocationPolicy** コマンドレットを呼び出しています。例 1 と同様、目的の FQDN を指定します。ただし、この例では、事前に構成されたユーザーを使用せずに、kenmyer@litwareinc.com という SIP アドレスを持つユーザーに対してテストを実行しています。その値を (sip: プレフィックスを付けて) UserSipAddress パラメーターに渡し、さらにそのユーザーの資格情報 ($cred 変数に格納済み) を UserCredential パラメーターに渡しています。

    $cred = Get-Credential "litwareinc\kenmyer"
    Test-CsLocationPolicy -TargetFqdn atl-cs-001.litwareinc.com -UserCredential $cred -UserSipAddress "sip:kenmyer@litwareinc.com"

## 例 3

この例は例 2 に似ていますが、ユーザー資格情報が指定されていません。ユーザー資格情報を指定せずに **Test-CsLocationPolicy** コマンドレットを呼び出すと、このコマンドレットが実行されているコンピューターのサーバー証明書を使用して、ユーザーの場所のポリシーの認証および検出が行われます。コンピューターにサーバー証明書がない場合は、例 2 のようにして資格情報を指定する必要があります。コンピューターにサーバー証明書が存在するかどうかを調べるには、**Get-CsCertificate** コマンドレットを呼び出します。

    Test-CsLocationPolicy -TargetFqdn atl-cs-001.litwareinc.com -UserSipAddress "sip:kenmyer@litwareinc.com"

## 例 4

この例では、サブネット ID が 172.15.11.0 であるサブネットの場所のポリシーを決定しています。サブネットが場所のポリシーと関連付けられていない場合、現在構成されているユーザーに対する場所のポリシーが取得されます。

注: 場所のポリシーをサブネットに設定するには、**Set-CsNetworkSite** コマンドレットの LocationPolicy パラメーターを場所のポリシーの ID に設定します。次に、**Set-CsNetworkSubnet** コマンドレットの NetworkSiteId パラメーターをそのサイトの ID に設定します。次に例を示します。

Set-CsNetworkSite Portland –LocationPolicy Reno

Set-CsNetworkSubnet 175.15.11.0 –NetworkSiteID Portland

    Test-CsLocationPolicy -TargetFqdn atl-cs-001.litwareinc.com -Subnet 172.15.11.0

## 解説

場所のポリシーを使用して、E9-1-1 の機能およびクライアントの場所に関連する設定を適用します。場所のポリシーにより、ユーザーを E9-1-1 で有効にするかどうか、および有効にする場合には緊急電話の動作が決まります。たとえば、場所のポリシーを使用して、緊急電話を構成する番号 (米国の場合は 911)、社内セキュリティに自動的に通知するかどうか、および通話をルーティングする方法を定義できます。このコマンドレットを実行すると、特定のプール、サブネット、スイッチ、またはワイヤレス アクセス ポイントの特定のクライアントからの通話時に使用する場所のポリシーに関する情報が戻されます。

このコマンドレットの呼び出しにユーザーが指定されていない場合、現在構成されているユーザーに対してテストが実行されます。現在構成されているユーザーを検出するには、**Get-CsHealthMonitoringConfiguration** コマンドレットを呼び出します。その構成されているユーザーを設定するには、**Set-CsHealthMonitoringConfiguration** コマンドレットを呼び出します。

そのユーザーまたはサブネットに対して場所のポリシーが検出されれば、テストは成功します。既定で戻される情報には、場所のポリシーの名前 (ユーザーごとのポリシーが割り当てられている場合)、およびユーザーまたはサブネットが E9-1-1 に対して有効かどうかが含まれます。テストに関する追加情報を取得するには、Windows PowerShell の共通パラメーター Verbose を含めます。

ユーザーまたはネットワーク サブネットに対して場所のポリシーをテストできます。サブネットに対してテストを実行する場合 (Subnet パラメーターに値を指定します)、コマンドレットはそのサブネット用の場所のポリシーの解決を試みます。サブネットに場所のポリシーが割り当てられていない場合、構成されているユーザーの場所のポリシーが取得されます。サブネットのポリシーが正常に取得された場合は、その出力に subnet-tagid で始まる LocationPolicyTagID の値が含まれます。サブネットの場所のポリシーが見つからなかった場合は、LocationPolicyTagID は user-tagid で始まります。

このコマンドレットを実行できるユーザー: 既定では、次のグループのメンバーが **Test-CsLocationPolicy** コマンドレットをローカルで実行することを承認されています。RTCUniversalServerAdmins。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsLocationPolicy"}

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
<td><p><em>TargetFqdn</em></p></td>
<td><p>必須</p></td>
<td><p>String</p></td>
<td><p>指定したユーザーまたはサブネットが所属しているプールの完全修飾ドメイン名 (FQDN) です (ユーザーが指定されていない場合は、事前に構成されたユーザーか現在のユーザーが想定されます)。</p></td>
</tr>
<tr class="even">
<td><p><em>UserCredential</em></p></td>
<td><p>必須かどうか</p></td>
<td><p>PSCredential</p></td>
<td><p>場所のポリシーがテストされているユーザー アカウントのユーザー ID およびパスワードを含んでいるオブジェクトです。<strong>Get-Credential</strong> コマンドレットを呼び出し、適切な情報を指定し、変数に出力を保存することによって、資格情報オブジェクトを取得できます。</p></td>
</tr>
<tr class="odd">
<td><p><em>Authentication</em></p></td>
<td><p>省略可能</p></td>
<td><p>SipSyntheticTransaction AuthenticationMechanism</p></td>
<td><p>テストで使用される認証の種類です。有効な値は次のとおりです。</p>
<p>* TrustedServer</p>
<p>* Negotiate</p>
<p>* ClientCertificate</p>
<p>* LiveID</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>省略可能</p></td>
<td><p>SwitchParameter</p></td>
<td><p>変更を行う前に表示されるように設定されているすべての確認メッセージを表示しないようにします。</p></td>
</tr>
<tr class="odd">
<td><p><em>OutLoggerVariable</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.String</p></td>
<td><p>コマンドレットを実行した結果の詳細な出力が、指定された変数に保存されます。この変数には、出力を HTML あるいは XML ファイルに保存する目的で使用する ToHTML と ToXML のペアのメソッドが含まれます。</p>
<p>$TestOutput という名前のロガー変数の出力を保存するには、以下の構文を使用します。</p>
<p>-OutLoggerVariable TestOutput</p>
<p>注: 変数名を指定するときは、先頭に $ 文字を付けないでください。ロガー変数に格納された情報を HTML ファイルに保存するには、次のような構文を使用します。</p>
<p>$TestOutput.ToHTML() &gt; C:\Logs\TestOutput.html</p>
<p>ロガー変数に保存された情報を XML ファイルに保存するには、以下のようなコマンドを使用します。</p>
<p></p>
<p>$TestOutput.ToXML() &gt; C:\Logs\TestOutput.xml</p></td>
</tr>
<tr class="even">
<td><p><em>OutVerboseVariable</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>コマンドレットを実行した結果の詳細な出力が、指定された変数に保存されます。たとえば、$TestOutput という名前の変数に出力を保存するには、次の構文を使用します。</p>
<p>-OutVerboseVariable TestOutput</p>
<p>変数名を指定するときは、先頭に $ 記号は使用しないでください。</p></td>
</tr>
<tr class="odd">
<td><p><em>RegistrarPort</em></p></td>
<td><p>省略可能</p></td>
<td><p>Int32</p></td>
<td><p>レジストラー サービスのポート番号。</p></td>
</tr>
<tr class="even">
<td><p><em>Subnet</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>場所のポリシーをテストする対象のネットワーク サブネットの ID (IP アドレス) です。</p></td>
</tr>
<tr class="odd">
<td><p><em>UserSipAddress</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>テスト対象とする場所のポリシーを持つユーザーの SIP アドレスです。このアドレスは、sip:&lt;ユーザー ID&gt; (たとえば、sip:kenmyer@litwareinc.com) の形式にする必要があります。</p></td>
</tr>
</tbody>
</table>


## 入力の種類

なし。

## 戻り値の種類

**Test-CsLocationPolicy** コマンドレットを実行すると、Microsoft.Rtc.SyntheticTransactions.TaskOutput オブジェクトのインスタンスが戻されます。

## 関連項目

#### その他のリソース

[New-CsLocationPolicy](new-cslocationpolicy.md)  
[Remove-CsLocationPolicy](remove-cslocationpolicy.md)  
[Set-CsLocationPolicy](set-cslocationpolicy.md)  
[Get-CsLocationPolicy](get-cslocationpolicy.md)  
[Grant-CsLocationPolicy](grant-cslocationpolicy.md)  
[Get-CsHealthMonitoringConfiguration](get-cshealthmonitoringconfiguration.md)  
[Set-CsHealthMonitoringConfiguration](set-cshealthmonitoringconfiguration.md)  
[Set-CsNetworkSite](set-csnetworksite.md)

