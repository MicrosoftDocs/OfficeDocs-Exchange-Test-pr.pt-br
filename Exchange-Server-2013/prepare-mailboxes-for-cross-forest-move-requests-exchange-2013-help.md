---
title: 'Preparar a caixas de correio para solicitações de movimentação entre florestas: Exchange 2013 Help'
TOCTitle: Preparar a caixas de correio para solicitações de movimentação entre florestas
ms:assetid: fdbed4fc-a77e-40d5-a211-863b05d74784
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ee633491(v=EXCHG.150)
ms:contentKeyID: 50487071
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Preparar a caixas de correio para solicitações de movimentação entre florestas

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2017-11-22_

**Resumo:** Saiba mais sobre a preparação de caixas de correio para Exchange 2013 move entre florestas.

Microsoft Exchange 2013 suporta movimentações de caixa de correio e migrações usando o Shell de gerenciamento do Exchange, especificamente os cmdlets **New-MoveRequest** e **New-MigrationBatch** . Você também pode mover a caixa de correio por meio do Centro de administração do Exchange (EAC). Observe que você pode mover caixas de correio do Exchange 2010 e Exchange 2013 para uma floresta do Exchange 2013.

Para mover uma caixa de correio de uma floresta Exchange para uma floresta Exchange 2013, a floresta de destino Exchange 2013 deve conter um usuário habilitado para email válido com um conjunto de atributos de Active Directory especificado. Se houver pelo menos um servidor de acesso para cliente Exchange 2013 implantado na floresta, a floresta é considerada uma floresta Exchange 2013.

Para preparar para a movimentação de caixa de correio, você deve criar usuários habilitados para email com os atributos necessários na floresta de destino. Aqui estão as duas abordagens recomendadas para a criação de email-habilitar usuários com os atributos necessários:

  - Se você implantou o Microsoft Identity Lifecycle Manager (ILM) para sincronização de lista (GAL) entre florestas de endereços global, a abordagem recomendada para criar o usuário habilitado para email é usar o Service Pack 1 (SP1) para o ILM 2007 Feature Pack 1 (FP1). Criamos exemplos de código que você pode usar para aprender a personalizar o ILM para sincronizar o usuário de caixa de correio de origem e o usuário de email de destino.
    
    Para obter mais informações, incluindo como baixar o código de amostra, consulte [Preparar a caixas de correio para movimentações entre florestas usando código de exemplo](prepare-mailboxes-for-cross-forest-moves-using-sample-code-exchange-2013-help.md).

  - Se você criou o usuário de email de destino usando uma ferramenta Active Directory que não seja o ILM/MIIS, use o cmdlet de **Update-Recipient** com o parâmetro *Identity* para executar o serviço de lista de endereços para gerar o **LegacyExchangeDN** para o usuário de email de destino. Criamos uma amostra Windows script do PowerShell que lê a partir e grava Active Directory e chama o cmdlet **Update-Recipient** .
    
    Para obter mais informações sobre como usar o script de amostra, consulte [Prepare a caixas de correio para movimentações entre florestas usando o script de preparação-MoveRequest.ps1 no Shell](prepare-mailboxes-for-cross-forest-moves-using-the-prepare-moverequest-ps1-script-in-the-shell-exchange-2013-help.md).

Após criar o usuário de email de destino, você poderá executar o **New-MoveRequest** ou os cmdlets **New-MigrationBatch** para mover a caixa de correio para a floresta de destino Exchange 2013.

Para obter mais informações sobre solicitações de movimentação remota, consulte os tópicos a seguir:

  - [New-MigrationBatch](https://technet.microsoft.com/pt-br/library/jj219166\(v=exchg.150\))

  - [New-MoveRequest](https://technet.microsoft.com/pt-br/library/dd351123\(v=exchg.150\))

Para obter mais informações sobre movimentações de caixa de correio remota e movimentações remotas de legado, consulte [Movimentações de caixa de correio no Exchange 2013](mailbox-moves-in-exchange-2013-exchange-2013-help.md).

O restante deste tópico descreve os atributos de usuário de email Active Directory que são necessários para uma movimentação de caixa de correio. Esses atributos forem configurados para você quando você usa o código ou o script para se preparar para a movimentação de caixa de correio. No entanto, você pode copiar manualmente esses atributos usando um editor de Active Directory.

## Mover de atributos de usuário do Active Directory necessários para uma caixa de correio

Para suportar uma movimentação de caixa de correio remota, o objeto de usuário de email na floresta de destino de Exchange 2013 deve ter os atributos de Active Directory descritos nesta seção:

  - Atributos obrigatórios

  - Atributos opcionais

  - Atributos vinculados

  - Atributos de usuário vinculado

  - Atributos de caixa de correio de recursos

  - Atributos adicionais

## Atributos obrigatórios

A tabela a seguir lista o conjunto mínimo de atributos que precisam ser configurados no ILM logon do usuário de email de destino para o cmdlet **New-MoveRequest** para funcionar corretamente.

### Atributos do usuário de email

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Atributos do Active Directory do usuário de email</th>
<th>Action</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>displayName</strong></p></td>
<td><p>Copie o atributo correspondente da caixa de correio de origem ou gerar um novo valor.</p></td>
</tr>
<tr class="even">
<td><p><strong>Mail</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="odd">
<td><p><strong>mailNickname</strong></p></td>
<td><p>Copie o atributo correspondente da caixa de correio de origem ou gerar um novo valor.</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchArchiveGUID and msExchArchiveName</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem. Atributos só estarão disponíveis se a caixa de correio de origem for Exchange 2010.</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchMailboxGUID</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchRecipientDisplayType</strong></p></td>
<td><p>-2147483642 //equivalent (decimal) para 0x80000006 (hex).</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchRecipientTypeDetails</strong></p></td>
<td><p>128 (decimal) / 0x80 (hex).</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchUserCulture</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchVersion</strong></p></td>
<td><p>44220983382016 (decimal).</p></td>
</tr>
<tr class="even">
<td><p><strong>cn</strong></p></td>
<td><p>Copie o atributo correspondente da caixa de correio de origem ou gerar um novo valor.</p></td>
</tr>
<tr class="odd">
<td><p><strong>proxyAddresses</strong></p></td>
<td><p>Copie o atributo de <strong>proxyAddresses</strong> do correio de origem. Além disso, a cópia fonte <strong>LegacyExchangeDN</strong> como um X500 da caixa de correio endereço no atributo <strong>proxyAddresses</strong> do usuário de email de destino.</p>

> [!TIP]
> O <STRONG>proxyAddresses</STRONG> do usuário de caixa de correio de origem deve conter um endereço SMTP que corresponde ao domínio autoritativo da floresta de destino. Isso permite que o cmdlet <STRONG>New-MoveRequest</STRONG> selecionar corretamente o <STRONG>targetAddress</STRONG> do usuário habilitado para email fonte (convertido de usuário de caixa de correio de origem após concluir a solicitação de movimentação de caixa de correio) para garantir que o mail roteamento ainda está funcionando.


</td>
</tr>
<tr class="even">
<td><p><strong>sAMAccountName</strong></p></td>
<td><p>Copie o atributo correspondente da caixa de correio de origem ou gerar um novo valor.</p>
<p>Certifique-se de que o valor seja exclusivo dentro do domínio da floresta de destino que pertence ao usuário de email de destino.</p></td>
</tr>
<tr class="odd">
<td><p><strong>targetAddress</strong></p></td>
<td><p>Defina como um endereço SMTP no atributo <strong>proxyAddresses</strong> da caixa de correio de origem.</p>
<p>Esse endereço SMTP deve pertencer ao domínio autoritativo da floresta de origem.</p></td>
</tr>
<tr class="even">
<td><p><strong>userAccountControl</strong></p></td>
<td><p>Constante: o //equivalent 514 para 0x202, ACCOUNTDISABLE | NORMAL_ACCOUNT.</p></td>
</tr>
<tr class="odd">
<td><p><strong>userPrincipalName</strong></p></td>
<td><p>Copie o atributo correspondente da caixa de correio de origem ou gerar um novo valor. Como o usuário de email é desabilitada de logon, esse <strong>userPrincipalName</strong> não serão usados.</p></td>
</tr>
</tbody>
</table>


## Atributos opcionais

Não é obrigatório se os seguintes atributos estão configurados para o cmdlet **New-MoveRequest** funcionar corretamente; No entanto, sincronizá-los fornece uma experiência de usuário de ponta a ponta melhor depois de mover a caixa de correio. Como a GAL na floresta de destino exibe esse usuário de email de destino, você deve definir os seguintes atributos relacionados a GAL.

### Atributos relacionados a GAL

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Atributos do Active Directory do usuário de email</th>
<th>Action</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>c</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="even">
<td><p><strong>co</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="odd">
<td><p><strong>countryCode</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="even">
<td><p><strong>company</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="odd">
<td><p><strong>department</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="even">
<td><p><strong>facsimileTelephoneNumber</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="odd">
<td><p><strong>givenName</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="even">
<td><p><strong>homePhone</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="odd">
<td><p><strong>info</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="even">
<td><p><strong>initials</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="odd">
<td><p><strong>l</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="even">
<td><p><strong>mobile</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchAssistantName</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchHideFromAddressLists</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="odd">
<td><p><strong>otherHomePhone</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="even">
<td><p><strong>otherTelephone</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="odd">
<td><p><strong>pager</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="even">
<td><p><strong>physicalDeliveryOfficeName</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="odd">
<td><p><strong>postalCode</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="even">
<td><p><strong>sn</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="odd">
<td><p><strong>st</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="even">
<td><p><strong>streetAddress</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="odd">
<td><p><strong>telephoneAssistant</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="even">
<td><p><strong>telephoneNumber</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="odd">
<td><p><strong>title</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
</tbody>
</table>


## Atributos vinculados

Um atributo vinculado é um atributo de Active Directory que faz referência a outros objetos Active Directory na floresta local. Você não pode copiar os valores de atributo vinculado diretamente a partir de uma caixa de correio na floresta de origem para um usuário de email na floresta de destino. Primeiro, você deve localizar os objetos Active Directory na floresta de origem que o atributo de caixa de correio de origem se refere ao. Em seguida, você deve localizar os objetos Active Directory correspondentes na floresta de destino para o objeto mencionados acima Active Directory na floresta de origem. E finalmente, defina o atributo do usuário de email de destino para referir-se aos objetos Active Directory na floresta de destino.

### Atributos vinculados

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Atributos do Active Directory do usuário de email</th>
<th>Action</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>altRecipient</strong></p></td>
<td><p>Correspondem ao atributo de <strong>altRecipient</strong> da caixa de correio de origem.</p></td>
</tr>
<tr class="even">
<td><p><strong>deliverAndRedirect</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem. Este atributo é um valor Boolean que deve ser definido juntamente com <strong>altRecipient</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Manager</strong> (e seus vínculos regressivos)</p></td>
<td><p>Correspondem ao atributo do gerente de caixa de correio de origem.</p></td>
</tr>
<tr class="even">
<td><p><strong>MemberOf</strong> (vínculos regressivos)</p></td>
<td><p>Esse é o backlink do atributo de membro do grupo.</p></td>
</tr>
<tr class="odd">
<td><p><strong>publicDelegates</strong> (e seus vínculos regressivos)</p></td>
<td><p>Correspondem ao atributo de <strong>publicDelegates</strong> da caixa de correio de origem.</p></td>
</tr>
</tbody>
</table>


## Atributos de usuário vinculado

Se você deseja mover uma caixa de correio para uma floresta de recursos Exchange 2013, a caixa de correio na floresta de recursos é considerada uma *caixa de correio vinculada*. Neste cenário, você precisará criar um usuário de email vinculados na floresta de recursos (de destino). Para criar um usuário de email vinculada, você precisará definir os atributos mostrados na tabela a seguir.

### Atributos do usuário de correio vinculada

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Atributos do Active Directory do usuário de email</th>
<th>Action</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>msExchMasterAccountHistory</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchMasterAccountSid</strong></p></td>
<td><p>Se a caixa de correio de origem tiver <strong>msExchMasterAccountSid</strong>, copiá-lo. Caso contrário, copie <strong>objectSid</strong> da caixa de correio de origem.</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchRecipientDisplayType</strong></p></td>
<td><p>Constante:-1073741818 a //equivalent (decimal) para * não assinados * 0xC0000006.</p></td>
</tr>
</tbody>
</table>



> [!TIP]
> Uma caixa de correio vinculada só pode ser criada se não houver relação de confiança de floresta entre a floresta de origem e a floresta de destino.



Se o objeto de origem está desabilitado e o atributo **msExchMasterAccountSid** está definido como auto (recurso caixa de correio, caixa de correio compartilhada), não carimbar nada do usuário de destino.

Se o objeto de origem está desabilitado e o atributo **msExchMasterAccountSid** não estiver definido, a caixa de correio é inválida.

Se o objeto de origem está habilitado e o atributo **msExchMasterAccountSid** for definido, a caixa de correio é inválida.

## Atributos de caixa de correio de recursos

Se você deseja mover uma caixa de correio de recurso para uma floresta Exchange 2013, você precisará definir os atributos mostrados na tabela a seguir sobre o usuário de email de destino.

### Atributos de caixa de correio de recursos

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Atributos do Active Directory do usuário de email</th>
<th>Action</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>msExchRecipientDisplayType</strong></p></td>
<td><p>Se a caixa de correio de origem for uma sala de conferência:</p>
<ul>
<li><p><strong>Constante</strong> -2147481850 //equivalent (decimal) para * não assinados * 0x80000706.</p></li>
</ul>
<p>Se a caixa de correio de origem for uma caixa de correio de equipamento:</p>
<ul>
<li><p><strong>Constante</strong> -2147481594 //equivalent (decimal) para * não assinados * 0x80000806.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>msExchResourceCapacity</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchResourceDisplay</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchResourceMetaData</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchResourceSearchProperties</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
</tbody>
</table>


## Atributos adicionais

Em Exchange 2007, o cmdlet **Move-Mailbox** também copiados os atributos mostrados na tabela a seguir ao mover uma caixa de correio. Opcionalmente, você pode copiar esses atributo se exigidas pela sua organização.

### Atributos de caixa de correio de recursos

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Atributos do Active Directory do usuário de email</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>comment</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="even">
<td><p><strong>deletedItemFlags</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="odd">
<td><p><strong>delivContLength</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="even">
<td><p><strong>departmentNumber</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="odd">
<td><p><strong>description</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="even">
<td><p><strong>division</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="odd">
<td><p><strong>employeeID</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="even">
<td><p><strong>employeeNumber</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="odd">
<td><p><strong>employeeType</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="even">
<td><p><strong>extensionAttribute1-15</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="odd">
<td><p><strong>homePostalAddress</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="even">
<td><p><strong>internationalISDNNumber</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="odd">
<td><p><strong>ipPhone</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="even">
<td><p><strong>language</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="odd">
<td><p><strong>lmPwdHistory</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="even">
<td><p><strong>localeID</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="odd">
<td><p><strong>mAPIRecipient</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="even">
<td><p><strong>middleName</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="odd">
<td><p><strong>msDS-PhoneticCompanyName</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="even">
<td><p><strong>msDS-PhoneticDepartment</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="odd">
<td><p><strong>msDS-PhoneticDisplayName</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="even">
<td><p><strong>msDS-PhoneticFirstName</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="odd">
<td><p><strong>msDS-PhoneticLastName</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchBlockedSendersHash</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchELCExpirySuspensionEnd</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchELCExpirySuspensionStart</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchELCMailboxFlags</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchExternalOOFOptions</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchMessageHygieneFlags</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchMessageHygieneSCLDeleteThreshold</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchMessageHygieneSCLJunkThreshold</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchMessageHygieneSCLQuarantineThreshold</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchMessageHygieneSCLRejectThreshold</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchMDBRulesQuota</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchPoliciesExcluded</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchSafeRecipientsHash</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchSafeSendersHash</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchUMSpokenName</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="odd">
<td><p><strong>otherFacsimileTelephoneNumber</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="even">
<td><p><strong>otherIpPhone</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="odd">
<td><p><strong>otherMobile</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="even">
<td><p><strong>otherPager</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="odd">
<td><p><strong>preferredDeliveryMethod</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="even">
<td><p><strong>personalPager</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="odd">
<td><p><strong>personalTitle</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="even">
<td><p><strong>photo</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="odd">
<td><p><strong>pOPCharacterSet</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="even">
<td><p><strong>pOPContentFormat</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="odd">
<td><p><strong>postalAddress</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="even">
<td><p><strong>postOfficeBox</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="odd">
<td><p><strong>primaryInternationalISDNNumber</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="even">
<td><p><strong>primaryTelexNumber</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="odd">
<td><p><strong>showInAdvancedViewOnly</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="even">
<td><p><strong>street</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="odd">
<td><p><strong>terminalServer</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="even">
<td><p><strong>textEncodedORAddress</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="odd">
<td><p><strong>thumbnailLogo</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="even">
<td><p><strong>thumbnailPhoto</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="odd">
<td><p><strong>url</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="even">
<td><p><strong>userCert</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="odd">
<td><p><strong>userCertificate</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="even">
<td><p><strong>userSMIMECertificate</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
<tr class="odd">
<td><p><strong>wWWHomePage</strong></p></td>
<td><p>Copie diretamente o atributo correspondente da caixa de correio de origem.</p></td>
</tr>
</tbody>
</table>

