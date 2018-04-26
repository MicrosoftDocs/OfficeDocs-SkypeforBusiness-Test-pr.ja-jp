---
title: パラメーターの操作
TOCTitle: パラメーターの操作
ms:assetid: 29ebda0f-ae5f-4512-ad59-240c3605b240
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn362778(v=OCS.15)
ms:contentKeyID: 56270059
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# パラメーターの操作

 

_**トピックの最終更新日:** 2015-06-22_

Identity パラメーターを使用する場合、パラメーター値 kenmyer@litwareinc.com は二重引用符に囲まれている場合があります。

    -Identity "kenmyer@litwareinc.com"

Windows PowerShell を初めて使うユーザーが避けて通れない疑問の 1 つとして、「二重引用符を使用する必要があるのはどのような場合で、二重引用符を使用してはならないのはどのような場合か?」という問題があります。この質問への単純な答えはありませんが、次の一般的な規則に従う必要があります。

  - 二重引用符は、通常、パラメーター値が数値である場合は必要ありません。たとえば、[Get-CsOnlineUser](get-csonlineuser.md) コマンドレットによって返されるユーザーの数を制限するには、次の構文を使用します。
    
        -ResultSize 100
    
    つまり、数値の前後に二重引用符を付けてはなりません。二重引用符を付けると、Windows PowerShell では値を数値として解釈する際に問題が発生する場合があります。
    
    同様に、数値の中にはカンマを含めないようにします。たとえば、結果のサイズを 10,000 に設定する場合、次の構文は正しくはありません。
    
        -ResultSize 10,000
    
    Windows PowerShell では引数値を区切る手段としてカンマを使用するため、この構文ではエラーが発生します。この場合、Windows PowerShell では、ユーザーは 2 つの別のパラメーター値である 10 と 000 を渡していると見なします。結果のサイズを同時に 10 と 0 に設定することはできないため、エラーが発生します。代わりに、カンマのない次の構文を使用します。
    
        -ResultSize 10000

  - 二重引用符は、通常、パラメーター値が日付である場合にも必要ありません。
    
        -StartDate 6/1/2013
    
    ただし、このことが該当するのは時間が含まれていない場合のみです。時間を含める (つまり、日付と時刻の間に空白を配置する) 場合は、二重引用符内にパラメーター値を囲む必要があります。
    
        -StartDate "6/1/2013 10:00AM"
    
    上記のコマンドは、地域設定に米国 (英語) を使用しているコンピューター用に書式設定されていることにご注意ください。米国 (英語) を使用していない場合は、コンピューターの設定に基づいて日付と時刻を書式設定する必要があります。Windows PowerShell で使用されている地域の設定を確認するには、Windows PowerShell プロンプトから次のコマンドを実行します。
    
        Get-Host | Select-Object CurrentUICulture

  - 文字列値 (人物の名前など) には、通常、二重引用符は必要ありません。主な例外は、文字列値に空白、カンマ、またはその他の句読点などの制限された文字が含まれる場合です。たとえば、次の構文は正常に動作しますが、これはユーザーの ID に制限された文字が含まれていないためです。
    
        -Identity "kenmyer@litwareinc.com"
    
    ただし、次のコマンドはエラーになります。これは、ID に空白が含まれているためです。
    
        -Identity Ken Myer
    
    上記のコマンドでエラーが発生するのは、Windows PowerShell では空白を使用して個々のパラメーターを区切るためです。つまり、Windows PowerShell では Identity パラメーターは Ken であり、Myer はまったく新しいパラメーターであると判断することを意味します。その結果、次のエラー メッセージが表示されます。
    
        Get-CsOnlineUser : 引数 'Myer' を受け入れる位置指定パラメーターが見つかりません.
    
    空白 (またはカンマなどの制限された文字) が含まれるパラメーター値を使用するには、二重引用符内にその値を囲みます。
    
        -Identity "Ken Myer"
    
    多くの場合、Windows PowerShell では二重引用符の代わりに単一引用符を使用できます。たとえば、次の構文は有効な Windows PowerShell の構文です。
    
        -Identity 'Ken Myer'
    
    ただし、文字列の先頭と末尾では同じ種類の引用符を使用する必要があることにご注意ください。次の構文は有効な Windows PowerShell の構文ではありません。
    
        -Identity "Ken Myer'
    
    このコマンドを実行しようとすると、Windows PowerShell コンソールでは次のように表示されます。
    
    ``` 
    >>
    ```
    
    双方向矢印は、ユーザーのコマンドの完了を通知する 1 つの手段です。開始が二重引用符であるため、Windows PowerShell では二重引用符で終了すると想定します。\>\> プロンプトが表示された場合は、Ctrl + C キーを押してコマンドをキャンセルし、やり直します。

  - 二重引用符と組み合わせてブール (True/False) 値を使用することはできません。また、True/False 値を指定する場合は、Windows PowerShell の変数である $True および $False を使用する必要があることにもご注意ください。次に例を示します。
    
        -EnterpriseVoiceEnabled $True

また、パラメーター値を使用できない、スイッチ パラメーターと呼ばれるある種の Windows PowerShell のパラメーターも存在します。

    -WhatIf

スイッチ パラメーターを使用する場合はパラメーター値が必要でないだけでなく、パラメーター値を含めると実際にエラーが発生します。たとえば、次のコマンドを実行しようとする場合を考えます。

    -WhatIf $True

このコマンドは、次のようなエラー メッセージが表示されてエラーになります。

    Set-CsUserAcp : 引数 'True' を受け入れる位置指定パラメーターが見つかりません。

Windows PowerShell を使用して Skype for Business Online を管理できるようになるには、どのコマンドレットが使用できるかを知っておく必要があります。また、各コマンドレットにどのパラメーターが使用できるか、および各パラメーターのデータ型 (つまり、パラメーターで日付の値、文字列値、数値などが使用できるかどうか) を知っておく必要もあります。この情報は (コマンドレットの使用法に関する多くの例と共に)、Skype for Business Online のコマンドレットのヘルプ トピックで確認できます。たとえば、[Set-CsTenantPublicProvider](set-cstenantpublicprovider.md) コマンドレットで使用できるパラメーターを以下に示します。

![特定の PowerShell コマンドレットのパラメーター](images/Dn362778.ead7add1-eec3-4fa4-8bbe-9aa72bb7a1ae(OCS.15).png "特定の PowerShell コマンドレットのパラメーター")

上記からわかるように、パラメーターの表は、コマンドレットの説明を提示し、パラメーターが必要 (必須) と省略可能のどちらであるかを示し、各パラメーターのデータ型を通知します。この表に示すデータ型は, .NET Framework により使用される正式なデータ型であることにご注意ください。これは、データ型が単なるスイッチ パラメーターではなく、System.Management.Automation.SwitchParameter として示されていることを意味します。以下に、Skype for Business Online のコマンドレットにより最も一般的に使用されるデータ型の簡易ガイドを示します。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>パラメーター</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
<td><p>ユーザーの Identity を表す文字列値です。通常は、ユーザーの UPN または SIP アドレスです。</p>
<pre><code>-Identity &quot;kenmyer@litwareinc.com&quot;</code></pre></td>
</tr>
<tr class="even">
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>FQDN は完全修飾ドメイン名です。次に例を示します。</p>
<pre><code>-Fqdn &quot;atl-lync-001.litwareinc.com&quot;</code></pre></td>
</tr>
<tr class="odd">
<td><p>System.Boolean</p></td>
<td><p>ブール値は True と False のいずれかの値です。ブール値を指定する場合は、Windows PowerShell の変数である $True および $False を使用する必要があることを忘れないでください。</p>
<pre><code>-Enabled $True -EnterpriseVoiceEnabled $False</code></pre></td>
</tr>
<tr class="even">
<td><p>System.Guid</p></td>
<td><p>GUID は Globally Unique Identifier (グローバル一意識別子) の頭文字で、Skype for Business Online では各 Skype for Business Online テナントに割り当てられる一意の識別子です。次に例を示します。</p>
<pre><code>-Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</code></pre>
<p>次のコマンドを実行すると、Skype for Business Online のテナントに割り当てられている GUID を取得できます。</p>
<pre><code>Get-CsTenant | Select-Object TenantId</code></pre></td>
</tr>
<tr class="odd">
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>スイッチ パラメーターは、スイッチがオンまたはオフであるためこのような名前が付けられています。このパラメーターが存在する場合、スイッチはオンです。このパラメーターが存在しなければスイッチはオフです。たとえば、Confirm パラメーターを使用して、コマンドの実行の前に確認を要請するには、コマンドの一部として (パラメーター値を付けることなく) Confirm パラメーターを含めます。次に例を示します。</p>
<pre><code>Remove-CsUserAcp -Identity &quot;Ken Myer&quot; -Confirm</code></pre>
<p>確認が必要でない場合は、Confirm パラメーターを含めません。</p>
<pre><code>Remove-CsUserAcp -Identity &quot;Ken Myer&quot;</code></pre></td>
</tr>
<tr class="even">
<td><p>System.String</p></td>
<td><p>文字列は英数字の値です。つまり、(一般的には) キーボードで入力できるすべての文字を含めることができます。次に例を示します。</p>
<pre><code>-Password &quot;abc123%&amp;*&quot;</code></pre>
<p>文字列値は、二重引用符の中に囲むことをお勧めします。これは常に必要ではありませんが、文字列値に空白やカンマが含まれる場合、または期せずして予約済みの Windows PowerShell のキーワードである場合には必須です (キーワードとは、Windows PowerShell 言語それ自体の一部であるコマンドやその他の要素です。たとえば、&quot;If&quot; と &quot;End&quot; は両方とも Windows PowerShell のキーワードです。詳しくは、Windows PowerShell コマンド プロンプトから次のコマンドを入力します)。</p>
<p>Get-Help about_Reserved_Words</p></td>
</tr>
</tbody>
</table>


## 関連項目

#### 概念

[Windows PowerShell と Lync Online の概要](an-introduction-to-windows-powershell-and-skype-for-business-online.md)

