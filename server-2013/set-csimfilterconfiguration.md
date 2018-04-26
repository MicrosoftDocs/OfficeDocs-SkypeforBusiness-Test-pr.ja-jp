---
title: Set-CsImFilterConfiguration
TOCTitle: Set-CsImFilterConfiguration
ms:assetid: c2b08cc0-8261-4b8b-b2e9-5efa902ceb40
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg412960(v=OCS.15)
ms:contentKeyID: 48273508
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsImFilterConfiguration

 

_**トピックの最終更新日:** 2015-03-09_

既存のインスタント メッセージング (IM) フィルター構成を変更します。IM フィルター設定は、ユーザーがライブの (クリック可能な) ハイパーリンクを含むインスタント メッセージを送信しないようにするときに使用されます。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Set-CsImFilterConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsImFilterConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Action <Allow | Block | Warn>] [-AllowMessage <String>] [-BlockFileExtension <$true | $false>] [-Confirm [<SwitchParameter>]] [-Enabled <$true | $false>] [-Force <SwitchParameter>] [-IgnoreLocal <$true | $false>] [-Prefixes <PSListModifier>] [-WarnMessage <String>] [-WhatIf [<SwitchParameter>]]

## 例

## 例 1

この例のコマンドを実行すると、site:Redmond という ID を持つ IM フィルター構成の URI フィルターが無効にされます。このタスクを実行するため、**Set-CsImFilterConfiguration** コマンドレットを呼び出して、Enabled パラメーターの値に $False を指定します。

    Set-CsImFilterConfiguration -Identity site:Redmond -Enabled $False

## 例 2

例 2 では、site:Redmond の IM フィルター構成で禁止されているプレフィックスのリストに、新しい URI プレフィックス (urn:) が追加されます。新しいプレフィックスを追加するため、**Get-CsImFilterConfiguration** コマンドレットを使用して site:Redmond の構成を取得し、その構成を示す戻されたオブジェクトを $x という名前の変数に格納します。設定の取得後、2 行目で Add() メソッドを呼び出し、Prefixes プロパティに格納されているプレフィックスのセットに urn: を追加します。これにより、オブジェクト参照 $x の値が変更されます。実際の構成そのものを変更するため、3 行目で **Set-CsImFilterConfiguration** コマンドレットを呼び出し、唯一のパラメーターの値として $x を渡します。

    $x = Get-CsImFilterConfiguration -Identity site:Redmond
    $x.Prefixes.Add("urn:")
    Set-CsImFilterConfiguration -Instance $x

## 例 3

例 3 では、例 2 とまったく同じアクションが実行されますが、同じアクションを 1 行で行います。このコマンドでは、**Set-CsImFilterConfiguration** コマンドレットの Prefixes パラメーターを使用して、urn: をプレフィックスのリストに追加します。add リスト修飾子を使用して、この値を Prefixes リストに追加しています。

    Set-CsImFilterConfiguration -Identity site:Redmond -Prefixes @{add="urn:"}

## 例 4

この例では、site:Redmond の IM フィルター構成で禁止されているプレフィックスのリストから、プレフィックス urn: が削除されます。この例は、リストにプレフィックスを追加するために add リスト修飾子を呼び出す代わりに、プレフィックスを削除するために remove 修飾子を呼び出していること以外は、例 3 と同じです。

    Set-CsImFilterConfiguration -Identity site:Redmond -Prefixes @{remove="urn:"}

## 解説

インスタント メッセージを送信するときに、ユーザーはメッセージのテキスト内に URI (Uniform Resource Identifier) を埋め込んで、会話している他の参加者に対して、特定の Web サイトまたは共有場所を参照させることができます。特定のプレフィックスを持つハイパーリンクをブロックするかアクティブではなくなるように、Lync Server を構成できます (つまり、参加者はリンクをクリックしただけでは URI の参照先のサイトにアクセスできず、リンクを手動でコピーしてブラウザーに貼り付ける必要があります)。

**Set-CsImFilterConfiguration** コマンドレットを使用すると、フィルター処理の対象となる URI プレフィックスのリストを変更できます。また、グローバルまたは特定のサイト内の、フィルター処理をすべてまとめて有効または無効にできます。このコマンドレットを使用すると、ユーザーへの警告に関するさまざまなメッセージを更新することもできます。

このコマンドレットを実行できるユーザー: 既定では、次のグループのメンバーが、**Set-CsImFilterConfiguration** コマンドレットのローカル実行を承認されています。RTCUniversalServerAdmins。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsImFilterConfiguration"}

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
<td><p><em>Action</em></p></td>
<td><p>省略可能</p></td>
<td><p>UrlFilterAction</p></td>
<td><p>このパラメーター値で、ハイパーリンクがインスタント メッセージに含まれていたときに実行されるアクションを、次から決定します。</p>
<p>Allow - ハイパーリンクの先頭にアンダースコアが付けられるため、リンクがアクティブになりません。また、AllowMessage プロパティにメッセージを指定すると、ハイパーリンクを含む各インスタント メッセージのはじめに、通知メッセージが挿入されます。</p>
<p>Block - アクティブなハイパーリンクを含むメッセージの配信がブロックされ、Lync Server から送信者にエラー メッセージが送信されます。</p>
<p>Warn - アクティブなハイパーリンクを含むメッセージが受信する参加者に配信されますが、メッセージのはじめに警告メッセージが挿入されます。警告メッセージは、WarnMessage プロパティを使用して指定できます。Warn を指定しても WarnMessage を入力しないと、IM フィルターは無効になりますが、BlockFileExtension プロパティの設定はそのまま優先されます。</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>AllowMessage</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>このパラメーターに値を指定した場合、Action プロパティの値に Allow が設定されていると、指定した文字列がハイパーリンクを含む各メッセージのはじめに挿入されます。このメッセージを使用して、未知のリンクをクリックすると発生する可能性のある危険や、組織の関連ポリシーや要件を、ユーザーに通知できます。</p></td>
</tr>
<tr class="odd">
<td><p><em>BlockFileExtension</em></p></td>
<td><p>省略可能</p></td>
<td><p>Boolean</p></td>
<td><p>このパラメーターを True に設定すると、Microsoft.Rtc.Management.WritableConfig.Settings.ImFilter.FileTransferFilterConfiguration クラス (<strong>Get-CsFileTransferFilterConfiguration</strong> コマンドレットを呼び出して取得) で定義する Extensions プロパティで指定された拡張子を持つ、ファイル パスを含むハイパーリンクがブロックされ、送信者にエラー メッセージが戻されます。このパラメーターを False に設定すると、ファイル パスや拡張子に対して特別な確認は行われません。</p>
<p>既定値は次のとおりです。True</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>省略可能</p></td>
<td><p>SwitchParameter</p></td>
<td><p>コマンドの実行前に確認メッセージが表示されます。</p></td>
</tr>
<tr class="odd">
<td><p><em>Enabled</em></p></td>
<td><p>省略可能</p></td>
<td><p>Boolean</p></td>
<td><p>この機能を有効または無効にします。このパラメーターを True に設定すると、インスタント メッセージがハイパーリンクを含むかどうか確認され、この構成のルールが適用されます。このパラメーターを False に設定すると、メッセージがハイパーリンクを含むかどうか確認されません。</p>
<p>既定値は次のとおりです。True</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>省略可能</p></td>
<td><p>SwitchParameter</p></td>
<td><p>変更を行う前に表示されるように設定されているすべての確認メッセージを表示しないようにします。</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>省略可能</p></td>
<td><p>XdsIdentity</p></td>
<td><p>変更する IM フィルター構成設定の一意の識別子。この値は、グローバルまたは site:&lt;サイト名&gt; のどちらかにします。&lt;サイト名&gt; は、構成を適用するサイトです (例: site:Redmond)。</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>IgnoreLocal</em></p></td>
<td><p>省略可能</p></td>
<td><p>Boolean</p></td>
<td><p>このパラメーターの値で、インスタント メッセージで渡されたローカル イントラネット URI をフィルター処理するかどうか制御します。このパラメーターを True に設定すると、ローカル コンピューターのイントラネット ゾーン内で定義された、すべての URI が無視されます (ローカル コンピューターとは、IM フィルター アプリケーションを実行する フロント エンド サーバー のことです)。このパラメーターを False に設定すると、指定したフィルター処理がすべてのハイパーリンクに適用されます。</p>
<p>既定値は次のとおりです。True</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>省略可能</p></td>
<td><p>ImFilterConfiguration</p></td>
<td><p>個々のパラメーター値を設定せずに、コマンドレットにオブジェクトへの参照を渡すことができます。このコマンドレットは、Microsoft.Rtc.Management.WritableConfig.Settings.ImFilter.ImFilterConfiguration 型のオブジェクトを受け入れます。このオブジェクトは <strong>Get-CsImFilterConfiguration</strong> コマンドレットを呼び出すと取得できます。</p></td>
</tr>
<tr class="even">
<td><p><em>Prefixes</em></p></td>
<td><p>省略可能</p></td>
<td><p>PSListModifier</p></td>
<td><p>フィルター処理の対象となる URI プレフィックスのリスト。このリストにあるいずれかのプレフィックスに一致するプレフィックスを持つ、インスタント メッセージ内に含まれるすべてのハイパーリンクが、指定した設定に基づいてフィルター処理されます。</p>
<p>既定値は次のとおりです。callto:、file:、ftp.、ftp:、gopher:、href、http:、https:、ldap:、mailto:、news:、nntp:、sip:、sips:、tel:、telnet:、www*。</p></td>
</tr>
<tr class="odd">
<td><p><em>WarnMessage</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>このパラメーターは、Action パラメーター値が Warn に設定されている場合に、ハイパーリンクを含む各インスタント メッセージのはじめに挿入される警告メッセージを設定します。通常このメッセージは、未知のリンクをクリックすることで発生する可能性のある危険の提示や、組織の関連ポリシーや要件への参照などを通知するのに使用されます。</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>省略可能</p></td>
<td><p>SwitchParameter</p></td>
<td><p>実際にコマンドを実行しなくてもコマンドの実行結果がわかります。</p></td>
</tr>
</tbody>
</table>


## 入力の種類

Microsoft.Rtc.Management.WritableConfig.Settings.ImFilter.ImFilterConfiguration オブジェクト。IM フィルター構成オブジェクトのパイプライン入力を受け入れます。

## 戻り値の種類

**Set-CsImFilterConfiguration** コマンドレットは、値またはオブジェクトを戻しません。代わりに、このコマンドレットは、Microsoft.Rtc.Management.WritableConfig.Settings.ImFilter.ImFilterConfiguration オブジェクトのインスタンスを構成します。

## 関連項目

#### その他のリソース

[New-CsImFilterConfiguration](new-csimfilterconfiguration.md)  
[Remove-CsImFilterConfiguration](remove-csimfilterconfiguration.md)  
[Get-CsImFilterConfiguration](get-csimfilterconfiguration.md)

