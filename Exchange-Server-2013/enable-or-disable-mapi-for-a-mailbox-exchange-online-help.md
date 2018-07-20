---
title: 'Habilitar ou desabilitar MAPI para uma caixa de correio: Exchange 2013 Help'
TOCTitle: Habilitar ou desabilitar MAPI para uma caixa de correio
ms:assetid: c2c6718c-a2c0-4ed2-b4ed-364c3cb1f592
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb124497(v=EXCHG.150)
ms:contentKeyID: 50556274
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Habilitar ou desabilitar MAPI para uma caixa de correio

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2017-12-31_

Você pode usar o Centro de administração do Exchange ou o Shell de Gerenciamento do Exchange para habilitar ou desabilitar o MAPI para uma caixa de correio do usuário. Quando o MAPI estiver habilitado, caixa de correio de um usuário pode ser acessada por Outlook ou outros clientes de email MAPI. Se o MAPI estiver desabilitado, ele não pode ser acessado por Outlook ou outros clientes MAPI. No entanto, a caixa de correio continuarão a receber mensagens de email e, supondo que a caixa de correio está habilitada para suportar o acesso por esses clientes, um usuário pode acessar a caixa de correio para enviar e receber emails usando um cliente IMAP, um cliente de email POP ou Outlook Web App.


> [!TIP]
> O suporte ao Outlook Web App e a clientes de email MAPI, POP3 e IMAP4 é habilitado por padrão quando uma caixa de correio de usuário é criada.



Para tarefas de gerenciamento adicionais relacionadas ao gerenciamento do acesso de clientes de email a uma caixa de correio, confira estes tópicos:

  - [Habilitar ou desabilitar o Outlook Web App para uma caixa de correio](enable-or-disable-outlook-web-app-for-a-mailbox-exchange-2013-help.md)

  - [Habilitar ou desabilitar o acesso de IMAP4 para um usuário](enable-or-disable-imap4-access-for-a-user-exchange-2013-help.md)

  - [Habilitar ou desabilitar o acesso POP3 de um usuário](enable-or-disable-pop3-access-for-a-user-exchange-2013-help.md)

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 2 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Configurações de usuário de Acesso para Cliente" no tópico [Permissões de dispositivos móveis e clientes](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Usar o EAC para habilitar ou desabilitar o MAPI

1.  No EAC, navegue até **Destinatários** \> **Caixas de correio**.

2.  Na lista de caixas de correio de usuário, clique na caixa de correio para a qual você deseja habilitar ou desabilitar o MAPI e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página de propriedades de caixa de correio, clique em **Recursos da Caixa de Correio**.

4.  Em **Conectividade de Email**, siga um dos procedimentos a seguir.
    
      - Para desabilitar o MAPI, em **MAPI: Habilitado**, clique em **Desabilitar**.
        
        Um aviso é exibido perguntando se você tem certeza de que deseja desabilitar o MAPI. Clique em **Sim**.
    
      - Para habilitar o MAPI, em **MAPI: Desabilitado**, clique em **Habilitar**.

5.  Clique em **Salvar** para salvar a alteração.

## Usar o Shell de gerenciamento do Exchange para habilitar ou desabilitar o MAPI

Este exemplo desabilita o MAPI para a caixa de correio de Ken Sanchez.

    Set-CASMailbox -Identity "Ken Sanchez" -MAPIEnabled $false

Este exemplo habilita o MAPI para a caixa de correio de Esther Valle.

    Set-CASMailbox -Identity "Esther Valle" -MAPIEnabled $true

Para obter informações detalhadas sobre sintaxes e parâmetros, confira [Set-CASMailbox](https://technet.microsoft.com/pt-br/library/bb125264\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar se você habilitou ou desabilitou com êxito o MAPI para uma caixa de correio de usuário, siga um destes procedimentos:

  - No EAC, navegue até **Destinatários** \> **Caixas de Correio**, clique na caixa de correio e em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

  - Na página de propriedades de caixa de correio, clique em **Recursos da Caixa de Correio**.

  - Em **Conectividade de Email**, verifique se o MAPI está habilitado ou desabilitado.

Ou

  - Execute o seguinte comando no Shell de Gerenciamento do Exchange.
    
        Get-CASMailbox <identity>
    
    Se MAPI estiver habilitado, o valor da propriedade *MapiEnabled* é `True`. Se MAPI estiver desabilitado, o valor é `False`.

