---
title: Get-CsTenantLicensingConfiguration
TOCTitle: Get-CsTenantLicensingConfiguration
ms:assetid: 0df23143-f1aa-4850-b0f7-750422762925
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn362770(v=OCS.15)
ms:contentKeyID: 56270051
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsTenantLicensingConfiguration

 

_**トピックの最終更新日:** 2015-03-09_

指定されたテナントに関するライセンス情報が Lync 管理センターで使用できるかどうかを示します。

このコマンドレットは、Lync Online のみで使用できます。

## 構文

    Get-CsTenantLicensingConfiguration [-Filter] <Object>] [-Identity] <Object>] [-Tenant] <Object>] [-LocalStore]

## 解説

Get-CsTenantLicensingConfiguration コマンドレットは、指定されたテナントに関するライセンス情報が Lync 管理センターで使用できるかどうかを示します。このコマンドレットは次のような情報を返します。

Identity : Global  
Status : Enabled

Status が Enabled である場合、ライセンス情報は Lync 管理センターで使用できます。Enabled ではない場合、ライセンス情報は Lync 管理センターで使用できません。

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
<th>必須</th>
<th>型</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Filter</strong></p></td>
<td><p>省略可能</p></td>
<td><p>System.String</p></td>
<td><p>テナント ライセンス構成設定のコレクションを返すときに、ワイルドカード文字を使用できるようにします。各テナントでは、ライセンス構成設定の 1 つのグローバル コレクションに制限されているため、Filter パラメーターを使用する必要はありません。</p></td>
</tr>
<tr class="even">
<td><p><strong>Identity</strong></p></td>
<td><p>省略可能</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>返すテナント ライセンス構成設定のコレクションを指定します。各テナントはライセンス設定の 1 つのグローバル コレクションに制限されているため、Get-CsTenantLicensingConfiguration コマンドレットを呼び出すときにこのパラメーターを含める必要はありません。</p></td>
</tr>
<tr class="odd">
<td><p><strong>LocalStore</strong></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>中央管理ストア自体からではなく、中央管理ストアのローカル レプリカからテナント ライセンス構成データを取得します。</p></td>
</tr>
<tr class="even">
<td><p><strong>Tenant</strong></p></td>
<td><p>省略可能</p></td>
<td><p>System.Guid</p></td>
<td><p>返されるライセンス設定が含まれるテナント アカウントのグローバル一意識別子 (GUID) です。次に例を示します。</p>
<p>-Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>次のコマンドを実行することにより、テナントの各々についてテナント ID を返すことができます。</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p></td>
</tr>
</tbody>
</table>


## 入力の種類

Get-CsTenantLicensingConfiguration コマンドレットは、パイプライン入力を受け入れません。

## 戻り値の種類

Get-CsTenantLicensingConfiguration コマンドレットは、Deserialized.Microsoft.Rtc.Management.WritableConfig.Settings.TenantConfiguration.TenantLicensingConfiguration オブジェクトのインスタンスを返します。

## 例

例 1 に示すコマンドは、現在のテナントに関するライセンス構成情報を返します。

    Get-CsTenantLicensingConfiguration

