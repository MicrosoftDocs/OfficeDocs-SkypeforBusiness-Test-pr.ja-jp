---
title: セキュリティのコマンドレット
TOCTitle: セキュリティのコマンドレット
ms:assetid: 9a6c654d-287d-434e-8d93-409f0d623f5a
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg398799(v=OCS.15)
ms:contentKeyID: 48272949
ms.date: 12/10/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# セキュリティのコマンドレット

 

_**トピックの最終更新日:** 2016-12-08_

Microsoft Lync Server 2013 に含まれるセキュリティのコマンドレットは、主に認証や、ユーザー権限とアクセス許可の管理に使用されます。認証の管理には、さまざまなコマンドレット (証明書と暗証番号 (PIN) の認証用のコマンドレットなど) を使用できます。また、新しい役割ベースのアクセス制御 (RBAC) 機能を使用して Lync Server の管理機能を委任できるようにするための多くのコマンドレットがあります。

## セキュリティのコマンドレット

セキュリティ設定に適用される管理タスクの多くは、Lync Server コントロール パネルから実行できます。主な例外はユーザー アクセス許可のコマンドレットです。ただし、すべてのセキュリティ管理タスクは、Lync Server 管理シェルまたはスクリプト内からコマンドレットを使用して実行できます。スクリプトを使用すると、特定のタスクを自動化できます。以下は、セキュリティ設定の管理に直接関連するコマンドレットの一覧です。

**[Lync Server 2013 での証明書および認証のコマンドレット](lync-server-2013-certificate-and-authentication-cmdlets.md)**

  - [Get-CsCertificate](get-cscertificate.md)

  - [Import-CsCertificate](import-cscertificate.md)

  - [Remove-CsCertificate](remove-cscertificate.md)

  - [Request-CsCertificate](request-cscertificate.md)

  - [Set-CsCertificate](set-cscertificate.md)

  - [Test-CsCertificateConfiguration](test-cscertificateconfiguration.md)

  - [Get-CsClientCertificate](get-csclientcertificate.md)

  - [Revoke-CsClientCertificate](revoke-csclientcertificate.md)

  - [Lock-CsClientPin](lock-csclientpin.md)

  - [Set-CsClientPin](set-csclientpin.md)

  - [Unlock-CsClientPin](unlock-csclientpin.md)

  - [Get-CsClientPinInfo](get-csclientpininfo.md)

  - [New-CsKerberosAccount](new-cskerberosaccount.md)

  - [Get-CsKerberosAccountAssignment](get-cskerberosaccountassignment.md)

  - [New-CsKerberosAccountAssignment](new-cskerberosaccountassignment.md)

  - [Remove-CsKerberosAccountAssignment](remove-cskerberosaccountassignment.md)

  - [Set-CsKerberosAccountAssignment](set-cskerberosaccountassignment.md)

  - [Test-CsKerberosAccountAssignment](test-cskerberosaccountassignment.md)

  - [Set-CsKerberosAccountPassword](set-cskerberosaccountpassword.md)

  - [Get-CsPinPolicy](get-cspinpolicy.md)

  - [Grant-CsPinPolicy](grant-cspinpolicy.md)

  - [New-CsPinPolicy](new-cspinpolicy.md)

  - [Remove-CsPinPolicy](remove-cspinpolicy.md)

  - [Set-CsPinPolicy](set-cspinpolicy.md)

  - [Get-CsProxyConfiguration](get-csproxyconfiguration.md)

  - [New-CsProxyConfiguration](new-csproxyconfiguration.md)

  - [Remove-CsProxyConfiguration](remove-csproxyconfiguration.md)

  - [Set-CsProxyConfiguration](set-csproxyconfiguration.md)

  - [Get-CsSipDomain](get-cssipdomain.md)

  - [New-CsSipDomain](new-cssipdomain.md)

  - [Remove-CsSipDomain](remove-cssipdomain.md)

  - [Set-CsSipDomain](set-cssipdomain.md)

**[ユーザー権限およびアクセス許可のコマンドレット](lync-server-2013-user-rights-and-permissions-cmdlets.md)**

  - [Get-CsAdminRole](get-csadminrole.md)

  - [New-CsAdminRole](new-csadminrole.md)

  - [Remove-CsAdminRole](remove-csadminrole.md)

  - [Set-CsAdminRole](set-csadminrole.md)

  - [Update-CsAdminRole](update-csadminrole.md)

  - [Get-CsAdminRoleAssignment](get-csadminroleassignment.md)

  - [Grant-CsOUPermission](grant-csoupermission.md)

  - [Revoke-CsOUPermission](revoke-csoupermission.md)

  - [Test-CsOUPermission](test-csoupermission.md)

  - [Grant-CsSetupPermission](grant-cssetuppermission.md)

  - [Revoke-CsSetupPermission](revoke-cssetuppermission.md)

  - [Test-CsSetupPermission](test-cssetuppermission.md)

**[相互運用性のコマンドレット](lync-server-2013-interoperability-cmdlets.md)**

  - [Get-CsOAuthConfiguration](get-csoauthconfiguration.md)

  - [Set-CsOAuthConfiguration](set-csoauthconfiguration.md)

  - [Get-CsOAuthServer](get-csoauthserver.md)

  - [New-CsOAuthServer](new-csoauthserver.md)

  - [Remove-CsOAuthServer](remove-csoauthserver.md)

  - [Set-CsOAuthServer](set-csoauthserver.md)

  - [Get-CsPartnerApplication](get-cspartnerapplication.md)

  - [New-CsPartnerApplication](new-cspartnerapplication.md)

  - [Remove-CsPartnerApplication](remove-cspartnerapplication.md)

  - [Set-CsPartnerApplication](set-cspartnerapplication.md)

## 関連項目

#### その他のリソース

[Lync Server PowerShell ブログ](http://go.microsoft.com/fwlink/?linkid=203150%26clcid=0x411)

