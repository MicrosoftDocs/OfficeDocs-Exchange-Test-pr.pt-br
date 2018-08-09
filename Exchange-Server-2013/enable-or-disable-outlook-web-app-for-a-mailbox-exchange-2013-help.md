---
title: 'Habilitar ou desabilitar o OWA para uma caixa de correio: Exchange Online Help'
TOCTitle: Habilitar ou desabilitar o Outlook Web App para uma caixa de correio
ms:assetid: abc19646-6211-4f18-a060-e347452dcc53
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb124124(v=EXCHG.150)
ms:contentKeyID: 50556257
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Habilitar ou desabilitar o Outlook Web App para uma caixa de correio

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2012-11-14_

Você pode usar o EAC ou o Shell para habilitar ou desabilitar o Outlook Web App para uma caixa de correio de usuário. Quando o Outlook Web App estiver habilitado, os usuários poderão usar o Outlook Web App para enviar e receber emails. Quando o Outlook Web App for desabilitado, a caixa de correio continuará recebendo mensagens de email, e o usuário poderá acessá-la para enviar e receber emails usando um cliente MAPI, como o Microsoft Outlook, ou com um cliente de email POP ou IMAP, supondo-se que a caixa de correio esteja habilitada para dar suporte ao acesso por esses clientes.


> [!TIP]
> O suporte ao Outlook Web App e a clientes de email MAPI, POP3 e IMAP4 é habilitado por padrão quando uma caixa de correio de usuário é criada.



Para tarefas de gerenciamento adicionais relacionadas ao gerenciamento do acesso de clientes de email a uma caixa de correio, confira estes tópicos:

  - [Habilitar ou desabilitar MAPI para uma caixa de correio](enable-or-disable-mapi-for-a-mailbox-exchange-online-help.md)

  - [Habilitar ou desabilitar o acesso de IMAP4 para um usuário](enable-or-disable-imap4-access-for-a-user-exchange-2013-help.md)

  - [Habilitar ou desabilitar o acesso POP3 de um usuário](enable-or-disable-pop3-access-for-a-user-exchange-2013-help.md)

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 2 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Configurações de usuário de Acesso para Cliente" no tópico [Permissões de dispositivos móveis e clientes](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para habilitar ou desabilitar o Outlook Web App

1.  Na EAC, navegue até **Destinatários** \> **Caixas de correio**.

2.  Na lista de caixas de correio de usuário, clique na caixa de correio para a qual você deseja habilitar ou desabilitar o Outlook Web App e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página de propriedades de caixa de correio, clique em **Recursos da Caixa de Correio**.

4.  Em **Conectividade de Email**, siga um destes procedimentos:
    
      - Para desabilitar o Outlook Web App, em **Outlook Web App: Habilitado**, clique em **Desabilitar**.
        
        Um aviso é exibido perguntando se você tem certeza de que deseja desabilitar o Outlook Web App. Clique em **Sim**.
    
      - Para habilitar o Outlook Web App, em **Outlook Web App: Desabilitado**, clique em **Habilitar**.

5.  Clique em **Salvar** para salvar a alteração.


> [!TIP]
> Você pode habilitar e desabilitar o Outlook Web App para caixas de correio de vários usuários usando o recurso de edição em massa do EAC. Para saber como fazer isso, confira a seção "Editar caixas de correio de usuários em massa" em <A href="manage-user-mailboxes-exchange-2013-help.md">Gerenciar caixas de correio do usuário</A>.



## Usar o Shell para habilitar ou desabilitar o Outlook Web App

Este exemplo desabilita o Outlook Web App para a caixa de correio de Paulo Araújo.

    Set-CASMailbox -Identity "Yan Li" -OWAEnabled $false

Este exemplo desabilita o Outlook Web App para a caixa de correio de Laura Cunha.

    Set-CASMailbox -Identity Ellyn@contoso.com -OWAEnabled $true

Para informações detalhadas sobre sintaxes e parâmetros, confira [Set-CASMailbox](https://technet.microsoft.com/pt-br/library/bb125264\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar se você habilitou ou desabilitou o Outlook Web App para uma caixa de correio de usuário com êxito, siga um destes procedimentos:

  - No EAC, navegue até **Destinatários** \> **Caixas de Correio**, clique na caixa de correio e em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

  - Na página de propriedades de caixa de correio, clique em **Recursos da Caixa de Correio**.

  - Em **Conectividade de Email**, verifique se o Outlook Web App está habilitado ou desabilitado.

Ou

  - Execute o seguinte comando no Shell.
    
        Get-CASMailbox <identity>
    
    Se o Outlook Web App estiver habilitado, o valor da propriedade *OWAEnabled* será `True`. Se o Outlook Web App estiver desabilitado, o valor será `False`.

