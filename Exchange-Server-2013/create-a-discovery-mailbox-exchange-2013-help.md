---
title: 'Criar uma caixa de correio de descoberta: Exchange 2013 Help'
TOCTitle: Criar uma caixa de correio de descoberta
ms:assetid: bc20285d-35e2-4e49-9bd3-38abf96114ba
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd638177(v=EXCHG.150)
ms:contentKeyID: 50486507
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Criar uma caixa de correio de descoberta

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2016-12-09_

Por padrão, o Microsoft Exchange Server 2013 instalação cria uma caixa de correio de descoberta. Em Exchange Online, uma caixa de correio de descoberta também é criada por padrão. Caixas de correio de descoberta são usadas como caixas de correio de destino para pesquisas de [Descoberta Eletrônica In-loco](in-place-ediscovery-exchange-2013-help.md) nos Centro de administração do Exchange (EAC). Você pode criar caixas de correio de descoberta adicionais conforme necessário. Depois de criar uma nova caixa de correio de descoberta, você precisará atribuir permissões de acesso total para os usuários apropriados para que eles possam acessar os resultados de pesquisa de descoberta eletrônica que são copiados para a caixa de correio de descoberta.


> [!WARNING]
> Após o gerenciador de descoberta copiar os resultados de uma pesquisa de Descoberta Eletrônica em determinada caixa de correio de descoberta, esta poderá conter informações confidenciais. Controle o acesso às caixas de correio de descoberta e certifique-se de que apenas usuários autorizados possam acessá-las.



Para obter mais informações, consulte [Discovery mailboxes](in-place-ediscovery-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 3 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Criar caixas de correio de descoberta" no tópico [Permissões de política e conformidade de mensagens](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - As caixas de correio de descoberta têm uma cota de armazenamento de 50 gigabytes (GB). Essa cota de armazenamento não pode ser aumentada.

  - Você não pode usar o EAC para criar uma caixa de correio de descoberta ou atribuir permissões para acessá-lo. Você precisa usar o Shell. No Office 365, use o PowerShell remoto conectado à sua organização Exchange Online.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## (Opcional) Etapa 1: conecte-se ao Exchange Online usando o PowerShell remoto

Você só precisa realizar esta etapa se você tiver uma organização Exchange Online ou Office 365. Se você tiver uma organização Exchange Server 2013, vá para a próxima etapa e execute o comando no Shell de Gerenciamento do Exchange.

1.  Em seu computador local, abra o Windows PowerShell e execute o comando a seguir.
    
        $UserCredential = Get-Credential
    
    Na caixa de diálogo **Solicitação de Credenciais do Windows PowerShell**, digite o nome de usuário e a senha de sua conta de administrador global do Office 365 e clique em **OK**.

2.  Execute o seguinte comando.
    
        $Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri https://outlook.office365.com/powershell-liveid/ -Credential $UserCredential -Authentication Basic -AllowRedirection

3.  Execute o seguinte comando.
    
        Import-PSSession $Session

4.  Para verificar se você está conectado à sua organização do Exchange Online, execute o comando a seguir para obter uma lista de todas as caixas de correio de sua organização.
    
        Get-Mailbox

Para obter mais informações ou se você tiver problemas para se conectar à sua organização Exchange Online, consulte [Connect to Exchange Online usando o PowerShell remoto](https://go.microsoft.com/fwlink/p/?linkid=517283).

## Etapa 2: Criar uma caixa de correio de descoberta

Este exemplo cria a caixa de correio de descoberta SearchResults.

    New-Mailbox -Name SearchResults -Discovery 

Para obter informações detalhadas sobre sintaxes e parâmetros, consulte [New-Mailbox](https://technet.microsoft.com/pt-br/library/aa997663\(v=exchg.150\)).

Para ver uma lista com todas as caixas de correio de descoberta da organização do Exchange, execute o seguinte comando:

    Get-Mailbox -Resultsize unlimited -Filter {RecipientTypeDetails -eq "DiscoveryMailbox"}

Para obter informações detalhadas sobre sintaxes e parâmetros, consulte [Get-Mailbox](https://technet.microsoft.com/pt-br/library/bb123685\(v=exchg.150\)).

## Etapa 3: Atribuir permissões a uma caixa de correio de descoberta

Você precisa atribuir explicitamente usuários ou grupos as permissões necessárias para abrir uma caixa de correio de descoberta que você criou. Use a seguinte sintaxe para atribuir permissões de grupo ou de um usuário para abrir uma caixa de correio de descoberta e acessar os resultados da pesquisa:

    Add-MailboxPermission <Name of the discovery mailbox> -User <Name of user or group> -AccessRights FullAccess -InheritanceType all

Por exemplo, o seguinte comando atribui uma permissão de Acesso Total para o grupo Gerentes de Litígios, portanto, os membros desse grupo podem abrir a caixa de correio de descoberta Litígios da Fabrikam.

    Add-MailboxPermission "Fabrikam Litigation" -User "Litigation Managers" -AccessRights FullAccess -InheritanceType all

Para obter informações detalhadas sobre sintaxes e parâmetros, consulte [Add-MailboxPermission](https://technet.microsoft.com/pt-br/library/bb124097\(v=exchg.150\)).

## Mais informações

  - Por padrão, os membros do grupo de função Gerenciamento de Descoberta têm permissão de Acesso Total apenas para a Caixa de Correio de Pesquisa de Descoberta padrão. Você precisará atribuir explicitamente a permissão Acesso Total ao grupo de função Gerenciamento de Descoberta se quiser permitir que os membros abram uma caixa de correio de descoberta que você criou.

  - Apesar de estar visível nas listas de endereços do Exchange, os usuários não poderão enviar emails a uma caixa de correio de descoberta. Há restrições de entrega que proíbem a entrega de emails em caixas de correio de descoberta. Isso preserva a integridade dos resultados de pesquisa copiados para uma caixa de correio de descoberta.

  - A caixa de correio de descoberta não pode ser realocada ou convertida em outro tipo de caixa de correio.

  - É possível remover uma caixa de correio de descoberta assim como você faria com qualquer outro tipo de caixa de correio.

