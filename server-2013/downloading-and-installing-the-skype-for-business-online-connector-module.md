---
title: Lync Online Connector モジュールのダウンロードとインストール
TOCTitle: Lync Online Connector モジュールのダウンロードとインストール
ms:assetid: a0c87219-b642-4201-85d4-a85c2163d1eb
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn362829(v=OCS.15)
ms:contentKeyID: 56270117
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Online Connector モジュールのダウンロードとインストール

 

_**トピックの最終更新日:** 2016-12-08_

Skype for Business Online Connector モジュールには **New-CsOnlineSession** コマンドレットが含まれます。このコマンドレットを使用して、Skype for Business Online に接続するリモート Windows PowerShell セッションを作成できます。このモジュールは 64 ビット コンピューターでの動作のみを前提としており (詳しくは「[Lync Online 管理用のコンピューターの構成](configuring-your-computer-for-skype-for-business-online-management.md)」をご覧ください)、Microsoft ダウンロード センター ([http://go.microsoft.com/fwlink/?LinkId=294688](http://go.microsoft.com/fwlink/?linkid=294688)) からダウンロードできます。LyncOnlinePowershell.exe ファイルをダウンロードして、次の手順を完了します。

1.  **LyncOnlinePowershell.exe** ファイルをダブルクリックします。

2.  Skype for Business Online Tenant PowerShell セットアップ ウィザードの \[**Microsoft Software License Terms**\] ページで \[**I accept the terms in the License Agreement**\] を選択し、\[**Install**\] をクリックします。\[**User Account Control**\] ダイアログ ボックスが表示されたら \[**Yes**\] をクリックしてインストールを続けます。

3.  \[**Completed the Microsoft Lync Online, Tenant PowerShell Setup** \] ページで \[**Finish**\] をクリックします。

セットアップ プログラムによって、Skype for Business Online Connector モジュール (および **New-CsOnlineSession** コマンドレット) がローカル コンピューターにコピーされます。このモジュールにアクセスするには、管理者の資格情報で Windows PowerShell セッションを開始し、次のコマンドを実行します。

    Import-Module LyncOnlineConnector

Windows PowerShell の起動のたびにこのコマンドを入力したくない場合は、Windows PowerShell プロファイルにコマンドを追加できます。この操作を行うには、Windows PowerShell プロンプトで次のコマンドを入力し、Enter キーを押します。

    notepad.exe $profile

メモ帳が表示されたら、プロファイルの既存のコマンド (ある場合) の下に次の行を追加します。

    Import-Module LyncOnlineConnector

ファイルを保存します。次に Windows PowerShell を起動すると、Skype for Business Online Connector モジュールが自動的にインポートされます。管理者の資格情報で Windows PowerShell を実行していないと、エラー メッセージが表示されてモジュールが読み込まれません。

LyncOnlinePowershell.exe では、Skype for Business Online Connector モジュールのほか, .NET Framework 4.5 と Microsoft Visual C++ 2012 再頒布可能パッケージ (x64) (バージョン 11.0.50727) の 2 つの追加コンポーネントもインストールされます。.NET Framework 4.5 では、Windows PowerShell など, .NET アプリケーションの構築、実行用のインフラストラクチャが提供されます。Visual C++ 再頒布可能パッケージによって、Microsoft Visual Studio 2012 がインストールされていないコンピューター用の Visual C++ ランタイム コンポーネントがインストールされます。

## 関連項目

#### 概念

[Lync Online 管理用のコンピューターの構成](configuring-your-computer-for-skype-for-business-online-management.md)

