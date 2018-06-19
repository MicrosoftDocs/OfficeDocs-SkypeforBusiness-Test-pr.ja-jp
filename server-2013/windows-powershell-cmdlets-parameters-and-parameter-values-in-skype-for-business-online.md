---
title: Windows PowerShell のコマンドレット、パラメーター、およびパラメーター値
TOCTitle: Windows PowerShell のコマンドレット、パラメーター、およびパラメーター値
ms:assetid: 04615700-099f-4ac5-a801-ddeffccb9e4f
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn362765(v=OCS.15)
ms:contentKeyID: 56270047
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Windows PowerShell のコマンドレット、パラメーター、およびパラメーター値

 

_**トピックの最終更新日:** 2015-06-22_

すべてのバージョンの Windows にあるコマンド ウィンドウに慣れている (または MS-DOS に慣れている) 方は、Windows PowerShell の使用方法の習得において有利な立場にあります。コマンド ウィンドウでは、コマンドを入力して Enter キーを押します。コンピューターはそれに応答し、コマンドまたは実行可能ファイルを実行します。たとえば、現在のディレクトリのすべてのファイルとフォルダーに関する情報を返すには、コマンド プロンプトで次のコマンドを入力して Enter キーを押します。

    dir

次のコマンドでは、現在のディレクトリのすべてのファイルとフォルダーに関する情報を取得します。

``` 
    Directory: C:\

03/21/2013  03:39 PM    <DIR>          Deploy
03/21/2013  02:55 PM    <DIR>          Intel
07/26/2012  12:33 AM    <DIR>          PerfLogs
04/10/2013  10:29 AM    <DIR>          Program Files
04/08/2013  10:28 AM    <DIR>          Program Files (x86)
03/22/2013  08:44 AM    <DIR>          Users
04/11/2013  03:00 PM    <DIR>              Windows
03/13/2013  02:53 PM                 117   pldok.log
03/21/2013  03:35 PM                 769   RHDSetup.exe
03/21/2013  03:37 PM            207   setup.doc
              3 File(s)        1,093 bytes
              7 Dir(s)21,386,002,432 bytes free
```

これは、コマンドまたは実行可能ファイルの名前のみを入力した場合の結果の例です。ただし、コマンド ウィンドウ内から実行されるコマンドの多くでは引数も使用できます。引数は、コマンドに渡される追加の情報で、コマンドの動作を変更します。たとえば、現在のディレクトリのファイルとフォルダーの名前のみを参照し、ファイルやフォルダーのサイズ、ファイルやフォルダーが作成された日付と時刻など、他の情報が不要である場合を考えます。このような場合、dir コマンドを実行する際に **/b** 引数を追加します。

    dir /b

**/b** 引数を含めると、**dir** コマンドは、現在のディレクトリにあるフォルダーとファイルの名前のみを報告して返します。

    Deploy
    Intel
    PerfLogs
    Program Files
    Program Files (x86)
    Users
    Windows
    pldok.log
    RHDSetup.exe
    setup.doc

上記のコマンドで、**/b** 引数は、返されるデータをファイルとフォルダーの名前に限定するのに必要な唯一の情報です。コマンドラインのコマンドにはこのようなケース、つまり単に引数が存在することが、コマンドの動作を変更するのに必要なすべての情報であるケースが多くあります (つまり、**/b** 引数を含めると他の情報が表示されず、**/b** 引数を含めないと追加の情報が表示されます)。また、引数値の指定が必要になる場合があります。引数値は、引数自体に渡される追加情報です。たとえば、**/o** 引数を使用すると、返されるデータを dir コマンドで並べ替える方法を指定できます。オプションは他にもありますが、引数値 **e** を使用するとファイル拡張子で並べ替え、引数値 **s** を使用するとファイル サイズで並べ替えることができます。たとえば、次のコマンドは返されるデータをファイル拡張子で並べ替えます。**/o** 引数の直後に引数値 **e** が含まれていることにご注意ください。

    dir /oe

サンプル フォルダーを使用すると、返されるデータは次のようになり、ファイルがファイル拡張子によりアルファベット順に並べ替えられます。

``` 
    Directory: C:\

03/21/2013  03:39 PM    <DIR>          Deploy
03/21/2013  02:55 PM    <DIR>          Intel
07/26/2012  12:33 AM    <DIR>          PerfLogs
04/10/2013  10:29 AM    <DIR>          Program Files
04/08/2013  10:28 AM    <DIR>          Program Files (x86)
03/22/2013  08:44 AM    <DIR>          Users
04/11/2013  03:00 PM    <DIR>              Windows
03/21/2013  03:37 PM            207   setup.doc
03/21/2013  03:35 PM                 769   RHDSetup.exe
03/13/2013  02:53 PM                 117   pldok.log
              3 File(s)        1,093 bytes
              7 Dir(s)21,386,002,432 bytes free
```

わかりやすくするため、説明しているファイルの並べ替えのみを示します。

setup. **doc**  
RHDSetup. **exe**  
pldok. **log**

Windows PowerShell では他とは異なる用語を使用しますが、Windows PowerShell を操作する基本的な方法はコマンド ウィンドウでの操作と同じです。つまり、コマンドを入力し、必要に応じて引数と引数値を含め、Enter キーを押してコマンドを実行します。ただし、上記のとおり、Windows PowerShell ではコマンド シェルで使用する用語とは異なる用語を使用します。Windows PowerShell では、実行するコマンドはコマンドレットと呼ばれます。さらに、コマンドレットに渡される引数はパラメーターと呼ばれ、パラメーターに渡される値はパラメーター値と呼ばれます。

上記の定義は、ある程度単純化した定義です。コマンドレットは、本質的には、Windows PowerShell 環境内からのみ実行できる小型アプリケーションです。ただし、Windows PowerShell 内からは他のコマンドとアプリケーション (コマンド ウィンドウから実行できるコマンドとアプリケーションの多くを含む) も実行できます。たとえば、Windows PowerShell 内からメモ帳を起動する場合は、以下のコマンドを入力して Enter キーを押すだけで済みます。

    notepad.exe

ただし、Skype for Business Online の管理に関しては、多くの管理者は管理タスクの実行を Windows PowerShell のコマンドレットに依存しています。場合によっては、Skype for Business Online の管理に使用できる他の種類のコマンドやアプリケーションがほとんどないことがあります。また、追加の引数を指定せずに Skype for Business Online のコマンドレットを使用できることもあります (既に説明したように、Windows PowerShell では引数はパラメーターと呼ばれます)。たとえば、次のコマンドは追加のパラメーターなしで [Get-CsOnlineUser](get-csonlineuser.md) コマンドレットを呼び出します。このコマンド自体は、Skype for Business Online のすべてのユーザーに関する情報を返します。

    Get-CsOnlineUser

ただし、Skype for Business Online のコマンドレットの多くではパラメーター (およびパラメーター値) も使用できます。次のコマンドの場合を考えます。

    Get-CsOnlineUser -Identity "kenmyer@litwareinc.com"

このコマンドは次の 3 つの要素から構成されています。

  - コマンドレット **Get-CsOnlineUser**。

  - Identity パラメーター。Windows PowerShell では、パラメーターの前には常にダッシュ (-) が付けられることにご注意ください。これは、この同じコマンドレットに UnassignedUser パラメーターを指定するには、次の構文を使用することを意味します。
    
        -UnassignedUser
    
    パラメーターの前にはダッシュを付ける必要があるだけでなく、このことは引数の前にスラッシュ (/) を付けるコマンド ウィンドウとは異なるため、念頭に置いておく価値があります。
    
    ``` 
    /b
    ```

  - パラメーター値 <strong>kenmyer@litwareinc.com</strong>。

ちなみにこのコマンドは、ID が kenmyer@litwareinc.com である特定のユーザーに関する情報を返します。

## 関連項目

#### 概念

[Windows PowerShell と Lync Online の概要](an-introduction-to-windows-powershell-and-skype-for-business-online.md)

