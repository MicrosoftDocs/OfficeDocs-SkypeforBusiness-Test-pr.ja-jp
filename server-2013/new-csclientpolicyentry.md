---
title: New-CsClientPolicyEntry
TOCTitle: New-CsClientPolicyEntry
ms:assetid: e975d048-4911-4ae6-9446-2a6363726a4a
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg399046(v=OCS.15)
ms:contentKeyID: 48274028
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsClientPolicyEntry

 

_**トピックの最終更新日:** 2015-03-09_

Lync Server クライアント ポリシーに新しいオプションを追加します。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    New-CsClientPolicyEntry -Name <String> -Value <String>

## 例

## 例 1

例 1 に示すコマンドは、グローバル クライアント ポリシーに新しいポリシー エントリを追加する方法を示しています。この例では、Lync に新しいフィードバック オプションを追加しています。ただし、この例はデモンストレーション用であり、これらのコマンドの実行によって Lync のコピーに同様のフィードバック オプションを追加できるとは考えないでください。

新しいポリシー エントリを追加するため、この例のコマンドではまず **New-CsClientPolicyEntry** コマンドレットを使用し、名前が OnlineFeedbackURL、値が http://www.litwareinc.com/feedback のエントリを作成しています。作成したポリシー エントリ オブジェクトを $x という名前の変数に格納しています。

2 番目のコマンドでは **Get-CsClientPolicy** コマンドレットを使用し、グローバル クライアント ポリシーへのオブジェクト参照 ($y) を作成しています。このオブジェクト参照を作成した後、Add メソッドを使用して、PolicyEntry プロパティに新しいポリシー エントリを追加しています。PolicyEntry に既に 1 つまたは複数のエントリがある場合は、単純に新しい値をそのコレクションの末尾に追加します。

この例の最後のコマンドでは、**Set-CsClientPolicy** コマンドレットを使用して、実際のグローバル ポリシーに変更を書き込んでいます。**Set-CsClientPolicy** コマンドレットを呼び出さなければ変更はメモリ内のみで存在し、Windows PowerShell セッションの終了後または変数 $x の削除後すぐに消滅します。

    $x = New-CsClientPolicyEntry -Name "OnlineFeedbackURL" -Value "http://www.litwareinc.com/feedback"
    
    $y = Get-CsClientPolicy -Identity global
    $y.PolicyEntry.Add($x)
    
    Set-CsClientPolicy -Instance $y

## 例 2

例 2 は例 1 に示したコマンドの変化形です。ただしこの場合、現在グローバル ポリシーの PolicyEntry プロパティ内にあるすべての項目を、新しいポリシー エントリに置き換えています。それを行うため、この例の最初のコマンドで新しいポリシー エントリを作成し、$x という名前の変数に格納しています。次に 2 つ目のコマンドでは、**Set-CsClientPolicy** コマンドレットを使用し、PolicyEntry プロパティの値を $x に設定しています。このコマンドが完了すると、PolicyEntry プロパティ内で実行している項目は新しいエントリだけになります。**Set-CsClientPolicy** コマンドレットを呼び出す前にこのプロパティ内に含まれていた項目は、すべて新しいエントリによって置き換えられます。

    $x = New-CsClientPolicyEntry -Name "OnlineFeedbackURL" -Value "http://www.litwareinc.com/feedback"
    Set-CsClientPolicy -Identity global -PolicyEntry $x

## 例 3

例 3 は、グローバル ポリシーからクライアント ポリシー エントリを削除する方法を示しています。それを行うため、この例の最初のコマンドでグローバル クライアント ポリシーを取得し、$y という名前の変数にその情報を格納しています。

グローバル ポリシーを取得した後、例の 2 番目のコマンドで RemoveAt() メソッドを使用して、ポリシー内にある最初のポリシー エントリを削除します。削除するポリシー エントリは、インデックス番号で示します。最初のポリシー エントリのインデックス番号は 0、2 番目のポリシー エントリのインデックス番号は 1、以下同様です。RemoveAt(0) という構文は、最初のポリシー エントリを削除することを意味します。

グローバル ポリシーのメモリ内インスタンスからそのポリシー エントリを削除した直後に、**Set-CsClientPolicy** コマンドレットを呼び出して、変更結果をグローバル クライアント ポリシーの実際のインスタンスに書き込みます。

    $y = Get-CsClientPolicy -Identity global
    $y.PolicyEntry.RemoveAt(0)
    
    Set-CsClientPolicy -Instance $y 

## 例 4

例 4 に示すコマンドを実行すると、グローバル ポリシーの一部として構成済みであるすべてのクライアント ポリシー エントリが削除されます。PolicyEntry パラメーターを使用し、パラメーター値を Null ($Null) に設定することによって、これを実行します。

    Set-CsClientPolicy -Identity global -PolicyEntry $Null

## 解説

クライアント ポリシーは、Lync のようなクライアント ソフトウェアを管理するために Lync Server によって使用される基本的なメカニズムです。クライアント ポリシーを作成または構成する際には、多数のオプションを使用できます。たとえば、Lync で写真を使用するかどうか、インスタント メッセージで絵文字の使用を許可するかどうか、Lync によるインスタント メッセージ セッションのチャット内容の自動保存を行うかどうかを指定できます。これらのオプションは、管理者による管理が必要なクライアント関連の設定の多くをカバーしています。

ただし、管理者による管理が必要なすべてのクライアント設定がこれらのオプションでカバーされない場合があります。管理の柔軟性と拡張性を高めるために、クライアント ポリシーには PolicyEntry というプロパティが含まれています。この複数値プロパティにより、管理者はクライアント ポリシー内で明示的には呼び出されることのない新しい管理オプションを追加できます。たとえば、Lync Server のリリース前に行われたベータ テストでは、Lync にフィードバック オプションを追加する機能が提供されていました。このオプションは、新しいポリシー エントリとして追加され、**New-CsClientPolicyEntry** コマンドレットを使用して作成されていました。

ただし、新しいポリシー エントリを任意に作成し、そうしたエントリによる Lync またはその他いくつかのクライアントアプリケーションの管理を期待することはできません。むしろ、新しいクライアント ポリシー エントリの作成に使用できる名前や値に関する、Microsoft からの通知を待つ必要があります。

このコマンドレットを実行できるユーザー: 既定では、次のグループのメンバーは **New-CsClientPolicyEntry** コマンドレットのローカル実行を承認されています。RTCUniversalServerAdmins。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsClientPolicyEntry"}

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
<td><p><em>Name</em></p></td>
<td><p>必須</p></td>
<td><p>System.String</p></td>
<td><p>新しいポリシー エントリの名前です。次に例を示します。-Name &quot;OnlineFeedbackURL&quot; です。</p></td>
</tr>
<tr class="even">
<td><p><em>Value</em></p></td>
<td><p>必須</p></td>
<td><p>System.String</p></td>
<td><p>新しいポリシー エントリに割り当てる値です。次に例を示します。-Value http://www.litwareinc.com/feedback です。</p></td>
</tr>
</tbody>
</table>


## 入力の種類

なし。New-CsClientPolicyEntry コマンドレットはパイプライン入力を受け入れません。

## 戻り値の種類

**New-CsClientPolicyEntry** コマンドレットを実行すると、Microsoft.Rtc.Management.WritableConfig.Policy.Client.PolicyEntryType オブジェクトの新しいインスタンスが作成されます。

## 関連項目

#### その他のリソース

[New-CsClientPolicy](new-csclientpolicy.md)  
[Set-CsClientPolicy](set-csclientpolicy.md)

