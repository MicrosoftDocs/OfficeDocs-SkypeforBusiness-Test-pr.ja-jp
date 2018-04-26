---
title: アーカイブ データベースと監視データベースのバックアップ
TOCTitle: アーカイブ データベースと監視データベースのバックアップ
ms:assetid: c120db81-b02c-4a4c-90cd-8aca6cff64f9
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Hh202188(v=OCS.15)
ms:contentKeyID: 52056694
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# アーカイブ データベースと監視データベースのバックアップ

 

_**トピックの最終更新日:** 2013-02-17_

アーカイブまたは監視を展開した場合は、組織の SQL Server バックアップ ポリシーに従ってこれらのデータベースをバックアップする必要があります。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412781.note(OCS.15).gif" title="note" alt="note" />注:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>中央管理ストアをバックアップするときに、アーカイブおよび監視の設定がバックアップされます。詳細については、「<a href="lync-server-2013-backing-up-core-data-and-settings.md">コア データと設定のバックアップ</a>」を参照してください。</td>
</tr>
</tbody>
</table>


アーカイブおよび監視の場合、SQL Server Management Studio などの SQL Server ツールを使用して手動でのバックアップを行ったり、SQL Server 管理ツールを使用して定期的な自動バックアップをスケジュールしたりできます。

