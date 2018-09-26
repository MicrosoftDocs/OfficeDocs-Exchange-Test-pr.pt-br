---
title: 'Habilitar ou desabilitar o acesso POP3 de um usuário: Exchange 2013 Help'
TOCTitle: Habilitar ou desabilitar o acesso POP3 de um usuário
ms:assetid: 57e12f07-3b14-45bd-9a82-e6032d14214f
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb691018(v=EXCHG.150)
ms:contentKeyID: 50485643
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Habilitar ou desabilitar o acesso POP3 de um usuário

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2014-01-06_

Você pode habilitar ou desabilitar POP3 para um usuário.


> [!NOTE]
> Depois de ter habilitado ou desabilitado o POP3 para um usuário, reinicie o serviço POP3 do Microsoft Exchange e o serviço de back-end POP3 do Microsoft Exchange. Para obter mais informações sobre como reiniciar o protocolo POP3, consulte <A href="start-and-stop-the-pop3-services-exchange-2013-help.md">Iniciar e interromper os serviços POP3</A>.



Para mais informações sobre como gerenciar caixas de correio do usuário, consulte [Gerenciar caixas de correio do usuário](https://docs.microsoft.com/pt-br/exchange/recipients-in-exchange-online/manage-user-mailboxes/manage-user-mailboxes).

Para mais informações relacionadas a POP3 e IMAP4, consulte [POP3 e IMAP4 no Exchange Server 2013](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 2 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Seção "Permissões de provisionamento do destinatário" do tópico [Permissões de destinatários](recipients-permissions-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para habilitar ou desabilitar POP3 para um usuário

1.  Na EAC, navegue até **Destinatários** \> **Caixas de correio**.

2.  No painel de resultados, selecione o usuário para o qual você deseja habilitar ou desabilitar o POP3 e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na caixa de diálogo **Caixa de Correio de Usuário**, na árvore do console, clique em **Recursos da Caixa de Correio**.
    
    No painel de resultados, em **Conectividade de Email**, siga um destes procedimentos:
    
      - Para desabilitar o POP3 para o usuário, em **POP3: Habilitado**, clique em **Desabilitar**.
    
      - Para habilitar o POP3 para o usuário, em **POP3: Desabilitado**, clique em **Habilitar**.

4.  Clique em **Salvar**.

## Usar o Shell para habilitar ou desabilitar POP3 para um usuário

Este exemplo habilita POP3 para o usuário John Smith.

```powershell
Set-CASMailbox -Identity "John Smith" -POPEnabled $true
```

Este exemplo desativa POP3 para o usuário John Smith.

```powershell
Set-CASMailbox -Identity "John Smith" -POPEnabled $false
```

## Como saber se funcionou?

1.  Na EAC, navegue até **Destinatários** \> **Caixas de correio**.

2.  No painel de resultados, selecione o usuário para o qual você deseja habilitar ou desabilitar o POP3 e clique em **Editar**.

3.  Na caixa de diálogo **Caixa de Correio de Usuário**, na árvore do console, clique em **Recursos da Caixa de Correio**.
    
    No painel de resultados, procure em **Conectividade de Email**.
    
      - Se o POP3 estiver habilitado para o usuário, você verá **POP3: Habilitado**.
    
      - Se o POP3 estiver desabilitado para o usuário, você verá **POP3: Desabilitado**.

4.  Clique em **Salvar**.

