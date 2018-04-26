---
title: New-CsImFilterConfiguration
TOCTitle: New-CsImFilterConfiguration
ms:assetid: 1964cbf9-d7f1-4b4e-99d1-951ac42d82fe
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg398244(v=OCS.15)
ms:contentKeyID: 48271411
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsImFilterConfiguration

 

_**トピックの最終更新日:** 2015-03-09_

新しいインスタント メッセージ (IM) フィルター構成を作成します。IM フィルターは、ユーザーがアクティブなハイパーリンクを含むインスタント メッセージを送信しないようにする目的で使用します。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    New-CsImFilterConfiguration -Identity <XdsIdentity> [-Action <Allow | Block | Warn>] [-AllowMessage <String>] [-BlockFileExtension <$true | $false>] [-Confirm [<SwitchParameter>]] [-Enabled <$true | $false>] [-Force <SwitchParameter>] [-IgnoreLocal <$true | $false>] [-InMemory <SwitchParameter>] [-Prefixes <PSListModifier>] [-WarnMessage <String>] [-WhatIf [<SwitchParameter>]]

## 例

## 例 1

例 1 では、**New-CsImFilterConfiguration** コマンドレットを使用して、site:Redmond という Identity を持つ新しい IM フィルター構成を作成します (追加パラメーターを指定していないので、これらの設定は既定値を使用して作成されます)。

    New-CsImFilterConfiguration -Identity site:Redmond

## 例 2

このコマンドで、**New-CsImFilterConfiguration** コマンドレットを使用して、site:Redmond という Identity を持つ新しい IM フィルター構成を作成します。Prefixes パラメーターを指定しているため、新しい構成には、すべての既定値 (フィルター処理する既定のプレフィックスなど) に加えて 2 つの追加の URI プレフィックス (rtsp:と urn:) が含まれます。add リスト修飾子を使用してこれらのプレフィックスを既定の一覧に追加することで、これらのプレフィックスを追加します。

    New-CsImFilterConfiguration -Identity site:Redmond -Prefixes @{add="rtsp:","urn:"}

## 例 3

このコマンドで、**New-CsFileTransferFilterConfiguration** コマンドレットを使用して、site:Redmond という Identity を持つ新しい IM フィルター構成を作成します。この例は、add リスト修飾子の代わりに replace リスト修飾子を使用している点を除き、例 2 と同様です。つまり、既定のすべての URI プレフィックスが、これらの 2 つのプレフィックス (rtsp:と urn:) に置き換えられます。したがって、サイト レドモンドでは、rtsp:または urn:というプレフィックスを持つ URI のみ、インスタント メッセージ内でフィルター処理されます。

    New-CsImFilterConfiguration -Identity site:Redmond -Prefixes @{replace="rtsp:","urn:"}

## 解説

インスタント メッセージを送信するときに、ユーザーはメッセージのテキスト内に Uniform Resource Identifier (URI) を埋め込んで、会話している他の参加者に対して、特定の Web サイトまたは共有場所を参照させることができます。特定のプレフィックスを持つハイパーリンクをブロックするかアクティブではなくなるように、Lync Server を構成できます (つまり、参加者はリンクをクリックしただけでは URI の参照先サイトにアクセスできず、リンクを手動でコピーしてブラウザーに貼り付ける必要があります)。

**New-CsImFilterConfiguration** コマンドレットを使用すると、フィルター処理する URI プレフィックスの一覧を定義して、特定のサイト内でフィルター処理を同時に有効および無効にできます。指定した ID のみ使用して **New-CsImFilterConfiguration** コマンドレットを呼び出すと、その ID を持つ新しい構成が作成されて、フィルター処理する既定のプレフィックスのセットが含まれた、そのサイトのプレフィックスの一覧が生成されます。

このコマンドレットを実行できるユーザー: 既定では、次のグループのメンバーが、**New-CsImFilterConfiguration** コマンドレットをローカルで実行することを承認されています。RTCUniversalServerAdmins。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsImFilterConfiguration"}

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
<td><p><em>Identity</em></p></td>
<td><p>必須</p></td>
<td><p>XdsIdentity</p></td>
<td><p>IM フィルター構成のスコープを指定する一意の識別子。グローバル設定は既定で存在するため、<strong>New-CsImFilterConfiguration</strong> コマンドレットを使用して再作成することはできませんが、site:&lt;サイト名&gt; という Identity を指定して、サイトレベルの設定を作成できます。ここで、&lt;サイト名&gt; は、設定を適用するサイトの名前です (site:Redmond など)。</p>
<p>完全なデータ型:Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
</tr>
<tr class="even">
<td><p><em>Action</em></p></td>
<td><p>省略可能</p></td>
<td><p>UrlFilterAction</p></td>
<td><p>このパラメーターの値で、インスタント メッセージにハイパーリンクが含まれている場合に実行するアクションを指定します。次の値を指定できます。</p>
<p>Allow - リンクを非アクティブにするために、ハイパーリンクの先頭にアンダースコアが付加されます。AllowMessage プロパティにメッセージを指定すると、ハイパーリンクを含む各インスタント メッセージのはじめに、そのメッセージが挿入されます。</p>
<p>Block - アクティブなハイパーリンクを含むメッセージの配信がブロックされ、Lync Server から送信者にエラー メッセージが送信されます。</p>
<p>Warn - アクティブなハイパーリンクを含むメッセージが受信側の参加者に配信され、それらのメッセージの先頭に警告メッセージが挿入されます。警告メッセージは、WarnMessage プロパティを使用して指定できます。Warn を指定して WarnMessage を入力していない場合、BlockFileExtension プロパティの設定が引き続き優先されますが、IM フィルター処理は無効になります。</p>
<p>既定値は次のとおりです。メッセージに含まれる URL が 1,000 以下の場合、Allow。1,001 以上の場合、既定値は Block です。</p>
<p>完全なデータ型:Microsoft.Rtc.Management.WritableConfig.Settings.ImFilter.UrlFilterAction</p></td>
</tr>
<tr class="odd">
<td><p><em>AllowMessage</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>Action プロパティの値を Allow に設定している場合、このパラメーターに値を指定すると、その文字列がハイパーリンクを含む各メッセージの先頭に挿入されます。このメッセージを使用して、未知のリンクをクリックすると発生する可能性のある危険や、組織の関連ポリシーや要件を、ユーザーに通知できます。</p></td>
</tr>
<tr class="even">
<td><p><em>BlockFileExtension</em></p></td>
<td><p>省略可能</p></td>
<td><p>Boolean</p></td>
<td><p>このパラメーターを True に設定すると、適用可能なファイル転送フィルター構成 (<strong>Get-CsFileTransferFilterConfiguration</strong> コマンドレットを呼び出して取得) で定義する Extensions プロパティで指定された拡張子を持つ、ファイル パスを含むハイパーリンクがブロックされ、送信者にエラー メッセージが戻されます。このパラメーターを False に設定すると、ファイル拡張子に対して特に確認は行われません。</p>
<p>既定値は次のとおりです。True</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>省略可能</p></td>
<td><p>SwitchParameter</p></td>
<td><p>コマンドの実行前に確認メッセージが表示されます。</p></td>
</tr>
<tr class="even">
<td><p><em>Enabled</em></p></td>
<td><p>省略可能</p></td>
<td><p>Boolean</p></td>
<td><p>この機能を有効または無効にします。このパラメーターを True に設定すると、インスタント メッセージでハイパーリンクがスキャンされて、この構成のルールが適用されます。このパラメーターを False に設定すると、メッセージでハイパーリンクは確認されません。</p>
<p>既定値は次のとおりです。True</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>省略可能</p></td>
<td><p>SwitchParameter</p></td>
<td><p>変更を行う前に表示されるように設定されているすべての確認メッセージを表示しないようにします。</p></td>
</tr>
<tr class="even">
<td><p><em>IgnoreLocal</em></p></td>
<td><p>省略可能</p></td>
<td><p>Boolean</p></td>
<td><p>このパラメーターの値で、インスタント メッセージで渡されるローカルのイントラネット URI に対してフィルター処理を実行するかどうかを制御します。このパラメーターを True に設定すると、ローカル コンピューターのイントラネット ゾーンに定義されているすべての URI が無視されます (ローカル コンピューターは、IM フィルター アプリケーションを実行する フロント エンド サーバー のことです)。このパラメーターを False に設定すると、指定のフィルター処理がすべてのハイパーリンクに適用されます。</p>
<p>既定値は次のとおりです。True</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>省略可能</p></td>
<td><p>SwitchParameter</p></td>
<td><p>永続的な変更としてオブジェクトをコミットせずに、オブジェクト参照を作成します。このパラメーターを指定して呼び出したコマンドレットの出力を変数に割り当てる場合、オブジェクト参照のプロパティを変更し、コマンドレットに対応する Set- コマンドレットを呼び出してそれらの変更をコミットできます。</p></td>
</tr>
<tr class="even">
<td><p><em>Prefixes</em></p></td>
<td><p>省略可能</p></td>
<td><p>PSListModifier</p></td>
<td><p>フィルター処理する URI プレフィックスの一覧。インスタント メッセージに含まれているハイパーリンクに、この一覧のいずれかのプレフィックスと一致するプレフィックスが付いている場合、そのハイパーリンクは指定の設定に従ってフィルター処理されます。</p>
<p>既定値は次のとおりです。callto:、file:、ftp.、ftp:、gopher:、href、http:、https:、ldap:、mailto:、news:、nntp:、sip:、sips:、tel:、telnet:、www*。</p></td>
</tr>
<tr class="odd">
<td><p><em>WarnMessage</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>Action プロパティの値を Warn に設定している場合、このパラメーターに、ハイパーリンクを含む各インスタント メッセージの先頭に挿入する警告メッセージを含めます。通常このメッセージは、未知のリンクをクリックすることで発生する可能性のある危険の提示や、組織の関連ポリシーや要件への参照などを通知するのに使用されます。</p></td>
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

なし。

## 戻り値の種類

Microsoft.Rtc.Management.WritableConfig.Settings.ImFilter.ImFilterConfiguration 型のオブジェクトが作成されます。

## 関連項目

#### その他のリソース

[Remove-CsImFilterConfiguration](remove-csimfilterconfiguration.md)  
[Set-CsImFilterConfiguration](set-csimfilterconfiguration.md)  
[Get-CsImFilterConfiguration](get-csimfilterconfiguration.md)

