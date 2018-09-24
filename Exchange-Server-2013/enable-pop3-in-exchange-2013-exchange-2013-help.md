---
title: 'Habilitar POP3 no Exchange 2013: Exchange 2013 Help'
TOCTitle: Habilitar POP3
ms:assetid: e226a5f1-429d-4046-b925-da6cc151709e
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb124934(v=EXCHG.150)
ms:contentKeyID: 50486834
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Habilitar POP3 no Exchange 2013

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2017-03-28_

Saiba como habilitar a conectividade do cliente de POP3 no Exchange 2016 usando o Console de Gerenciamento Microsoft (MMC) ou o Shell de Gerenciamento do Exchange (EMS).

Ao instalar o Exchange Server 2016, a conectividade do cliente de POP3 não é habilitada. Para habilitar a conectividade do cliente POP3, você precisa iniciar dois serviços POP3, o serviço Microsoft Exchange POP3 e o serviço de Back-end do Microsoft Exchange POP3. Após habilitar o POP3, o Exchange 2016 aceita comunicações com clientes POP3 desprotegidas na porta 110 e na porta 995 usando SSL (Secure Sockets Layer).

Gerencie serviços POP3 e POP3 Backend no mesmo computador do Exchange 2016 que executa a função de servidor de Caixa de Correio. No Exchange 2016, os serviços de Acesso para Cliente fazem parte da função de servidor de Caixa de Correio, para que você não precise mais gerenciar os serviços separadamente.

Para saber mais sobre como configurar POP3 e IMAP4, confira [POP3 e IMAP4 no Exchange Server 2013](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 2 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Seção "Permissões de POP3 e IMAP4" no tópico [Permissões de dispositivos móveis e clientes](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Usar o Console de Gerenciamento Microsoft (MMC) para habilitar POP3

No computador que executa a função de servidor de Caixa de Correio:

1.  No snap-in **Serviços**, na árvore do console, clique em **Serviços (Local)**.

2.  No painel de resultados, clique com o botão direito do mouse em **Microsoft Exchange POP3** e clique em **Propriedades**.

3.  No painel de resultados, clique com o botão direito do mouse em **Back-end do Microsoft Exchange POP3** e clique em **Propriedades**.

4.  Na guia **Geral**, em **Tipo de inicialização**, selecione **Automática** e clique em **Aplicar**.

5.  Em **Status do Serviço**, clique em **Iniciar** e em **OK**.

## Usar o Shell de Gerenciamento do Exchange para habilitar POP3

No computador que executa a função de servidor de Caixa de Correio:

1.  Defina o serviço POP3 do Microsoft Exchange para iniciar automaticamente.
    
    ```powershell
    Set-service msExchangePOP3 -startuptype automatic
    ```

2.  Inicie o serviço POP3 do Microsoft Exchange.
    
    ```powershell
    Start-service msExchangePOP3
    ```

3.  Defina o serviço Back-end do Microsoft Exchange POP3 para iniciar automaticamente.
    
    ```powershell
    Set-service msExchangePOP3BE -startuptype automatic
    ```

4.  Inicie o serviço Back-end POP3 do Microsoft Exchange.
    
    ```powershell
    Start-service msExchangePOP3BE
    ```

## Como saber se funcionou?

No servidor de Caixa de Correio do Exchange 2016, abra o Gerenciador de Tarefas do Windows. Na guia **Serviços**, o status de **MSExchangePOP3** e **MSExchangePOP3BE**aparecerá como **Em execução**, se POP3 estiver habilitado.

