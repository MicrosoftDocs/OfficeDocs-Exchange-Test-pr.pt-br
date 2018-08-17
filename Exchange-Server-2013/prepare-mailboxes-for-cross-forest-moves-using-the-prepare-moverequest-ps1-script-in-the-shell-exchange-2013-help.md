---
title: 'Preparar para mover entre florestas com Prepare-MoveRequest.ps1 no Shell'
TOCTitle: Prepare a caixas de correio para movimentações entre florestas usando o script de preparação-MoveRequest.ps1 no Shell
ms:assetid: 2cea59fb-69b7-4a2f-833f-de4d93cf1810
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ee861103(v=EXCHG.150)
ms:contentKeyID: 50485250
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Prepare a caixas de correio para movimentações entre florestas usando o script de preparação-MoveRequest.ps1 no Shell

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2017-11-22_

**Resumo:**  Saiba como gerenciar movimentações de caixa de correio entre florestas e migrações em Exchange 2013 usando o script de preparar-MoveRequest.ps1 no Shell de Gerenciamento do Exchange.

Microsoft Exchange 2013 oferece suporte a movimentações de caixa de correio e migrações usando os cmdlets **New-MoveRequest** e **New-MigrationBatch** . Você também pode mover a caixa de correio por meio do Centro de administração do Exchange (EAC). Você pode mover do Exchange 2010 ou caixa de correio do Exchange 2013 de uma floresta de Exchange de fonte para uma floresta de Exchange 2013 de destino.

Para executar os cmdlets **New-MoveRequest** e **New-MigrationBatch**, um usuário de email deve existir na floresta de destino do Exchange e deve ter um conjunto mínimo de atributos necessários do Active Directory.

O script do PowerShell Windows de exemplo descrito neste tópico suporta essa tarefa, sincronizando usuários de caixa de correio de uma floresta de origem do Exchange 2013 para florestas de destino do Exchange 2013 como usuários habilitados para email. O script copia os atributos do Active Directory dos usuários de caixa de correio na floresta de origem para a floresta de destino e então utiliza o cmdlet **Update-Recipient** para transformar os objetos de destino em usuários habilitados para email.

Para obter mais informações sobre como usar e escrever scripts, consulte [Script com o Shell de Gerenciamento do Exchange](https://technet.microsoft.com/pt-br/library/bb123798\(v=exchg.150\)). Para mais informações sobre a preparação de movimentações entre florestas, consulte [Preparar a caixas de correio para solicitações de movimentação entre florestas](prepare-mailboxes-for-cross-forest-move-requests-exchange-2013-help.md).

Procurando outras tarefas de gerenciamento relacionadas a solicitações de movimentação remota? Consulte [Gerenciar movimentações de local](manage-on-premises-moves-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Localize o script no seguinte local: Arquivos de Programas\\Microsoft\\Exchange Server\\V15\\Scripts

  - Para executar o script de exemplo, você precisa do seguinte:
    
      - Uma Exchange floresta de origem, em que a caixa de correio reside no momento. Isso pode ser uma caixa de correio do Exchange 2010 ou Exchange 2013.
    
      - Uma floresta de destino com o Exchange 2013 instalado, para onde a caixa de correio será movida.


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Usar o script Prepare-MoveRequest.ps1 a fim de preparar caixas de correio para movimentações entre florestas

Execute o script do Shell em uma função de servidor do Exchange 2013 na floresta de destino do Exchange 2013. O script copia os atributos de caixa de correio da floresta de origem.

Para atribuir uma credencial de autenticação específica para o controlador de domínio da floresta remota, primeiro você deve executar o cmdlet de **Get-Credential**Windows PowerShell e armazenar a entrada do usuário em uma variável temporária. Quando você executa o cmdlet **Get-Credential** , o cmdlet solicita o nome de usuário e senha da conta usada durante a autenticação com o controlador de domínio da floresta remota. Em seguida, você pode usar variável temporária no script Prepare-MoveRequest.ps1. Para obter mais informações sobre o cmdlet **Get-Credential** , consulte [Get-Credential](https://go.microsoft.com/fwlink/p/?linkid=142122).


> [!NOTE]
> Certifique-se de usar duas credenciais separadas para a floresta local e a floresta remota ao chamar esse script.



1.  Execute os seguintes comandos para obter as credenciais de floresta local e floresta remota.
    
        $LocalCredentials = Get-Credential
        $RemoteCredentials = Get-Credential

2.  Em seguida, execute os seguintes comandos para passar as informações de credenciais aos parâmetros *LocalForestCredential* e *RemoteForestCredential* no script Prepare-MoveRequest.ps1.
    
        Prepare-MoveRequest.ps1 -Identity JohnSmith@Fabrikan.com -RemoteForestDomainController DC001.Fabrikam.com -RemoteForestCredential $RemoteCredentials -LocalForestDomainController DC001.Contoso.com -LocalForestCredential $LocalCredentials

## Conjunto de parâmetros do script

A tabela a seguir descreve o parâmetro definido para o script.

### Parâmetro definido para o script Prepare-MoveRequest.ps1

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Parâmetro</th>
<th>Obrigatório</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Obrigatório</p></td>
<td><p>O parâmetro <em>Identity</em> identifica exclusivamente uma caixa de correio na floresta de origem. A identidade pode ser qualquer uma das seguintes:</p>
<ul>
<li><p>CN (nome comum)</p></li>
<li><p>Alias</p></li>
<li><p>Propriedade <strong>proxyAddress</strong></p></li>
<li><p>Propriedade <strong>objectGuid</strong></p></li>
<li><p>Propriedade <strong>DisplayName</strong></p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><em>RemoteForestCredential</em></p></td>
<td><p>Obrigatório</p></td>
<td><p>O parâmetro <em>RemoteForestCredential</em> especifica o administrador que possui permissões para copiar dados do Active Directory da floresta de origem.</p></td>
</tr>
<tr class="odd">
<td><p><em>RemoteForestDomainController</em></p></td>
<td><p>Obrigatório</p></td>
<td><p>O parâmetro <em>RemoteForestDomainController</em> especifica o controlador de domínio na floresta de origem em que reside a caixa de correio.</p></td>
</tr>
<tr class="even">
<td><p><em>DisableEmailAddressPolicy</em></p></td>
<td><p>Opcional</p></td>
<td><p>O parâmetro <em>DisableEmailAddressPolicy</em> especifica se a Política de Endereço de Email (EAP) deve ser desabilitada ao se criar um objeto <strong>MailUser</strong> na floresta de destino.</p>
<p>Quando você especificar esse parâmetro, o EAP na floresta de destino não será aplicado.</p>

> [!NOTE]
> Quando você especificar esse parâmetro, o objeto <STRONG>MailUser</STRONG> não terá mapeamento de endereço de email no domínio de floresta local carimbado. Isso costuma ser carimbado pelo EAP.


</td>
</tr>
<tr class="odd">
<td><p><em>LinkedMailUser</em></p></td>
<td><p>Opcional</p></td>
<td><p>O switch <em>LinkedMailUser</em> especifica se deve ser criado um MailUser vinculado na floresta local para o usuário de caixa de correio na floresta remota.</p>
<p>Se o switch for fornecido, o script criará um objeto <strong>MailUser</strong> de destino vinculado à caixa de correio de origem. Se o switch é omitido, o script criará um objeto <strong>MailUser</strong> regular de destino.</p></td>
</tr>
<tr class="even">
<td><p><em>LocalForestCredential</em></p></td>
<td><p>Opcional</p></td>
<td><p>O parâmetro <em>LocalForestCredential</em> especifica o administrador com permissões para gravar dados no Active Directory da floresta de destino.</p>
<p>Recomendamos que você especifique explicitamente esse parâmetro para evitar problemas de permissão no Active Directory.</p>
<p>Se a floresta remota e a floresta local tiverem uma relação de confiança configurada, não use uma conta de usuário da floresta remota como a credencial da floresta local, embora a conta de usuário remota possa ter permissão para modificar o Active Directory na floresta local.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalForestDomainController</em></p></td>
<td><p>Opcional</p></td>
<td><p>O parâmetro <em>LocalForestDomainController</em> especifica um controlador de domínio na floresta de destino em que o usuário habilitado para email será criado.</p>
<p>Recomendamos que você especifique esse parâmetro para evitar possíveis problemas de atraso na replicação do controlador de domínio na floresta local que podem ocorrer caso um controlador de domínio aleatório seja selecionado.</p></td>
</tr>
<tr class="even">
<td><p><em>MailboxDeliveryDomain</em></p></td>
<td><p>Opcional</p></td>
<td><p>O parâmetro <em>MailboxDeliveryDomain</em> especifica um domínio autoritativo da floresta de origem de modo que o script possa selecionar a propriedade <strong>proxyAddress</strong> correta do usuário de caixa de correio de origem como a propriedade <strong>targetAddress</strong> do usuário de destino habilitado para email.</p>
<p>Como padrão, o endereço SMTP primário do usuário de caixa de correio de origem está definido como as propriedade <strong>targetAddress</strong> do usuário de destino habilitado para email.</p></td>
</tr>
<tr class="odd">
<td><p><em>OverWriteLocalObject</em></p></td>
<td><p>Opcional</p></td>
<td><p>O parâmetro <em>OverWriteLocalObject</em> é usado para usuários criados pela ferramenta de migração do Active Directory. As propriedades são copiadas do contato de email existente para o usuário de email recém-criado. Porém, após essa cópia, o script também copia as propriedades do usuário de floresta de origem para o usuário de email recém-criado.</p></td>
</tr>
<tr class="even">
<td><p><em>TargetMailUserOU</em></p></td>
<td><p>Opcional</p></td>
<td><p>O parâmetro <em>TargetMailuserOU</em> especifica a unidade organizacional (OU) sob a qual o usuário de destino habilitado para email será criado.</p></td>
</tr>
<tr class="odd">
<td><p><em>UseLocalObject</em></p></td>
<td><p>Opcional</p></td>
<td><p>O parâmetro <em>UseLocalObject</em> especifica se deve ser convertido o objeto local existente para o usuário habilitado para email solicitado caso o script detecte um objeto na floresta local que entra em conflito com o usuário habilitado para email a ser criado.</p></td>
</tr>
</tbody>
</table>


## Exemplos

Esta seção contém vários exemplos de como você pode usar o script Prepare-MoveRequest.ps1.

## Exemplo: Único usuário habilitado para email vinculado

Este exemplo apresenta um único usuário vinculado e habilitado para email na floresta local quando há confiança de floresta entre a floresta remota e a floresta local.

1.  Execute os seguintes comandos para obter as credenciais de floresta local e floresta remota.
    
        $LocalCredentials = Get-Credential
        $RemoteCredentials = Get-Credential

2.  Depois, execute o seguinte comando para passar as informações de credenciais aos parâmetros *LocalForestCredential* e *RemoteForestCredential* no script Prepare-MoveRequest.ps1.
    
        Prepare-MoveRequest.ps1 -Identity JamesAlvord@Contoso.com -RemoteForestDomainController DC001.Fabrikam.com -RemoteForestCredential $RemoteCredentials -LocalForestDomainController DC001.Contoso.com -LocalForestCredential $LocalCredentials -LinkedMailUser 

## Exemplo: Pipelining

Este exemplo suporta pipelining caso você forneça uma lista de identidades de caixa de correio.

1.  Execute o seguinte comando.
    
        $UserCredentials = Get-Credential

2.  Execute o seguinte comando para passar as informações de credenciais ao parâmetro *RemoteForestCredential* no script Prepare-MoveRequest.ps1.
    
        "IanP@Contoso.com", "JoeAn@Contoso.com" | Prepare-MoveRequest.ps1 -RemoteForestDomainController DC001.Fabrikam.com -RemoteForestCredential $UserCredentials

## Exemplo: Usar um arquivo. csv para criar usuários habilitados para email em massa

Você pode gerar um arquivo .csv que contém uma lista de identidades de caixa de correio da floresta de origem, a qual permite canalizar o conteúdo desse arquivo no script para criar usuários de destino em massa habilitados para email.

Por exemplo, o conteúdo do arquivo .csv pode ser:

Identidade

Ian@contoso.com

John@contoso.com

Cindy@contoso.com

Este exemplo chama um arquivo .csv para criar usuários de destino em massa habilitados para email.

1.  Execute o seguinte comando para obter as credenciais de floresta remota.
    
        $UserCredentials = Get-Credential

2.  Execute o seguinte comando para passar as informações de credenciais ao parâmetro *RemoteForestCredential* no script Prepare-MoveRequest.ps1.
    
        Import-Csv Test.csv | Prepare-MoveRequest.ps1 -RemoteForestDomainController DC001.Fabrikam.com -RemoteForestCredential $UserCredentials

## Comportamento do script por objeto de destino

Esta seção descreve como o script se comporta em relação aos vários cenários para objetos de destino.

## Objeto de destino habilitado para email duplicado

Quando o script tenta criar um usuário de destino habilitado para email pelo usuário de caixa de correio de origem e detecta um objeto local duplicado habilitado para email, a seguinte lógica é usada:

  - Se o atributo **masterAccountSid** do usuário da caixa de correio de origem for igual a qualquer atributo **objectSid** ou **masterAccountSid** do objeto de destino:
    
      - Se o objeto de destino não for habilitado para email, o script retorna um erro porque não oferece suporte à conversão de um objeto que não é habilitado para email em um usuário habilitado para email.
    
      - Se o objeto de destino for habilitado para email, o objeto de destino é uma cópia.

  - Se um endereço nas propriedades **proxyAddress** (smtp/x500 somente) de usuário de caixa de correio de origem for igual a um endereço nas propriedades **proxyAddress** (smtp/x500 somente) de objeto de destino, então o objeto de destino é uma cópia.

O script informa o usuário sobre objetos duplicados.

Se o objeto de destino habilitado para email for um contato ou usuário habilitado para email, que é muito provavelmente criado por uma implantação de sincronização de lista de endereços global (GAL) (com base no Identity Lifecycle Management 2007 Service Pack 1) entre florestas, o usuário poderá executar novamente o script com o parâmetro *UseLocalObject* para usar o objeto de destino habilitado para email na migração de caixa de correio.

## Usuário habilitado para email

Se o objeto de destino for um usuário habilitado para email, o script copia os seguintes atributos do usuário de caixa de correio de origem para o usuário de destino habilitado para email :

  - **msExchMailboxGUID**

  - **msExchArchiveGUID**

  - **msExchArchiveName**

Se o parâmetro *LinkedMailUser* for definido, o script copiará o atributo **objectSid**/**masterAccountSid** de origem.

## Contato habilitado para email

Se o objeto de destino for um contato habilitado para email, o script exclui o contato existente e copia todos os seus atributos para um novo usuário habilitado para email. O script também copia os seguintes atributos de um usuário de caixa de correio de origem:

  - **msExchMailboxGUID**

  - **msExchArchiveGUID**

  - **msExchArchiveName**

  - **sAMAccountName**

  - **userAccountControl** (definido como 514 //equivalente a 0x202, ACCOUNTDISABLE | NORMAL\_ACCOUNT)

  - **userPrincipalName**

Se o parâmetro *LinkedMailUser* for definido, o script copiará o atributo **objectSid**/**masterAccountSid** de origem.

## Atributo LegacyExchangeDN

Quando o cmdlet **Update-Recipient** é chamado para converter o objeto de destino em um usuário habilitado para email, um novo atributo **LegacyExchangeDN** é gerado para o usuário habilitado para email de destino. O script copia o atributo **LegacyExchangeDN** do usuário habilitado para email destino como um x500 endereço às propriedades **proxyAddress** do usuário de caixa de correio de origem.

