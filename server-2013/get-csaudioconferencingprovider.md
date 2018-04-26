---
title: Get-CsAudioConferencingProvider
TOCTitle: Get-CsAudioConferencingProvider
ms:assetid: 4632e9d0-aa87-459f-ad7e-27125c11da5b
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ994030(v=OCS.15)
ms:contentKeyID: 52056580
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsAudioConferencingProvider

 

_**トピックの最終更新日:** 2015-03-09_

組織で使用するために認証されている電話会議プロバイダーに関する情報を返します。電話会議プロバイダーとは、電話会議サービスを組織に提供するサード パーティの企業です。

**Get-CsAudioConferencingProvider** コマンドレットは、Microsoft Lync Online でのみ使用できます。

## 構文

    Get-CsAudioConferencingProvider [[-Identity] <XdsGlobalRelativeIdentity>] [-LocalStore][<CommonParameters>]Get-CsAudioConferencingProvider [-Filter <string>] [-LocalStore] [<CommonParameters>]

## 例

## 例 1

例 1 に示すコマンドは、組織で使用できるすべての電話会議プロバイダーに関する情報を返します。

    Get-CsAudioConferencingProvider

## 例 2

例 2 では、1 つの電話会議プロバイダー (Fabrikam Telecom という Identity を持つプロバイダー) に関する情報が返されます。

    Get-CsAudioConferencingProvider -Identity "Fabrikam Telecom"

## 例 3

例 3 は、ワイルドカード値 (および Filter パラメーター) を使用して、電話会議プロバイダーに関する情報を返す方法を示しています。この例では、フィルター値 "\*Fabrikam\*" によって、Identity の任意の場所に文字列値 "Fabrikam" が含まれるすべての電話会議プロバイダーが返されます。

    Get-CsAudioConferencingProvider -Filter "*Fabrikam*"

## 解説

電話会議プロバイダーとは、電話会議サービスを組織に提供するサード パーティの企業です。重要な点は、電話会議プロバイダーを利用すると、社外にいて企業ネットワークまたはインターネットに接続されていないユーザーが、電話会議または会議の音声部分に参加できるようになることです。電話会議プロバイダーは多くの場合、リアルタイム通訳、トランスクリプション、オペレーターによる各電話会議のリアルタイム サポートなど、高度なサービスを提供します。

組織が電話会議プロバイダーと契約した後、**Set-CsUserAcp** コマンドレットを使用してユーザーをプロバイダーに割り当てることができます。管理者は、**Get-CsAudioConferencingProvider** コマンドレットを使用して、ユーザーが使用できる電話会議プロバイダーに関する情報を取得することができます。

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
<td><p>返される電話会議プロバイダー (複数も可) を指定する際に、ワイルドカード文字を使用することができます。たとえば、次の構文を使用すると、Identity の任意の場所に文字列値 &quot;fabrikam&quot; を含むすべての電話会議プロバイダーに関する情報が返されます。</p>
<p>-Filter &quot;*fabrikam*&quot;</p>
<p>Filter パラメーターと Identity パラメーターは、同じコマンドで同時に使用できないことに注意してください。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>省略可能</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>返される電話会議プロバイダーの一意識別子です。次に例を示します。</p>
<p>-Identity &quot;Fabrikam Telecom&quot;</p>
<p>コマンドに Identity パラメーターも Filter パラメーターも含まれていない場合、<strong>Get-CsAudioConferencingProvider</strong> コマンドレットは、使用可能なすべてのプロバイダーに関する情報を返します。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>中央管理ストア自体からではなく、中央管理ストアのローカル レプリカから電話会議プロバイダーのデータを取得します。</p></td>
</tr>
</tbody>
</table>


## 入力の種類

なし。**Get-CsAudioConferencingProvider** コマンドレットはパイプライン入力を受け入れません。

## 戻り値の種類

**Get-CsAudioConferencingProvider** コマンドレットは、Microsoft.Rtc.Management.WritableConfig.Settings.AudioConferencingProvider.AudioConferencingProvider\#Decorated オブジェクトのインスタンスを返します。

## 関連項目

#### その他のリソース

[Get-CsUserAcp](get-csuseracp.md)  
[Remove-CsUserAcp](remove-csuseracp.md)  
[Set-CsUserAcp](set-csuseracp.md)

