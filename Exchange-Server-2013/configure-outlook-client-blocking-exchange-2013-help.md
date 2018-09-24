---
title: 'Configurar o bloqueio de cliente do Outlook: Exchange 2013 Help'
TOCTitle: Configurar o bloqueio de cliente do Outlook
ms:assetid: 3a579c83-8bc7-4adc-a25c-8eb6eed7220c
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd335207(v=EXCHG.150)
ms:contentKeyID: 51407852
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar o bloqueio de cliente do Outlook

 

_**Aplica-se a:** Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013_

_**Tópico modificado em:** 2015-03-09_

Exchange Server 2013, você pode usar as políticas de retenção ou pastas gerenciadas para mensagens (MRM) de gerenciamento de registros. Somente os usuários executando o Microsoft Outlook 2010 e versões posteriores possuem acesso a todos os recursos de cliente para políticas de retenção. No entanto, as políticas de retenção são aplicadas no servidor de caixa de correio pelo Assistente de pasta gerenciada, independentemente da versão do cliente Outlook usada pelo usuário. Clientes mais antigos do Outlook não exponham a funcionalidade de MRM desses recursos. Por exemplo, porque o Outlook 2007 não oferece suporte a políticas de retenção, os usuários não podem aplicar marcas pessoais a itens ou pastas.

Você pode impedir que os usuários que estão executando versões mais antigas do Outlook de acessar suas caixas de correio Exchange. Você também pode bloquear o acesso por uma caixa de correio ou em uma base do servidor de acesso por cliente.

Para mais tarefaas de gerenciamento relacionadas à MRM, veja [Procedimentos de gerenciamento de registros de mensagens](messaging-records-management-procedures-exchange-2013-help.md).

## Disponibilidade de recursos MRM pelo aplicativo cliente e versão

A tabela a seguir lista os recursos MRM disponíveis em vários aplicativos clientes e versões.

### Recursos MRM

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Aplicativo cliente</th>
<th>Recursos do cliente MRM disponíveis</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Outlook 2013 e Outlook 2010</p></td>
<td><p>Todos</p></td>
</tr>
<tr class="even">
<td><p>Outlook 2007</p></td>
<td><p>Pastas gerenciadas</p></td>
</tr>
<tr class="odd">
<td><p>Outlook 2003 antigas e</p></td>
<td><p>Não suportado</p></td>
</tr>
<tr class="even">
<td><p>Outro software de cliente de email</p></td>
<td><p>Nenhum</p></td>
</tr>
</tbody>
</table>


A tabela a seguir mostra os números de versão para Outlook.

### Versões do Outlook

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Versão do Outlook</th>
<th>Número de versão</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Outlook 2013</p></td>
<td><p>15</p></td>
</tr>
<tr class="even">
<td><p>Outlook 2010</p></td>
<td><p>14</p></td>
</tr>
<tr class="odd">
<td><p>Outlook 2007</p></td>
<td><p>12</p></td>
</tr>
<tr class="even">
<td><p>Outlook 2003</p></td>
<td><p>11</p></td>
</tr>
<tr class="odd">
<td><p>Outlook 2002</p></td>
<td><p>10</p></td>
</tr>
<tr class="even">
<td><p>Outlook 2000</p></td>
<td><p>9</p></td>
</tr>
<tr class="odd">
<td><p>Outlook 98</p></td>
<td><p>8.5</p></td>
</tr>
<tr class="even">
<td><p>Outlook 97</p></td>
<td><p>8</p></td>
</tr>
</tbody>
</table>



> [!NOTE]
> Antes de fazer alterações, observe que versões de pacote de hotfixes e serviço podem afetar a cadeia de caracteres de versão do cliente. Tenha cuidado quando você restringir o acesso do cliente porque os componentes do servidor Exchange também devem usar o MAPI para logon. Alguns componentes relatá sua versão do cliente como o nome do componente (por exemplo, SMTP ou OLE DB), enquanto outros relatório a Exchange número (por exemplo, 6.0.4712.0) da compilação. Por esse motivo, evite restringindo clientes que têm números de versão que começam com 6. &lt;<EM>x</EM>. <EM>x</EM>. &gt;. Por exemplo, para impedir o acesso MAPI completamente, em vez de especificar <STRONG>0.0.0-6.5535.65535.65535</STRONG>, especifique os dois intervalos para que os componentes do servidor podem fazer logon. Por exemplo, especifique o seguinte: <STRONG>0.0.0-5.9.9; 7.0.0-</STRONG>.



Depois de executar estes procedimentos, lembre-se de que, quando os usuários são impedidos de acessar suas caixas de correio, eles receberão a seguinte mensagem de aviso.


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>O administrador do servidor Exchange bloqueou a versão do Outlook que você está usando. Contate o administrador para obter assistência.</p></td>
</tr>
</tbody>
</table>


Para ignorar o aviso de que os recursos MRM não são suportados para os clientes de email que executam versões do Outlook anteriores ao Outlook 2010, você pode usar o parâmetro *ManagedFolderMailboxPolicyAllowed* dos cmdlets **New-Mailbox**, **Enable-Mailbox**e **Set-Mailbox** no Shell. Quando uma diretiva de caixa de correio de pasta gerenciada é atribuída a uma caixa de correio usando o parâmetro *ManagedFolderMailboxPolicy* , o aviso aparece por padrão, a menos que você use o parâmetro *ManagedFolderMailboxPolicyAllowed* .

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 1 minuto.

  - Não é possível usar o EAC (Centro de administração do Exchange) para realizar esses procedimentos. É necessário usar o Shell.

  - Os procedimentos neste tópico exigem permissões específicas. Consulte cada procedimento para ver informações sobre permissões.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), ou [Proteção do Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=285351).

## O que você deseja fazer?

## Versões de bloqueio do Outlook em uma base por caixa de correio

Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Caixas de correio do usuário" no tópico [Permissões de destinatários](recipients-permissions-exchange-2013-help.md) .

Este exemplo bloqueia todas as versões de Outlook anteriores ao 11.8010.8036.

```powershell
Set-CASMailbox -Identity adam@contoso.com -MAPIBlockOutlookVersions "-11.8010.8036"
```

Este exemplo restaura o acesso a uma caixa de correio que seja bloqueada por uma versão do Outlook.

```powershell
Set-CASMailbox -Identity adam@contoso.com -MAPIBlockOutlookVersions $null
```

Para informações detalhadas sobre sintaxes e parâmetros, confira [Set-CASMailbox](https://technet.microsoft.com/pt-br/library/bb125264\(v=exchg.150\)).

## Bloquear as versões do Outlook em um servidor de acesso para cliente

Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Configurações de acesso para cliente RPC" no tópico [Permissões de dispositivos móveis e clientes](clients-and-mobile-devices-permissions-exchange-2013-help.md) .

Este exemplo bloqueia Outlook clientes anteriores à versão 12.0.0 de acessar a caixa de correio em um servidor de acesso para cliente posterior ou o Exchange 2010.


> [!IMPORTANT]
> Os valores usados com o parâmetro <EM>BlockedClientVersions</EM> são exemplos. Para determinar as versões de software corretas do cliente, analise os arquivos de log do Acesso para Cliente RPC em <CODE>%ExchangeInstallPath%Logging\RPC Client Access</CODE>.



    Set-RpcClientAccess -Server CAS01 -BlockedClientVersions "0.0.0-5.65535.65535;7.0.0;8.02.4-11.65535.65535"

Para detalhadas de sintaxes e de definição do parâmetro, consulte [Set-RpcClientAccess](https://technet.microsoft.com/pt-br/library/dd351072\(v=exchg.150\)).

