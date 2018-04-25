---
title: Windows PowerShell と Lync Online の概要
TOCTitle: Windows PowerShell と Lync Online の概要
ms:assetid: 4b4cf534-c950-4d6c-abd9-d3d0e6f53bb7
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn362785(v=OCS.15)
ms:contentKeyID: 56270070
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Windows PowerShell と Lync Online の概要

 

_**トピックの最終更新日:** 2015-06-22_

Windows PowerShell は、Skype for Business Online の管理に使用できるコマンド シェルとスクリプト言語です。グラフィカルな Skype for Business Online 管理センターを使用して Skype for Business Online を管理するのではなく、代わりに次のようなコマンドライン コマンドを使用して製品を管理できます。

    Get-CsOnlineUser -Identity "kenmyer@litwareinc.com"

(UPN kenmyer@litwareinc.com を持つユーザーに関する情報を返す) 上記の例などのシンプルなコマンドを実行する以外にも、Windows PowerShell に精通したユーザーは、これらのコマンドをスクリプトに編成することもできます。これらのスクリプトは、プロセスの自動化や繰り返しの多いタスクの実行に使用できます。

一般には、Skype for Business Online 管理センターを使用して実行できるすべてのタスクは Windows PowerShell を使用しても実行できます。たとえば、管理センターを使用すると、携帯電話の通知 (別名、プッシュ通知) を管理できます。プッシュ通知により、iPhone や Windows Phone などのモバイル デバイスに、イベント (新しいインスタント メッセージや新しいボイス メールなど) に関する通知を送信できます。これらのモバイル デバイス上の Lync アプリケーションがバックグラウンドで実行されている場合であっても、これらの通知をモバイル デバイスで受信できます。

プッシュ通知を管理する方法の 1 つとしては、Skype for Business Online 管理センターを使用します。管理センターでは、\[**組織**\] タブから適切なオプションを選ぶと、プッシュ通知の有効/無効を切り替えることができます。

![LyncOnlinePowerShell\_Push\_Notifications](images/Dn362807.0a6ec1f5-1999-427f-880b-0587c98d7670(OCS.15).png "LyncOnlinePowerShell_Push_Notifications")

また、リモート Windows PowerShell セッションと [Set-CsPushNotificationConfiguration](set-cspushnotificationconfiguration.md) コマンドレットを使用して、プッシュ通知の有効/無効を切り替えることもできます。たとえば、次のコマンドは iPhone と Windows Phone 両方のプッシュ通知を無効にします。

    Set-CsPushNotificationConfiguration -EnableApplePushNotificationService $False -EnableMicrosoftPushNotificationService $False

このように、**Set-CsPushNotificationConfiguration** コマンドレットと共に使用されるパラメーター (つまり EnableApplePushNotificationService と EnableMicrosoftPushNotificationService) は、Skype for Business Online 管理センターで使用できるオプションに対応します。

![Lync オプション/PS コマンドレット間で表示される関連付け](images/Dn362785.f20086fd-3b51-4bbf-8d81-e643d9bf3a2e(OCS.15).png "Lync オプション/PS コマンドレット間で表示される関連付け")

つまり、プッシュ通知を管理するには、管理センターか、Windows PowerShell のコマンドレットと適切なパラメーターの組み合わせのいずれかを使用できます。どちらの方法も同じように問題なく機能します。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412781.note(OCS.15).gif" title="note" alt="note" />注:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>コマンドレット、パラメーター、パラメーター値、および引数など、特定の Windows PowerShell の用語の定義については、「<a href="windows-powershell-cmdlets-parameters-and-parameter-values-in-skype-for-business-online.md">Windows PowerShell のコマンドレット、パラメーター、およびパラメーター値</a>」をご覧ください。</td>
</tr>
</tbody>
</table>


ここで、「Skype for Business Online 管理センターと Windows PowerShell でまったく同じ機能が提供されるのであれば、どちらか一方を優先して使用することを選択する理由は何か?」という当然の疑問が生じます。さらに、「管理センターでチェック ボックスのオン/オフを切り替えるだけの作業ではなく、Windows PowerShell にコマンドを入力することを選択する理由は何か?」という問題もあります。

上記の例のような単純なケースでは、どちらの方法を使用するかの決定は個人的な好みになります。グラフィカル ユーザー インターフェイスを使用する方が好きな人もいれば、Windows PowerShell などのコマンドライン ツールの方が好きな人もいます。ただし、Windows PowerShell が管理タスクを実行する最も効率的な方法である場合や、ある管理タスクを実行する唯一の方法である場合があります。たとえば、Skype for Business Online 管理センターでは会議への招待をカスタマイズできます。

![Lync 管理センター、会議への招待の設定](images/Dn362785.3fb00c33-0bd4-46dd-beb1-8f71e24cf630(OCS.15).png "Lync 管理センター、会議への招待の設定")

[Set-CsMeetingConfiguration](set-csmeetingconfiguration.md) コマンドレットを使用して、これらの同じカスタマイズを行うことができます。ただし、**Set-CsMeetingConfiguration** コマンドレットには、Skype for Business Online 管理センターでは使用できないオプションも含まれています。たとえば、組織内のあるユーザーが会議に参加する場合、既定では、そのユーザーは自動的に会議の発表者として構成されます。この設定は、Skype for Business Online 管理センターを使用しても変更できません。手段は、Windows PowerShell と **Set-CsMeetingConfiguration** コマンドレットを使用する方法に限られます。具体的には、このコマンドは DesignateAsPresenter プロパティを None に設定しますが、これは会議の開催者のみが会議への参加時に発表者として構成されることを意味します。

    Set-CsMeetingConfiguration -DesignateAsPresenter "Everyone"

Windows PowerShell の使用法について詳しくは、次のトピックをご覧ください。

  - [Windows PowerShell のコマンドレット、パラメーター、およびパラメーター値](windows-powershell-cmdlets-parameters-and-parameter-values-in-skype-for-business-online.md)

  - [パラメーターの操作](working-with-parameters-in-skype-for-business-online.md)

  - [必須パラメーターとオプション パラメーター](mandatory-and-optional-parameters-in-skype-for-business-online.md)

  - [パラメーターとプロパティの対比](parameters-vs-properties-in-skype-for-business-online.md)

  - [Lync Online コマンドレットとその他の Windows PowerShell コマンドレットとの組み合わせ](combining-skype-for-business-online-cmdlets-with-other-windows-powershell-cmdlets-in.md)

  - [Windows PowerShell の詳しいヘルプ](more-help-for-using-windows-powershell-in-skype-for-business-online.md)

