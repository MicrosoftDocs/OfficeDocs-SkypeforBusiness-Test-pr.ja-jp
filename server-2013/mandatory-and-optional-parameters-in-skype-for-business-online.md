---
title: 必須パラメーターとオプション パラメーター
TOCTitle: 必須パラメーターとオプション パラメーター
ms:assetid: e766362f-e2e9-4598-a595-fdf5eedd9ad6
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn362851(v=OCS.15)
ms:contentKeyID: 56270154
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 必須パラメーターとオプション パラメーター

 

_**トピックの最終更新日:** 2015-06-22_

Windows PowerShell パラメーターは、必須とオプションの 2 つのカテゴリに分けられます。*必須パラメーター*とは、コマンドの実行時に含める必要があるパラメーターです。たとえば、[Remove-CsUserAcp](remove-csuseracp.md) コマンドレットは、以前ユーザーに割り当てられていた電話会議プロバイダーの割り当て解除に使用します。**the Remove-CsUserAcp** コマンドレットを実行する際には、Identity パラメーターを使用する必要があります。このパラメーターをコマンドレットで使用することで、電話会議プロバイダーの削除が必要なユーザーが指定されます。ご推察のとおり、このコマンドをパラメーターなしで実行しても意味はありません。

    Remove-CsUserAcp

このような場合コマンドレットでは、どのユーザーの電話会議プロバイダーを削除すべきなのかわからないので、ユーザーの ID を指定する必要があります。

    Remove-CsUserAcp -Identity "Ken Myer"

通常は、コマンドの実行時に必須パラメーターを省略すると、Windows PowerShell にプロンプトが表示されます。たとえば、次のコマンドを入力して Enter キーを押したとします。

    Remove-CsUserAcp

この場合、Windows PowerShell でこの不完全なコマンドは実行されず、必須パラメーターの入力を指示するプロンプトが表示されます。

    コマンド パイプライン位置 1 のcmdlet Remove-CsUserAcp
    次のパラメーターの値を指定してください:
    ID:

有効な Identity パラメーターを入力して Enter キーを押すと、Windows PowerShell で **Remove-CsUserAcp** コマンドレットが実行され、電話会議プロバイダーが削除されます。気が変わってこのコマンドを実行しない場合は、Ctrl + C を押してコマンドを終了します。

これは確実なシステムではなく、Windows PowerShell で必要なパラメーター セットの入力が指示されない場合もあります。たとえば、一部のコマンドレットではパラメーター A とパラメーター B のうち、(両方ではなく) 一方が必須であるように構築されています。Windows PowerShell ではパラメーター A と B の両方の入力を指示されるかもしれませんが、パラメーター A と B は同じコマンドで使用できないため、このコマンドは失敗します。このような場合があるため、コマンドの実行前に必要なパラメーターをすべて含めておき、Windows PowerShell からの必要情報の入力指示に頼らないようにしてください。

また、パラメーター値のフォーマット化も少し難しいプロセスかもしれません。たとえば、空白のスペースを含むパラメーター値を含める場合は、その値を二重引用符で囲む必要があります。

    -Identity "Ken Myer"

ただし二重引用符の使用が必要なのは、実行するコマンドの一部としてパラメーターとパラメーター値を入力する場合だけです。**Remove-CsUserAcp** コマンドレットを実行する際に Identity パラメーターを入力しないと、Windows PowerShell によってユーザー ID の入力を求められます。

    コマンド パイプライン位置 1 のcmdlet Remove-CsUserAcp
    次のパラメーターの値を指定してください:
    ID:

Identity パラメーターを二重引用符で囲んで「Ken Myer」と入力します。

    コマンド パイプライン位置 1 のcmdlet Remove-CsUserAcp
    次のパラメーターの値を指定してください:
    ID:"Ken Myer"

この結果コマンドは失敗し、次のエラー メッセージが表示されます。

    Remove-CsUserAcp : ID ""Ken Myer"" の管理オブジェクトが見つかりません。

この場合、ID パラメーターの一部として二重引用符付きの "Ken Myer" という ID が含まれるユーザーが検索されます。パラメーター値の入力を求められたら、二重引用符は含めないでください。

    コマンド パイプライン位置 1 のcmdlet Remove-CsUserAcp
    次のパラメーターの値を指定してください:
    ID:Ken Myer

これに対し、*オプション パラメーター*は名前の意味のとおりに処理されます。コマンドレットを実行するのに、このパラメーターを含める必要はありません。たとえば、Remove-CsUserAcp コマンドレットには Name というオプション パラメーターがあります。Name パラメーターがコマンドに含まれていると、指定した電話会議プロバイダーのみが削除されます。このコマンドを実行すると、Consolidated Messenger という名前の電話会議プロバイダーは削除されますが、Ken Myer に割り当てられているその他の電話会議プロバイダーは削除されません。

    Remove-CsUserAcp -Identity "Ken Myer" -Name "Fabrikam ACP"

このパラメーターを設定しなくてもコマンドは実行されます。ただしこの場合、Remove-CsUserAcp を実行すると Ken Myer に割り当てられた電話会議プロバイダーがすべて削除されます。

    Remove-CsUserAcp -Identity "Ken Myer"

## 関連項目

#### 概念

[Windows PowerShell と Lync Online の概要](an-introduction-to-windows-powershell-and-skype-for-business-online.md)

