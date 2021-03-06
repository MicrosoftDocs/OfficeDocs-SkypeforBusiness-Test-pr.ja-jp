﻿---
title: 'Lync Server 2013: 音声ルーティング テスト ケースの作成'
TOCTitle: 音声ルーティング テスト ケースの作成
ms:assetid: 43a07a5b-2f20-462a-81e5-d628c18391e0
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg425935(v=OCS.15)
ms:contentKeyID: 48271925
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 での音声ルーティング テスト ケースの作成

 

_**トピックの最終更新日:** 2014-02-07_

## テスト ケースを作成するには

1.  RTCUniversalServerAdmins グループのメンバーとして、あるいは CsVoiceAdministrator、CsServerAdministrator、または CsAdministrator の役割のメンバーとしてコンピューターにログオンします。詳細については、「[Lync Server 2013 でのセットアップのアクセス許可の委任](lync-server-2013-delegate-setup-permissions.md)」を参照してください。

2.  ブラウザー ウィンドウを開いて管理 URL を入力し、Lync Server コントロール パネルを開きます。Lync Server コントロール パネルを開くために使用できる他の方法の詳細については、「[Lync Server 2013 管理ツールを開く](lync-server-2013-open-lync-server-administrative-tools.md)」を参照してください。

3.  左側のナビゲーション バーで \[**音声ルーティング**\] をクリックし、\[**音声ルーティングのテスト**\] をクリックします。

4.  \[**音声ルーティングのテスト**\] ページで、\[**新規**\] をクリックして、新しいテスト ケースを作成します。

5.  \[**名前**\] フィールドに、テスト ケースの一意の名前を入力します。
    
    名前は、エンタープライズ VoIP 展開内のすべての音声ルーティング テスト ケースの中で一意である必要があります。名前は最大 32 文字長まで指定でき、英数字のほか、円記号 (\\)、ピリオド (.) または下線 (\_) を含めることができます。

6.  \[**テスト対象のダイヤル番号**\] に、このテスト ケースで指定しているルーティング構成のテストに使用されるダイヤル番号を入力します。この番号は、ダイヤル プラン、ルート、および音声ポリシーに基づいて正規化され、出力として表示されます。

7.  \[**ダイヤル プラン**\] リストで、テスト実行時に使用するダイヤル プランを選択します。 既定値はグローバル ダイヤル プランです。

8.  \[**音声ポリシー**\] リストで、テスト実行時に使用する音声ポリシーを選択します。 既定値はグローバル音声ポリシーです。

9.  \[**予想される変換**\] に、変換後の予想表示形式で電話番号を入力します。これは、選択したダイヤル プランで最初に一致する正規化ルールによって変換された後の、テスト対象の電話番号の値です。テスト ケースの実行時に、テスト対象の番号が \[**予想される変換**\] の値にならない場合、テストは不合格です。

10. (オプション) \[**予想される PSTN 使用法**\] リストで、指定したダイヤル プランおよび音声ポリシーに基づいて、テスト ケースの実行時に使用されることが予想される公衆交換電話網 (PSTN) 使用法レコードを選択できます。別の PSTN 使用法レコードが使用される場合、テストは不合格です。

11. (オプション) \[**予想されるルート**\] リストで、指定したダイヤル プランおよび音声ポリシーに基づいて、テスト ケースの実行時に使用されることが予想されるボイス ルートを選択できます。 別のボイス ルートが使用される場合、テストは不合格です。

12. (オプション) \[**実行**\] をクリックして、テスト ケースを実行します。 結果は、ページの右パネルに表示されます。

13. \[**OK**\] をクリックします。

14. \[**確定**\] をクリックし、\[**すべて確定**\] をクリックします。
    
    > [!NOTE]
    > 音声ルーティング テスト ケースを作成するときは常に、[<strong>すべて確定</strong>] コマンドを実行して、構成の変更を公開する必要があります。詳細については、「操作」のドキュメントの「<a href="lync-server-2013-publish-pending-changes-to-the-voice-routing-configuration.md">Lync Server 2013 での音声ルーティング構成に対する保留中の変更の公開</a>」を参照してください。
    
    プラス記号で始まる電話番号 (+12065551219 など) がテスト用で利用するダイヤル プランによって正規化される場合、そのために音声ルーティング テストが失敗することがあります (ダイヤル プランと音声ルーティングは正常に動作して、Test-CsDialPlan も成功しますが、音声ルーティング テストが失敗することがあります)。音声ルーティングのテストでは、そのことを念頭に置いてください。

## 関連項目

#### タスク

[Lync Server 2013 での音声ルーティング テスト ケースのエクスポート](lync-server-2013-export-voice-routing-test-cases.md)  
[Lync Server 2013 音声ルーティング テスト ケースのインポート](lync-server-2013-import-voice-routing-test-cases.md)  

#### その他のリソース

[Lync Server 2013 でのダイヤル プランの構成](lync-server-2013-configuring-dial-plans.md)  
[Lync Server 2013 での音声ポリシー、PSTN 使用法レコード、およびボイス ルートの構成](lync-server-2013-configuring-voice-policies-pstn-usage-records-and-voice-routes.md)

