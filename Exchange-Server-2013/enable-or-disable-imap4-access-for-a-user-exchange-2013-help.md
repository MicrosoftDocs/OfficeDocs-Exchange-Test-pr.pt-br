---
title: 'Habilitar ou desabilitar o acesso de IMAP4 para um usuário: Exchange 2013 Help'
TOCTitle: Habilitar ou desabilitar o acesso de IMAP4 para um usuário
ms:assetid: a685fae4-b6f1-42fe-8bdc-5f99f9617799
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb676481(v=EXCHG.150)
ms:contentKeyID: 50486318
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Habilitar ou desabilitar o acesso de IMAP4 para um usuário

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2013-01-18_

É possível habilitar ou desabilitar o IMAP4 para um usuário.


> [!TIP]
> Depois de habilitada ou desabilitada IMAP4 para um usuário, você deve reiniciar o serviço IMAP4 do Microsoft Exchange e o serviço de back-end do Microsoft Exchange IMAP4. Para obter mais informações sobre como reiniciar o serviço IMAP4, consulte <A href="start-and-stop-the-imap4-services-exchange-2013-help.md">Iniciar e interromper os serviços de IMAP4</A>.



Para mais informações sobre como gerenciar caixas de correio do usuário, consulte [Gerenciar caixas de correio do usuário](https://docs.microsoft.com/pt-br/exchange/recipients-in-exchange-online/manage-user-mailboxes/manage-user-mailboxes).

Para mais informações relacionadas a POP3 e IMAP4, consulte [POP3 e IMAP4 no Exchange Server 2013](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 2 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Seção "Permissões de provisionamento do destinatário" do tópico [Permissões de destinatários](recipients-permissions-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para habilitar ou desabilitar o IMAP4 para um usuário

1.  No EAC, navegue até **Destinatários** \> **Caixas de Correio**.

2.  No painel de resultados, selecione o usuário para o qual você deseja habilitar ou desabilitar o IMAP4 e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na caixa de diálogo **Caixa de Correio de Usuário**, na árvore do console, clique em **Recursos da Caixa de Correio**.
    
    No painel de resultados, em **Conectividade de Email**, siga um destes procedimentos:
    
      - Para desabilitar o IMAP4 para o usuário, em **IMAP4: Habilitado**, clique em **Desabilitar**.
    
      - Para ativar o IMAP4 para o usuário, em **IMAP4: Desabilitado**, clique em **Habilitar**.

4.  Clique em **Salvar**.

## Usar o Shell para habilitar ou desabilitar o IMAP4 para um usuário

Este exemplo ativa o IMAP4 para o usuário Paulo Silva.

```powershell
Set-CASMailbox -Identity "John Smith" -IMAPEnabled $true
```

Este exemplo desativa o IMAP4 para o usuário Paulo Silva.

```powershell
Set-CASMailbox -Identity "John Smith" -IMAPEnabled $false
```

## Como saber se funcionou?

1.  Na EAC, navegue até **Destinatários** \> **Caixas de correio**.

2.  No painel de resultados, selecione o usuário para o qual você deseja habilitar ou desabilitar o IMAP4 e clique em **Editar**.

3.  Na caixa de diálogo **Caixa de Correio de Usuário**, na árvore do console, clique em **Recursos da Caixa de Correio**.
    
    No painel de resultados, procure em **Conectividade de Email**.
    
      - Se IMAP4 estiver habilitado para o usuário, você verá **IMAP4: Enabled**.
    
      - Se IMAP4 não estiver habilitado para o usuário, você verá **IMAP4: desabilitado**.

4.  Clique em **Salvar**.

